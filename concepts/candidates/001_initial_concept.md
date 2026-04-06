---
title: "local_llm concept note"
date: 2026-04-06
status: final
tags:[concept, concept_context]
category: architecture
chunk_type: template
---

# Concept

Et stopp-sikkert, lokal-først kontrollrom for LLM-arbeid på egen PC som velger
en god default, holder state, kjenner lokale referanser og eskalerer til annen
modell eller hybrid før brukeren blir sittende fast.

# Problem

Materialet er lovende, men ligger i flere pakker med ulik modenhet. Uten en
gjennomgang blir resultatet lett dupliserte dokumenter, utydelig fallback og
for mye bryderi for brukeren når en lokal modell stopper eller mangler kontekst.

# Inputs

- source note: `source_notes/001_combined_package_source.md`
- source note: `source_notes/004_stifinner_mvp_source.md`
- source note: `source_notes/005_llm_controller_source.md`

# Shape

- target users: deg som lokal operatør og neste Codex-pass
- main workflow: lokal referansebevisst review, deretter konsolidering før repo
- likely outputs:
  - hovedreview
  - anbefalt repoform
  - tydelig fallback- og referansekontrakt

# Open Questions

- question: hvor mye av controllerkoden er klar nok til å være kanonisk?
- question: hvilken minste konsolidering må gjøres før `LLM-local` finnes som
  ren repoform?
