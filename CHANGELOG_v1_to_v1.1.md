# CHANGELOG — RMM v1 → v1.1

**Release type:** Engineering bug-fix (no architecture change)
**Authoritative base:** RMM v1 (`Status: FINAL`, 79 entities, 10 matrices)
**Released as:** `RMM_v1.1.md` (`Status: RELEASED`, `Version: 1.1`)
**Scope rule:** Only objective engineering defects were corrected. No entity was added, removed, merged, split, renamed, or re-tiered. No relationship in the formal graph was added or deleted. Governance, lifecycle, ontology, and the repository model are unchanged.

**Integrity guarantee:** The Part II directed relationship graph (the normative relationship model) is **byte-for-byte identical** between v1 and v1.1 — verified programmatically (640 source edges, identical tuple list). Every change below is a correction to a *derived* statistic, a *terminology* token, or a *matrix cell*, never to the architecture.

---

## Summary of applied fixes

| # | Fix | Class | Surfaces touched |
|---|-----|-------|------------------|
| 1 | Entity count `78 → 79` in catalog summary heading | Contradiction | Part I summary |
| 2 | Relationship count `636 → 640` (actual edge count) | Inconsistent stat | Top stats, Part II metadata, Part II header, closing line, validation block |
| 3 | Average relationships/entity `16.1 → 16.2` | Inconsistent stat | Part II metadata |
| 4 | Relationship-types claim `30 → 201` and full legend regenerated with true per-type counts | Inconsistent stat | Part II "Relationship Types Used" |
| 5 | Per-entity inline degree headers (`#### X — A outgoing, B incoming`) recomputed | Inconsistent stat | Part II (58 headers were wrong) |
| 6 | Appendix A entity-statistics table recomputed (out/in/total) | Inconsistent matrix | Part II Appendix A (49 rows were wrong) |
| 7 | Appendix B hub figure `GovernanceBody (30 → 31 total)` | Inconsistent stat | Part II Appendix B |
| 8 | Owner alias `Governance Board → GovernanceBody` (canonical entity name) | Terminology / broken ref | 19 catalog `Owner` fields |
| 9 | `Stakeholder → Actor` (per RMM's own dedup decision) | Broken ref | Credential & Signature `Owner`; Sanction/Appeal/Dispute/Recusal `Allowed Relationships`; Matrix 1 column header; Matrix 9 cell |
| 10 | Matrix 1: removed dual-primary (self) ownership of **Process** and **Session** | Duplicated ownership | Matrix 1 rows 19, 34 |
| 11 | Matrix 1: cleared Actor self-secondary mark introduced by the column relabel | Consistency | Matrix 1 row 35 |
| 12 | Source-of-truth path casing `01-META-Model/ → 01-META-MODEL/` | Terminology | Catalog (State), Matrix 6 |
| 13 | Header: `Status: FINAL → RELEASED`, added `Version: 1.1` / revision note | Release metadata | Document header |
| 14 | Validation block rewritten to reflect the recomputed, honest state | Self-contradiction | Part I validation block |

---

## Detail and evidence

### 1. Entity count 78 → 79
- **Defect:** Top statistics and the tier breakdown both total **79**, but the Part I summary heading read `SUMMARY: 78 CANONICAL ENTITIES`.
- **Action:** `78 → 79`. Tier sum independently verified = 79.
- **Findings resolved:** R2-C4, R3-D2, R1-m11 (count discrepancy).

### 2–7. Relationship statistics recomputed from the actual graph
- **Defect:** The document claimed `636` relationships and `30 semantic types`. The actual Part II graph contains **640** directed edge lines (no duplicate edges) using **201** distinct directed relationship types. Derived tables were widely inconsistent with the graph: **58** inline `outgoing/incoming` headers and **49** Appendix A rows did not match the graph (e.g., `Concern` was listed as `0 incoming` though `Domain/Layer/Slice → crossed-by → Concern` give it 3; `TraceabilityLink` listed `2 incoming`, actually 4).
- **Action:** All counts recomputed *from the 640 unchanged edges* and written back:
  - Total relationships `636 → 640`; average `16.1 → 16.2`; types `30 → 201`.
  - Legend block regenerated; its per-type occurrences now sum to exactly 640.
  - Every inline degree header and every Appendix A row regenerated; 0 mismatches remain (verified).
  - Appendix B hub total for `GovernanceBody` `30 → 31`.
  - `Minimum 10` and `Maximum Outgoing 14 (GovernanceBody)` were already correct and were left unchanged.
- **Note:** The count was corrected *up to the graph* (640), **not** by deleting edges down to 636 — deleting relationships would be an architecture change. The "636" figure was the erroneous metadata; the 640 edges are the model.
- **Findings resolved:** R2-C5, R3-D1/D2, R1-m12/m13; Concern-incoming (R2-C6 statistic, R3-D1).

### 8. `Governance Board → GovernanceBody`
- **Defect:** 19 `Owner` fields used `Governance Board`, an alias that is **not** a canonical entity; the canonical governance entity is `GovernanceBody`.
- **Action:** Normalized all 19 to `GovernanceBody`. No governance authority changed — only the label now matches the entity it denotes.
- **Findings resolved:** R1-M11/M12, R2-C2 (alias portion), R3-C2 (alias portion).

### 9. `Stakeholder → Actor`
- **Defect:** RMM's own deduplication log states *"Stakeholder (Governance) → subsumed into Actor"*, yet `Stakeholder` survived as the `Owner` of Credential & Signature, as a Matrix 1 column, in a Matrix 9 cell, and in four `Allowed Relationships` clauses. The **formal graph already used `Actor`** for those same relations (`Sanction → on → Actor`, `Appeal → filed-by → Actor`, `Dispute → between → Actor`, `Recusal → withdraws → Actor`), so the prose contradicted the graph.
- **Action:** Replaced the surviving `Stakeholder` references with `Actor`, applying RMM's own subsumption decision. The historical dedup-log line itself was left intact (it documents the merge).
- **Rejected alternative:** "Restore Stakeholder as a separate entity" (R1-C09, R2-C1 Option A) — this *overrides* RMM's explicit dedup decision and is a forbidden entity addition. Routed to `RMM_FUTURE_PROPOSALS.md`.
- **Findings resolved:** R1-C09 (reference half), R2-C1 (Option B), R3-C3 (Stakeholder half).

### 10–11. Process / Session dual-primary ownership
- **Defect:** Matrix 1 marked **two** primary owners (`●`) for `Process` (Governance ● **and** Process ●) and `Session` (Governance ● **and** Session ●) — i.e., each entity owned itself, violating "every ownership is unique." Catalog `Owner` for both = the governance body (single owner).
- **Action:** Removed the self-referential primary mark, leaving a single primary owner (Governance ●) consistent with the catalog. The column relabel (Stakeholder→Actor) then left `Actor` with a vacuous self-secondary mark, which was cleared.
- **Scope guard:** A regex bug in an intermediate build had overwritten the Process/Session/Actor rows of *all ten* matrices with the ownership pattern; this was caught in verification and the edit was re-scoped to Matrix 1 only. Final verification confirms all other matrices' Process/Session/Actor rows are intact.
- **Findings resolved:** R2-M1, R3 (Matrix-1 self-ownership).

### 12. Path casing `01-META-Model → 01-META-MODEL`
- **Defect:** The `State` entity's source-of-truth used mixed casing (`01-META-Model/`) vs the uniform `01-META-MODEL/` everywhere else — a case-sensitive-filesystem hazard.
- **Action:** Normalized both occurrences (catalog + Matrix 6).
- **Findings resolved:** R2-M6, R3-m2.

### 13–14. Release metadata & honest validation block
- Header set to `Status: RELEASED`, `Version: 1.1`, supersedes RMM v1.
- The validation checklist (which in v1 asserted properties the document did not meet) was rewritten to the **recomputed, evidenced** state, with explicit pointers to `VALIDATION_REPORT.md` and `RMM_FUTURE_PROPOSALS.md` for the items deferred as architectural.

---

## What was deliberately **not** changed (and why)

Every finding that would require architecture work was excluded from this bug-fix release and is catalogued in `RMM_FUTURE_PROPOSALS.md` with a classification of `FUTURE_PROPOSAL` or `ARCHITECT_DECISION_REQUIRED`. Headlines:

- **No entities added** (Product, Namespace, Extension/CRD, Event, Port, Bridge, Adapter, Bus, EmergencyOverride, Stakeholder, LifecycleStage, …).
- **No entities merged/removed/degraded** (Exception+Waiver, Approval+Authorization, Finding+Conclusion, Decision+DecisionRecord, Topology, TraceabilityLink, Concern, View, Measurement, Snapshot, Review/Audit/Assessment).
- **No schema change** (Source-of-Truth and AI/Human-permission properties retained; no 16th property added).
- **No re-tiering, no renames** (the `Tier` entity vs catalog-"Tier" collision was left as-is).
- **No dependency-semantics redesign** (the Matrix 9 "Depends-On/Required-By" structural reciprocity was left intact; the downward *authority* subgraph was verified acyclic).
- **No governance change** (Invariant immutability, Constitution `Static`+`Versionable`, Founders-Circle owner left as authored).

See `RMM_FUTURE_PROPOSALS.md` for the full disposition of all ~140 review findings across the three review documents.
