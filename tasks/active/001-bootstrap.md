---
title: "Bootstrap concept-context workspace"
date: 2026-04-06
status: done
tags:[task, concept-context]
category: task
chunk_type: task-definition
---

# Goal

Etablere en `concept_context`-workspace for `local_llm`, stage relevante lokale
kilder og produsere en reviewpakke som vurderer stoppvern, riktig LLM-ruting og
lav brukerfriksjon før eventuell repoforming.

# Context

Arbeidet starter fra blandede lokale kilder: zip-pakker, QA-notat og en levende
controllerkodebase. Målet er å skille mellom det som er nyttig, det som er
duplisert og det som fortsatt må revideres før noe blir `LLM-local`.

# Inputs

- files to inspect:
  - `intake/local_files/raw/local_llm_updated_packages.zip`
  - `intake/local_files/raw/local_llm_control_room_full_v2.zip`
  - `intake/local_files/raw/github_local_llm_qa_report.md.txt`
  - `intake/local_files/raw/stifinner_mvp.zip`
- decisions to honor:
  - behold `Ollama + Qwen3-Coder` som default
  - review-først, ikke repo-først
  - spør etter lokale referanser bare når de faktisk mangler
- external references if needed:
  - `C:\Users\larse\Documents\Prosjekter\llm-controller`

# Acceptance Criteria

- [x] The requested work is completed.
- [x] The chosen structure still matches the selected profile.
- [x] Tests or checks were run when relevant.
- [x] Validation notes are recorded before handoff.

# Expected Output

- created files:
  - `state/context/local_reference_registry.md`
  - `source_notes/001_combined_package_source.md`
  - `source_notes/002_control_room_duplicate_source.md`
  - `source_notes/003_qa_report_source.md`
  - `source_notes/004_stifinner_mvp_source.md`
  - `source_notes/005_llm_controller_source.md`
  - `deliverables/local_llm_package_review.md`
  - `deliverables/recommended_repo_structure.md`
  - `deliverables/next_codex_handoff.md`
- updated files:
  - workspace context files
  - concept packet files
  - checkpoint and intake summary
- follow-up work:
  - ett konsolideringspass før eventuell repooppretting

# Verification

- commands:
  - `python scripts/harness_validator.py`
  - `python -m unittest discover -s tests`
- evidence:
  - harness validation passed
  - 11 tests passed
- remaining risks:
  - ekstern QA-csv mangler fortsatt i `Downloads`
  - `llm-controller` trenger README, tester og fallbackstige før repoform
