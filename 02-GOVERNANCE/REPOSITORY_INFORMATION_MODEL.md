<!--
  ============================================
  REPOSITORY_INFORMATION_MODEL.md — Engineering Kernel (Operational Layer)
  Phase 1.5 — MISSION-019
  Governed by DOCUMENT_STANDARD_SPEC.md. Derived only from frozen Kernel sources.
  This document OPERATIONALIZES the frozen Kernel. It introduces no entity,
  renames nothing, and modifies neither the RMM nor the Constitution.
  ============================================
-->

# REPOSITORY INFORMATION MODEL (RIM)

## A. Header

| Property | Value |
|---|---|
| **Title** | Repository Information Model |
| **Short Title** | REPOSITORY_INFORMATION_MODEL |
| **Entity Type** | SPECIFICATION |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody (per RMM SPECIFICATION #4 = Governance) |
| **Source of Truth** | `02-GOVERNANCE/REPOSITORY_INFORMATION_MODEL.md` |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Date** | 2026-06-26 |
| **Authority** | MISSION-019 (per DOCUMENT_STANDARD_SPEC §3.6: MISSION-NNN is a valid Authority) |

## B. Metadata

```metadata
Entity Type: SPECIFICATION
Entity Purpose: To define the physical representation, serialization, and
                logical-to-physical mapping of Kernel artifacts.
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
NORMATIVE — mandatory specification (DOCUMENT_STANDARD_SPEC §3.3). Requires an Acceptance Block (§I).

## D. Status
Active. Lifecycle state: Active (per RMM SPECIFICATION #5).

## E. Version
1.0.0 — semantic versioning per KERNEL_STRUCTURE_SPEC §4.4 / §5.

## F. Authority
Authority: MISSION-019. Owner: GovernanceBody (RMM SPECIFICATION #4 = Governance). Authority chain: MISSION-019 → GovernanceBody → Charter → Constitution (per KERNEL_AUTHORITY_MODEL §2). This document SHALL NOT contradict the Constitution (KERNEL_SCOPE_DEFINITION §7).

## G. Dependencies

### G.1 Allowed Dependencies (Normative)
| Reference | Type | Required |
|---|---|---|
| `01-META-MODEL/RMM_v1.1.md` (Matrix 6 #15; ARTIFACT/DOCUMENT entities) | Normative | Yes |
| `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` (§2, §3, §4, §7) | Structural | Yes |
| `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` (§14 Constraints) | Normative | Yes |
| `01-META-MODEL/DOCUMENT_STANDARD_SPEC.md` (§3.1, §3.2) | Structural | Yes |
| `01-META-MODEL/ARTIFACT_META_MODEL.md` (artifact identity) | Normative | Yes |
| `01-META-MODEL/Repository_State_Model.md` (object state) | Normative | Yes |

### G.2 Forbidden Dependencies
| Reference | Rationale |
|---|---|
| Product-specific artifacts | KERNEL_SCOPE_DEFINITION §3.1; RMM #7 |
| Technology-specific artifacts (languages, datastores, frameworks, serializers) | KERNEL_SCOPE_DEFINITION §3.2, §10.1 |
| Serialization formats (JSON, YAML) | Phase 1.5 constraint; kernel defines none |

## H. Revision History
| Version | Date | Author | Change Type | Authority | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | GovernanceBody | Added | MISSION-019 | Initial Repository Information Model |

## I. Acceptance
| Status | Approver | Date | Method | Conditions |
|---|---|---|---|---|
| Granted | MISSION-019 (GovernanceBody) | 2026-06-26 | Record | Phase 1.5 quality gates PASS (see Quality Gate footer) |

## J. Canonical References
| Reference | Location |
|---|---|
| Repository Meta Model v1.1 | `01-META-MODEL/RMM_v1.1.md` |
| Kernel Structure Spec | `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` |
| Document Standard Spec | `01-META-MODEL/DOCUMENT_STANDARD_SPEC.md` |
| Kernel Scope Definition | `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` |
| Artifact Meta Model | `01-META-MODEL/ARTIFACT_META_MODEL.md` |
| Repository State Model | `01-META-MODEL/Repository_State_Model.md` |

---

# PART II — INFORMATION MODEL

## 1. Physical Representation

RIM-PR-01. Every logical Kernel object (an RMM entity instance) is represented physically as exactly **one file** ("one concept per file", KERNEL_STRUCTURE_SPEC §7.1).

RIM-PR-02. A file is a **human-readable text artifact** (KERNEL_SCOPE_DEFINITION §14 Constraint 2). The representation form is Markdown; plain text is acceptable (KERNEL_SCOPE_DEFINITION §14 Constraint 6).

RIM-PR-03. Permitted non-text representation is restricted to image diagrams in PNG or SVG only (KERNEL_SCOPE_DEFINITION §14 Constraint 3). No other binary representation is permitted.

RIM-PR-04. A file SHALL NOT exceed the maximum artifact size of 1 MB (KERNEL_SCOPE_DEFINITION §14 Constraint 4).

RIM-PR-05. A file SHALL NOT contain executable code (KERNEL_SCOPE_DEFINITION §14 Constraint 7).

RIM-PR-06. Every file SHALL carry the document structure mandated by DOCUMENT_STANDARD_SPEC (the ten sections §3.1–§3.10), beginning with the Document Header (§3.1) and Metadata Block (§3.2).

RIM-PR-07. The physical encoding below the "human-readable text" level (character encoding, line terminator, checksum) is **[UNSUPPORTED]** — the frozen Kernel does not define it. Consumers SHALL treat it as out of scope per KERNEL_SCOPE_DEFINITION §10.8 (Minimal Sufficiency).

## 2. Serialization Rules

RIM-SR-01. The canonical serialization of a Kernel object is its text file content as written; the file at the Source of Truth location is the authoritative serialization (RMM property #15; KERNEL_STRUCTURE_SPEC §3).

RIM-SR-02. Internal structure within a serialized object uses only DOCUMENT_STANDARD_SPEC constructs: the delimited Metadata Block (§3.2), key/value fields (§3.1), and tables (§3.7–§3.10). No external structured-data format is defined.

RIM-SR-03. **[UNSUPPORTED]** — The Kernel defines no machine serialization format (no JSON, no YAML, no binary schema). Any such format is forbidden by Phase 1.5 constraints and absent from the frozen sources.

RIM-SR-04. Versioning of a serialized object follows RMM property #10 (Versionable) and KERNEL_STRUCTURE_SPEC §5:
- Versionable = Yes: each change produces a new version; history is preserved (KERNEL_STRUCTURE_SPEC §5.1).
- Versionable = No (RMM Matrix 4): in-place overwrite; no version history (KERNEL_STRUCTURE_SPEC §5.2).

RIM-SR-05. A serialized object that is Frozen (RMM property #11; KERNEL_STRUCTURE_SPEC §6) SHALL NOT be re-serialized except through the unfreeze → modify → refreeze cycle (KERNEL_STRUCTURE_SPEC §6.1) authorized by an Approval entity.

## 3. Logical-to-Physical Mapping

RIM-LP-01. The logical layer is the RMM: 79 entity types, their properties (#1–#15), tiers, and relationships (`01-META-MODEL/RMM_v1.1.md`).

RIM-LP-02. The physical layer is the repository directory tree as defined by KERNEL_STRUCTURE_SPEC §2 (directory responsibilities) and §3 (entity-to-directory mapping).

RIM-LP-03. **Mapping rule:** a logical object of RMM entity type *E* is stored physically in the directory that KERNEL_STRUCTURE_SPEC §2/§3 assigns to *E*, which is *E*'s RMM property #15 Source of Truth. The authoritative entity-to-directory assignment is KERNEL_STRUCTURE_SPEC §3 (this RIM does not restate or alter it).

RIM-LP-04. Logical stores named in RMM Matrix 6 that are not numbered directories resolve to their structural home per KERNEL_STRUCTURE_SPEC §2:
- Governance Ledger → `02-GOVERNANCE/`
- Evidence Vault / Audit Log → `05-EVIDENCE/`
- Artifact Repository → **[UNSUPPORTED]** — KERNEL_STRUCTURE_SPEC assigns no numbered directory to the Repository class; binding is reserved to the architecture and not created here.

RIM-LP-05. A logical collection (all instances of entity type *E*) maps physically to the set of files in *E*'s directory. Cardinality of the collection follows RMM property #8.

RIM-LP-06. Mapping is total and unidirectional in the sense of KERNEL_SCOPE_DEFINITION §9.2: every physical file resolves to exactly one logical entity type; no physical file may exist without an associated entity (KERNEL_STRUCTURE_SPEC §8.1).

## 4. Repository Object Mapping

RIM-OM-01. Object taxonomy (physical containment), derived from KERNEL_STRUCTURE_SPEC §2 and DOCUMENT_STANDARD_SPEC §3:

```
Repository
  └── Directory            (one per RMM Source-of-Truth domain; KSS §2)
        └── Document/Artifact  (one file = one RMM entity instance; KSS §7.1)
              └── Section        (the ten standard sections; DSS §3.1–§3.10)
                    └── Field        (an RMM property #1–#15; DSS §3.2)
```

RIM-OM-02. Object identity is the RMM entity Name (property #1) realized as the file's UPPER_SNAKE_CASE name (KERNEL_STRUCTURE_SPEC §4.2/§4.3). Artifact identity semantics are governed by `ARTIFACT_META_MODEL.md` (referenced, not restated).

RIM-OM-03. Object state and permitted transitions are governed by `Repository_State_Model.md` and RMM property #5 (Lifecycle) / Matrix 2 (referenced, not restated). This RIM maps state to representation only: a Frozen state (RMM #11) constrains serialization per RIM-SR-05.

RIM-OM-04. Object location is the RMM property #15 Source of Truth, resolved through RIM-LP-03. The location is immutable for a given object (KERNEL_STRUCTURE_SPEC §8.1: directory numbers are immutable).

RIM-OM-05. Object references between physical objects SHALL use relative paths from the repository root (KERNEL_STRUCTURE_SPEC §7.4; DOCUMENT_STANDARD_SPEC §3.7).

RIM-OM-06. An object that maps to no RMM entity type is **non-canonical** and SHALL NOT be placed in directories `00`–`07` or `99` without an associated entity (KERNEL_STRUCTURE_SPEC §8.1); reserved directories `04`, `08`, `09` may hold objects only by explicit governance decision (KERNEL_STRUCTURE_SPEC §8.1).

---

## QUALITY GATE (PCS) — PASS

| Gate | Result | Note |
|---|---|---|
| Engineering Self Review | PASS | All rules cite a frozen source (RMM / KSS / KSD / DSS / AMM / RSM); none invented. |
| PCS Compliance Review | PASS | No redesign, no new/renamed/merged/split entity, no RMM/Constitution modification, no technology, no product, no code, no JSON/YAML. |
| Correction Cycle | PASS | Undefined items (encoding, machine serialization, Repository-class binding) marked `[UNSUPPORTED]` rather than invented. |
| Final Verification | PASS | Conforms to DOCUMENT_STANDARD_SPEC ten-section format; placed at RMM-consistent Source of Truth `02-GOVERNANCE/`. |

*END OF DOCUMENT*
