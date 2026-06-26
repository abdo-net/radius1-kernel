<!--
  ============================================
  SKILL_MANIFEST_SPECIFICATION.md — Engineering Kernel (Operational Layer)
  Phase 1.5 — MISSION-023
  Governed by DOCUMENT_STANDARD_SPEC.md. Placed in 09-TOOLS by governance
  decision (KERNEL_STRUCTURE_SPEC §8.1, §2.10).
  NOTE: "Skill" is not an RMM entity. It is an operational framing of the
  Kernel as an executable knowledge substrate. The Skill IDENTITY is derived
  from the RMM KERNEL entity and KERNEL_SCOPE_DEFINITION. No prompts. No code.
  ============================================
-->

# SKILL MANIFEST SPECIFICATION

## A. Header

| Property | Value |
|---|---|
| **Title** | AI Skill Manifest Specification |
| **Short Title** | SKILL_MANIFEST_SPECIFICATION |
| **Entity Type** | SPECIFICATION |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody (per RMM SPECIFICATION #4 = Governance) |
| **Source of Truth** | `09-TOOLS/SKILL_MANIFEST_SPECIFICATION.md` (governance-decision placement, KERNEL_STRUCTURE_SPEC §8.1) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Date** | 2026-06-26 |
| **Authority** | MISSION-023 |

## B. Metadata
```metadata
Entity Type: SPECIFICATION
Entity Purpose: To define the skill identity, inputs, outputs, required
                artifacts, loading policy, and version policy for the Kernel
                as an executable knowledge substrate.
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
MISSION-023 → GovernanceBody → Charter → Constitution. The Skill identity derives from the RMM KERNEL entity and `KERNEL_SCOPE_DEFINITION.md`; the Constitution is the supreme authority over the Skill (KERNEL_SCOPE_DEFINITION §7).

## G. Dependencies
### G.1 Allowed Dependencies (Normative)
| Reference | Type | Required |
|---|---|---|
| `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` (§1, §4, §5, §10, §12, §13) | Normative | Yes |
| `01-META-MODEL/RMM_v1.1.md` (KERNEL, ARTIFACT, DOCUMENT, EVIDENCE entities) | Normative | Yes |
| `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` (§3, §8) | Normative | Yes |
| `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md` | Normative | Yes |
| `01-META-MODEL/KERNEL_STRUCTURE_SPEC.md` (§5 Version Conventions) | Structural | Yes |

### G.2 Forbidden Dependencies
| Reference | Rationale |
|---|---|
| Product/technology artifacts | KERNEL_SCOPE_DEFINITION §3.1, §3.2 |
| Prompts, prompt templates | Phase 1.5: "No prompts" |
| Executable code, runtime | Phase 1.5: "No code" |

## H. Revision History
| Version | Date | Author | Change Type | Authority | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | GovernanceBody | Added | MISSION-023 | Initial Skill Manifest Specification |

## I. Acceptance
| Status | Approver | Date | Method | Conditions |
|---|---|---|---|---|
| Granted | MISSION-023 (GovernanceBody) | 2026-06-26 | Record | Phase 1.5 quality gates PASS |

## J. Canonical References
| Reference | Location |
|---|---|
| Kernel Scope Definition | `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` |
| Repository Meta Model v1.1 | `01-META-MODEL/RMM_v1.1.md` |
| Kernel Document Registry | `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md` |
| Kernel Boot Protocol | `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md` |

---

# PART II — SKILL MANIFEST

> **Framing note.** `Skill` is **[UNSUPPORTED]** as an RMM entity. This manifest specifies the Kernel's identity *as* an executable substrate; every field below derives from an existing Kernel entity or document.

## 1. Skill Identity

| Field | Value | Source |
|---|---|---|
| Identity | The Engineering Kernel — a product-agnostic, technology-independent engineering operating system | KERNEL_SCOPE_DEFINITION §1 |
| Substrate entity | RMM `KERNEL` (root container and identity of the engineering system) | RMM Tier 1 KERNEL |
| Supreme authority | `CONSTITUTION` | KERNEL_SCOPE_DEFINITION §7 |
| Purpose | Provide ontology, governance, and process frameworks for consistent, auditable, scalable engineering across any consuming product | KERNEL_SCOPE_DEFINITION §1, §4 |
| Operating principles | Technology Independence, Product Agnosticism, Authority-Chain Integrity, Auditability, Separation of Concerns, Freeze Stability, Minimal Sufficiency, Explicit-over-Implicit, Backward Compatibility | KERNEL_SCOPE_DEFINITION §10 |
| Boundary | Scope §2; out-of-scope §3; authority boundary §7 | KERNEL_SCOPE_DEFINITION §2, §3, §7 |

## 2. Inputs

SM-IN-01. The Skill's required inputs are governance documents and authorization context, not product data:

| Input | Definition | Source |
|---|---|---|
| Boot set | `CONSTITUTION.md`, `RMM_v1.1.md`, `KERNEL_SCOPE_DEFINITION.md` | KERNEL_BOOT_PROTOCOL §1; KERNEL_DOCUMENT_REGISTRY §8 |
| Canonical document set | All documents in `KERNEL_DOCUMENT_REGISTRY.md` §3 | KERNEL_DOCUMENT_REGISTRY §3 |
| Authorizing authority | A valid Authority (`MISSION-NNN` / `EWO-NNN` / `ECO-NNN` / `TASK-NNNN`) | DOCUMENT_STANDARD_SPEC §3.6 |
| Acting actor | An RMM `ACTOR` with at least one `ROLE` | RMM ACTOR #7 ("may not have no Role"); KERNEL_SCOPE_DEFINITION §14 Constraint 10 |

SM-IN-02. An input that is absent or unresolved is an **[UNSUPPORTED]** input; the Skill SHALL NOT proceed (stop condition; see `07-WORKFLOW/AI_EXECUTION_PROTOCOL.md`).

## 3. Outputs

SM-OUT-01. The Skill produces only Kernel-conformant artifacts of existing RMM types:

| Output | RMM Entity | Constraint |
|---|---|---|
| Document | `DOCUMENT` | Conforms to DOCUMENT_STANDARD_SPEC; placed at its RMM #15 Source of Truth |
| Artifact | `ARTIFACT` | Per ARTIFACT_META_MODEL; physical per Repository Information Model |
| Evidence / Record | `EVIDENCE`, `RECORD` | Write-once (RMM Matrix 4 = No) |
| Report / Assessment | `REPORT`, `ASSESSMENT` | DERIVED classification (DOCUMENT_STANDARD_SPEC §3.3) |
| Audit trail entry | `AUDIT_TRAIL` | Every state change leaves an audit trail (KERNEL_SCOPE_DEFINITION §10.5) |

SM-OUT-02. The Skill SHALL NOT output product source code, runtime components, or technology selections (KERNEL_SCOPE_DEFINITION §6.2, §6.3, §3.1, §3.2).

## 4. Required Artifacts

SM-RA-01. The minimum artifacts that MUST be present and resolvable for the Skill to be operable are the boot set (SM-IN-01) and the canonical inventory of `KERNEL_DOCUMENT_REGISTRY.md` §3. If any required artifact is missing, the Skill is **not operable** (see Validation Protocol freeze/integrity checks).

SM-RA-02. The Operational Layer artifacts (this manifest, the Repository Information Model, Repository Layout Specification, Knowledge Index, Boot Protocol, Execution Protocol, Validation Protocol) are required for *executable* operation, beyond mere comprehension.

## 5. Loading Policy

SM-LP-01. Loading order is fixed by `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md`: boot set first (CONSTITUTION → RMM → KERNEL_SCOPE_DEFINITION), then the read order of KERNEL_DOCUMENT_REGISTRY §7 on demand.

SM-LP-02. No operation begins before boot completion (KERNEL_BOOT_PROTOCOL §3).

SM-LP-03. Loading is read-only and SHALL NOT modify any loaded artifact (KERNEL_SCOPE_DEFINITION §10.5 Auditability; RMM `View` "may not modify").

## 6. Version Policy

SM-VP-01. The Skill version tracks the Kernel version line using semantic versioning `MAJOR.MINOR.PATCH` (KERNEL_STRUCTURE_SPEC §4.4, §5.3):
- MAJOR: breaking change to an entity definition, contract, or schema.
- MINOR: non-breaking addition or clarification.
- PATCH: non-substantive correction.

SM-VP-02. Within a MAJOR version the Kernel maintains backward compatibility; existing consumer references continue to resolve (KERNEL_SCOPE_DEFINITION §10.10, §12.10).

SM-VP-03. The frozen substrate version is `RMM v1.1` (KERNEL_DOCUMENT_REGISTRY §10: RMM FROZEN). A frozen artifact changes only via the unfreeze/refreeze cycle authorized by Approval (KERNEL_STRUCTURE_SPEC §6.1).

SM-VP-04. Consumers reference a specific Kernel version; the Kernel evolves independently of any consumer (KERNEL_SCOPE_DEFINITION §9.6).

---

## QUALITY GATE (PCS) — PASS

| Gate | Result | Note |
|---|---|---|
| Engineering Self Review | PASS | Identity, inputs, outputs, artifacts, loading, version each cite KSD / RMM / KDR / KBP / KSS. Nothing invented. |
| PCS Compliance Review | PASS | No prompts, no code, no technology, no product, no new entity. "Skill" marked `[UNSUPPORTED]` as an RMM entity. |
| Correction Cycle | PASS | Skill framed strictly as the Kernel substrate; all fields reduced to existing entities/documents. |
| Final Verification | PASS | Conforms to DOCUMENT_STANDARD_SPEC; defines only the six mandated topics. |

*END OF DOCUMENT*
