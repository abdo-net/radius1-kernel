<!--
  ============================================
  KERNEL_CHARTER.md — Engineering Kernel
  ============================================
  Classification:   CANONICAL
  Authority:        Constitution (per RMM CHARTER #4)
  Source of Truth:  00-CONSTITUTION/Charters/ (per RMM CHARTER #15)
  Status:           Active
  Version:          1.0.0

  This document is governed by DOCUMENT_STANDARD_SPEC.md.
  Any deviation from the Document Standard Specification format
  constitutes a non-canonical artifact and SHALL be rejected.
  ============================================
-->

# KERNEL CHARTER

## Section A: Header

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Title**         | Kernel Charter                                           |
| **Short Title**   | KERNEL_CHARTER                                           |
| **Entity Type**   | CHARTER                                                  |
| **Classification**| CANONICAL                                                |
| **Owner**         | Constitution (per RMM CHARTER #4)                        |
| **Source of Truth**| `00-CONSTITUTION/Charters/` (per RMM CHARTER #15)       |
| **Status**        | Active                                                   |
| **Version**       | 1.0.0                                                    |
| **Created**       | 2026-06-26                                               |
| **Last Updated**  | 2026-06-26                                               |
| **RMM Entity**    | CHARTER                                                  |
| **RMM Properties**| #1 Name, #2 Purpose, #3 Responsibility, #4 Owner, #5 Lifecycle, |
|                   | #6 Allowed Relationships, #7 Forbidden Relationships, #8 Cardinality, |
|                   | #9 Stability, #10 Versionable, #11 Freezable, #12 AI Creatable, |
|                   | #13 AI Modifiable, #14 Human Modifiable, #15 SourceOfTruth |

---

## Section B: Metadata

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Entity**        | CHARTER                                                  |
| **Family**        | GOVERNANCE                                               |
| **Layer**         | KERNEL                                                   |
| **Stability**     | Slow (per RMM CHARTER #9)                                |
| **Versionable**   | Yes (per RMM CHARTER #10)                                |
| **Freezable**     | Yes (per RMM CHARTER #11)                                |
| **AI Creatable**  | With Approval (per RMM CHARTER #12)                      |
| **AI Modifiable** | With Approval (per RMM CHARTER #13)                      |
| **Human Modifiable**| With Approval (per RMM CHARTER #14)                     |
| **Review Cycle**  | [UNSUPPORTED — RMM does not define review cycle for CHARTER] |
| **Supersedes**    | None                                                     |
| **Superseded By** | None                                                     |

---

## Section C: Classification

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Classification**| CANONICAL                                                |
| **Basis**         | RMM CHARTER #1 (Name = Charter), #4 (Owner = Constitution), #15 (SourceOfTruth = 00-CONSTITUTION/Charters/) |
| **Scope**         | Meta-charter — defines what any Charter IS within the Kernel. This document instance is stored at `00-CONSTITUTION/Charters/KERNEL_CHARTER.md`, conforming to RMM CHARTER #15 (SourceOfTruth = `00-CONSTITUTION/Charters/`); per RMM CHARTER #8 (Cardinality = 1:N), additional Charters shall also be stored in `00-CONSTITUTION/Charters/`. |
| **Jurisdiction**  | All Charter entities within the Kernel                   |

---

## Section D: Status

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Current Status**| Active                                                   |
| **Lifecycle State**| Active (per RMM CHARTER #5: Draft → Proposed → Ratified → Active → Suspended → Dissolved) |
| **Effective Date**| 2026-06-26                                               |
| **Freeze Status** | Unfrozen                                                 |
| **Next Review**   | [UNSUPPORTED — RMM does not define review schedule for CHARTER] |

---

## Section E: Version

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Current Version**| 1.0.0                                                   |
| **Versioning Scheme**| Semantic versioning (per RMM CHARTER #10: Versionable = Yes) |
| **Version History**| See Section J: Revision History                         |
| **Baseline**      | v1.0.0 — Initial Charter                                 |

---

## Section F: Authority

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Owner**         | Constitution (per RMM CHARTER #4)                        |
| **Authority Derivation**| Established by Constitution (RMM CONSTITUTION #6: "Establishes Charter") |
| **Authority Chain**| CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR (per KSD Section 7.2) |
| **May Govern**    | GovernanceBody (per RMM CHARTER #6: "Governs GovernanceBody") |
| **May Delegate**  | Authority (per RMM CHARTER #6: "Delegates Authority")    |
| **May Reference** | Constitution (per RMM CHARTER #6: "References Constitution") |
| **Cardinality**   | 1:N — Multiple Charters may exist within the Kernel (per RMM CHARTER #8) |

**Normative Statement:** This document is the meta-charter — it defines what any Charter IS. Due to 1:N cardinality, the Kernel may contain multiple Charters, each governing a distinct GovernanceBody, project, or module. This Charter is the Charter of Charters.

---

## Section G: Dependencies

### G.1 Normative References (Allowed)

The following documents are normative references upon which this Charter depends. All are classified as **Normative**.

| # | Document | Entity Type | Owner | Source of Truth | Relationship |
|---|----------|-------------|-------|-----------------|--------------|
| 1 | RMM_v1.1.md | DOCUMENT (contains 79 entity definitions) | Constitution (per RMM KERNEL #4) | 01-META-MODEL/ | Defines the CHARTER entity (RMM CHARTER #1-#15); Status: FROZEN |
| 2 | CONSTITUTION.md | CONSTITUTION | Constitution (self) | 00-CONSTITUTION/ | Establishes this Charter (RMM CONSTITUTION #6: "Establishes Charter"); supreme authority |
| 3 | KERNEL_SCOPE_DEFINITION.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines governance domain scope; KSD constraint 4 binds Charter scope |
| 4 | KERNEL_AUTHORITY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines KAM-CH authority profile for CHARTER entity |

### G.2 Forbidden Dependencies

This Charter SHALL NOT depend upon, reference, or incorporate the following:

- **Product-specific artifacts** — No product implementation document, specification, or artifact (per KERNEL_SCOPE_DEFINITION constraint 7: "No product may claim ownership of the Kernel").
- **Technology-specific artifacts** — No technology implementation document, tool specification, or infrastructure definition (per KERNEL_SCOPE_DEFINITION constraint 8: "No technology may be mandated by the Kernel").
- **Implementation-specific artifacts** — No workflow, procedure, or operational document.
- **External governance instruments** — No external authority, regulation, or governance framework outside the Kernel's jurisdiction.

---

## Section H: Revision History

| Version | Date       | Author      | Action  | Reference   | Description                |
|---------|------------|-------------|---------|-------------|----------------------------|
| 1.0.0   | 2026-06-26 | Constitution| Added   | MISSION-011 | Initial Charter            |

---

## Section I: Acceptance Block

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Status**        | Granted                                                  |
| **Approver**      | Constitution                                             |
| **Date**          | 2026-06-26                                               |
| **Method**        | Ratification                                             |
| **Conditions**    | None                                                     |
| **Basis**         | RMM CHARTER #5 Lifecycle includes Ratified state; RMM CONSTITUTION #6: "Establishes Charter" |

---

## Section J: Canonical References

| Reference | Target | Description |
|-----------|--------|-------------|
| RMM CHARTER #1 | CHARTER.Name | Name = Charter |
| RMM CHARTER #2 | CHARTER.Purpose | "To establish the existence, authority, and operating parameters of a governance body, project, or module within the kernel." |
| RMM CHARTER #3 | CHARTER.Responsibility | "Defining scope of authority, decision rights, membership, and dissolution conditions." |
| RMM CHARTER #4 | CHARTER.Owner | Owner = Constitution |
| RMM CHARTER #5 | CHARTER.Lifecycle | Draft → Proposed → Ratified → Active → Suspended → Dissolved |
| RMM CHARTER #6 | CHARTER.Allowed Relationships | "Governs GovernanceBody; Delegates Authority; References Constitution." |
| RMM CHARTER #7 | CHARTER.Forbidden Relationships | "May not be deleted (only Dissolved); may not bypass Constitution; may not self-amend." |
| RMM CHARTER #8 | CHARTER.Cardinality | Cardinality = 1:N |
| RMM CHARTER #9 | CHARTER.Stability | Stability = Slow |
| RMM CHARTER #10 | CHARTER.Versionable | Versionable = Yes |
| RMM CHARTER #11 | CHARTER.Freezable | Freezable = Yes |
| RMM CHARTER #12 | CHARTER.AI_Creatable | AI Creatable = With Approval |
| RMM CHARTER #13 | CHARTER.AI_Modifiable | AI Modifiable = With Approval |
| RMM CHARTER #14 | CHARTER.Human_Modifiable | Human Modifiable = With Approval |
| RMM CHARTER #15 | CHARTER.SourceOfTruth | SourceOfTruth = 00-CONSTITUTION/Charters/ |
| RMM CONSTITUTION #6 | CONSTITUTION.Empowers | "Establishes Charter" — The Constitution is the instrument by which Charters are established |
| RMM CONSTITUTION #6 | CONSTITUTION.Empowers | "Empowers GovernanceBody" — The Constitution empowers GovernanceBody |
| Constitution P-2 | CHARTER.Constraint | "The Charter may not bypass the Constitution." (RMM CHARTER #7) |
| KAM-CH | KAM Identifier | Identifier = KAM-CH |
| KAM-CH | KAM Purpose | "To establish the existence, authority, and operating parameters of a governance body, project, or module within the kernel." |
| KAM-CH | KAM Authority Scope | "Governs GovernanceBody; Delegates Authority; References Constitution" |
| KAM-CH | KAM Owns | [NONE — no entity lists CHARTER as Owner per RMM #4] |
| KAM-CH | KAM Controls | "Defining scope of authority, decision rights, membership, and dissolution conditions." |
| KAM-CH | KAM May Freeze | Yes (RMM CHARTER #11) |
| KAM-CH | KAM Explicit Restrictions | "May not be deleted (only Dissolved); may not bypass Constitution; may not self-amend." |
| KAM-CH | KAM Required Dependencies | Constitution |
| KSD Section 2.2 | Charter definition | "Charters, which establish the existence and operating parameters of governance bodies." |
| KSD constraint 4 | Charter scope limit | "No governance action may exceed the scope defined in the acting GovernanceBody's Charter." |
| KSD Glossary | Governance Domain | "The scope of authority assigned to a GovernanceBody by its Charter." |
| KSD Section 7.2 | Authority chain | Constitution > Charter > GovernanceBody > Role > Actor |

---
---

# PART II: CHARTER PROVISIONS

---

## 1. Purpose

**RMM Basis:** RMM CHARTER #2.

"To establish the existence, authority, and operating parameters of a governance body, project, or module within the kernel." (RMM CHARTER #2).

**Normative Statement:** A Charter is a governance instrument established by the Constitution that defines the existence, authority scope, and operating parameters of a GovernanceBody, project, or module within the Kernel. This document — the Kernel Charter — is the meta-charter that defines what any Charter must be.

**Cardinality Implication:** RMM CHARTER #8: Cardinality = 1:N. Multiple Charters may exist within the Kernel. Each Charter governs a distinct GovernanceBody, project, or module. The 1:N cardinality means one Constitution establishes many Charters. This Charter (KERNEL_CHARTER.md) is the first Charter and the template for all Charters.

---

## 2. Source of Authority

**RMM Basis:** RMM CHARTER #4; RMM CONSTITUTION #6.

RMM CHARTER #4: Owner = Constitution.

RMM CONSTITUTION #6: "Establishes Charter".

**Normative Statements:**

- The Charter derives its authority from the Constitution.
- The Constitution is the sole instrument that may establish a Charter.
- No other entity may create or authorize a Charter.
- A Charter may not bypass the Constitution (RMM CHARTER #7; Constitution P-2).
- In case of conflict between a Charter and the Constitution, the Constitution prevails (RMM CONSTITUTION #3: "overriding all other instruments in case of conflict").

---

## 3. Authority Scope

**RMM Basis:** RMM CHARTER #6 (Allowed Relationships).

A Charter exercises authority through the following mechanisms:

| Mechanism | RMM Citation | Description |
|-----------|--------------|-------------|
| **Governs GovernanceBody** | RMM CHARTER #6: "Governs GovernanceBody" | A Charter governs the GovernanceBody to which it applies. |
| **Delegates Authority** | RMM CHARTER #6: "Delegates Authority" | A Charter delegates authority from the Constitution to the governed entity. |
| **References Constitution** | RMM CHARTER #6: "References Constitution" | A Charter references the Constitution as its source of authority. |

**Normative Statement:** These three mechanisms are the complete set of authority expressions available to a Charter. No additional mechanisms are defined by RMM.

---

## 4. Scope of Control

**RMM Basis:** RMM CHARTER #3 (Responsibility).

RMM CHARTER #3: "Defining scope of authority, decision rights, membership, and dissolution conditions."

A Charter defines the following for the entity it governs:

| Control Element | RMM Basis | Description |
|-----------------|-----------|-------------|
| **Scope of authority** | RMM CHARTER #3 | What the governed entity may do. |
| **Decision rights** | RMM CHARTER #3 | What decisions the governed entity may make. |
| **Membership** | RMM CHARTER #3 | Who belongs to the governed entity. |
| **Dissolution conditions** | RMM CHARTER #3 | When and how the governed entity ceases to exist. |

**Normative Statement:** These four control elements are the complete set of responsibilities assigned to a Charter. No additional control elements are defined by RMM.

---

## 5. Charter Lifecycle

**RMM Basis:** RMM CHARTER #5.

RMM CHARTER #5: Draft → Proposed → Ratified → Active → Suspended → Dissolved.

### 5.1 States

| State | Description |
|-------|-------------|
| **Draft** | Initial creation; under development. |
| **Proposed** | Submitted for ratification. |
| **Ratified** | Formally approved as a governing instrument. |
| **Active** | In force; governing the entity to which it applies. |
| **Suspended** | Temporarily inactive; provisions not in force. |
| **Dissolved** | Permanently terminated; entity no longer governed. |

### 5.2 Transitions

```
Draft → Proposed → Ratified → Active → Suspended → Dissolved
```

### 5.3 Properties

| Property | Value | RMM Basis |
|----------|-------|-----------|
| Stability | Slow | RMM CHARTER #9 |
| Versionable | Yes | RMM CHARTER #10 |
| Freezable | Yes | RMM CHARTER #11 |
| AI Creatable | With Approval | RMM CHARTER #12 |
| AI Modifiable | With Approval | RMM CHARTER #13 |
| Human Modifiable | With Approval | RMM CHARTER #14 |

---

## 6. Charter Constraints

**RMM Basis:** RMM CHARTER #7 (Forbidden Relationships).

RMM CHARTER #7: "May not be deleted (only Dissolved); may not bypass Constitution; may not self-amend."

| Constraint | RMM Citation |
|------------|-------------|
| May not be deleted (only Dissolved) | RMM CHARTER #7 |
| May not bypass Constitution | RMM CHARTER #7; Constitution P-2 |
| May not self-amend | RMM CHARTER #7 |

**Normative Statements:**

- These constraints are absolute. No exception mechanism exists at the Charter level.
- A Charter is Dissolved, not deleted (RMM CHARTER #7).
- A Charter may not modify itself (RMM CHARTER #7: "May not self-amend").
- A Charter may not bypass the Constitution (RMM CHARTER #7; Constitution P-2).

---

## 7. Charter Cardinality

**RMM Basis:** RMM CHARTER #8.

RMM CHARTER #8: Cardinality = 1:N.

**Normative Statements:**

- Multiple Charters may exist within the Kernel.
- Each Charter governs a distinct GovernanceBody, project, or module.
- The 1:N cardinality means one Constitution establishes many Charters.
- There is no upper bound on the number of Charters defined by RMM.
- This Charter (KERNEL_CHARTER.md) is the meta-charter — it defines the pattern that all Charters must follow.

---

## 8. Relationship with the Constitution

**RMM Basis:** RMM CONSTITUTION #6; RMM CHARTER #4; RMM CHARTER #6; RMM CHARTER #7.

| Aspect | RMM Citation | State |
|--------|-------------|-------|
| Establishment | RMM CONSTITUTION #6: "Establishes Charter" | The Constitution establishes the Charter. |
| Ownership | RMM CHARTER #4: Owner = Constitution | The Constitution owns the Charter. |
| Reference | RMM CHARTER #6: "References Constitution" | The Charter references the Constitution. |
| Constraint | RMM CHARTER #7: "May not bypass Constitution" | The Charter may not bypass the Constitution. |

**Normative Statements:**

- The Constitution is the sole source of authority for any Charter (RMM CONSTITUTION #6).
- The Charter references the Constitution as its source of authority (RMM CHARTER #6).
- The Charter may not bypass the Constitution (RMM CHARTER #7; Constitution P-2).
- In case of conflict, the Constitution prevails (RMM CONSTITUTION #3: "overriding all other instruments in case of conflict").

---

## 9. Relationship with GovernanceBody

**RMM Basis:** RMM CHARTER #6; RMM GOVERNANCE_BODY #6.

| Direction | RMM Citation | State |
|-----------|-------------|-------|
| Charter → GovernanceBody | RMM CHARTER #6: "Governs GovernanceBody" | A Charter governs a GovernanceBody. |
| GovernanceBody → Charter | RMM GOVERNANCE_BODY #6: "CharteredBy Charter" | A GovernanceBody is chartered by a Charter. |

**Normative Statement:** This is a bidirectional relationship: the Charter provides the governing framework; the GovernanceBody operates within that framework. A GovernanceBody may not exist without a Charter (implied by RMM GOVERNANCE_BODY #6: "CharteredBy Charter" and KSD authority chain).

---

## 10. Relationship with Every Canonical Kernel Document

**RMM Basis:** RMM CHARTER #4, #6, #15; KAM; KERNEL_STRUCTURE_SPEC.

The following table defines the relationship between this Charter and every canonical Kernel document:

| # | Document | Entity Type | Owner | Source of Truth | Relationship to this Charter |
|---|----------|-------------|-------|-----------------|------------------------------|
| 1 | README.md | DOCUMENT | Module | Repository root | Provides human-readable entry point; governed by Kernel standards. Subordinate to Constitution and Charter. |
| 2 | RMM_v1.1.md | DOCUMENT (contains 79 entity definitions) | Constitution (per RMM KERNEL #4) | 01-META-MODEL/ | Defines the CHARTER entity (RMM CHARTER #1-#15). This Charter is an instance of the CHARTER entity. Status: FROZEN. |
| 3 | KERNEL_SCOPE_DEFINITION.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines Kernel boundaries and governance domain. KSD constraint 4: "No governance action may exceed the scope defined in the acting GovernanceBody's Charter." |
| 4 | KERNEL_STRUCTURE_SPEC.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines repository structure. Charter artifact location per RMM CHARTER #15. |
| 5 | DOCUMENT_STANDARD_SPEC.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines universal document format. This Charter conforms to this standard. |
| 6 | ARTIFACT_META_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines what an Artifact IS. This Charter is an Artifact. |
| 7 | ARTIFACT_FAMILY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Classifies all artifact families and entities (13 families, 42 entities). CHARTER is in the GOVERNANCE family. |
| 8 | Repository_State_Model.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines 10 canonical states across 2 lifecycle tracks. Charter lifecycle per RMM CHARTER #5. |
| 9 | KERNEL_DEPENDENCY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Maps dependencies between 7 documents and 7 entities (60 total dependencies). Charter dependencies per Section G. |
| 10 | KERNEL_AUTHORITY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Extracts authority from RMM for 10 entities. KAM-CH defines the authority profile of the CHARTER entity. |
| 11 | CONSTITUTION.md | CONSTITUTION | Constitution (self) | 00-CONSTITUTION/Constitution.md | Supreme governance instrument. Establishes this Charter (RMM CONSTITUTION #6). Owner of this Charter (RMM CHARTER #4). |

---

## 11. Charter Operating Parameters

**RMM Basis:** RMM CHARTER #3; KSD Section 2.2; KSD constraint 4.

A Charter SHALL define the following operating parameters for the entity it governs:

| Parameter | RMM / KSD Basis | Description |
|-----------|-----------------|-------------|
| **Existence** | RMM CHARTER #2 | The entity is established by the Charter. |
| **Authority scope** | RMM CHARTER #3 | What the entity may and may not do. |
| **Decision rights** | RMM CHARTER #3 | What decisions the entity may make. |
| **Membership** | RMM CHARTER #3 | Who belongs to the entity. |
| **Dissolution conditions** | RMM CHARTER #3 | When the entity ceases to exist. |
| **Governance domain** | KSD Glossary | The scope of authority assigned to the entity. |

**Normative Statement:** KSD constraint 4: "No governance action may exceed the scope defined in the acting GovernanceBody's Charter." This constraint binds all governance actions to the operating parameters defined in their Charter.

---

## 12. Normative References

The following documents are normatively referenced by this Charter and are binding upon its interpretation:

| # | Document | Description | Status |
|---|----------|-------------|--------|
| 1 | RMM_v1.1.md | Repository Meta-Model v1.1 — defines all 79 canonical entities and their properties. | FROZEN |
| 2 | CONSTITUTION.md | Constitution of the Engineering Kernel — supreme governance instrument. | Active |
| 3 | KERNEL_SCOPE_DEFINITION.md | Kernel Scope Definition — defines what is and is not within the Kernel. | Active |
| 4 | KERNEL_AUTHORITY_MODEL.md | Kernel Authority Model — extracts and formalizes authority relationships from RMM. | Active |

**Normative Statement:** In case of conflict between this Charter and any normative reference, the Constitution SHALL prevail (RMM CONSTITUTION #3: "overriding all other instruments in case of conflict"). In case of conflict between normative references where the Constitution is silent, RMM_v1.1.md SHALL prevail as the canonical ontology.

---

# END OF KERNEL CHARTER

<!--
  ============================================
  Document Footer
  ============================================
  Entity:        CHARTER
  Classification: CANONICAL
  Authority:     Constitution
  Version:       1.0.0
  Status:        Active
  Source:        00-CONSTITUTION/Charters/KERNEL_CHARTER.md
  ============================================
-->
