---
title: "Workspace AGENTS for local_llm"
date: 2026-04-06
status: final
tags:[workspace, agents, concept_context]
category: architecture
chunk_type: process
---

# Workspace AGENTS

Denne workspacen følger `concept_context` og er review-først.

## Working Rules

- ikke bygg sluttrepo eller ny arkitektur i denne workspacen
- bruk `state/context/local_reference_registry.md` som sannhetskilde for kjente
  lokale referanser
- hvis en lokal referanse mangler for neste steg, si eksplisitt hva som mangler
  i stedet for å gjette
- vurder alt materiale ut fra tre mål:
  - hindre stopp
  - bruke riktig LLM for oppgaven
  - redusere bryderi for brukeren
- hold råmateriale under `intake/**/raw/`
- hold vurderinger og anbefalinger i `deliverables/`

## Validate Before Handoff

```powershell
python ..\..\scripts\harness_validator.py
python -m unittest discover -s ..\..\tests
```
