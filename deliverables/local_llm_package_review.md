---
title: "local_llm package review"
date: 2026-04-06
status: final
tags:[review, local-llm, concept_context]
category: architecture
chunk_type: report
---

# Kort oppsummering

Materialet er verdifullt og retningen er god: lokal controller først, hybrid
senere, n8n til slutt. Det finnes både dokumentert arbeidslogikk og faktisk
controllerkode. Samtidig er pakken ikke ren nok til å bli `LLM-local` direkte.
Den er fortsatt preget av duplikater, blandet modenhet og en uklar kanonisk
sannhetskilde mellom dokumentpakke og levende kode.

# Hva pakken faktisk inneholder

- en samlet dokumentpakke med:
  - et kortere `local_llm_context_pack_v2`
  - et større `local_llm_control_room_full_v2`
  - QA-rapport i markdown og csv
- en separat `local_llm_control_room_full_v2.zip` som er duplikat av samme del i
  samlepakken
- en separat `github_local_llm_qa_report.md` som er identisk med den innebygde
  kopien i samlepakken
- en enkel referansecontroller i `stifinner_mvp.zip`
- en levende lokal kodebase i `C:\Users\larse\Documents\Prosjekter\llm-controller`

# Sterkeste deler

- retningen er riktig: lokal scan og forståelse før hybrid og lenge før n8n
- QA-notatet støtter valg av `Ollama + Qwen3-Coder` som tydelig default
- control-room-dokumentene forklarer ruting, prompt-back og kontrollgrenser på
  en nyttig måte
- `stifinner_mvp` gjør konseptet konkret med liten Windows-først arbeidsenhet
- `llm-controller` viser at timeout, retry, kontekstkrymping, state og MCP-bro
  allerede er påbegynt i kode

# Svakeste deler

- det finnes for mange dubletter og parallelle pakker
- mange sentrale dokumenter står fortsatt som `draft`
- det mangler én tydelig README-fortelling som binder dokumenter og kode sammen
- `llm-controller` mangler README, tester og repo-hygiene
- fallback er ikke ferdig operasjonalisert; mesteparten av koden har retry, men
  ikke reell provider- eller modellfallback

# Duplikater og overlapp

- `local_llm_control_room_full_v2.zip` er duplikat av `local_llm_control_room_full_v2`
  inne i `local_llm_updated_packages.zip`
- control-room-innholdet har identisk SHA-256 på begge steder:
  `5df4d6759c00be48531773887c5a6125cf291e603e9d9033c2b8e44c157b6757`
- `github_local_llm_qa_report.md` er identisk både standalone og inne i pakken
- QA-validering og modellanbefaling er duplisert mellom context-pack og
  control-room
- `stifinner_mvp` ligger både standalone og som referansekopi inne i pakkene

# Hva som er uklart

- hvilken del som skal være kanonisk startpunkt for et senere repo
- hvor grensene går mellom docs som er pedagogiske og docs som er operative
- om `llm-controller` skal bli direkte basekode eller bare en sterk referanse
- hvordan et delbart lokalt referanseregister skal se ut uten å lekke absolute
  stier

# Hva som mangler før repo

- en konsolidert README som sier hva repoet er og ikke er
- én valgt docs-struktur uten dubletter
- en eksplisitt fallbackstige, ikke bare retry
- et tydelig lokalt referanseregister med "spør hvis ukjent"-regel
- oppryddet controllerkode med README, tester og ryddig skille mellom kode og
  kjøretidsartefakter

# Vurdering av stoppvern

## Dokumentert stoppvern

Dokumentpakken tar stopp på alvor. `Execution controller specification` nevner
timeout, teknisk vs kvalitetsstopp, retry med mindre input og fallback til
enklere oppgave eller annen modell. `Control limits and stop rules` beskriver
stoppsignaler og når ruten skal byttes.

## Faktisk stoppvern i kode

`llm-controller` ivaretar deler av dette i praksis:

- `config.yaml` setter `timeout_s: 600`
- `controller.py` har `MAX_ATTEMPTS = 3`
- nye forsøk krymper konteksten fra full liste til halv liste til én fil
- `llm_runner.py` håndterer `timeout`, `error` og `empty`
- `validator.py` graderer svar som `ok`, `weak` eller `fail`
- state og logger gjør det mulig å se hva som faktisk skjedde

## Hvor stoppvern fortsatt svikter

