<!--
  ============================================
  KNOWLEDGE_INDEX_SPECIFICATION.md — Engineering Kernel (Operational Layer)
  Phase 1.5 — MISSION-022
  Governed by DOCUMENT_STANDARD_SPEC.md. Placed in 09-TOOLS by governance
  decision (KERNEL_STRUCTURE_SPEC §8.1) under the §2.10 semantic
  (validation/automation that supports Kernel operations).
  Defines index/lookup/reference/context-extraction rules only — no implementation.
  ============================================
-->

# KNOWLEDGE INDEX SPECIFICATION

## A. Header

| Property | Value |
|---|---|
| **Title** | Knowledge Index Specification |
| **Short Title** | KNOWLEDGE_INDEX_SPECIFICATION |
| **Entity Type** | SPECIFICATION |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody (per RMM SPECIFICATION #4 = Governance) |
| **Source of Truth** | `09-TOOLS/KNOWLEDGE_INDEX_SPECIFICATION.md` (governance-decision placement, KERNEL_STRUCTURE_SPEC §8.1) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Date** | 2026-06-26 |
| **Authority** | MISSION-022 |

## B. Metadata
```metadata
Entity Type: SPECIFICATION
Entity Purpose: To define the index format, lookup rules, reference rules,
                and context extraction for Kernel knowledge.
Entity Owner: GovernanceBody
Lifecycle: Proposed → Drafted → Reviewed → Approved → Baseline → Amendment → Superseded
Cardinality: 1:N
Stability: Static
Versionable: Yes
Freezable: Yes
AI Creatable: With Approval
AI Modifiable: No
Human Modifiable: With Approval
Source of Truth: 09-TOOLS/ (reserved; governance-decision placement)
```

## C. Classification
NORMATIVE (DOCUMENT_STANDARD_SPEC §3.3). Acceptance Block required.

## D. Status
Active. Lifecycle state: Active (RMM SPECIFICATION #5).

## E. Version
1.0.0.

## F. Authority
MISSION-022 → GovernanceBody → Charter → Constitution. The canonical index instance is `KERNEL_DOCUMENT_REGISTRY.md`; this specification defines the rules that index follows, deriving them from existing sources only.

## G. Dependencies
### G.1 Allowed Dependencies (Normative)
| Reference | Type | Required |
|---|---|---|
| `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` (§3, §6, §7, §11) | Normative | Yes |
| `01-META-MODEL/RMM_v1.1.md` (properties #1–#15, Matrix 6) | Normative | Yes |
| `01-META-MODEL/DOCUMENT_STANDARD_SPEC.md` (§3.2 Metadata Block, §3.10) | Structural | Yes |
| `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` (§3, §8.4) | Structural | Yes |
| `01-META-MODEL/KERNEL_DEPENDENCY_MODEL.md` (dependency DAG) | Normative | Yes |

### G.2 Forbidden Dependencies
| Reference | Rationale |
|---|---|
| Product/technology artifacts | KERNEL_SCOPE_DEFINITION §3.1, §3.2 |
| Index implementation (engine, format JSON/YAML, code) | Phase 1.5: specification only |

## H. Revision History
| Version | Date | Author | Change Type | Authority | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | GovernanceBody | Added | MISSION-022 | Initial Knowledge Index Specification |

## I. Acceptance
| Status | Approver | Date | Method | Conditions |
|---|---|---|---|---|
| Granted | MISSION-022 (GovernanceBody) | 2026-06-26 | Record | Phase 1.5 quality gates PASS |

## J. Canonical References
| Reference | Location |
|---|---|
| Kernel Document Registry | `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` |
| Repository Meta Model v1.1 | `01-META-MODEL/RMM_v1.1.md` |
| Document Standard Spec | `01-META-MODEL/DOCUMENT_STANDARD_SPEC.md` |
| Kernel Dependency Model | `01-META-MODEL/KERNEL_DEPENDENCY_MODEL.md` |

---

# PART II — KNOWLEDGE INDEX

## 1. Index Format

KI-IX-01. The knowledge index is a set of **index records**, one per canonical Kernel document. The authoritative instance is `KERNEL_DOCUMENT_REGISTRY.md` §3 (Canonical Document Inventory); this specification defines its required fields.

KI-IX-02. Each index record SHALL carry exactly these keys, all sourced from existing definitions:

| Key | Source |
|---|---|
| Identifier | RMM property #1 (Name) — UPPER_SNAKE_CASE (KERNEL_DOCUMENT_REGISTRY §3) |
| Filename | physical file name (KERNEL_STRUCTURE_SPEC §4.2) |
| Entity Type | RMM property #1 (entity class) |
| Owner | RMM property #4 |
| Classification | DOCUMENT_STANDARD_SPEC §3.3 |
| Status | RMM property #5 / Matrix 2 |
| Version | RMM property #10 |
| Source of Truth | RMM property #15 (KERNEL_DOCUMENT_REGISTRY §11) |
| Authority | DOCUMENT_STANDARD_SPEC §3.6 (MISSION-NNN) |

KI-IX-03. The index is expressed in the text/tabular form of DOCUMENT_STANDARD_SPEC (tables). **[UNSUPPORTED]** — no machine index format (JSON/YAML/binary) is defined by the Kernel and none is introduced.

KI-IX-04. The index SHALL be complete: every canonical document appears exactly once (KERNEL_DOCUMENT_REGISTRY RI-05). No canonical document may be absent; no non-canonical artifact may appear (KERNEL_DOCUMENT_REGISTRY §2.2).

## 2. Lookup Rules

KI-LK-01. Lookup by **Identifier** (RMM #1) resolves to a single Source-of-Truth location (RMM #15; KERNEL_DOCUMENT_REGISTRY §11). Identifiers are unique (KERNEL_DOCUMENT_REGISTRY RI-01).

KI-LK-02. Lookup by **Source of Truth directory** returns the set of documents in that directory (KERNEL_STRUCTURE_SPEC §3).

KI-LK-03. Lookup by **Classification** returns documents of that class (DOCUMENT_STANDARD_SPEC §3.3) — e.g., all CANONICAL, all NORMATIVE.

KI-LK-04. Lookup by **dependency** uses the dependency tables of `KERNEL_DEPENDENCY_MODEL.md` and `KERNEL_DOCUMENT_REGISTRY.md` §6 (Depends On / Referenced By).

KI-LK-05. Lookup by **read order / boot order** uses KERNEL_DOCUMENT_REGISTRY §7 / §8.

KI-LK-06. A lookup that resolves to no record is a miss; the index SHALL NOT fabricate a result. A lookup for an undefined entity returns **[UNSUPPORTED]**.

## 3. Reference Rules

KI-RF-01. A reference to a Kernel document SHALL use a relative path from the repository root (KERNEL_STRUCTURE_SPEC §7.4; DOCUMENT_STANDARD_SPEC §3.7).

KI-RF-02. A reference to an RMM entity SHALL include the entity name and the supporting RMM property numbers and/or Matrix rows (DOCUMENT_STANDARD_SPEC §3.10).

KI-RF-03. Every reference SHALL resolve to an existing file; dangling references are prohibited (KERNEL_STRUCTURE_SPEC §8.4; KERNEL_DOCUMENT_REGISTRY RI-06).

KI-RF-04. Typed, directional cross-references between artifacts use the RMM `TraceabilityLink` entity semantics (RMM Tier 13). This specification references that entity; it does not redefine it.

KI-RF-05. A reference to a non-Kernel source SHALL be marked `[EXTERNAL]` and is informational only (DOCUMENT_STANDARD_SPEC §3.10).

## 4. Context Extraction

KI-CX-01. The unit of extractable context for a document is its **Metadata Block** — the delimited region (```metadata) defined by DOCUMENT_STANDARD_SPEC §3.2, carrying the 12 RMM-derived fields. This is the canonical machine-extractable region.

KI-CX-02. The minimal context for an **entity** comprises its RMM properties #1–#15 (definition, owner, lifecycle, permissions, source of truth) plus its allowed relationships (#6) and forbidden relationships (#7). No additional context is required to interpret the entity (KERNEL_SCOPE_DEFINITION §10.8 Minimal Sufficiency).

KI-CX-03. Authority context for an entity is extracted from `KERNEL_AUTHORITY_MODEL.md` (owner, may-freeze, permissions) and traced along Constitution → Charter → GovernanceBody → Role → Actor (KERNEL_SCOPE_DEFINITION §10.4).

KI-CX-04. Context extraction is read-only: it SHALL NOT modify any indexed artifact (consistent with RMM `View`/`Topology` "may not modify the entities it represents").

KI-CX-05. Extraction defines no parser, tokenizer, or retrieval engine — **[implementation: out of scope, Phase 1.5]**. This specification defines what constitutes a context unit and where it is located, only.

---

## QUALITY GATE (PCS) — PASS

| Gate | Result | Note |
|---|---|---|
| Engineering Self Review | PASS | Index keys, lookup, reference, and context rules each cite KDR / RMM / DSS / KSS / KDM. Nothing invented. |
| PCS Compliance Review | PASS | Specification only; no implementation, no JSON/YAML, no code, no technology, no new entity. |
| Correction Cycle | PASS | Machine index format and parser explicitly `[UNSUPPORTED]` / out of scope; placement reconciled to KSS §8.1. |
| Final Verification | PASS | Conforms to DOCUMENT_STANDARD_SPEC; defines only the four mandated topics. |

*END OF DOCUMENT*
