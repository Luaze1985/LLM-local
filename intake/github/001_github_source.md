---
title: "local_llm github source"
date: 2026-09-27
status: final
tags:[source, github, concept_context]
category: architecture
chunk_type: template
---

# Source Type

`github`

# Origin

Offentlig repo `alexadark/jev-openrouter-skill`, delt av brukeren som et
LinkedIn-innlegg om en Codex-skill som spør TypeSafe Jev (via OpenRouter) om
modell- og reasoning-effort-anbefaling før Codex selv gjør jobben.

# Raw Reference

- path or URL: `https://github.com/alexadark/jev-openrouter-skill`
- owner or source system: Alexandra Spalato (MIT-lisensiert)
- commit hentet: `7a281156d0d77046f072537c3b6883c08e1ecc31` (2026-09-25)
- lokal råkopi: `intake/github/raw/jev-openrouter-skill_2026-09-27.zip`

# What It Contains

En Codex CLI-skill (`jev-openrouter`) som:

- kaller OpenRouters alpha `Decisions`-endepunkt (`~typesafe/jev-latest`) for å
  få en strukturert modellanbefaling, aldri for å utføre selve oppgaven
- sammenligner en datert modellgrid: OpenAI `gpt-6-luna/sol/astra` (low/medium/
  high/xhigh), Claude Opus 5.5, og betinget DeepSeek V4.1 Flash via Ollama Cloud
- leser policy/profiler fra `references/model-profiles.json`, med valgfri
  kobling til en ekstern RIFF-katalog
- eksplisitt IKKE bytter aktiv modell, ikke starter oppgaven, og ikke sender
  hele repo/samtale til Jev — bare et bevisst avgrenset `state`

# Sharing Guidance

- safe for Project: ja, hele repoet er MIT-lisensiert og fritt for hemmeligheter
- safe for GitHub: ja, ingen API-nøkkel eller personlig data i kildekoden
- must stay local: en eventuell personlig `~/.config/jev-openrouter/preferences.json`
  eller `OPENROUTER_API_KEY` skal aldri legges i repoet

# Notes

Brukeren valgte eksplisitt (etter oppklaringsrunde) å få en ferdig tilpasset
skill-pakke for eget Codex CLI-oppsett nå, ikke bare en vurdering. Se
`deliverables/jev_openrouter_skill_review.md` og
`context_packets/github_ready/002_jev_openrouter_skill_ready.md` for hva som
faktisk er tilpasset og levert som nedlastbar pakke utenfor denne workspacen.
