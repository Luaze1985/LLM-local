---
title: "local_llm llm-controller source"
date: 2026-04-06
status: final
tags:[source, local_files, concept_context]
category: architecture
chunk_type: concept
---

# Source Type

`local_files`

# Origin

Lokal Python-kodebase i `C:\Users\larse\Documents\Prosjekter\llm-controller`.

# Raw Reference

- path or URL: `C:\Users\larse\Documents\Prosjekter\llm-controller`
- owner or source system: lokal utviklingsmappe

# What It Contains

Repoet inneholder en faktisk controllerimplementasjon med:

- `controller.py` som CLI
- `mcp_server.py` som MCP-wrapper
- `core/`-moduler for scanning, kontekstbygging, LLM-kall, validering og state
- `config.yaml` med runtime- og scanning-parametre
- `state/` og `logs/` fra ekte kjøringer

Styrker:

- har faktisk timeout, retry og state
- krymper kontekst ved nye forsøk
- skiller scanning, promptbygging, kjøring og validering
- viser en realistisk bro til MCP

Svakheter:

- mangler README
- mangler tester
- blander kode med logger, state og `__pycache__`
- har ikke full modell- eller provider-fallback
- faktiske state-filer viser `Not Found`, timeout og hengende kjøringer

# Sharing Guidance

- safe for Project: ja, som oppsummert implementasjonskilde
- safe for GitHub: kode etter opprydding, README og test/kontraktsarbeid
- must stay local: rå state, logger, absolutte paths og maskinspesifikke spor

# Notes

Dette er den sterkeste faktiske kodekilden i materialet og bør være første
kandidat når senere repoform trenger controllerkode.
