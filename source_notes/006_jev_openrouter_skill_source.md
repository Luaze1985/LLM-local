---
title: "local_llm jev-openrouter-skill source"
date: 2026-09-27
status: final
tags:[source, github, concept_context]
category: architecture
chunk_type: concept
---

# Source Type

`github`

# Origin

`alexadark/jev-openrouter-skill`, MIT-lisensiert Codex CLI-skill delt av
brukeren via et LinkedIn-innlegg. Commit `7a281156d0d77046f072537c3b6883c08e1ecc31`
(2026-09-25).

# Raw Reference

- path or URL: `https://github.com/alexadark/jev-openrouter-skill`
- lokal råkopi: `intake/github/raw/jev-openrouter-skill_2026-09-27.zip`

# What It Contains

- `SKILL.md` — selve Codex-skilldefinisjonen (`allow_implicit_invocation: false`,
  må kalles eksplisitt med `$jev-openrouter`)
- `scripts/jev_decide.py` — kaller `https://openrouter.ai/api/alpha/decisions`,
  leser `OPENROUTER_API_KEY` fra miljøet, støtter `--dry-run`
- `scripts/model_catalog.py` — leser `references/model-profiles.json` (bundlet
  snapshot) eller en ekstern RIFF-katalog via `RIFF_MODEL_CATALOG` /
  `~/.config/jev-openrouter/catalog.json`
- `references/model-profiles.json` — datert modellgrid (2026-09-25.1): Luna/
  Sol/Astra (OpenAI), Opus 5.5 (Anthropic), DeepSeek V4.1 Flash (Ollama Cloud,
  betinget)
- `MODEL-GUIDE.md`, `README.md`, `index.html` — menneskelesbar guide og
  visuell håndbok
- `agents/openai.yaml` — display-navn og default-prompt for Codex sin
  skill-oppdagelse

Styrker:

- klart avgrenset ansvar: rådgivning, ikke utførelse eller auto-ruting
- ingen hemmeligheter i repoet, nøkkel hentes fra miljøvariabel
- eksplisitt filtreringslogikk for "OpenAI only" / "strictly local data"
- MIT-lisens, fritt å kopiere og tilpasse

Svakheter / ting som må vurderes før bruk:

- Codex-only v1 — ingen støtte for annet CLI-oppsett i selve skillen
- avhenger av et alpha-endepunkt (`openrouter.ai/api/alpha/decisions`) og en
  spesifikk modellkatalog (`gpt-6-luna/sol/astra`) som kan endre seg
- krever en OpenRouter-nøkkel med tilgang til Decisions-endepunktet — ekstra
  kostnad/oppsett utover eksisterende Codex-abonnement
- installasjonsinstruksjonene i README er kun for Unix-skall (bash), ingen
  PowerShell/Windows-oppskrift, selv om `jev_decide.py`/`model_catalog.py` er
  ren cross-platform Python

# Sharing Guidance

- safe for Project: ja
- safe for GitHub: ja, hele originalrepoet er allerede offentlig og MIT
- must stay local: en eventuell personlig `preferences.json` eller
  `OPENROUTER_API_KEY`

# Notes

Dette skiller seg fra resten av materialet i denne workspacen: det er ikke et
uferdig internt utkast, men en ferdig, fungerende ekstern skill. Den nyttige
jobben her er derfor ikke konsolidering, men et tilpasningspass (Windows/
Codex-oppsett for brukeren) pluss en ærlig vurdering av avhengigheter (alpha-
endepunkt, ekstra OpenRouter-kostnad) før brukeren kobler den inn i sin egen
Codex CLI.
