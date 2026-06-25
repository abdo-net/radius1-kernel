# 01-META-MODEL

## Purpose

This directory contains the Repository Meta Model (RMM) — the universal ontology of the Radius1 Kernel. The RMM answers one question: "What exists inside this repository?" It defines every entity, how they relate, who owns them, and how they evolve.

## What Belongs Here

- `RMM_v1.1.md` — The canonical Repository Meta Model specification (Frozen)
- `CHANGELOG_v1_to_v1.1.md` — Change log from v1 to v1.1
- `VALIDATION_REPORT.md` — Validation report confirming zero defects
- `RMM_FUTURE_PROPOSALS.md` — Architectural proposals deferred to future releases
- Domain definitions, subsystem descriptions, and structural documentation

## What Is Forbidden Here

- Implementation code, scripts, or executable artifacts
- Product-specific business logic
- Operational workflows or procedures
- Governance policies or decision records (belong in `02-GOVERNANCE/`)
- Evidence or audit artifacts (belong in `05-EVIDENCE/`)
- Anything that violates the technology-independence mandate of the RMM

## Relation With the Rest of the Repository

- Derives authority from `00-CONSTITUTION/`
- Governs the entity model used by all other directories
- `02-GOVERNANCE/` uses RMM entities for roles, bodies, and policies
- `03-STANDARDS/` applies to entities defined in the RMM
- `04-PATTERNS/` operates on RMM structural entities
- All artifacts in other directories are instances of RMM entities