- det finnes ikke en ferdig implementert modell- eller providerfallback
- historisk state viser både `Not Found` og timeout-feil
- minst én kjøring ble stående som `running`
- brukeropplevelsen er ikke pakket godt nok inn; du må fortsatt selv vite for
  mye om hvilke lokale referanser og hvilke ruter som finnes

Konklusjon: timeout og retry er delvis ivaretatt, men reell stoppforebygging er
ikke ferdig før fallback og referansebevissthet blir operasjonalisert.

# Vurdering av riktig LLM

Defaultvalget er godt nok:

- `Ollama + Qwen3-Coder` som førstelinje
- `Qwen2.5-Coder`, LocalAI eller Jan som praktiske reservevalg
- hybrid til Claude eller Codex når oppgaven blir flerspors, usikker eller
  tidskritisk

Dette er bra fordi det gir en tydelig start uten å låse hele systemet til én
modell. Det som mangler er en tydelig, implementert beslutningsstige som sier:

1. prøv default lokalt
2. prøv mindre kontekst
3. prøv annen lokal modell eller provider hvis problemet ser modellspesifikt ut
4. gå til hybrid før brukeren sitter fast

# Vurdering av brukerfriksjon

Opplegget reduserer friksjon når alt går bra, men flytter fortsatt for mye jobb
til brukeren når noe er uklart.

Det gode:

- tydelig default-stack
- fokus på små arbeidsenheter
- lokalt state og rapporter
- sterk idé om at man ikke skal sende alt til sky med en gang

Det som fortsatt skaper bryderi:

- flere parallelle pakker med overlappende informasjon
- ingen samlet README rundt faktisk kode
- manglende lokalt referanseregister i selve materialet før denne workspacen
- for lite eksplisitt "spør hvis ukjent"-mekanikk

# Stifinner MVP vs llm-controller

## Stifinner MVP

- best som enkel pedagogisk referanse
- lav oppstartsfriksjon
- tydelig Windows-først eksperiment
- for smal til å være hovedrepo uten videre

## llm-controller

- best som kandidat til faktisk controllerkode
- har CLI, MCP-wrapper, scanning, state og validator
- avslører også hvor den operative robustheten fortsatt mangler

Konklusjon: `stifinner_mvp` bør beholdes som referanseeksempel, mens
`llm-controller` bør være første kandidat når kode skal konsolideres.

# Hva som bør brukes som standard arbeidsflyt

Bruk denne standarden:

1. kjør lokal default med `Ollama + Qwen3-Coder`
2. bruk kjent lokalt referanseregister før noen større antakelser
3. start med én liten arbeidsenhet
4. ved feil: prøv mindre kontekst
5. ved ny feil: prøv alternativ lokal modell eller provider hvis problemet ser
   lokalt ut
6. hvis oppgaven fortsatt er usikker eller bred: eskaler til hybrid
7. spør brukeren om ny lokal referanse bare når det faktisk mangler sannhetskilde

# Hva som bør inn i `LLM-local` senere

- renset controllerkode basert på `llm-controller`
- utvalgte control-room- og context-pack-dokumenter i én samlet docs-struktur
- promptene som faktisk støtter routing, prompt-back og handoff
- et eksempel på lokalt referanseregister
- en kort QA-oppsummering som begrunner default-stack og fallback

# Hva som ikke bør inn ennå

- rå zip-filer
- dublerte docs
- logger, `__pycache__` og state-snapshots fra `llm-controller`
- absolutt-sti-basert kontekst
- n8n som førstelinje
- tung autonom patching eller repo-wide batchløp uten sterkere stopperegler

# Beslutning i tre nivåer

## Behold nå

- lokal-først retning
- `Ollama + Qwen3-Coder` som default
- hybrid som neste lag
- `stifinner_mvp` som enkel referanse
- `llm-controller` som hovedkandidat for kode

## Revider før repo

- dubletter mellom pakker og docs
- README-fortelling
- fallbackstige
- lokalt referanseregister og spør-regel
- repo-hygiene og tester for `llm-controller`

## Vent med dette

- n8n som tidlig arbeidsflate
- tung agentplattform som første lag
- offentlig repo som later som materialet allerede er konsolidert

# Er materialet klart nok til å formes til repoet `LLM-local`?

Nei, ikke ennå.

Minste neste nødvendige bearbeiding er én konsolideringspass som:

- velger kanoniske docs og prompts
- rydder `llm-controller` til repoform
- formaliserer fallbackstigen
- formaliserer lokalt referanseregister med "spør hvis ukjent"-regel

Først etter det gir det mening å lage et rent repooppsett.
