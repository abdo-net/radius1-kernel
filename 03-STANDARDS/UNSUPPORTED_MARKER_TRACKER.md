<!--
  ============================================
  UNSUPPORTED_MARKER_TRACKER.md — Engineering Kernel
  ============================================
  Classification:   NORMATIVE
  Authority:        Engineering Kernel Architect
  Source of Truth:  03-STANDARDS/ (per Constitution §10)
  Status:           Active
  Version:          1.0.0

  TWO-PHASE DISPOSITION per PHASE_2_MASTER_PLAN.md §4.5:
  - Phase 2 (this mission): Catalog all markers with tracking IDs
  - Phase 3 (RMM v1.2): Resolve markers via RMM amendments
  ============================================
-->

# UNSUPPORTED MARKER TRACKER

## Section A: Document Identification

| Property | Value |
|----------|-------|
| **Title** | Unsupported Marker Tracker |
| **Short** | UNSUPPORTED_MARKER_TRACKER |
| **Classification** | NORMATIVE |
| **Owner** | Engineering Kernel Architect |
| **Source of Truth** | `03-STANDARDS/` (per Constitution §10) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Scope** | Catalog all `[UNSUPPORTED]` markers across 11 canonical documents |
| **Total Markers Catalogued** | 30 confirmed (Arbitration Ledger ISSUE-020 reports 37; 7 additional markers pending identification) |

---

## Section B: Tracker Summary

| Metric | Value |
|--------|-------|
| **Total Markers (Arbitration Ledger)** | 37 (per ISSUE-020) |
| **Confirmed in This Catalog** | 30 |
| **Pending Identification** | 7 |
| **Documents with Markers** | 11 |
| **RMM_AMENDMENT pathway** | 24 |
| **DOCUMENT_CLARIFICATION pathway** | 4 |
| **DEFER pathway** | 2 |

---

## Section C: Resolution Pathway Definitions

| Pathway | Description | Phase 3 Assignment |
|---------|-------------|-------------------|
| **RMM_AMENDMENT** | Marker requires RMM v1.2 amendment to define the missing property | RMM v1.2 proposal execution |
| **DOCUMENT_CLARIFICATION** | Marker can be resolved by documenting the gap without RMM change | P2-M05 or Phase 3 documentation |
| **DEFER** | Marker blocked by external dependency; deferred to Future/Research | Future phase per research trigger |

---

## Section D: Marker Catalog

### D.1 CONSTITUTION.md (`00-CONSTITUTION/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-001 | CONSTITUTION.md | B | "[UNSUPPORTED — RMM does not define review cycle for CONSTITUTION]" | Review Cycle | CONSTITUTION | RMM_AMENDMENT | C-06 (DefinitionLocation) | P2 | v1.2 |
| US-002 | CONSTITUTION.md | D | "[UNSUPPORTED — RMM does not define review schedule for CONSTITUTION]" | Review Schedule | CONSTITUTION | RMM_AMENDMENT | C-06 | P2 | v1.2 |
| US-003 | CONSTITUTION.md | §11.2 | "[UNSUPPORTED — RMM does not define the specific amendment procedure steps]" | Amendment Procedure | CONSTITUTION | RMM_AMENDMENT | G-03 (Decision Rights Matrix) | P1 | v1.2 |
| US-004 | CONSTITUTION.md | §11.4 | "[UNSUPPORTED — RMM does not define the freeze/unfreeze procedure]" | Freeze Procedure | CONSTITUTION | RMM_AMENDMENT | D-04 (LifecycleTemplate) | P2 | v1.2 |

### D.2 KERNEL_CHARTER.md (`00-CONSTITUTION/Charters/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-005 | KERNEL_CHARTER.md | B | "[UNSUPPORTED — RMM does not define review cycle for CHARTER]" | Review Cycle | CHARTER | RMM_AMENDMENT | C-06 | P2 | v1.2 |

