---
title: "local_llm local reference registry"
date: 2026-04-06
status: final
tags:[references, local-files, concept_context]
category: architecture
chunk_type: process
---

# Purpose

Dette dokumentet er workspace-sannhetskilden for kjente lokale referanser.
Fremtidige arbeidsflyter skal bruke denne oversikten før de gjetter, og de skal
spørre eksplisitt når en nødvendig lokal referanse ikke finnes her.

# Known References

- `local_llm_updated_packages.zip`
  - path: `C:\Users\larse\Downloads\local_llm_updated_packages.zip`
  - type: `zip`
  - role: primær dokumentkilde
  - sharing: må kurateres før Project eller GitHub

- `local_llm_control_room_full_v2.zip`
  - path: `C:\Users\larse\Downloads\local_llm_control_room_full_v2.zip`
  - type: `zip`
  - role: duplikatbekreftelse for control-room-delen i samlepakken
  - sharing: ikke nødvendig som egen delbar kilde

- `github_local_llm_qa_report.md`
  - path: `C:\Users\larse\Downloads\github_local_llm_qa_report.md`
  - type: `doc`
  - role: QA-grunnlag for modell- og stackvalg
  - sharing: kan oppsummeres videre

- `github_local_llm_qa_report.csv`
  - path: mangler som egen fil i `C:\Users\larse\Downloads`
  - type: `doc`
  - role: finnes bare inne i samlepakken per denne gjennomgangen
  - sharing: ikke bruk som ekstern filreferanse uten ny bekreftelse

- `stifinner_mvp.zip`
  - path: `C:\Users\larse\Downloads\stifinner_mvp.zip`
  - type: `zip`
  - role: enkel referansecontroller for Windows-først testing
  - sharing: kan brukes som kuratert referanse senere

- `llm-controller`
  - path: `C:\Users\larse\Documents\Prosjekter\llm-controller`
  - type: `repo`
  - role: sterkeste faktiske implementasjonskilde
  - sharing: kode kan renses og deles senere, men repoet som helhet må først
    ryddes

# Internal Truth Files For llm-controller

- `config.yaml`
- `controller.py`
- `mcp_server.py`
- `core/repo_scanner.py`
- `core/context_builder.py`
- `core/llm_runner.py`
- `core/state_manager.py`
- `core/validator.py`
- `state/progress.json`
- `state/repo_index.json`

# Use Rules

- oppgi alltid hvilke kjente lokale referanser som allerede brukes
- ikke anta at en fil finnes hvis den ikke er bekreftet her eller i repoet
- hvis neste steg krever en ny lokal referanse, be om:
  - sti
  - hva referansen er
  - hvorfor den er relevant
- hold rå, absolutte stier lokale og ikke behandle dem som GitHub-klare data

# Missing Reference Trigger

Spør tilbake før videre arbeid når minst ett av disse gjelder:

- neste steg krever et repo, dokument eller config som ikke finnes i registeret
- det er uklart hvilken lokal kilde som er kanonisk
- en ekstern referanse nevnes, men bare en innebygd eller eldre kopi er kjent
- en ny oppgave krever lokal sannhetskilde for å unngå spekulasjon

# Prompt-Back Contract

Fremtidige prompts bør kreve fire faste punkter:

1. hvilke lokale referanser agenten allerede kjenner
2. hvilke lokale referanser som mangler
3. hvilken minste nyttige neste arbeidsenhet som unngår stopp
4. hvilken modell eller rute som anbefales og hvorfor
