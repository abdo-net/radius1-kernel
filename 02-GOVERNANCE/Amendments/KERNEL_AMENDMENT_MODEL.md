# KERNEL_AMENDMENT_MODEL.md

**Short Name:** KERNEL_AMENDMENT_MODEL  
**Entity:** AMENDMENT  
**Classification:** CANONICAL  
**Owner:** Actor (RMM AMENDMENT #4)  
**Source of Truth:** `02-GOVERNANCE/Amendments/KERNEL_AMENDMENT_MODEL.md`  
**Status:** Active  
**Version:** 1.0.0  
**RMM Entity:** AMENDMENT  
**RMM Properties:** #1-#15  

---

## Section A: Document Identification

| Property | Value |
|----------|-------|
| Title | Kernel Amendment Model |
| Short | KERNEL_AMENDMENT_MODEL |
| Entity | AMENDMENT |
| Classification | CANONICAL |
| Owner | Actor (RMM AMENDMENT #4) |
| Source of Truth | `02-GOVERNANCE/Amendments/KERNEL_AMENDMENT_MODEL.md` |
| Status | Active |
| Version | 1.0.0 |
| RMM Entity | AMENDMENT |
| RMM Properties | #1-#15 |

---

## Section B: Entity Properties

| Property | Value | Basis |
|----------|-------|-------|
| Entity | AMENDMENT | RMM AMENDMENT #1 |
| Family | GOVERNANCE | ARTIFACT_FAMILY_MODEL.md |
| Layer | KERNEL | KERNEL_STRUCTURE_SPEC.md |
| Stability | Fast | RMM AMENDMENT #9 |
| Versionable | Yes | RMM AMENDMENT #10 |
| Freezable | Yes | RMM AMENDMENT #11 |
| AI Creatable | With Approval | RMM AMENDMENT #12 |
| AI Modifiable | With Approval | RMM AMENDMENT #13 |
| Human Modifiable | With Approval | RMM AMENDMENT #14 |
| Review Cycle | [UNSUPPORTED] | — |
| Supersedes | None | — |
| Superseded By | None | — |

---

## Section C: Classification

| Property | Value | Basis |
|----------|-------|-------|
| Classification | CANONICAL | RMM AMENDMENT #1, #4, #15 |
| Scope | Defines what an Amendment IS | RMM AMENDMENT #1 |
| Jurisdiction | All Amendment entities | RMM AMENDMENT #1 |

---

## Section D: Status

| Property | Value | Basis |
|----------|-------|-------|
| Status | Active | RMM AMENDMENT #5 |
| Lifecycle | Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded | RMM AMENDMENT #5 |
| Freeze Status | Unfrozen | RMM AMENDMENT #11 |

---

## Section E: Version

| Property | Value | Basis |
|----------|-------|-------|
| Version | 1.0.0 | Semantic versioning |
| Baseline | Initial | — |

---

## Section F: Ownership and Authority

| Property | Value | Basis |
|----------|-------|-------|
| Owner | Actor | RMM AMENDMENT #4 |
| Authority Scope | Amends Entity; ProposedBy Role; ReviewedBy Review; ApprovedBy GovernanceBody | RMM AMENDMENT #6 |
| Cardinality | N:M | RMM AMENDMENT #8 |

**UNIQUE:** Amendment is owned by Actor, not Constitution or GovernanceBody. No other entity claims ownership of Amendment per RMM AMENDMENT #4.

---

## Section G: Normative References

### Normative

| Document | Location | Purpose |
|----------|----------|---------|
| RMM_v1.1.md | `01-META-MODEL/` | Defines AMENDMENT entity — FROZEN |
| CONSTITUTION.md | `00-CONSTITUTION/` | Constitution is amendable; AmendmentInProgress state |
| KERNEL_ROLE_MODEL.md | `00-CONSTITUTION/` | Role proposes Amendment |
| KERNEL_REVIEW_MODEL.md | `05-EVIDENCE/Reviews/` | Review reviews Amendment |
| KERNEL_GOVERNANCE_MODEL.md | `02-GOVERNANCE/` | GovernanceBody approves Amendment |

### Forbidden

Product, Technology, Implementation.

---

## Section H: Change Log

| Version | Date | Changed By | Change Type | Reference | Description |
|---------|------|------------|-------------|-----------|-------------|
| 1.0.0 | 2026-06-26 | Constitution | Added | MISSION-017 | Initial amendment model |

---

## Section I: Approval

| Property | Value | Basis |
|----------|-------|-------|
| Status | Granted | RMM AMENDMENT #5 |
| Approver | Constitution | RMM AMENDMENT #5 |
| Date | 2026-06-26 | — |
| Method | Ratification | RMM AMENDMENT #5 |
| Conditions | None | — |
| Basis | RMM AMENDMENT #5 | — |

---

## Section J: RMM Properties Manifest

| # | Property | Value | Basis |
|---|----------|-------|-------|
| 1 | Name | Amendment | RMM AMENDMENT #1 |
| 2 | Purpose | To propose and record a formal change to an existing governance instrument that alters its substance | RMM AMENDMENT #2 |
| 3 | Responsibility | Documenting the proposed change, rationale, impact assessment, and required approval path | RMM AMENDMENT #3 |
| 4 | Owner | Actor | RMM AMENDMENT #4 |
| 5 | Lifecycle | Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded | RMM AMENDMENT #5 |
| 6 | Allowed | Amends Entity; ProposedBy Role; ReviewedBy Review; ApprovedBy GovernanceBody | RMM AMENDMENT #6 |
| 7 | Forbidden | May not be applied without approval; may not alter entities outside proposer's jurisdiction | RMM AMENDMENT #7 |
| 8 | Cardinality | N:M | RMM AMENDMENT #8 |
| 9 | Stability | Fast | RMM AMENDMENT #9 |
| 10 | Versionable | Yes | RMM AMENDMENT #10 |
| 11 | Freezable | Yes | RMM AMENDMENT #11 |
| 12 | AI Creatable | With Approval | RMM AMENDMENT #12 |
| 13 | AI Modifiable | With Approval | RMM AMENDMENT #13 |
| 14 | Human Modifiable | With Approval | RMM AMENDMENT #14 |
| 15 | Source of Truth | `02-GOVERNANCE/Amendments/` | RMM AMENDMENT #15 |

---

# PART II: AMENDMENT PROVISIONS

## 1. Purpose

> **RMM AMENDMENT #2:** "To propose and record a formal change to an existing governance instrument that alters its substance."

An Amendment exists to propose and record a formal change to an existing governance instrument that alters its substance. The purpose is not to create new instruments, but to alter existing ones through a governed process.

---

## 2. Source of Authority

> **RMM AMENDMENT #4:** Owner = Actor.

Amendment derives from Actor — the Actor proposes the amendment. The Actor is the originating authority for all Amendments. No Amendment exists without an Actor as its proposer and owner.

---

## 3. Authority Scope

> **RMM AMENDMENT #6:** Amends Entity; ProposedBy Role; ReviewedBy Review; ApprovedBy GovernanceBody.

| Relationship | Target Entity | Direction | Basis |
|--------------|-------------|-----------|-------|
| Amends | Entity | Amendment → Entity | RMM AMENDMENT #6 |
| ProposedBy | Role | Amendment ← Role | RMM AMENDMENT #6 |
| ReviewedBy | Review | Amendment ← Review | RMM AMENDMENT #6 |
| ApprovedBy | GovernanceBody | Amendment ← GovernanceBody | RMM AMENDMENT #6 |

---

## 4. Scope of Control

> **RMM AMENDMENT #3:** "Documenting the proposed change, rationale, impact assessment, and required approval path."

The Amendment entity is responsible for documenting:
- The proposed change to the target entity
- The rationale for the change
- The impact assessment of the change
- The required approval path for the change

---

## 5. Amendment Lifecycle

> **RMM AMENDMENT #5:** Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded.

### 5.1 Lifecycle States

| State | Name | Description | Entry Condition | Exit Condition |
|-------|------|-------------|-----------------|----------------|
| S1 | Drafted | Amendment is being prepared by Actor | Actor initiates | Actor submits |
| S2 | Submitted | Amendment is formally submitted for review | Exit S1 | Review begins |
| S3 | Reviewed | Amendment is under review | Exit S2 | Review completes |
| S4 | Approved | Amendment is approved by GovernanceBody | Exit S3 | Ratification begins |
| S5 | Ratified | Amendment is ratified | Exit S4 | Application begins |
| S6 | Applied | Amendment is applied to target entity | Exit S5 | Recording completes |
| S7 | Recorded | Amendment is recorded as complete | Exit S6 | Terminal state |

### 5.2 Lifecycle Properties

| Property | Value | Basis |
|----------|-------|-------|
| Total States | 7 | RMM AMENDMENT #5 |
| Initial State | Drafted | RMM AMENDMENT #5 |
| Terminal State | Recorded | RMM AMENDMENT #5 |
| Reversible | [UNSUPPORTED] | — |
| Concurrency | [UNSUPPORTED] | — |
| Timeout | [UNSUPPORTED] | — |

---

## 6. Amendment Constraints

> **RMM AMENDMENT #7:** "May not be applied without approval; may not alter entities outside proposer's jurisdiction."

| Constraint | Text | Exception |
|------------|------|-----------|
| AC-01 | May not be applied without approval | None |
| AC-02 | May not alter entities outside proposer's jurisdiction | None |

No exception. Both constraints are absolute.

---

## 7. Amendment Cardinality

> **RMM AMENDMENT #8:** N:M.

An Amendment may amend multiple entities (N), and an entity may be subject to multiple Amendments (M). The relationship between Amendment and Entity is many-to-many.

---

## 8. Amendment Ownership

> **RMM AMENDMENT #4:** Owner = Actor.

**UNIQUE:** Actor owns Amendment. Amendment is not owned by Constitution, GovernanceBody, Role, or Review. The Actor is the sole owner class for Amendment entities per RMM AMENDMENT #4.

---

## 9. Relationship with Constitution

> **RMM CONSTITUTION #5:** Lifecycle includes AmendmentInProgress state.

> **CONSTITUTION.md Section 11:** Amendment Authority — Constitution is amendable.

The Constitution is itself amendable. When the Constitution is under amendment, it enters the AmendmentInProgress state per RMM CONSTITUTION #5. The Amendment model applies to the Constitution as it applies to all amendable entities.

> **RMM CONSTITUTION #7:** May not be overridden except by own amendment procedure.

The Constitution's amendment procedure is the sole mechanism for overriding the Constitution. The Amendment model is the vehicle for this procedure.

---

## 10. Relationship with Role, Review, GovernanceBody

> **RMM AMENDMENT #6:** ProposedBy Role, ReviewedBy Review, ApprovedBy GovernanceBody.

### Amendment Flow

| Step | Actor | Action | Entity |
|------|-------|--------|--------|
| 1 | Role | Proposes | Amendment |
| 2 | Review | Reviews | Amendment |
| 3 | GovernanceBody | Approves | Amendment |

Amendment flows through three governance entities:
- **Role** proposes the Amendment (RMM AMENDMENT #6: ProposedBy Role)
- **Review** evaluates the Amendment (RMM AMENDMENT #6: ReviewedBy Review)
- **GovernanceBody** approves the Amendment (RMM AMENDMENT #6: ApprovedBy GovernanceBody)

> **RMM ROLE #6:** Role may propose Amendment (implied from "ProposedBy Role").

> **RMM REVIEW #6:** Review reviews Amendment (implied from "ReviewedBy Review").

> **RMM GOVERNANCE_BODY #6:** GovernanceBody approves Amendment (implied from "ApprovedBy GovernanceBody").

---

## 11. Amendment Invariants

| ID | Invariant | Basis |
|----|-----------|-------|
| AI-01 | Every Amendment has Owner = Actor | RMM AMENDMENT #4 |
| AI-02 | Every Amendment Amends an Entity | RMM AMENDMENT #6 |
| AI-03 | No Amendment may be applied without approval | RMM AMENDMENT #7 |
| AI-04 | No Amendment may alter entities outside proposer's jurisdiction | RMM AMENDMENT #7 |
| AI-05 | Every Amendment must be ProposedBy a Role | RMM AMENDMENT #6 |

---

## 12. Relationship with Every Canonical Kernel Document

The Amendment model maintains the following relationships with Canonical Kernel documents:

| # | Document | Location | Relationship | Nature |
|---|----------|----------|--------------|--------|
| 1 | RMM_v1.1.md | `01-META-MODEL/` | RMM defines AMENDMENT entity | Normative, FROZEN |
| 2 | CONSTITUTION.md | `00-CONSTITUTION/` | Constitution is amendable; AmendmentInProgress state | Normative |
| 3 | KERNEL_SCOPE_DEFINITION.md | `01-META-MODEL/` | Defines scope within which Amendment operates | Normative |
| 4 | KERNEL_STRUCTURE_SPEC.md | `01-META-MODEL/` | `02-GOVERNANCE/Amendments/` per RMM #15 | Normative |
| 5 | DOCUMENT_STANDARD_SPEC.md | `01-META-MODEL/` | This document's format | Normative |
| 6 | ARTIFACT_META_MODEL.md | `01-META-MODEL/` | Artifact definition for Amendment | Normative |
| 7 | ARTIFACT_FAMILY_MODEL.md | `01-META-MODEL/` | AMENDMENT in GOVERNANCE family | Normative |
| 8 | Repository_State_Model.md | `01-META-MODEL/` | State framework for lifecycle | Normative |
| 9 | KERNEL_DEPENDENCY_MODEL.md | `01-META-MODEL/` | Dependencies between Amendment and other entities | Normative |
| 10 | KERNEL_AUTHORITY_MODEL.md | `01-META-MODEL/` | Authority derivation for Amendment | Normative |
| 11 | KERNEL_DOCUMENT_REGISTRY.md | `00-CONSTITUTION/` | This document is registered | Normative |
| 12 | KERNEL_CHARTER.md | `00-CONSTITUTION/Charters/` | Charter scope includes Amendment | Normative |
| 13 | KERNEL_ROLE_MODEL.md | `00-CONSTITUTION/` | Role proposes Amendment | Normative |
| 14 | KERNEL_GOVERNANCE_MODEL.md | `02-GOVERNANCE/` | GovernanceBody approves Amendment | Normative |
| 15 | KERNEL_DECISION_MODEL.md | `05-EVIDENCE/` | Decision process may involve Amendment | Normative |
| 16 | KERNEL_EVIDENCE_MODEL.md | `05-EVIDENCE/` | Evidence may support Amendment | Normative |
| 17 | KERNEL_REVIEW_MODEL.md | `05-EVIDENCE/Reviews/` | Review reviews Amendment | Normative |
| 18 | KERNEL_AMENDMENT_MODEL.md (this) | `02-GOVERNANCE/Amendments/` | This document | Self-referential |

---

## 13. Normative References

| # | Reference | Citation | Purpose |
|---|-----------|----------|---------|
| 1 | RMM_v1.1.md | RMM AMENDMENT #1-#15 | Defines all Amendment properties |
| 2 | CONSTITUTION.md | Section 11; RMM CONSTITUTION #5, #7 | Amendment authority and procedure |
| 3 | KERNEL_ROLE_MODEL.md | RMM ROLE #6 | Role proposes Amendment |
| 4 | KERNEL_REVIEW_MODEL.md | RMM REVIEW #6 | Review reviews Amendment |
| 5 | KERNEL_GOVERNANCE_MODEL.md | RMM GOVERNANCE_BODY #6 | GovernanceBody approves Amendment |
| 6 | ARTIFACT_FAMILY_MODEL.md | GOVERNANCE family | Amendment family classification |

---

# CROSS REFERENCES

- **CONSTITUTION.md Section 11:** Amendment Authority — Constitution is amendable.
- **RMM CONSTITUTION #5:** Lifecycle includes AmendmentInProgress state.
- **RMM CONSTITUTION #7:** May not be overridden except by own amendment procedure.
- **RMM ROLE #6:** Role may propose Amendment (implied from "ProposedBy Role").
- **RMM REVIEW #6:** Review reviews Amendment (implied from "ReviewedBy Review").
- **RMM GOVERNANCE_BODY #6:** GovernanceBody approves Amendment (implied from "ApprovedBy GovernanceBody").

---

# APPENDIX: RMM AMENDMENT ENTITY (COMPLETE)

| # | Property | Value |
|---|----------|-------|
| 1 | Name | Amendment |
| 2 | Purpose | To propose and record a formal change to an existing governance instrument that alters its substance |
| 3 | Responsibility | Documenting the proposed change, rationale, impact assessment, and required approval path |
| 4 | Owner | Actor |
| 5 | Lifecycle | Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded |
| 6 | Allowed | Amends Entity; ProposedBy Role; ReviewedBy Review; ApprovedBy GovernanceBody |
| 7 | Forbidden | May not be applied without approval; may not alter entities outside proposer's jurisdiction |
| 8 | Cardinality | N:M |
| 9 | Stability | Fast |
| 10 | Versionable | Yes |
| 11 | Freezable | Yes |
| 12 | AI Creatable | With Approval |
| 13 | AI Modifiable | With Approval |
| 14 | Human Modifiable | With Approval |
| 15 | Source of Truth | `02-GOVERNANCE/Amendments/` |

---

*End of KERNEL_AMENDMENT_MODEL.md*
