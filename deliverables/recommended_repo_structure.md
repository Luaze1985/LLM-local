---
title: "local_llm recommended repo structure"
date: 2026-04-06
status: final
tags:[repo, structure, local-llm, concept_context]
category: architecture
chunk_type: report
---

# Summary

Et senere `LLM-local`-repo bør være en konsolidert, stopp-sikker arbeidsflate
for lokal analyse og kontrollert hybrid eskalering. Repoet bør ikke ta inn rå
zip-er eller maskinspesifikk state. Det bør i stedet samle renset controllerkode,
kanoniske docs, operative prompts og en tydelig kontrakt for lokale referanser.

# What Should Live In The Repo

- `README.md`
- `docs/`
- `prompts/`
- `controller/` eller `src/controller/` for faktisk Python-kode
- `scripts/` for tynne kjøre- og hjelpeinnganger
- `config/`
- `reference/` for liten, kuratert bakgrunn som fortsatt er nyttig

# What Should Live In docs

- `docs/01_overview.md`
  - hva repoet er
  - hva repoet ikke er
- `docs/02_default_stack_and_routing.md`
  - defaultvalg
  - når lokal er nok
  - når hybrid tar over
- `docs/03_stop_rules_and_fallbacks.md`
  - timeout
  - retry
  - fallbackstige
  - recovery
- `docs/04_local_reference_contract.md`
  - hva lokale referanser er
  - hva som må være kjent før bredere arbeid
  - "spør hvis ukjent"-regelen
- `docs/05_hybrid_handoff.md`
  - når Claude eller Codex bør overta
- `docs/06_n8n_later.md`
  - hvorfor n8n er senere lag
- `docs/07_qa_validation.md`
  - kort oppsummering av QA-funn som støtter stackvalgene

# What Should Live In prompts

- `prompts/router_prompt.md`
- `prompts/local_repo_agent_prompt.md`
- `prompts/handoff_prompt.md`
- `prompts/prompt_back_template.md`
- `prompts/codex_task_prompt.md`
- `prompts/claude_reasoning_prompt.md`

Alle promptene bør oppdateres så de alltid krever:

1. kjente lokale referanser
2. manglende lokale referanser
3. minste nyttige neste arbeidsenhet
4. anbefalt modell eller rute og hvorfor

# What Should Live In controller

Bruk `llm-controller` som base og flytt inn rensede versjoner av:

- `controller.py`
- `mcp_server.py`
- `core/repo_scanner.py`
- `core/context_builder.py`
- `core/llm_runner.py`
- `core/state_manager.py`
- `core/validator.py`

Legg samtidig til:

- README for controllerdelen
- en enkel testpakke
- tydelig skille mellom kode og runtime-data

# What Should Live In scripts

`scripts/` bør bare holde tynne entrypoints og hjelpeverktøy, for eksempel:

- `run_local_scan.ps1`
- `review_repo.ps1`
- `export_reference_registry_example.ps1`
- `validate_local_setup.ps1`

Selve Python-logikken bør ikke bo løst i `scripts/` hvis målet er en ryddig og
testbar kodebase.

# What Should Live In config

- `config/defaults.yaml`
  - default runtime
  - default modell
  - kontekstgrenser
  - timeout og retry
- `config/local_reference_registry.example.yaml`
  - delbar eksempelstruktur uten private paths

Ved senere repoform bør en bruker-spesifikk `local_reference_registry.local.yaml`
være `.gitignore`-et.

# What Should Stay In Local Staging

- rå zip-pakker
- standalone QA-arbeidskopier
- absolutte stier
- `llm-controller/logs/`
- `llm-controller/state/`
- `__pycache__/`
- maskinspesifikke prøvefiler og scratch-notater

# Recommended Fallback Ladder

Repoet bør beskrive denne operative standarden:

1. default: `Ollama + Qwen3-Coder`
2. ved feil: mindre kontekst
3. ved ny feil: alternativ lokal modell eller provider
4. ved fortsatt høy usikkerhet eller bred oppgave: hybrid
5. spør om ny lokal referanse bare hvis sannhetskilden faktisk mangler

# How GitHub-QA Findings Should Be Incorporated

- legg QA som kort, kuratert evidens i `docs/07_qa_validation.md`
- bruk QA-funnene til å begrunne default-stack og reservevalg
- ikke ta inn hele rå arbeidsrunden som styrende struktur
- gjør QA til beslutningsstøtte, ikke til en ny kilde for dubletter

# Recommended First Consolidation Scope

Før repooppretting bør én konsolideringspass gjøre dette:

- velg kanoniske docs fra control-room og context-pack
- rydd `llm-controller` til delbar kode
- skriv én tydelig README
- formaliser lokalt referanseregister og prompt-back-kontrakt

Først etter det er repooppretting verdt innsatsen.
