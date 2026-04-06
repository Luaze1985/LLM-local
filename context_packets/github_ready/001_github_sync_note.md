---
title: "local_llm GitHub sync note"
date: 2026-04-06
status: final
tags:[github, handoff, concept_context]
category: architecture
chunk_type: template
---

# Ready to Share

- `deliverables/local_llm_package_review.md`
- `deliverables/recommended_repo_structure.md`
- utvalgte og omskrevne docs/prompts etter én konsolideringspass
- renset controllerkode basert på `llm-controller`, men ikke rå repoet slik det
  står nå

# Keep Local

- `intake/local_files/raw/`
- `state/context/local_reference_registry.md`
- absolutte stier til lokale repoer
- `llm-controller/logs/`
- `llm-controller/state/`
- `llm-controller/core/__pycache__/`

# Cleanup Before Push

- sanitize:
  - fjern absolute stier og maskinspesifikke detaljer
- remove:
  - pycache, kjøringslogger, lokale state-filer og rå zip-drop
- rename:
  - slå sammen dublerte docs til én kanonisk mappe- og navnestruktur

# Commit Scope

Minste fornuftige delbare scope er ikke råmaterialet, men en konsolidert pakke
med README, utvalgte docs/prompts og en ryddet controller-modul. Alt før det
vil dele for mye støy og for lite beslutning.