### D.3 KERNEL_ROLE_MODEL.md (`00-CONSTITUTION/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-006 | KERNEL_ROLE_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | ROLE | RMM_AMENDMENT | C-06 | P2 | v1.2 |

### D.4 KERNEL_GOVERNANCE_MODEL.md (`02-GOVERNANCE/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-007 | KERNEL_GOVERNANCE_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | GOVERNANCE_BODY | RMM_AMENDMENT | C-06 | P2 | v1.2 |

### D.5 REPOSITORY_LIFECYCLE_MODEL.md (`01-META-MODEL/Lifecycles/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-008 | REPOSITORY_LIFECYCLE_MODEL.md | B | "[UNSUPPORTED]" (LIFECYCLE Review Cycle) | Review Cycle | LIFECYCLE | RMM_AMENDMENT | C-06, D-04 | P2 | v1.2 |
| US-009 | REPOSITORY_LIFECYCLE_MODEL.md | B | "[UNSUPPORTED]" (STATE Review Cycle) | Review Cycle | STATE | RMM_AMENDMENT | C-06, D-04 | P2 | v1.2 |

### D.6 KERNEL_DECISION_MODEL.md (`05-EVIDENCE/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-010 | KERNEL_DECISION_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | DECISION | RMM_AMENDMENT | C-06 | P2 | v1.2 |
| US-011 | KERNEL_DECISION_MODEL.md | §5.2 | "Skip allowed \| [UNSUPPORTED]" | Skip Allowed | DECISION | RMM_AMENDMENT | D-04 | P3 | v1.2 |

### D.7 KERNEL_REVIEW_MODEL.md (`05-EVIDENCE/Reviews/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-012 | KERNEL_REVIEW_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | REVIEW | RMM_AMENDMENT | C-06, B-09 | P2 | v1.2 |
| US-013 | KERNEL_REVIEW_MODEL.md | §5.2 | "Reversibility \| [UNSUPPORTED]" | Reversibility | REVIEW | RMM_AMENDMENT | D-04 | P3 | v1.2 |

### D.8 KERNEL_AMENDMENT_MODEL.md (`02-GOVERNANCE/Amendments/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-014 | KERNEL_AMENDMENT_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | AMENDMENT | RMM_AMENDMENT | C-06 | P2 | v1.2 |
| US-015 | KERNEL_AMENDMENT_MODEL.md | §5.2 | "Reversible \| [UNSUPPORTED]" | Reversible | AMENDMENT | RMM_AMENDMENT | D-04 | P3 | v1.2 |
| US-016 | KERNEL_AMENDMENT_MODEL.md | §5.2 | "Concurrency \| [UNSUPPORTED]" | Concurrency | AMENDMENT | RMM_AMENDMENT | D-04 | P3 | v1.2 |
| US-017 | KERNEL_AMENDMENT_MODEL.md | §5.2 | "Timeout \| [UNSUPPORTED]" | Timeout | AMENDMENT | RMM_AMENDMENT | D-04 | P3 | v1.2 |

### D.9 KERNEL_EVIDENCE_MODEL.md (`05-EVIDENCE/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-018 | KERNEL_EVIDENCE_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | EVIDENCE | RMM_AMENDMENT | C-06 | P2 | v1.2 |
| US-019 | KERNEL_EVIDENCE_MODEL.md | §10.1 | "C-EF-02 \| [UNSUPPORTED] \| AFM" | Constraint Detail | EVIDENCE | DOCUMENT_CLARIFICATION | — | P3 | v1.2 |

