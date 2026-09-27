---
title: "jev-openrouter-skill github-ready note"
date: 2026-09-27
status: final
tags:[github, handoff, concept_context]
category: architecture
chunk_type: template
---

# Ready to Share

- hele `intake/github/raw/jev-openrouter-skill_2026-09-27.zip` — allerede
  offentlig, MIT-lisensiert, ingen hemmeligheter
- den tilpassede pakken (`SKILL.md`, `scripts/`, `references/`, `README.md`,
  `MODEL-GUIDE.md`, `index.html`, `LICENSE`, ny `README-NO.md`) — levert
  direkte til brukeren som nedlastbar zip, ikke committet inn i denne
  workspacen som ny arkitektur

# Keep Local

- brukerens `OPENROUTER_API_KEY`
- en eventuell personlig `~/.config/jev-openrouter/preferences.json` eller
  `catalog.json` med brukerens egen RIFF-katalogsti
- ev. fremtidig kobling til `llm-controller` eller OpenClaw — ikke del av
  denne runden, og skal ikke antas

# Cleanup Before Push

- ingen — originalrepoet inneholder ingen maskinspesifikke stier, loggfiler
  eller nøkler. Den tilpassede kopien legger bare til én ny dokumentfil
  (`README-NO.md`), ingen sanering nødvendig.

# Commit Scope

Denne workspacens git-tre får kun dokumentasjonssporet: råkopi i
`intake/github/raw/`, kildenotat, konsept, denne noten og reviewet i
`deliverables/`. Selve den ferdige, tilpassede skill-pakken går til brukeren
som fil, ikke som ny mappe/arkitektur i `LLM-local`-repoet — i tråd med
AGENTS.md sin regel om at denne workspacen ikke skal bygge sluttrepo, og etter
brukerens eget, eksplisitte valg om at leveransen skal være en nedlastbar
pakke for eget Codex CLI-oppsett.
