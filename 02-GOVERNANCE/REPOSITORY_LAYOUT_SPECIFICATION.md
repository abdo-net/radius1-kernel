<!--
  ============================================
  REPOSITORY_LAYOUT_SPECIFICATION.md — Engineering Kernel (Operational Layer)
  Phase 1.5 — MISSION-020
  Governed by DOCUMENT_STANDARD_SPEC.md. Operationalizes the frozen Kernel.
  Restates and indexes existing structure; introduces no new structure.
  ============================================
-->

# REPOSITORY LAYOUT SPECIFICATION

## A. Header

| Property | Value |
|---|---|
| **Title** | Repository Layout Specification |
| **Short Title** | REPOSITORY_LAYOUT_SPECIFICATION |
| **Entity Type** | SPECIFICATION |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody (per RMM SPECIFICATION #4 = Governance) |
| **Source of Truth** | `02-GOVERNANCE/REPOSITORY_LAYOUT_SPECIFICATION.md` |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Date** | 2026-06-26 |
| **Authority** | MISSION-020 |

## B. Metadata
```metadata
Entity Type: SPECIFICATION
Entity Purpose: To define directory semantics, file placement, canonical
                locations, path invariants, and repository navigation.
Entity Owner: GovernanceBody
Lifecycle: Proposed → Drafted → Reviewed → Approved → Baseline → Amendment → Superseded
Cardinality: 1:N
Stability: Static
Versionable: Yes
Freezable: Yes
AI Creatable: With Approval
AI Modifiable: No
Human Modifiable: With Approval
Source of Truth: 02-GOVERNANCE/ (Governance Ledger)
```

## C. Classification
NORMATIVE (DOCUMENT_STANDARD_SPEC §3.3). Acceptance Block required.

## D. Status
Active. Lifecycle state: Active (RMM SPECIFICATION #5).

## E. Version
1.0.0 (KERNEL_STRUCTURE_SPEC §4.4).

## F. Authority
MISSION-020 → GovernanceBody → Charter → Constitution (KERNEL_AUTHORITY_MODEL §2). SHALL NOT contradict the Constitution or KERNEL_STRUCTURE_SPEC; this specification only restates and operationalizes them.

## G. Dependencies
### G.1 Allowed Dependencies (Normative)
| Reference | Type | Required |
|---|---|---|
| `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` (§2, §3, §4, §7, §8) | Structural | Yes |
| `01-META-MODEL/RMM_v1.1.md` (Matrix 6 #15) | Normative | Yes |
| `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` (§11, §12) | Normative | Yes |
| `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` (§14 Constraints) | Normative | Yes |

### G.2 Forbidden Dependencies
| Reference | Rationale |
|---|---|
| Product-specific directory/file names | KERNEL_STRUCTURE_SPEC §8.2; KERNEL_SCOPE_DEFINITION §3.1 |
| Technology-specific names | KERNEL_STRUCTURE_SPEC §8.2; KERNEL_SCOPE_DEFINITION §3.2 |

## H. Revision History
| Version | Date | Author | Change Type | Authority | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | GovernanceBody | Added | MISSION-020 | Initial Repository Layout Specification |

## I. Acceptance
| Status | Approver | Date | Method | Conditions |
|---|---|---|---|---|
| Granted | MISSION-020 (GovernanceBody) | 2026-06-26 | Record | Phase 1.5 quality gates PASS |

## J. Canonical References
| Reference | Location |
|---|---|
| Kernel Structure Spec | `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` |
| Repository Meta Model v1.1 | `01-META-MODEL/RMM_v1.1.md` |
| Kernel Document Registry | `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` |

---

# PART II — LAYOUT SPECIFICATION

## 1. Directory Semantics

LS-DS-01. The repository has exactly eleven canonical directories. Their semantics are defined by KERNEL_STRUCTURE_SPEC §2 and are restated here as an index only (the Structure Spec governs):

| Directory | Semantic (KERNEL_STRUCTURE_SPEC §2) | Reserved? |
|---|---|---|
| `00-CONSTITUTION/` | Supreme governance instrument and bodies; root of all authority (§2.1) | No |
| `01-META-MODEL/` | Complete ontology: RMM, entity definitions, matrices (§2.2) | No |
| `02-GOVERNANCE/` | Authority framework: roles, actors, sessions, permissions (§2.3) | No |
| `03-STANDARDS/` | Lifecycle rules: states, transitions, freeze, approval (§2.4) | No |
| `04-PATTERNS/` | Reserved — no entities assigned (§2.5) | Yes |
| `05-EVIDENCE/` | Process artifacts: evidence, audit trail, artifact, document (§2.6) | No |
| `06-CONTRACTS/` | Interface agreements: contract, interface, service level (§2.7) | No |
| `07-WORKFLOW/` | Process execution: workflow, process, task, EWO, ECO (§2.8) | No |
| `08-TEMPLATES/` | Reserved — no entities assigned (§2.9) | Yes |
| `09-TOOLS/` | Reserved — tool configurations, validation, automation that support Kernel operations (§2.10) | Yes (governance-decision gated, §8.1) |
| `99-STATE/` | Cross-cutting concerns; global/shared mechanisms; system-wide invariants (§2.11) | No |

## 2. File Placement

LS-FP-01. Every artifact SHALL be stored in the directory matching its RMM property #15 Source of Truth (KERNEL_STRUCTURE_SPEC §3; KERNEL_DOCUMENT_REGISTRY §12 Rule 1).

LS-FP-02. One concept per file; no monolithic multi-entity files (KERNEL_STRUCTURE_SPEC §7.1).

LS-FP-03. No file may exist in directories `00`–`07` or `99` without an associated RMM entity (KERNEL_STRUCTURE_SPEC §8.1).

LS-FP-04. Files in reserved directories `04`, `08`, `09` are permitted only by explicit governance decision (KERNEL_STRUCTURE_SPEC §8.1). The Phase 1.5 operational-layer artifacts placed in `09-TOOLS/` (Knowledge Index, Skill Manifest, Validation Protocol) are authorized by MISSION-022/023/025 as such governance decisions, and fall within the `09-TOOLS/` semantic "validation, and automation definitions that support Kernel operations" (KERNEL_STRUCTURE_SPEC §2.10).

LS-FP-05. Every directory SHALL contain a `README.md` index (KERNEL_STRUCTURE_SPEC §7.6). No file may be orphaned: every file SHALL be referenced by an RMM Source of Truth, another document's normative references, or a directory README (KERNEL_STRUCTURE_SPEC §7.5).

## 3. Canonical Locations

LS-CL-01. The canonical location of an object is its RMM property #15 Source of Truth, resolved through KERNEL_STRUCTURE_SPEC §3 (KERNEL_DOCUMENT_REGISTRY §11).

LS-CL-02. The authoritative inventory of canonical document locations is `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` §11 (Source-of-Truth Map). This specification does not duplicate or override that registry.

LS-CL-03. Operational-layer canonical locations established under Phase 1.5 (this and sibling missions):

| Artifact | Canonical Location | Authority |
|---|---|---|
| Repository Information Model | `02-GOVERNANCE/REPOSITORY_INFORMATION_MODEL.md` | MISSION-019 |
| Repository Layout Specification | `02-GOVERNANCE/REPOSITORY_LAYOUT_SPECIFICATION.md` | MISSION-020 |
| Kernel Boot Protocol | `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md` | MISSION-021 |
| Knowledge Index Specification | `09-TOOLS/KNOWLEDGE_INDEX_SPECIFICATION.md` | MISSION-022 |
| Skill Manifest Specification | `09-TOOLS/SKILL_MANIFEST_SPECIFICATION.md` | MISSION-023 |
| AI Execution Protocol | `07-WORKFLOW/AI_EXECUTION_PROTOCOL.md` | MISSION-024 |
| Kernel Validation Protocol | `09-TOOLS/KERNEL_VALIDATION_PROTOCOL.md` | MISSION-025 |

LS-CL-04. A canonical object has exactly one canonical location; copies elsewhere are non-canonical (KERNEL_SCOPE_DEFINITION §16 "Canonical").

## 4. Path Invariants

LS-PI-01. Directory numbers are immutable (KERNEL_STRUCTURE_SPEC §8.1; KERNEL_DOCUMENT_REGISTRY RI-08).

LS-PI-02. Directory name format is `NN-DESCRIPTOR/` — two-digit prefix `00`–`99`, single-word uppercase descriptor (KERNEL_STRUCTURE_SPEC §4.1).

LS-PI-03. Kernel artifact file names are UPPER_SNAKE_CASE `DESCRIPTOR_TYPE.md` (KERNEL_STRUCTURE_SPEC §4.2).

LS-PI-04. No technology name and no product name may appear in any directory or file name (KERNEL_STRUCTURE_SPEC §8.2; KERNEL_SCOPE_DEFINITION §10.1, §10.2).

LS-PI-05. Internal references use relative paths from the repository root (KERNEL_STRUCTURE_SPEC §7.4); all references SHALL resolve to existing files (KERNEL_STRUCTURE_SPEC §8.4).

LS-PI-06. Source of Truth declared in a file's header SHALL match its actual directory path (KERNEL_STRUCTURE_SPEC §8.3).

## 5. Repository Navigation

LS-NV-01. The navigation rules are defined by KERNEL_DOCUMENT_REGISTRY §12 (restated as an index; the Registry governs):

| Rule | Statement | Source |
|---|---|---|
| 1 | Every artifact is stored in the directory matching its RMM Source of Truth. | KSS §3.1 |
| 2 | Directory numbers are immutable. | KSS §8.1 |
| 3 | No product-specific directory names. | KSS §8.2 |
| 4 | Canonical directories contain text artifacts (`.md`). | KSS §4.2 |
| 5 | Reserved directories (04, 08, 09) hold files only by governance decision. | KSS §8.1 |
| 6 | `00-CONSTITUTION/` documents are supreme authority. | KSS §2.1 |
| 7 | `01-META-MODEL/` documents are ontology/meta-model. | KSS §2.2 |
| 8 | RMM #15 Source of Truth is the canonical location per entity type. | RMM #15 |

LS-NV-02. The authoritative **read order** (dependencies before dependents, topological) is KERNEL_DOCUMENT_REGISTRY §7. The authoritative **boot order** is KERNEL_DOCUMENT_REGISTRY §8 (operationalized by `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md`).

LS-NV-03. To locate any object: resolve its RMM entity type → its Source of Truth directory (KERNEL_STRUCTURE_SPEC §3) → the file named for the entity (LS-PI-03). To enumerate a directory's contents: read its `README.md` index (KERNEL_STRUCTURE_SPEC §7.6).

LS-NV-04. The single authoritative index of all canonical documents is `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` (its §1: "the Boot Index for every future AI session").

---

## QUALITY GATE (PCS) — PASS

| Gate | Result | Note |
|---|---|---|
| Engineering Self Review | PASS | Every rule restates/cites KERNEL_STRUCTURE_SPEC, RMM #15, or KERNEL_DOCUMENT_REGISTRY; nothing invented. |
| PCS Compliance Review | PASS | No new structure, no redesign, no renamed/added entity, no technology, no product. |
| Correction Cycle | PASS | `09-TOOLS/` placement reconciled to KSS §8.1 governance-decision clause and §2.10 semantic; Artifact-Repository binding left to the architecture. |
| Final Verification | PASS | Conforms to DOCUMENT_STANDARD_SPEC; defines only the five mandated topics. |

*END OF DOCUMENT*
