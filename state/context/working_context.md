---
title: "local_llm working context"
date: 2026-04-06
status: final
tags:[context, workspace, concept_context]
category: architecture
chunk_type: template
---

# Current Goal

Produsere en konkret og ærlig gjennomgang av lokal-LLM-materialet, med særlig
vekt på stoppvern, fallback, riktig LLM-ruting og lav brukerfriksjon.

# Decisions to Respect

- decision: bruk `concept_context` og hold arbeidet review-først
- decision: behold `Ollama + Qwen3-Coder` som tydelig default, men ikke som
  eneste legitime rute
- decision: behandle `local_llm_updated_packages.zip` som primær dokumentkilde
- decision: behandle `llm-controller` som sterkeste faktiske kodekilde
- decision: krev at fremtidig opplegg kjenner lokale referanser og spør hvis en
  nødvendig referanse mangler

# Sources Reviewed

- `intake/local_files/raw/local_llm_updated_packages.zip`
- `intake/local_files/raw/local_llm_control_room_full_v2.zip`
- `intake/local_files/raw/github_local_llm_qa_report.md.txt`
- `intake/local_files/raw/stifinner_mvp.zip`
- `C:\Users\larse\Documents\Prosjekter\llm-controller`

# What Currently Reduces Stops

- dokumentpakken beskriver stoppsignaler, timeout, retry og fallback som
  arbeidsprinsipper
- `llm-controller` har faktisk timeout, retry-løkke, kontekstkrymping,
  validator og state/logg
- `stifinner_mvp` viser en enkel Windows-først referanseflyt med state og
  rapportering

# What Still Creates Friction

- control-room-delen er duplisert både som egen zip og inne i samlepakken
- flere nøkkeldokumenter er fortsatt `draft`
- ekstern `github_local_llm_qa_report.csv` mangler i `Downloads`
- `llm-controller` mangler README, tester og ryddig repo-fortelling
- `llm-controller` har retry, men ikke full modell- eller provider-fallback
- faktiske kjøringer viser både `Not Found`, timeout og en hengende `running`
  status i state

# Open Questions

- question: hvor mye av `llm-controller` bør bli kanonisk kodebase i et senere
  repo, og hvor mye bør bare informere strukturen?
- question: bør fremtidig repo bruke en enkel `controller/`-pakke eller fortsatt
  legge Python-koden under `scripts/`?
- question: hvordan bør et delbart lokalt referanseregister se ut uten å lekke
  brukerens absolutte stier?

# Next Output

De viktigste neste outputene er hovedreviewet, anbefalt repo-struktur og et
kort neste-pass-handoff som peker på minste nødvendige konsolidering før
eventuell repoforming.
