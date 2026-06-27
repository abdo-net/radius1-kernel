<!--
  ============================================
  CROSS_DOCUMENT_VALIDATOR.md — Engineering Kernel
  ============================================
  Classification:   NORMATIVE
  Authority:        GovernanceBody (per RMM STANDARD #4)
  Source of Truth:  03-STANDARDS/ (per Constitution §10)
  Status:           Active
  Version:          1.0.0

  SCOPE: Procedural checklist only. Automated validation tool
  is OUT OF SCOPE for Phase 2; deferred to Phase 3 per
  PHASE_2_MASTER_PLAN.md §4.4 acceptance criterion 6.
  ============================================
-->

# CROSS-DOCUMENT VALIDATOR

## Section A: Document Identification

| Property | Value |
|----------|-------|
| **Title** | Cross-Document Validator |
| **Short** | CROSS_DOCUMENT_VALIDATOR |
| **Entity** | STANDARD |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody (RMM STANDARD #4) |
| **Source of Truth** | `03-STANDARDS/` (per Constitution §10) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Scope** | Procedural checklist for cross-document validation |

---

## Section B: Scope Statement

This document defines the **procedural checklist** for cross-document validation within the Engineering Kernel repository. It specifies what validations must run, how often, what constitutes PASS/FAIL, and who is responsible.

**IMPORTANT — SCOPE BOUNDARY:** This document is a **procedural checklist** (human-executable validation procedure). An **automated validation tool** (code, script, or software) is explicitly OUT OF SCOPE for Phase 2 per `PHASE_2_MASTER_PLAN.md` absolute constraint "No implementation code." The procedural checklist satisfies the `CANONICAL_ARBITRATION_LEDGER.md` ISSUE-019 requirement for cross-document validation via the non-code option. Automated tool development is deferred to Phase 3.

---

## Section C: Validation Overview

### C.1 Validation Frequency

| Trigger | Frequency | Responsible |
|---------|-----------|-------------|
| Pre-commit | Every commit | Committing Actor |
| Post-mission | After every mission | Engineering Kernel Architect |
| Pre-release | Before phase transition | GovernanceBody |
| On-demand | Ad hoc | Any Actor with Role |

### C.2 Documents Under Validation

The procedural checklist covers **all 28 documents** in the repository:

**21 Canonical Documents:**

| # | Document | Entity | SOT Path |
|---|----------|--------|----------|
| 1 | `CONSTITUTION.md` | CONSTITUTION | `00-CONSTITUTION/` |
| 2 | `KERNEL_CHARTER.md` | CHARTER | `00-CONSTITUTION/Charters/` |
| 3 | `KERNEL_ROLE_MODEL.md` | ROLE | `00-CONSTITUTION/` |
| 4 | `RMM_v1.1.md` | DOCUMENT (79 entities) | `01-META-MODEL/` |
| 5 | `KERNEL_SCOPE_DEFINITION.md` | DOCUMENT | `01-META-MODEL/` |
| 6 | `KERNEL_STRUCTURE_SPEC.md` | DOCUMENT | `01-META-MODEL/` |
| 7 | `DOCUMENT_STANDARD_SPEC.md` | DOCUMENT | `01-META-MODEL/` |
| 8 | `ARTIFACT_META_MODEL.md` | DOCUMENT | `01-META-MODEL/` |
| 9 | `ARTIFACT_FAMILY_MODEL.md` | DOCUMENT | `01-META-MODEL/` |
| 10 | `Repository_State_Model.md` | DOCUMENT | `01-META-MODEL/` |
| 11 | `KERNEL_DEPENDENCY_MODEL.md` | DOCUMENT | `01-META-MODEL/` |
| 12 | `KERNEL_AUTHORITY_MODEL.md` | DOCUMENT | `01-META-MODEL/` |
| 13 | `KERNEL_GOVERNANCE_MODEL.md` | GOVERNANCE_BODY | `02-GOVERNANCE/` |
| 14 | `KERNEL_AMENDMENT_MODEL.md` | AMENDMENT | `02-GOVERNANCE/Amendments/` |
| 15 | `KERNEL_DECISION_MODEL.md` | DECISION | `05-EVIDENCE/` |
| 16 | `KERNEL_EVIDENCE_MODEL.md` | EVIDENCE (family) | `05-EVIDENCE/` |
| 17 | `KERNEL_REVIEW_MODEL.md` | REVIEW | `05-EVIDENCE/Reviews/` |
| 18 | `REPOSITORY_LIFECYCLE_MODEL.md` | LIFECYCLE + STATE | `01-META-MODEL/Lifecycles/` |
| 19 | `KERNEL_DOCUMENT_REGISTRY.md` | DOCUMENT | `00-CONSTITUTION/` |
| 20 | `PHASE_2_MASTER_PLAN.md` | PLAN | `03-PLANNING/` |
| 21 | `CONSTITUTIONAL_EXECUTION_REPORT.md` | REPORT | `05-EVIDENCE/` |

**7 Operational-Layer Documents:**

| # | Document | MISSION Authority | Location |
|---|----------|------------------|----------|
| 22 | `REPOSITORY_INFORMATION_MODEL.md` | MISSION-019 | `02-GOVERNANCE/` |
| 23 | `REPOSITORY_LAYOUT_SPECIFICATION.md` | MISSION-020 | `02-GOVERNANCE/` |
| 24 | `KERNEL_BOOT_PROTOCOL.md` | MISSION-022 | `07-WORKFLOW/` |
| 25 | `AI_EXECUTION_PROTOCOL.md` | MISSION-021 | `07-WORKFLOW/` |
| 26 | `KNOWLEDGE_INDEX_SPECIFICATION.md` | MISSION-024 | `09-TOOLS/` |
| 27 | `SKILL_MANIFEST_SPECIFICATION.md` | MISSION-023 | `09-TOOLS/` |
| 28 | `KERNEL_VALIDATION_PROTOCOL.md` | MISSION-025 | `09-TOOLS/` |

---

## Section D: Validation Checks

### CHECK-1: SOT Path Verification

**Purpose:** Verify every document's actual repository location matches its RMM §15 Source of Truth path.

**Input:** Document inventory (Section C.2); RMM §15 SOT matrix; actual repository file listing.

**Procedure:**
1. For each of the 21 canonical documents, read its RMM §15 Source of Truth value.
2. Verify the file exists at that path in the repository.
3. For documents where RMM §15 specifies a directory (not a filename), verify the file exists within that directory.
4. For the 7 operational-layer documents, verify they exist at their documented locations.
5. For `PHASE_2_MASTER_PLAN.md` (SOT = `03-PLANNING/`), note that this directory is not listed in Constitution §10 — document this as KNOWN GAP.
6. For `KERNEL_PROCESS_MODEL.md` (SOT = `07-WORKFLOW/` per RMM PROCESS #15), verify it exists at that path.

**PASS Criteria:** All 28 documents exist at their declared SOT paths. Any KNOWN GAP is explicitly documented.

**FAIL Criteria:** Any canonical document does not exist at its RMM §15 SOT path; any document location is undocumented.

---

### CHECK-2: Section Naming Consistency

**Purpose:** Verify all documents follow a consistent section naming scheme.

**Input:** All 28 documents; `DOCUMENT_STANDARD_SPEC.md` §3; `SECTION_NAMING_STANDARD.md` (when produced by P2-M05).

**Procedure:**
1. Inventory the section naming scheme used by each document:
   - Lettered sections (A, B, C...) — e.g., `KERNEL_GOVERNANCE_MODEL.md`
   - Numbered sections (1, 2, 3...) — e.g., `CONSTITUTION.md`
   - Mixed (lettered Part I + numbered Part II) — e.g., `KERNEL_CHARTER.md`
2. Compare each document's scheme against the authoritative standard (DSS §3 or P2-M05 output).
3. Identify deviations.
4. Document each deviation with: document name, current scheme, target scheme, harmonization priority.

**PASS Criteria:** Every document's naming scheme is inventoried; deviations are documented with remediation targets.

**FAIL Criteria:** Any document's naming scheme is unclassified; deviations exist without documented remediation plan.

---

### CHECK-3: RMM Citation Accuracy

**Purpose:** Verify every RMM citation in every document resolves to a valid RMM entity and property.

**Input:** All 28 documents; `RMM_v1.1.md` (79 entities, 15 properties each).

**Procedure:**
1. Extract all RMM citations from each document (pattern: "RMM ENTITY #N" or "RMM ENTITY #N–#M").
2. For each citation, verify:
   a. The cited ENTITY exists in RMM v1.1.
   b. The cited property #N is defined for that entity (1 ≤ N ≤ 15).
   c. The cited value matches RMM v1.1.
3. Flag any citation that references a non-existent entity or property.
4. Flag any citation where the document's stated value disagrees with RMM.

**PASS Criteria:** 100% of RMM citations resolve to valid RMM entities and properties; zero value mismatches.

**FAIL Criteria:** Any RMM citation is unresolvable; any document states an RMM value that disagrees with RMM v1.1.

---

### CHECK-4: AFM Consistency

**Purpose:** Verify Artifact Family Model assignments in all documents match AFM definitions.

**Input:** All documents referencing AFM; `ARTIFACT_FAMILY_MODEL.md`.

**Procedure:**
1. Extract all AFM references from each document (pattern: "AFM Section N" or "AFM N.N").
2. For each entity claimed to be in an AFM family, verify against `ARTIFACT_FAMILY_MODEL.md`.
3. Check that `KERNEL_EVIDENCE_MODEL.md` §J AFM Reference column matches AFM for all 7 TIER 10 entities.
4. Verify no entity is assigned to a family that contradicts AFM.

**PASS Criteria:** All AFM family assignments match `ARTIFACT_FAMILY_MODEL.md`; ISSUE-014 corrections verified.

**FAIL Criteria:** Any entity's AFM family assignment contradicts `ARTIFACT_FAMILY_MODEL.md`.

---

### CHECK-5: [UNSUPPORTED] Marker Tracking

**Purpose:** Ensure all [UNSUPPORTED] markers are catalogued and tracked for resolution.

**Input:** All 28 documents; `UNSUPPORTED_MARKER_TRACKER.md` (produced by P2-M04).

**Procedure:**
1. Search all documents for "[UNSUPPORTED]" markers.
2. For each marker found:
   a. Record the document, section, and context.
   b. Identify which RMM property is unsupported.
   c. Check if the marker is already catalogued in `UNSUPPORTED_MARKER_TRACKER.md`.
3. Compare total count against expected count (37 per ISSUE-020, minus 4 resolved by ISSUE-014 = 33 remaining, or 37 if counting before ISSUE-014).
4. Flag any undocumented [UNSUPPORTED] markers.

**PASS Criteria:** All [UNSUPPORTED] markers are catalogued in `UNSUPPORTED_MARKER_TRACKER.md` with tracking IDs; zero undocumented markers.

**FAIL Criteria:** Any [UNSUPPORTED] marker exists in a document but not in the tracker; marker count mismatch.

---

### CHECK-6: Authority Chain Consistency

**Purpose:** Verify authority chains across documents are consistent with Constitution §4.1.

**Input:** All 28 documents; `CONSTITUTION.md` §4.1; `KERNEL_AUTHORITY_MODEL.md`.

**Procedure:**
1. Extract the authority chain declared by each document.
2. Verify each chain conforms to: CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR.
3. Verify document Owner fields match RMM #4 for their entity type.
4. Verify no document claims authority from an entity outside the chain.
5. Cross-check Owner declarations between documents (e.g., KGM says GOVERNANCE_BODY owns ROLE; KRM says ROLE Owner = GOVERNANCE_BODY — these must agree).

**PASS Criteria:** All authority chains are consistent with Constitution §4.1; all Owner declarations match RMM #4; cross-document Owner references agree.

**FAIL Criteria:** Any authority chain violates Constitution §4.1; any Owner declaration contradicts RMM #4; cross-document Owner references disagree.

---

### CHECK-7: Dependency Graph Acyclicity

**Purpose:** Verify the document dependency graph remains a directed acyclic graph (DAG).

**Input:** All 28 documents; `KERNEL_DEPENDENCY_MODEL.md`; `PHASE_2_MASTER_PLAN.md` §5.

**Procedure:**
1. Extract all document-to-document dependencies from each document's Dependencies section.
2. Build a directed graph where nodes are documents and edges are dependencies.
3. Apply a cycle detection algorithm (procedural: trace each path; if a node is revisited, a cycle exists).
4. Verify the Phase 2 mission dependency graph (P2-M01 → P2-M02/M03/M04 → P2-M05 → P2-M06 → P2-M07 → P2-M08) is acyclic.

**PASS Criteria:** Document dependency graph has zero cycles; Phase 2 mission DAG has zero cycles.

**FAIL Criteria:** Any cycle detected in document dependency graph; any cycle detected in mission dependency graph.

---

### CHECK-8: Registry Completeness

**Purpose:** Verify `KERNEL_DOCUMENT_REGISTRY.md` inventory matches actual repository documents.

**Input:** `KERNEL_DOCUMENT_REGISTRY.md`; actual repository directory listing; all 28 documents.

**Procedure:**
1. Read `KERNEL_DOCUMENT_REGISTRY.md` inventory.
2. For each entry in the registry, verify the file exists at its SOT path.
3. For each of the 28 documents (21 canonical + 7 operational), verify it appears in the registry.
4. Check that no registry entry points to a non-existent file.
5. Check that no existing document is missing from the registry.
6. Verify registry metadata (SHA, Owner, Classification) matches actual document headers.

**PASS Criteria:** Registry contains all 28 documents; all registry entries resolve to existing files; zero orphan documents; metadata matches.

**FAIL Criteria:** Any document missing from registry; any registry entry points to non-existent file; metadata mismatch.

---

## Section E: Validation Execution Log

Every execution of this procedural checklist SHALL be logged:

| Field | Description |
|-------|-------------|
| **Execution ID** | Unique identifier (VAL-YYYY-MM-DD-NNN) |
| **Date/Time** | When validation was performed |
| **Executor** | Actor who performed the validation |
| **Checks Run** | Which of the 8 checks were executed |
| **Results** | PASS/FAIL for each check |
| **Failures** | Description of any failures found |
| **Remedial Action** | Action taken to resolve failures |
| **Residue** | Any open items requiring follow-up |

---

## Section F: Roles and Responsibilities

| Role | Validation Responsibility |
|------|--------------------------|
| **Engineering Kernel Architect** | Executes post-mission validation; reviews validation logs; escalates failures |
| **GovernanceBody** | Executes pre-release validation; approves validation standard changes |
| **Committing Actor** | Executes pre-commit validation (CHECK-1 and CHECK-3 minimum) |
| **Any Actor with Role** | May execute on-demand validation; must log results |

---

## Section G: Failure Escalation

| Severity | Condition | Action | Escalation Path |
|----------|-----------|--------|-----------------|
| **Critical** | Frozen artifact (RMM, Constitution) appears modified | STOP all work immediately | Engineering Kernel Architect → GovernanceBody |
| **High** | Authority chain violation; RMM citation mismatch | STOP affected mission | Engineering Kernel Architect |
| **Medium** | SOT path mismatch; AFM inconsistency | Document; schedule correction | Engineering Kernel Architect |
| **Low** | Section naming inconsistency; missing registry entry | Document; batch for next maintenance window | Engineering Kernel Architect |

---

## Section H: Automated Tool Deferral

**Status:** AUTOMATED VALIDATION TOOL — DEFERRED TO PHASE 3.

**Rationale:** Phase 2 absolute constraint "No implementation code" prohibits creation of automated validation scripts, tools, or software. The procedural checklist defined in this document provides equivalent coverage via human-executable procedures.

**Phase 3 Trigger:** When RMM v1.2 execution plan reaches mission for automated validation tool development.

**Phase 3 Scope (Preliminary):**
- Implement CHECK-1 through CHECK-8 as automated scripts
- Integrate with repository CI/CD pipeline
- Generate automated validation reports
- Alert on critical and high severity findings

**Reference:** `PHASE_2_MASTER_PLAN.md` §4.4 (P2-M03 acceptance criterion 6); `CANONICAL_ARBITRATION_LEDGER.md` ISSUE-019.

---

## Section I: Revision History

| Version | Date | Authority | Change Type | Mission | Description |
|---------|------|-----------|-------------|---------|-------------|
| 1.0.0 | 2026-06-27 | GovernanceBody | Added | P2-M03 | Initial cross-document validation procedural checklist |

---

## Section J: Canonical References

| Reference | Location | Role |
|-----------|----------|------|
| RMM_v1.1.md | `01-META-MODEL/` | Defines all entity SOT paths (Matrix 6) |
| CONSTITUTION.md | `00-CONSTITUTION/` | Authority chain (§4.1); directory structure (§10) |
| DOCUMENT_STANDARD_SPEC.md | `01-META-MODEL/` | Document format standard |
| ARTIFACT_FAMILY_MODEL.md | `01-META-MODEL/` | AFM family assignments |
| KERNEL_AUTHORITY_MODEL.md | `01-META-MODEL/` | Authority chain derivation |
| KERNEL_DEPENDENCY_MODEL.md | `01-META-MODEL/` | Document dependency graph |
| KERNEL_DOCUMENT_REGISTRY.md | `00-CONSTITUTION/` | Document inventory |
| CANONICAL_ARBITRATION_LEDGER.md | `05-EVIDENCE/` | ISSUE-019 (cross-document validation gap) |
| PHASE_2_MASTER_PLAN.md | `03-PLANNING/` | P2-M03 scope definition |

---

*END OF CROSS-DOCUMENT VALIDATOR*
