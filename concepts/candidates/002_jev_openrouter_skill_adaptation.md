---
title: "jev-openrouter-skill adaptation concept"
date: 2026-09-27
status: final
tags:[concept, concept_context]
category: architecture
chunk_type: template
---

# Concept

En personlig, Windows/Codex-tilpasset kopi av `jev-openrouter-skill` som kan
droppes rett i brukerens eget Codex CLI-skillbibliotek, uten å røre
`llm-controller` eller OpenClaw-oppsettet.

# Problem

Originalskillen er ferdig og fungerende, men README dekker bare bash/Unix-
installasjon og forutsetter at brukeren selv finner riktig skill-mappe og
setter miljøvariabelen manuelt. Uten en liten tilpasning må brukeren selv
oversette hvert steg til PowerShell og selv huske sikker håndtering av
`OPENROUTER_API_KEY`.

# Inputs

- source note: `source_notes/006_jev_openrouter_skill_source.md`
- avklaring fra bruker: full tilpasset pakke nå, mål er Codex CLI direkte
  (ikke llm-controller, ikke OpenClaw), ingen mellomstopp

# Shape

- target users: brukeren selv i sitt eget Codex CLI-oppsett på Windows
- main workflow: kopiere skillen uendret i logikk, legge til en norsk,
  PowerShell-basert oppsettsguide og en tydelig personlig-bruk-merkelapp
- likely outputs:
  - nedlastbar zip med tilpasset `README-NO.md` + uendret `SKILL.md`/scripts/
    references
  - kort vurdering i `deliverables/jev_openrouter_skill_review.md`
  - github_ready-notat om hva som er delbart og hva som må holdes lokalt

# Open Questions

- question: skal brukeren senere koble skillens rådgivning til
  `llm-controller` sin egen modell-ruting, eller forbli en frittstående
  Codex-only rådgiver? (utenfor scope for denne runden — brukeren valgte
  Codex CLI direkte)
- question: er en OpenRouter-nøkkel med tilgang til alpha
  Decisions-endepunktet allerede anskaffet, eller er det neste steg brukeren
  må gjøre selv før skillen virker?