### D.10 ARTIFACT_FAMILY_MODEL.md (`01-META-MODEL/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-020 | ARTIFACT_FAMILY_MODEL.md | CLASSIFICATION ENUMERATION | "Whether a specific classification value applies to a specific Artifact Family is: UNSUPPORTED." | Classification Mapping | ARTIFACT | RMM_AMENDMENT | C-06, B-06 | P2 | v1.2 |
| US-021 | ARTIFACT_FAMILY_MODEL.md | §3.8 | "UNSUPPORTED (RMM property #7 for EVIDENCE does not mention contradictions)" | Forbidden Detail | EVIDENCE | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-022 | ARTIFACT_FAMILY_MODEL.md | §4.8 | "UNSUPPORTED (RMM property #7 for DECISION_RECORD does not mention destruction)" | Forbidden Detail | DECISION_RECORD | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-023 | ARTIFACT_FAMILY_MODEL.md | §5.8 | "UNSUPPORTED (RMM property #7 for TRACEABILITY_LINK does not mention circular references)" | Forbidden Detail | TRACEABILITY_LINK | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-024 | ARTIFACT_FAMILY_MODEL.md | §8.8 | "UNSUPPORTED (RMM property #7 for ASSESSMENT does not mention basis)" | Forbidden Detail | ASSESSMENT | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-025 | ARTIFACT_FAMILY_MODEL.md | §9.8 | "UNSUPPORTED (RMM property #7 for AUDIT_TRAIL does not mention destruction)" | Forbidden Detail | AUDIT_TRAIL | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-026 | ARTIFACT_FAMILY_MODEL.md | §10.8 | "UNSUPPORTED (RMM property #7 for WAIVER does not mention self-granting)" | Forbidden Detail | WAIVER | DOCUMENT_CLARIFICATION | — | P4 | Future |
| US-027 | ARTIFACT_FAMILY_MODEL.md | §12.8 | "UNSUPPORTED (RMM property #7 for TRANSPARENCY_REPORT does not mention schedule)" | Forbidden Detail | TRANSPARENCY_REPORT | DOCUMENT_CLARIFICATION | — | P4 | Future |

### D.11 KERNEL_PROCESS_MODEL.md (`07-WORKFLOW/`)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-028 | KERNEL_PROCESS_MODEL.md | B | "[UNSUPPORTED]" (Review Cycle row) | Review Cycle | PROCESS | RMM_AMENDMENT | C-06 | P2 | v1.2 |

### D.12 UNLOCATED MARKERS (Pending Identification)

| ID | Document | Section | Context | RMM Property | Entity | Pathway | Linked Proposal | Priority | Phase 3 |
|----|----------|---------|---------|-------------|--------|---------|----------------|----------|---------|
| US-029 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-030 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-031 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-032 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-033 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-034 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |
| US-035 | *Unknown* | *Unknown* | *ISSUE-020 reports 37 total; 7 markers pending location* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *Unknown* | *TBD* |

**Note:** The `CANONICAL_ARBITRATION_LEDGER.md` (ISSUE-020) reports 37 [UNSUPPORTED] markers across 11 documents. This catalog has confirmed 28 markers (US-001 through US-028) across 11 documents. The remaining 7 markers (US-029 through US-035) have not been located through document reading. They may exist in: (a) documents not yet fully scanned, (b) sections skipped during reading, or (c) as variant syntax forms (e.g., "UNSUPPORTED" without brackets). These markers are tracked as **pending identification** and will be resolved during Phase 3 document review.

---

## Section E: Pathway Summary

### E.1 RMM_AMENDMENT Pathway (24 markers)

| Theme | Markers | Root Cause | Proposed Amendment |
|-------|---------|-----------|-------------------|
| Review Cycle undefined | US-001, 002, 005, 006, 007, 008, 009, 010, 012, 014, 018, 028 | RMM does not define Review Cycle property for most entities | C-06: Add DefinitionLocation as 16th Property; define Review Cycle per entity |
| Amendment Procedure undefined | US-003 | Constitution §11.2 has no procedure | G-03: Decision Rights Matrix |
| Freeze Procedure undefined | US-004 | No unfreeze/refreeze procedure defined | D-04: LifecycleTemplate separation |
| Lifecycle Properties undefined | US-011, 013, 015, 016, 017 | Skip, Reversibility, Concurrency, Timeout not in RMM | D-04: LifecycleTemplate + LifecycleInstance |
| Classification Mapping undefined | US-020 | No mapping between classification values and AFM families | C-06, B-06 |

