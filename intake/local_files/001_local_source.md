---
title: "local_llm local file source"
date: 2026-04-06
status: final
tags:[source, local_files, concept_context]
category: architecture
chunk_type: template
---

# Source Type

`local_files`

# Origin

lokale zip-filer, QA-notat og en lokal Python-controller på denne maskinen

# Raw Reference

- path or URL:
  - `C:\Users\larse\Downloads\local_llm_updated_packages.zip`
  - `C:\Users\larse\Downloads\local_llm_control_room_full_v2.zip`
  - `C:\Users\larse\Downloads\github_local_llm_qa_report.md`
  - `C:\Users\larse\Downloads\stifinner_mvp.zip`
  - `C:\Users\larse\Documents\Prosjekter\llm-controller`
- owner or source system:
  - lokale arbeidsfiler og lokal utviklingsmappe

# What It Contains

Denne kilden kombinerer:

- en samlet dokumentpakke for lokal LLM-arbeidsflyt
- en separat kontrollrom-zip som viser seg å være duplikat
- et QA-notat som begrunner stack- og rutingsvalg
- en enkel MVP-controller i zip-format
- en levende lokal controller-kodebase med CLI, MCP-wrapper, state og logger

# Sharing Guidance

- safe for Project:
  - kuraterte sammendrag og anbefalinger er trygge
- safe for GitHub:
  - bare renset controllerkode, utvalgte docs og prompts kan bli delbare senere
- must stay local:
  - rå zip-filer
  - absolutte stier
  - lokale logger, state og maskinspesifikke spor

# Notes

Samlepakken er primærkilden. `llm-controller` er viktig fordi den viser hva som
allerede er implementert, ikke bare hva dokumentene ønsker å få til.
