# Kernel Role Model

| | |
|---|---|
| **Title** | Kernel Role Model |
| **Short Title** | KERNEL_ROLE_MODEL |
| **Entity** | ROLE |
| **Classification** | CANONICAL |
| **Owner** | GovernanceBody |
| **Source of Truth** | `00-CONSTITUTION/` (per RMM ROLE #15) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **RMM Entity** | ROLE |
| **RMM Properties** | #1–#15 |

---

## B. METADATA

| Attribute | Value |
|---|---|
| **Entity** | ROLE |
| **Family** | GOVERNANCE |
| **Layer** | KERNEL |
| **Stability** | Slow (RMM ROLE #9) |
| **Versionable** | Yes (RMM ROLE #10) |
| **Freezable** | Yes (RMM ROLE #11) |
| **AI Creatable** | No (RMM ROLE #12) |
| **AI Modifiable** | No (RMM ROLE #13) |
| **Human Modifiable** | Yes (RMM ROLE #14) |
| **Review Cycle** | [UNSUPPORTED] |
| **Supersedes** | None |
| **Superseded By** | None |

---

## C. CLASSIFICATION

| Attribute | Value |
|---|---|
| **Classification** | CANONICAL |
| **Basis** | RMM ROLE #1 (Name = Role), RMM ROLE #4 (Owner = GovernanceBody), RMM ROLE #15 (Source of Truth = 00-CONSTITUTION/) |
| **Scope** | Defines what a Role IS within the Engineering Kernel. This document instance is stored at `02-GOVERNANCE/KERNEL_ROLE_MODEL.md`; per RMM ROLE #15 (SourceOfTruth = 00-CONSTITUTION/), Role definitions reside in 00-CONSTITUTION/. |
| **Jurisdiction** | All Role entities within the Engineering Kernel |

---

## D. STATUS

| Attribute | Value |
|---|---|
| **Status** | Active |
| **Freeze Status** | Unfrozen |

**Lifecycle (RMM ROLE #5):**

```
Proposed → Reviewed → Approved → Active → Deprecated → Retired
```

| State | Description |
|---|---|
| **Proposed** | Role definition has been drafted and submitted for review. |
| **Reviewed** | Role definition has been examined for consistency with the Constitution and RMM. |
| **Approved** | Role definition has been ratified and may become Active. |
| **Active** | Role is in effect and may be assigned to Actors. |
| **Deprecated** | Role is scheduled for retirement; no new assignments permitted. |
| **Retired** | Role is no longer in effect; existing assignments must be migrated. |

---

## E. VERSION

| Attribute | Value |
|---|---|
| **Version** | 1.0.0 |
| **Scheme** | Semantic Versioning |
| **Baseline** | Initial canonical definition of ROLE within the Engineering Kernel. |

---

## F. AUTHORITY

| Attribute | Value |
|---|---|
| **Owner** | GovernanceBody (RMM ROLE #4) |

**Authority Derivation:** Role is owned by GovernanceBody; established through Charter.

**Authority Scope (RMM ROLE #6):**

| Capability | Description |
|---|---|
| **Has Responsibility** | A Role defines what an Actor is responsible for. |
| **Has Permission** | A Role defines what an Actor is permitted to do. |
| **assigned to Actor** | A Role may be assigned to one or more Actors. |
| **may delegate to Role** | A Role may delegate authority to another Role. |

**Cardinality (RMM ROLE #8):** N — multiple Roles may exist within the Engineering Kernel. No upper bound is specified.

**Owned By Role (KAM-RL #4):** Approval, Veto.

---

## G. DEPENDENCIES

**Normative:**

| Document | Purpose |
|---|---|
| RMM_v1.1.md | Role Model Metadata — defines the schema for ROLE properties #1–#15 |
| CONSTITUTION.md | Constitution — establishes supreme constraints; RMM ROLE #7, P-3, V-12 |
| KERNEL_CHARTER.md | Charter — establishes GovernanceBody authority over Role |
| KERNEL_SCOPE_DEFINITION.md | Scope — defines Engineering Kernel boundaries |
| KERNEL_AUTHORITY_MODEL.md | Authority — defines KAM-RL profile |
| GOVERNANCE_BODY | Entity definition | GovernanceBody composes Role (RMM GOVERNANCE_BODY #6) — defined in RMM_v1.1.md |

**Forbidden Dependencies:**

| Category | Restriction |
|---|---|
| **Product-specific** | Role must not reference any product, product line, or product identifier |
| **Technology-specific** | Role must not reference any technology stack, platform, or tool |
| **Implementation-specific** | Role must not reference any implementation detail, deployment configuration, or runtime concern |

---

## H. REVISION HISTORY

| Version | Date | Author | Action | Ticket | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | Constitution | Added | MISSION-012 | Initial role model for the Engineering Kernel |

---

## I. ACCEPTANCE BLOCK

| Attribute | Value |
|---|---|
| **Status** | Granted |
| **Approver** | Constitution |
| **Date** | 2026-06-26 |
| **Method** | Ratification |
| **Conditions** | None |
| **Basis** | RMM ROLE #5: Lifecycle includes Approved state; Constitution is the supreme authority |

---

## J. CANONICAL REFERENCES

| Reference ID | Text | Source |
|---|---|---|
| **RMM ROLE #1** | Name: Role | RMM_v1.1.md |
| **RMM ROLE #2** | Purpose: To define a named set of responsibilities, permissions, and authority boundaries that can be assigned to actors. | RMM_v1.1.md |
| **RMM ROLE #3** | Responsibility: Making explicit what an actor may do, must do, and cannot do within the repository. | RMM_v1.1.md |
| **RMM ROLE #4** | Owner: GovernanceBody | RMM_v1.1.md |
| **RMM ROLE #5** | Lifecycle: Proposed → Reviewed → Approved → Active → Deprecated → Retired | RMM_v1.1.md |
| **RMM ROLE #6** | Allowed: Has Responsibility, Permission; assigned to Actor; may delegate to Role. | RMM_v1.1.md |
| **RMM ROLE #7** | Forbidden: May not contradict Constitution; may not have circular delegation. | RMM_v1.1.md |
| **RMM ROLE #8** | Cardinality: N | RMM_v1.1.md |
| **RMM ROLE #9** | Stability: Slow | RMM_v1.1.md |
| **RMM ROLE #10** | Versionable: Yes | RMM_v1.1.md |
| **RMM ROLE #11** | Freezable: Yes | RMM_v1.1.md |
| **RMM ROLE #12** | AI Creatable: No | RMM_v1.1.md |
| **RMM ROLE #13** | AI Modifiable: No | RMM_v1.1.md |
| **RMM ROLE #14** | Human Modifiable: Yes | RMM_v1.1.md |
| **RMM ROLE #15** | Source of Truth: 00-CONSTITUTION/ | RMM_v1.1.md |
| **KAM-RL** | Authority Profile for Role: Has Responsibility, Permission; assigned to Actor; may delegate to Role; owns Approval, Veto; Tier 3 | KERNEL_AUTHORITY_MODEL.md |
| **Constitution P-3** | The Role may not contradict the Constitution. | CONSTITUTION.md |
| **Constitution V-12** | No entity may contradict the Constitution. | CONSTITUTION.md |
| **RMM GOVERNANCE_BODY #4** | Owner = Constitution | RMM_v1.1.md |
| **RMM ROLE #4** | Owner = GovernanceBody — Role is owned by GovernanceBody | RMM_v1.1.md |
| **RMM GOVERNANCE_BODY #6** | ComposedOf Role — GovernanceBody is composed of Roles | RMM_v1.1.md |
| **RMM ACTOR #6** | Has Role — Actor has a Role | RMM_v1.1.md |
| **RMM ACTOR #7** | May not have no Role — Actor must have at least one Role | RMM_v1.1.md |
| **KSD Section 7.2** | Authority chain: Constitution > Charter > GovernanceBody > Role > Actor | KERNEL_SCOPE_DEFINITION.md |

---

# PART II: ROLE PROVISIONS

---

## 1. PURPOSE

> *"To define a named set of responsibilities, permissions, and authority boundaries that can be assigned to actors."* — RMM ROLE #2

A Role defines responsibilities, permissions, and authority boundaries assigned to actors. A Role makes explicit what an actor may do, must do, and cannot do within the repository.

---

## 2. SOURCE OF AUTHORITY

RMM ROLE #4: Owner = GovernanceBody.

RMM GOVERNANCE_BODY #6: "ComposedOf Role" — GovernanceBody is composed of Roles.

Role derives authority from GovernanceBody. GovernanceBody is composed of Roles. The bidirectional nature of this relationship is resolved by the authority chain defined in KSD Section 7.2: Constitution > Charter > GovernanceBody > Role > Actor.

---

## 3. AUTHORITY SCOPE

**From RMM ROLE #6:**

| Capability | Description |
|---|---|
| **Has Responsibility** | The Role defines responsibilities that an Actor must fulfill. |
| **Has Permission** | The Role defines permissions that an Actor is granted. |
| **assigned to Actor** | The Role may be assigned to one or more Actors. |
| **may delegate to Role** | The Role may delegate its authority to another Role. |

**From KAM-RL:**

| Attribute | Value |
|---|---|
| **Controls** | Making explicit what an actor may do, must do, and cannot do within the repository. |
| **May Freeze** | Yes (RMM ROLE #11) |
| **Tier** | TIER 3 |

---

## 4. SCOPE OF CONTROL

RMM ROLE #3: *"Making explicit what an actor may do, must do, and cannot do within the repository."*

| Control Dimension | Description | RMM Basis |
|---|---|---|
| **Responsibilities** | Obligations an Actor must discharge | RMM ROLE #6 |
| **Permissions** | Actions an Actor is authorized to perform | RMM ROLE #6 |
| **Authority Boundaries** | Limits beyond which an Actor may not act | RMM ROLE #2 |

---

## 5. ROLE LIFECYCLE

RMM ROLE #5: `Proposed → Reviewed → Approved → Active → Deprecated → Retired`

### 5.1 Lifecycle States

| State | Definition | Entry Criteria | Exit Criteria |
|---|---|---|---|
| **Proposed** | Role definition has been drafted | Role is created | Submitted for review |
| **Reviewed** | Role definition has been examined | Proposed role passes review gate | Approved or rejected |
| **Approved** | Role definition has been ratified | Reviewed role passes approval gate | Activated or held |
| **Active** | Role is in effect | Approved role is deployed | Deprecated by authority |
| **Deprecated** | Role is scheduled for retirement | Active role is marked deprecated | All assignments migrated |
| **Retired** | Role is no longer in effect | Deprecated role has no assignments | Terminal state |

### 5.2 Lifecycle Properties

| Property | Value | RMM Basis |
|---|---|---|
| Stability | Slow | RMM ROLE #9 |
| Versionable | Yes | RMM ROLE #10 |
| Freezable | Yes | RMM ROLE #11 |
| AI Creatable | No | RMM ROLE #12 |
| AI Modifiable | No | RMM ROLE #13 |
| Human Modifiable | Yes | RMM ROLE #14 |

---

## 6. ROLE CONSTRAINTS

RMM ROLE #7 exact text: *"May not contradict Constitution; may not have circular delegation."*

### 6.1 Constitutional Constraint

No Role may contradict the Constitution. Constitution P-3: *"The Role may not contradict the Constitution."* Constitution V-12: *"No entity may contradict the Constitution."*

### 6.2 Delegation Constraint

No Role may have circular delegation. If Role A delegates to Role B, then Role B (directly or through a chain of delegations) may not delegate back to Role A.

### 6.3 Exception Mechanism

There is no exception mechanism. Constraints are absolute.

---

## 7. ROLE CARDINALITY

RMM ROLE #8: N.

Multiple Roles may exist within the Engineering Kernel. There is no upper bound on the number of Roles. A single Actor may hold multiple Roles; a single Role may be assigned to multiple Actors.

---

## 8. ROLE OWNERSHIP

RMM ROLE #4: Owner = GovernanceBody.

KAM-RL #4: Role owns Approval, Veto.

| Ownership Dimension | Value | Source |
|---|---|---|
| **Owned By** | GovernanceBody | RMM ROLE #4 |
| **Owns** | Approval, Veto | KAM-RL #4 |

RMM APPROVAL #4: Owner = Role.

RMM VETO #4: Owner = Role.

---

## 9. ROLE DEPENDENCIES

KAM-RL #12: Required Dependencies.

| Dependency | Type | RMM / Source |
|---|---|---|
| Constitution | Normative | RMM ROLE #7, Constitution P-3, Constitution V-12 |
| Charter | Normative | Authority derivation — GovernanceBody established by Charter |
| GovernanceBody | Structural | RMM ROLE #4 — Owner; RMM GOVERNANCE_BODY #6 — composition |
| Actor | Structural | RMM ROLE #6 — assigned to Actor; RMM ACTOR #6, RMM ACTOR #7 |

---

## 10. RELATIONSHIP WITH CONSTITUTION

RMM ROLE #7: May not contradict Constitution.

Constitution P-3: *"The Role may not contradict the Constitution."*

Constitution V-12: *"No entity may contradict the Constitution."*

The Constitution is the supreme authority. In any conflict between a Role definition and the Constitution, the Constitution prevails. No Role may be Approved or Active if it contradicts the Constitution. This constraint applies to all lifecycle states.

---

## 11. RELATIONSHIP WITH GOVERNANCEBODY

RMM GOVERNANCE_BODY #6: *"ComposedOf Role"* — GovernanceBody is composed of Roles.

RMM ROLE #4: Owner = GovernanceBody.

The relationship between Role and GovernanceBody is bidirectional:
- GovernanceBody **owns** Role (RMM ROLE #4).
- GovernanceBody **is composed of** Roles (RMM GOVERNANCE_BODY #6).

This bidirectional relationship does not create a circular dependency because ownership flows from GovernanceBody to Role, while composition flows from GovernanceBody through Role. The authority chain (Constitution > Charter > GovernanceBody > Role > Actor) resolves any ambiguity.

---

## 12. RELATIONSHIP WITH ACTOR

RMM ROLE #6: *"assigned to Actor"* — Role may be assigned to Actor.

RMM ACTOR #6: *"Has Role"* — Actor has a Role.

RMM ACTOR #7: *"May not have no Role"* — Actor must have at least one Role.

| Relationship | Direction | Cardinality | Source |
|---|---|---|---|
| Role assigned to Actor | Role → Actor | 1:N | RMM ROLE #6 |
| Actor has Role | Actor → Role | N:1 | RMM ACTOR #6 |
| Actor must have ≥1 Role | Constraint | — | RMM ACTOR #7 |

KAM-AC #7: Actor may not have no Role.

An Actor must have at least one Role. An Actor without a Role is not a valid Actor within the Engineering Kernel. A Role without an Actor assignment may exist (in Approved or Active state), but it does not grant any authority until assigned.

---

## 13. RELATIONSHIP WITH APPROVAL AND VETO

KAM-RL #4: Role owns Approval, Veto.

RMM APPROVAL #4: Owner = Role.

RMM VETO #4: Owner = Role.

| Entity | Relationship | Source |
|---|---|---|
| Role | Owns Approval | KAM-RL #4, RMM APPROVAL #4 |
| Role | Owns Veto | KAM-RL #4, RMM VETO #4 |

The ownership of Approval and Veto by Role means that a Role is the entity through which Approval and Veto are exercised within the authority chain. Approval and Veto are not owned directly by Actors; they flow through the Role assigned to the Actor.

---

## 14. RELATIONSHIP WITH EVERY CANONICAL KERNEL DOCUMENT

| # | Document | Source of Truth | Relationship to ROLE |
|---|----------|----------------|----------------------|
| 1 | RMM_v1.1.md | 01-META-MODEL/ | Defines ROLE entity (RMM ROLE #1-#15). Status: FROZEN. |
| 2 | CONSTITUTION.md | 00-CONSTITUTION/ | ROLE may not contradict Constitution (RMM ROLE #7; Constitution P-3, V-12). |
| 3 | KERNEL_SCOPE_DEFINITION.md | 01-META-MODEL/ | Defines governance domain; ROLE operates within scope boundaries. |
| 4 | KERNEL_STRUCTURE_SPEC.md | 01-META-MODEL/ | ROLE stored in 02-GOVERNANCE/ per repository structure. |
| 5 | DOCUMENT_STANDARD_SPEC.md | 01-META-MODEL/ | Defines document format; this document conforms. |
| 6 | ARTIFACT_META_MODEL.md | 01-META-MODEL/ | Defines what an Artifact IS; ROLE is an Artifact. |
| 7 | ARTIFACT_FAMILY_MODEL.md | 01-META-MODEL/ | ROLE is in GOVERNANCE family (13 families, 42 entities). |
| 8 | Repository_State_Model.md | 01-META-MODEL/ | Defines generic state model framework. Role states defined by RMM ROLE #5. |
| 9 | KERNEL_DEPENDENCY_MODEL.md | 01-META-MODEL/ | ROLE dependencies per KAM-RL #12. |
| 10 | KERNEL_AUTHORITY_MODEL.md | 01-META-MODEL/ | KAM-RL defines authority profile of ROLE entity. |
| 11 | KERNEL_DOCUMENT_REGISTRY.md | 00-CONSTITUTION/ | Registry catalogues this document. |
| 12 | KERNEL_CHARTER.md | 00-CONSTITUTION/ | ROLE derives authority through Charter → GovernanceBody chain. |
| 13 | KERNEL_ROLE_MODEL.md (this) | 02-GOVERNANCE/ | This document — defines ROLE entity. |

---

## 15. ROLE INVARIANTS

| Invariant ID | Statement | RMM Basis |
|---|---|---|
| **RI-01** | Every Role has an Owner = GovernanceBody. | RMM ROLE #4 |
| **RI-02** | Every Role has explicit Responsibilities and Permissions. | RMM ROLE #6 |
| **RI-03** | No Role may contradict the Constitution. | RMM ROLE #7, Constitution P-3, Constitution V-12 |
| **RI-04** | No Role may have circular delegation. | RMM ROLE #7 |
| **RI-05** | Every Actor must have at least one Role. | RMM ACTOR #7, KAM-AC #7 |

These invariants hold in all lifecycle states except Proposed (where invariants are validated during Review).

---

## 16. NORMATIVE REFERENCES

| Reference | Description | Role in this Document |
|---|---|---|
| RMM_v1.1.md | Role Model Metadata — defines the schema and properties for all Kernel entities | Schema authority for ROLE #1–#15 |
| CONSTITUTION.md | Constitution — supreme governing document of the Engineering Kernel | Constraint authority; P-3, V-12 |
| KERNEL_CHARTER.md | Charter — establishes GovernanceBody and its authority over Kernel entities | Authority chain derivation |
| KSD (Kernel Standards Document) | Defines the authority chain in Section 7.2 | Authority chain: Constitution > Charter > GovernanceBody > Role > Actor |
| KAM (Kernel Authority Model) | Defines authority profiles including KAM-RL | Authority scope, ownership, tier |

---

*END OF KERNEL ROLE MODEL*

| | |
|---|---|
| **Document Classification** | CANONICAL |
| **Entity** | ROLE |
| **Owner** | GovernanceBody |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Last Updated** | 2026-06-26 |
| **Source of Truth** | `00-CONSTITUTION/` (per RMM ROLE #15) |