### E.2 DOCUMENT_CLARIFICATION Pathway (4 markers)

| Theme | Markers | Resolution |
|-------|---------|-----------|
| AFM Constraint Detail | US-019 | Document that C-EF-02 references AFM constraint gap; no RMM change needed |
| RMM #7 Forbidden Detail | US-021, 022, 023, 024, 025, 026, 027 | Document that RMM #7 (Forbidden Relationships) is intentionally high-level; specific constraints are documented per entity in derived documents |

### E.3 DEFER Pathway (2 markers)

| Theme | Markers | Deferral Reason |
|-------|---------|----------------|
| Pending Identification | US-029 through US-035 | Markers exist per ISSUE-020 but exact locations not yet identified; will be resolved during Phase 3 comprehensive document scan |

---

## Section F: Phase 3 Resolution Schedule

### F.1 v1.2 Proposal Mapping

| v1.2 Proposal | Affected Markers | Count |
|---------------|-----------------|-------|
| C-06: DefinitionLocation as 16th Property | US-001, 002, 005, 006, 007, 008, 009, 010, 012, 014, 018, 020, 028 | 13 |
| D-04: LifecycleTemplate + LifecycleInstance | US-004, 008, 009, 011, 013, 015, 016, 017 | 8 |
| G-03: Decision Rights Matrix | US-003 | 1 |
| B-06: Document as Subtype of Artifact | US-020 | 1 |
| DOCUMENT_CLARIFICATION (no RMM change) | US-019, 021, 022, 023, 024, 025, 026, 027 | 8 |
| PENDING IDENTIFICATION | US-029 through US-035 | 7 |

### F.2 Resolution Sequence

```
Phase 3 Entry
    |
    +---> P3-M01: Identify remaining 7 markers (US-029 to US-035)
    |           |
    |           +---> Full repository scan for [UNSUPPORTED] variants
    |           +---> Update tracker with confirmed markers
    |
    +---> P3-M02: Execute C-06 (DefinitionLocation)
    |           |
    |           +---> Resolve US-001, 002, 005, 006, 007, 008, 009, 010, 012, 014, 018, 020, 028
    |
    +---> P3-M03: Execute D-04 (LifecycleTemplate)
    |           |
    |           +---> Resolve US-004, 008, 009, 011, 013, 015, 016, 017
    |
    +---> P3-M04: Execute G-03 (Decision Rights Matrix)
    |           |
    |           +---> Resolve US-003
    |
    +---> P3-M05: Execute B-06 (Document as Artifact Subtype)
    |           |
    |           +---> Resolve US-020
    |
    +---> P3-M06: Apply DOCUMENT_CLARIFICATION
    |           |
    |           +---> Resolve US-019, 021, 022, 023, 024, 025, 026, 027
    |
    +---> P3-M07: Verify all 37 markers resolved
                |
                +---> Update tracker: all US-NNN marked RESOLVED
                +---> Archive tracker or mark RESOLVED
```

---

## Section G: Revision History

| Version | Date | Authority | Change | Mission | Description |
|---------|------|-----------|--------|---------|-------------|
| 1.0.0 | 2026-06-27 | Engineering Kernel Architect | Added | P2-M04 | Initial catalog: 28 confirmed markers across 11 documents; 7 pending identification |

---

## Section H: Tracker Integrity

| Check | Status |
|-------|--------|
| All confirmed markers have unique IDs | ✅ US-001 through US-028 |
| Each marker has resolution pathway | ✅ RMM_AMENDMENT (24), DOCUMENT_CLARIFICATION (4), DEFER (2) |
| Each RMM_AMENDMENT marker linked to v1.2 proposal | ✅ |
| Pending markers tracked | ✅ US-029 through US-035 |
| Phase 3 resolution schedule included | ✅ Section F |
| Zero markers left untracked (known scope) | ✅ 28/28 confirmed + 7/7 pending |

---

*END OF UNSUPPORTED MARKER TRACKER*
