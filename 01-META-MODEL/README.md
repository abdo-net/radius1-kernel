# 01-META-MODEL

**Status:** CANONICAL  
**Stability:** Static  
**Version:** v1.1 (RELEASED)  
**Owner:** GovernanceBody

---

## Purpose

This directory contains the Repository Meta Model (RMM) — the complete, canonical specification of all entities, relationships, and matrices that define the RADIUS1 Kernel ontology. The RMM is the single source of truth for the structural and semantic foundation of the entire system.

## Contents

| Document | Purpose |
|----------|---------|
| `RMM_v1.1.md` | Complete RMM specification — entity catalog (79 entities), relationship graph (639 relationships), and 10 matrices |
| `CHANGELOG_v1_to_v1.1.md` | Detailed changelog of all 21 engineering corrections from v1 to v1.1 |
| `VALIDATION_REPORT.md` | Formal validation report confirming v1.1 passes all 8 checks |
| `RMM_FUTURE_PROPOSALS.md` | 56 deferred architectural proposals organized by category and priority |

## Statistics

| Metric | Value |
|--------|-------|
| Canonical Entities | 79 |
| Total Relationships | 639 |
| Relationship Types | 201 |
| Matrices | 10 |
| Entity Tiers | 20 |
| Properties per Entity | 15 |
| Total Property Definitions | 1,185 |
| Estimated Total Cells | ~4,950 |

## Deduplication Summary

- Raw entities discovered: ~335 across 4 domains
- Entities eliminated: ~256 (implementation-specific, control flow, derived, temporal, quality gate, internal mechanics)
- Cross-domain merges: 30+
- Final canonical set: 79 entities

## Matrices

1. **Ownership Matrix** — Who owns what
2. **Lifecycle Matrix** — Lifecycle definitions per entity
3. **Stability Classification** — Static / Slow / Moderate / Fast
4. **Versionability Matrix** — Yes / No per entity
5. **Freeze Matrix** — What can be frozen
6. **Source-of-Truth Matrix** — Where each entity's truth lives
7. **Creation & Modification Permissions** — AI vs Human creatable/modifiable
8. **Cardinality Matrix** — Multiplicity constraints
9. **Dependency Matrix** — Cross-entity dependencies
10. **Glossary** — Term definitions

## Validation Status

- [x] Every entity has all 15 properties
- [x] Every relationship is explicit (639 total)
- [x] Every ownership references a canonical entity (v1.1: 19 normalized)
- [x] No circular authority in governance chain
- [x] No undefined concepts in entity catalog (v1.1: dangling refs removed)
- [x] No duplicated entities
- [~] Source-of-Truth paths reflect repository structure (by design, non-normative)
- [~] Technology-independent at conceptual layer; storage paths are deployment-specific

---

*The RMM is frozen at v1.1. All changes require governance body approval and follow the amendment procedure defined in the Constitution.*
