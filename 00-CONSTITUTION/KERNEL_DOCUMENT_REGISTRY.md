<!--
  ============================================
  KERNEL_DOCUMENT_REGISTRY.md — Engineering Kernel
  ============================================
  Classification:   CANONICAL
  Authority:        Constitution (per CONSTITUTION.md, the Constitution
                    is the supreme authority; this Registry lives in
                    00-CONSTITUTION/)
  Source of Truth:  00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md
  Status:           Active
  Version:          1.1.0

  This document is governed by DOCUMENT_STANDARD_SPEC.md.
  Any deviation from the Document Standard Specification format
  constitutes a non-canonical artifact and SHALL be rejected.
  ============================================
-->

# KERNEL DOCUMENT REGISTRY

## Section A: Header

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Title**         | Kernel Document Registry                                 |
| **Short Title**   | KERNEL_DOCUMENT_REGISTRY                                 |
| **Entity Type**   | DOCUMENT                                                 |
| **Classification**| CANONICAL                                                |
| **Owner**         | Constitution                                             |
| **Source of Truth**| `00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md`           |
| **Status**        | Active                                                   |
| **Version**       | 1.1.0                                                    |
| **Created**       | 2026-06-26                                               |
| **Last Updated**  | 2026-06-27                                               |
| **RMM Entity**    | DOCUMENT                                                 |
| **RMM Properties**| #1 Name, #2 Purpose, #3 Scope, #4 Owner, #5 Lifecycle,  |
|                   | #6 Empowers, #7 Constraint, #8 Cardinality, #9 Stability,|
|                   | #10 Versionable, #11 Freezable, #12 AI Creatable,        |
|                   | #13 AI Modifiable, #14 Human Modifiable, #15 SourceOfTruth |

---

## Section B: Metadata

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Entity**        | KERNEL_DOCUMENT_REGISTRY                                 |
| **Family**        | DOCUMENT (per ARTIFACT_FAMILY_MODEL Section 2)           |
| **Layer**         | KERNEL                                                   |
| **Stability**     | Moderate (per RMM DOCUMENT #9)                           |
| **Versionable**   | Yes (per RMM DOCUMENT #10)                               |
| **Freezable**     | Yes (per RMM DOCUMENT #11)                               |
| **AI Creatable**  | No (per RMM DOCUMENT #12, modified by Constitution)      |
| **AI Modifiable** | With Approval (per RMM DOCUMENT #13)                     |
| **Human Modifiable**| With Approval (per RMM DOCUMENT #14, CANONICAL class)  |
| **Review Cycle**  | [UNSUPPORTED — RMM does not define review cycle for DOCUMENT] |
| **Supersedes**    | None                                                     |
| **Superseded By** | None                                                     |

---

## Section C: Classification

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Classification**| CANONICAL                                                |
| **Basis**         | DOCUMENT_STANDARD_SPEC Section 3.3; RMM DOCUMENT properties 1-15 |
| **Scope**         | Single authoritative registry of all canonical Kernel documents plus Phase 2 normative documents |
| **Jurisdiction**  | All canonical and normative documents within the Kernel  |

---

## Section D: Status

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Current Status**| Active                                                   |
| **Lifecycle State**| Active (per RMM DOCUMENT #5: Draft → Review → Approved → Published → Superseded → Archived) |
| **Effective Date**| 2026-06-27                                               |
| **Freeze Status** | Unfrozen                                                 |
| **Next Review**   | [UNSUPPORTED — RMM does not define review schedule for DOCUMENT] |

---

## Section E: Version

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Current Version**| 1.1.0                                                   |
| **Versioning Scheme**| Semantic versioning (per RMM DOCUMENT #10: Versionable = Yes) |
| **Version History**| See Section J: Revision History                         |
| **Baseline**      | v1.1.0 — Phase 2 synchronized registry                   |

---

## Section F: Authority

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Owner**         | Constitution (per RMM KERNEL #4: Owner = Constitution)   |
| **Authority Derivation**| Constitution is supreme authority (CONSTITUTION.md Section 2: "supreme governance instrument") |
| **Authority Derivation**| Constitution is the sole self-owning entity (RMM CONSTITUTION #4); KDR Owner = Constitution |
| **May Empower**   | All canonical document registration (per CONSTITUTION #6: Supersedes AllGovernanceEntities) |
| **May Establish** | Registry invariants (per RMM CONSTITUTION #6: Defines Rule) |
| **May Define**    | Document inventory, dependency matrix, ordering sequences |
| **May Supersede** | None (this is the first registry)                        |
| **May Be Overridden By**| Constitution only, by amendment procedure (per RMM CONSTITUTION #7) |
| **Cardinality**   | 1:1 — There is exactly one Kernel Document Registry      |

---

## Section G: Dependencies

### G.1 Normative References (Allowed)

The following documents are normative references upon which this Registry depends. All are classified as **Normative**.

| # | Document | Entity Type | Owner | Source of Truth | Relationship |
|---|----------|-------------|-------|-----------------|--------------|
| 1 | RMM_v1.1.md | DOCUMENT (contains 79 entity definitions) | Constitution (per RMM KERNEL #4) | 01-META-MODEL/ | Defines canonical ontology; provides entity properties #1-#15; Status: FROZEN |
| 2 | CONSTITUTION.md | CONSTITUTION | Constitution (self) | 00-CONSTITUTION/ | Supreme authority; establishes governance; authorizes this Registry |
| 3 | KERNEL_SCOPE_DEFINITION.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines Kernel boundaries; determines included/excluded documents |
| 4 | KERNEL_STRUCTURE_SPEC.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines directory structure; Source of Truth mapping |
| 5 | DOCUMENT_STANDARD_SPEC.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines document format standard; this Registry conforms |
| 6 | ARTIFACT_META_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines Artifact identity, lifecycle, invariants |
| 7 | ARTIFACT_FAMILY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines Artifact family classification |
| 8 | Repository_State_Model.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines states, transitions, prohibited transitions |
| 9 | KERNEL_DEPENDENCY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Defines document-level dependency DAG |
| 10 | KERNEL_AUTHORITY_MODEL.md | DOCUMENT | Constitution | 01-META-MODEL/ | Extracts authority from RMM for 10 entities; Constitution is supreme |

### G.2 Forbidden Dependencies

This Registry SHALL NOT depend upon, reference, or incorporate the following:

- **Product-specific artifacts** — No product implementation document (per KERNEL_SCOPE_DEFINITION Section 3.1).
- **Technology-specific artifacts** — No technology implementation document (per KERNEL_SCOPE_DEFINITION Section 3.2).
- **Implementation-specific artifacts** — No workflow, procedure, or operational document.
- **External governance instruments** — No external authority outside the Kernel's jurisdiction.
- **Derived artifacts** — No review reports, validation reports, changelogs, changesets, or future proposals.

---

## Section H: Revision History

| Version | Date       | Author      | Action  | Reference   | Description                |
|---------|------------|-------------|---------|-------------|----------------------------|
| 1.0.0   | 2026-06-26 | Constitution| Added   | MISSION-010 | Initial document registry  |
| 1.1.0   | 2026-06-27 | Engineering Kernel Architect | Updated | P2-M07 | Phase 2 synchronization: added 8 Phase 2 documents; inventoried 7 operational-layer documents |

---

## Section I: Acceptance Block

| Property          | Value                                                    |
|-------------------|----------------------------------------------------------|
| **Status**        | Granted                                                  |
| **Approver**      | Constitution                                             |
| **Date**          | 2026-06-26                                               |
| **Method**        | Ratification                                             |
| **Conditions**    | None                                                     |
| **Basis**         | RMM CONSTITUTION #5 Lifecycle: Draft → Ratified → Active → AmendmentInProgress → Ratified |

---

## Section J: Canonical References

| Reference | Target | Description |
|-----------|--------|-------------|
| RMM DOCUMENT #1 | DOCUMENT.Name | Name = Document |
| RMM DOCUMENT #2 | DOCUMENT.Purpose | "To carry structured human-readable and machine-processable information in a coherent, navigable form." |
| RMM DOCUMENT #4 | DOCUMENT.Owner | Owner = Module |
| RMM DOCUMENT #5 | DOCUMENT.Lifecycle | Draft → Review → Approved → Published → Superseded → Archived |
| RMM DOCUMENT #8 | DOCUMENT.Cardinality | Cardinality = 1:N |
| RMM DOCUMENT #9 | DOCUMENT.Stability | Stability = Moderate |
| RMM DOCUMENT #10 | DOCUMENT.Versionable | Versionable = Yes |
| RMM DOCUMENT #11 | DOCUMENT.Freezable | Freezable = Yes |
| RMM DOCUMENT #15 | DOCUMENT.SourceOfTruth | SourceOfTruth = Artifact Repository |
| RMM KERNEL #4 | KERNEL.Owner | Owner = Constitution |
| RMM CONSTITUTION #4 | CONSTITUTION.Owner | Owner = Constitution (self-owning) |
| RMM CONSTITUTION #6 | CONSTITUTION.Empowers | "Supersedes AllGovernanceEntities" |
| KSS 3.1 | Artifact Location Rule | Every artifact stored in directory matching RMM Source of Truth |
| KSS 8.1 | Directory Immutability | Directory numbers are immutable |
| KDM CAC-01 | DAG Verification | Document dependency graph is acyclic |
| KDM CAC-04 | Explicit Dependencies | All document-level dependencies stated in Normative References |

---

# PART II: REGISTRY CONTENT

---

## 1. Purpose

This document is the single authoritative registry of all canonical Kernel documents and Phase 2 normative documents. It answers:

- What documents exist?
- Which are Canonical?
- Which are Frozen?
- Which are Active?
- Which is the Source of Truth for each?
- Which document depends on which?
- Which document authorizes which?
- Which document must be read first?
- Which document is allowed to reference another?

This document is the Boot Index for every future AI session.

---

## 2. Registry Scope

The Registry covers **29 canonical and normative documents** stored in the Engineering Kernel repository (21 pre-Phase 2 canonical + 8 Phase 2 documents). It does NOT cover derived artifacts, informational entry points, or operational-layer documents (which are inventoried separately in `OPERATIONAL_DOCUMENT_INVENTORY.md`).

### 2.1 Included Documents

**21 Pre-Phase 2 Canonical Documents:**

- **3 documents** in `00-CONSTITUTION/`:
  - `CONSTITUTION.md`
  - `KERNEL_CHARTER.md`
  - `KERNEL_DOCUMENT_REGISTRY.md` (this file)
- **9 documents** in `01-META-MODEL/`:
  - `RMM_v1.1.md`
  - `KERNEL_SCOPE_DEFINITION.md`
  - `KERNEL_STRUCTURE_SPEC.md`
  - `DOCUMENT_STANDARD_SPEC.md`
  - `ARTIFACT_META_MODEL.md`
  - `ARTIFACT_FAMILY_MODEL.md`
  - `Repository_State_Model.md`
  - `KERNEL_DEPENDENCY_MODEL.md`
  - `KERNEL_AUTHORITY_MODEL.md`
- **5 documents** in `02-GOVERNANCE/`:
  - `KERNEL_ROLE_MODEL.md`
  - `KERNEL_GOVERNANCE_MODEL.md`
  - `KERNEL_DECISION_MODEL.md`
  - `KERNEL_REVIEW_MODEL.md`
  - `KERNEL_AMENDMENT_MODEL.md`
- **3 documents** in `05-EVIDENCE/`:
  - `KERNEL_EVIDENCE_MODEL.md`
  - `CANONICAL_ISSUE_LEDGER.md`
  - `CANONICAL_ARBITRATION_LEDGER.md`
- **1 document** in `99-STATE/`:
  - `REPOSITORY_LIFECYCLE_MODEL.md`

**8 Phase 2 Documents (NEW):**

- **1 document** in `03-PLANNING/`:
  - `PHASE_2_MASTER_PLAN.md`
- **4 documents** in `03-STANDARDS/`:
  - `CROSS_DOCUMENT_VALIDATOR.md`
  - `UNSUPPORTED_MARKER_TRACKER.md`
  - `SECTION_NAMING_STANDARD.md`
  - `RMM_v1.2_EXECUTION_PLAN.md`
- **2 documents** in `05-EVIDENCE/`:
  - `CONSTITUTIONAL_EXECUTION_REPORT.md` (updated)
  - `OPERATIONAL_DOCUMENT_INVENTORY.md`
- **1 document** in `07-WORKFLOW/`:
  - `KERNEL_PROCESS_MODEL.md`

### 2.2 Excluded Artifacts

The following are **NOT** covered by this Registry:

| Artifact | Classification | Reason |
|----------|---------------|--------|
| `README.md` | INFORMATIONAL | Informational entry point, not canonical |
| Review Reports | DERIVED | Computed from canonical sources |
| Validation Reports | DERIVED | Computed from canonical sources |
| Changelogs | DERIVED | Computed from canonical sources |
| Changesets | DERIVED | Computed from canonical sources |
| Future Proposals | DRAFT | Pre-approval; not canonical |
| Plan Files | PROCEDURAL | Execution instructions |
| `PHASE_2_COMPLETION_REPORT.md` | REPORT | Created by P2-M08; will be added upon completion |

### 2.3 Operational-Layer Documents

The following 7 operational-layer documents are **acknowledged** per `REPOSITORY_LAYOUT_SPECIFICATION.md` §3 LS-CL-03 but are **not registered** as canonical documents. They are inventoried in `OPERATIONAL_DOCUMENT_INVENTORY.md` (D-08):

| # | Document | Location | MISSION Authority |
|---|----------|----------|------------------|
| 1 | `REPOSITORY_INFORMATION_MODEL.md` | `02-GOVERNANCE/` | MISSION-019 |
| 2 | `REPOSITORY_LAYOUT_SPECIFICATION.md` | `02-GOVERNANCE/` | MISSION-020 |
| 3 | `KERNEL_BOOT_PROTOCOL.md` | `07-WORKFLOW/` | MISSION-022 |
| 4 | `AI_EXECUTION_PROTOCOL.md` | `07-WORKFLOW/` | MISSION-021 |
| 5 | `KNOWLEDGE_INDEX_SPECIFICATION.md` | `09-TOOLS/` | MISSION-024 |
| 6 | `SKILL_MANIFEST_SPECIFICATION.md` | `09-TOOLS/` | MISSION-023 |
| 7 | `KERNEL_VALIDATION_PROTOCOL.md` | `09-TOOLS/` | MISSION-025 |

---

## 3. Canonical Document Inventory

### 3.1 Pre-Phase 2 Canonical Documents (1–21)

| # | Identifier | Filename | Entity Type | Owner | Classification | Status | Version | Source of Truth | Mission |
|---|------------|----------|-------------|-------|----------------|--------|---------|-----------------|---------|
| 1 | REPOSITORY_META_MODEL | RMM_v1.1.md | DOCUMENT | Constitution (per RMM KERNEL #4) | CANONICAL | FROZEN | 1.1 | 01-META-MODEL/ | Pre-Constitution |
| 2 | KERNEL_SCOPE_DEFINITION | KERNEL_SCOPE_DEFINITION.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-002 |
| 3 | KERNEL_STRUCTURE_SPEC | KERNEL_STRUCTURE_SPEC.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-002 |
| 4 | DOCUMENT_STANDARD_SPEC | DOCUMENT_STANDARD_SPEC.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0.0 | 01-META-MODEL/ | MISSION-003 |
| 5 | ARTIFACT_META_MODEL | ARTIFACT_META_MODEL.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-004 |
| 6 | ARTIFACT_FAMILY_MODEL | ARTIFACT_FAMILY_MODEL.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-005 |
| 7 | REPOSITORY_STATE_MODEL | Repository_State_Model.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-006 |
| 8 | KERNEL_DEPENDENCY_MODEL | KERNEL_DEPENDENCY_MODEL.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0.0 | 01-META-MODEL/ | MISSION-007 |
| 9 | KERNEL_AUTHORITY_MODEL | KERNEL_AUTHORITY_MODEL.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0 | 01-META-MODEL/ | MISSION-008 |
| 10 | CONSTITUTION | CONSTITUTION.md | CONSTITUTION | Constitution (self) | CANONICAL | Active | 1.0.0 | 00-CONSTITUTION/Constitution.md | MISSION-009 |
| 11 | KERNEL_DOCUMENT_REGISTRY | KERNEL_DOCUMENT_REGISTRY.md | DOCUMENT | Constitution | CANONICAL | Active | 1.1.0 | 00-CONSTITUTION/KERNEL_DOCUMENT_REGISTRY.md | MISSION-010 |
| 12 | KERNEL_CHARTER | KERNEL_CHARTER.md | CHARTER | Constitution | CANONICAL | Active | 1.0.0 | 00-CONSTITUTION/Charters/ | MISSION-011 |
| 13 | KERNEL_ROLE_MODEL | KERNEL_ROLE_MODEL.md | ROLE | GovernanceBody | CANONICAL | Active | 1.0.0 | 00-CONSTITUTION/ | MISSION-012 |
| 14 | KERNEL_GOVERNANCE_MODEL | KERNEL_GOVERNANCE_MODEL.md | GOVERNANCE_BODY | Constitution | CANONICAL | Active | 1.0.0 | 02-GOVERNANCE/KERNEL_GOVERNANCE_MODEL.md | MISSION-013 |
| 15 | KERNEL_DECISION_MODEL | KERNEL_DECISION_MODEL.md | DECISION | Actor | CANONICAL | Active | 1.0.0 | 05-EVIDENCE/KERNEL_DECISION_MODEL.md | MISSION-014 |
| 16 | KERNEL_EVIDENCE_MODEL | KERNEL_EVIDENCE_MODEL.md | EVIDENCE | GovernanceBody | CANONICAL | Active | 1.0.0 | 05-EVIDENCE/KERNEL_EVIDENCE_MODEL.md | MISSION-015 |
| 17 | KERNEL_REVIEW_MODEL | KERNEL_REVIEW_MODEL.md | REVIEW | GovernanceBody | CANONICAL | Active | 1.0.0 | 05-EVIDENCE/Reviews/KERNEL_REVIEW_MODEL.md | MISSION-016 |
| 18 | KERNEL_AMENDMENT_MODEL | KERNEL_AMENDMENT_MODEL.md | AMENDMENT | Actor | CANONICAL | Active | 1.0.0 | 02-GOVERNANCE/Amendments/KERNEL_AMENDMENT_MODEL.md | MISSION-017 |
| 19 | REPOSITORY_LIFECYCLE_MODEL | REPOSITORY_LIFECYCLE_MODEL.md | LIFECYCLE + STATE | GovernanceBody | CANONICAL | Active | 1.0.0 | 01-META-MODEL/Lifecycles/REPOSITORY_LIFECYCLE_MODEL.md | MISSION-018 |
| 20 | CANONICAL_ISSUE_LEDGER | CANONICAL_ISSUE_LEDGER.md | DOCUMENT | Constitution | CANONICAL | Active | 1.0.0 | 05-EVIDENCE/CANONICAL_ISSUE_LEDGER.md | Post-MISSION-018 |
| 21 | CANONICAL_ARBITRATION_LEDGER | CANONICAL_ARBITRATION_LEDGER.md | DOCUMENT | GovernanceBody | CANONICAL | Active | 1.0.0 | 05-EVIDENCE/CANONICAL_ARBITRATION_LEDGER.md | Post-MISSION-018 |

### 3.2 Phase 2 Documents (22–29)

| # | Identifier | Filename | Entity Type | Owner | Classification | Status | Version | Source of Truth | Mission |
|---|------------|----------|-------------|-------|----------------|--------|---------|-----------------|---------|
| 22 | CONSTITUTIONAL_EXECUTION_REPORT | CONSTITUTIONAL_EXECUTION_REPORT.md | REPORT | Engineering Kernel Architect | NORMATIVE | Active | 1.0.0 | 05-EVIDENCE/CONSTITUTIONAL_EXECUTION_REPORT.md | P2-M01 |
| 23 | PHASE_2_MASTER_PLAN | PHASE_2_MASTER_PLAN.md | PLAN | Engineering Kernel Architect | NORMATIVE | Active | 1.1.1 | 03-PLANNING/PHASE_2_MASTER_PLAN.md | P2-M06 |
| 24 | KERNEL_PROCESS_MODEL | KERNEL_PROCESS_MODEL.md | PROCESS | GovernanceBody | CANONICAL | Active | 1.0.0 | 07-WORKFLOW/KERNEL_PROCESS_MODEL.md | P2-M02 |
| 25 | CROSS_DOCUMENT_VALIDATOR | CROSS_DOCUMENT_VALIDATOR.md | STANDARD | GovernanceBody | NORMATIVE | Active | 1.0.0 | 03-STANDARDS/CROSS_DOCUMENT_VALIDATOR.md | P2-M03 |
| 26 | UNSUPPORTED_MARKER_TRACKER | UNSUPPORTED_MARKER_TRACKER.md | STANDARD | Engineering Kernel Architect | NORMATIVE | Active | 1.0.0 | 03-STANDARDS/UNSUPPORTED_MARKER_TRACKER.md | P2-M04 |
| 27 | SECTION_NAMING_STANDARD | SECTION_NAMING_STANDARD.md | STANDARD | GovernanceBody | NORMATIVE | Active | 1.0.0 | 03-STANDARDS/SECTION_NAMING_STANDARD.md | P2-M05 |
| 28 | RMM_v1.2_EXECUTION_PLAN | RMM_v1.2_EXECUTION_PLAN.md | PLAN | GovernanceBody | NORMATIVE | Active | 1.0.0 | 03-STANDARDS/RMM_v1.2_EXECUTION_PLAN.md | P2-M06 |
| 29 | OPERATIONAL_DOCUMENT_INVENTORY | OPERATIONAL_DOCUMENT_INVENTORY.md | INVENTORY | Engineering Kernel Architect | NORMATIVE | Active | 1.0.0 | 05-EVIDENCE/OPERATIONAL_DOCUMENT_INVENTORY.md | P2-M07 |

---

## 4. Document Classification Matrix

Per DOCUMENT_STANDARD_SPEC Section 3.3, the classification values are:

| Classification | Definition | Applicable Documents |
|----------------|------------|---------------------|
| CANONICAL | Supreme authority; frozen state | Documents 1-21, 24 (entity-defining documents) |
| NORMATIVE | Mandatory standards; approved | Documents 22-23, 25-29 (Phase 2 operational documents) |
| DERIVED | Computed from canonical sources | Excluded: review reports, validation reports |
| PROCEDURAL | Execution instructions | Excluded: plan files |
| INFORMATIONAL | Reference material | README.md (excluded, not part of Registry) |
| DRAFT | Work in progress; pre-approval | Excluded: future proposals |

---

## 5. Authority Matrix

Derived from KAM (Kernel Authority Model) and CONSTITUTION.md.

| Document | Authorized By | Authorizes |
|----------|--------------|------------|
| CONSTITUTION.md | Self (RMM CONSTITUTION #4: Owner = Constitution) | All other documents (supreme authority) |
| RMM_v1.1.md | Constitution (RMM KERNEL #4: Owner = Constitution) | All entity definitions (79 entities) |
| KERNEL_SCOPE_DEFINITION | Constitution | Scope definitions; in-scope/out-of-scope determination |
| KERNEL_STRUCTURE_SPEC | Constitution | Directory structure; naming conventions; artifact locations |
| DOCUMENT_STANDARD_SPEC | Constitution | Document format standard (10 sections) |
| ARTIFACT_META_MODEL | Constitution | Artifact definition; artifact identity; artifact lifecycle |
| ARTIFACT_FAMILY_MODEL | Constitution | Artifact family classification |
| Repository_State_Model | Constitution | State definitions; state transitions; prohibited transitions |
| KERNEL_DEPENDENCY_MODEL | Constitution | Dependency mapping; DAG verification |
| KERNEL_AUTHORITY_MODEL | Constitution | Authority extraction; authority chain validation |
| KERNEL_DOCUMENT_REGISTRY | Constitution | Document registry; read/boot/build/freeze orderings |
| PHASE_2_MASTER_PLAN | Engineering Kernel Architect | Phase 2 mission execution (planning authority only) |
| KERNEL_PROCESS_MODEL | GovernanceBody | PROCESS entity definition |

**The Constitution is the sole authorizing instrument** (CONSTITUTION.md Section 2: "supreme governance instrument").

---

## 6. Dependency Matrix

Extracted from KDM (Kernel Dependency Model) Sections 3.1-3.7.

### 6.1 Document Dependency DAG

```
RMM_v1.1.md (root)
├──→ KERNEL_SCOPE_DEFINITION.md
│       └──→ ARTIFACT_META_MODEL.md
│               └──→ ARTIFACT_FAMILY_MODEL.md
│                       └──→ Repository_State_Model.md
├──→ KERNEL_STRUCTURE_SPEC.md
│       ├──→ DOCUMENT_STANDARD_SPEC.md
│       │       ├──→ ARTIFACT_FAMILY_MODEL.md
│       │       └──→ Repository_State_Model.md
│       └──→ ARTIFACT_META_MODEL.md
└──→ (all documents reference RMM as root)
```

Total documents in DAG: 7 (per KDM Document Dependency Summary)
Total explicit document-to-document dependencies: 18
Root: RMM_v1.1.md (6 downstream dependents)
Leaf: Repository_State_Model.md (0 downstream dependents)
Cycles: None detected (KDM CAC-01: DAG verified).

### 6.2 Extended Dependencies (Constitution and KDR)

Additional dependencies from Constitution Normative References (CONSTITUTION.md Section G) and KAM Normative References:

| Document | Depends On | Referenced By |
|----------|-----------|---------------|
| CONSTITUTION.md | RMM, KSD, KSS, DSS, KAM | KSD, KDR |
| KDM | RMM, AMM, AFM, KSD, DSS | KAM, KDR |
| KAM | RMM, KSD, KSS, DSS, AMM, AFM, RSM, KDM | CONSTITUTION, KDR |
| KDR (this) | All 10 normative references (Section G.1) | None (terminal registry) |

### 6.3 Dependency Table

| Document | Depends On (Direct) | Referenced By (Direct) |
|----------|--------------------|-----------------------|
| RMM_v1.1.md | (none — root) | KSD, KSS, DSS, AMM, AFM, RSM, CONSTITUTION, KDM, KAM, KDR |
| KERNEL_SCOPE_DEFINITION | RMM (KDM 3.2) | AMM, AFM, CONSTITUTION, KDM, KAM, KDR |
| KERNEL_STRUCTURE_SPEC | RMM | DSS, AMM, AFM, CONSTITUTION, KAM, KDR |
| DOCUMENT_STANDARD_SPEC | RMM, KSS | AFM, RSM, CONSTITUTION, KDM, KAM, KDR |
| ARTIFACT_META_MODEL | RMM, KSD, KSS | AFM, RSM, CONSTITUTION, KDM, KAM, KDR |
| ARTIFACT_FAMILY_MODEL | RMM, KSD, KSS, DSS, AMM | RSM, CONSTITUTION, KDM, KAM, KDR |
| Repository_State_Model | RMM, AMM, AFM, DSS | (none — leaf in core DAG; extended: KDM, KAM, KDR) |
| KERNEL_DEPENDENCY_MODEL | RMM, AMM, AFM, KSD, DSS | KAM, KDR |
| KERNEL_AUTHORITY_MODEL | RMM, KSD, KSS, DSS, AMM, AFM, RSM, KDM | CONSTITUTION, KDR |
| CONSTITUTION.md | RMM, KSD, KSS, DSS, KAM | KSD, KDR |
| KERNEL_DOCUMENT_REGISTRY | All 10 normative references | (none — terminal) |

---

## 7. Read Order

Derived from the dependency DAG (topological sort — read dependencies before dependents):

| Order | Document | Rationale |
|-------|----------|-----------|
| 1 | RMM_v1.1.md | Root ontology; defines all 79 entities; no dependencies (KDM 3.1) |
| 2 | KERNEL_SCOPE_DEFINITION.md | Parallel with KSS; both depend only on RMM |
| 2 | KERNEL_STRUCTURE_SPEC.md | Parallel with KSD; both depend only on RMM (KDM 3.3) |
| 3 | DOCUMENT_STANDARD_SPEC.md | Depends on RMM + KSS (KDM 3.4) |
| 3 | ARTIFACT_META_MODEL.md | Depends on RMM + KSD + KSS (KDM 3.5) |
| 4 | ARTIFACT_FAMILY_MODEL.md | Depends on RMM + KSD + KSS + DSS + AMM (KDM 3.6) |
| 5 | Repository_State_Model.md | Depends on RMM + AMM + AFM + DSS (KDM 3.7) |
| 6 | KERNEL_DEPENDENCY_MODEL.md | Depends on RMM + AMM + AFM + KSD + DSS (KDM Section 8) |
| 7 | KERNEL_AUTHORITY_MODEL.md | Depends on RMM + KSD + KSS + DSS + AMM + AFM + RSM + KDM (KAM Section 14) |
| 8 | CONSTITUTION.md | Depends on RMM + KSD + KSS + DSS + KAM (CONSTITUTION.md Section G) |
| 9 | KERNEL_DOCUMENT_REGISTRY.md | This document; depends on all (Section G.1) |

---

## 8. Boot Order

Minimum set to bootstrap understanding of the Kernel (3 documents):

| Order | Document | Purpose |
|-------|----------|---------|
| 1 | CONSTITUTION.md | Supreme authority; establishes the Kernel's governance |
| 2 | RMM_v1.1.md | Root ontology; defines all 79 entities across 20 tiers |
| 3 | KERNEL_SCOPE_DEFINITION.md | Defines what is and is not in scope |

These three documents provide sufficient context to understand any other Kernel document.

---

## 9. Build Order

Historical creation sequence (MISSION order):

| Order | Document | Mission Reference |
|-------|----------|-------------------|
| 1 | RMM_v1.1.md | Pre-Constitution |
| 2 | KERNEL_SCOPE_DEFINITION.md | MISSION-002 |
| 3 | KERNEL_STRUCTURE_SPEC.md | MISSION-002 |
| 4 | DOCUMENT_STANDARD_SPEC.md | MISSION-003 |
| 5 | ARTIFACT_META_MODEL.md | MISSION-004 |
| 6 | ARTIFACT_FAMILY_MODEL.md | MISSION-005 |
| 7 | Repository_State_Model.md | MISSION-006 |
| 8 | KERNEL_DEPENDENCY_MODEL.md | MISSION-007 |
| 9 | KERNEL_AUTHORITY_MODEL.md | MISSION-008 |
| 10 | CONSTITUTION.md | MISSION-009 |
| 11 | KERNEL_DOCUMENT_REGISTRY.md | MISSION-010 |
| 12 | KERNEL_CHARTER.md | MISSION-011 |
| 13 | KERNEL_ROLE_MODEL.md | MISSION-012 |
| 14 | KERNEL_GOVERNANCE_MODEL.md | MISSION-013 |
| 15 | KERNEL_DECISION_MODEL.md | MISSION-014 |
| 16 | KERNEL_EVIDENCE_MODEL.md | MISSION-015 |
| 17 | KERNEL_REVIEW_MODEL.md | MISSION-016 |
| 18 | KERNEL_AMENDMENT_MODEL.md | MISSION-017 |
| 19 | REPOSITORY_LIFECYCLE_MODEL.md | MISSION-018 |
| 20 | CANONICAL_ISSUE_LEDGER.md | Post-MISSION-018 |
| 21 | CANONICAL_ARBITRATION_LEDGER.md | Post-MISSION-018 |
| 22 | CONSTITUTIONAL_EXECUTION_REPORT.md | P2-M01 |
| 23 | PHASE_2_MASTER_PLAN.md | P2-M06 |
| 24 | KERNEL_PROCESS_MODEL.md | P2-M02 |
| 25 | CROSS_DOCUMENT_VALIDATOR.md | P2-M03 |
| 26 | UNSUPPORTED_MARKER_TRACKER.md | P2-M04 |
| 27 | SECTION_NAMING_STANDARD.md | P2-M05 |
| 28 | RMM_v1.2_EXECUTION_PLAN.md | P2-M06 |
| 29 | OPERATIONAL_DOCUMENT_INVENTORY.md | P2-M07 |

---

## 10. Freeze Order

Documents frozen to date:

| Document | Status | Freeze Date |
|----------|--------|-------------|
| RMM_v1.1.md | FROZEN | 2026-06-26 |
| All other documents | Active | N/A |

Per RMM CONSTITUTION #11 (Freezable = Yes) and RMM DOCUMENT #11 (Freezable = Yes).
FROZEN documents may not be modified without Amendment (RMM CONSTITUTION #7).

---

## 11. Source-of-Truth Map

Maps each document to its canonical storage location (RMM #15):

| Document | Source of Truth | Directory |
|----------|----------------|-----------|
| CONSTITUTION.md | 00-CONSTITUTION/Constitution.md | 00-CONSTITUTION/ |
| RMM_v1.1.md | 01-META-MODEL/ | 01-META-MODEL/ |
| KERNEL_SCOPE_DEFINITION | 01-META-MODEL/ | 01-META-MODEL/ |
| KERNEL_STRUCTURE_SPEC | 01-META-MODEL/ | 01-META-MODEL/ |
| DOCUMENT_STANDARD_SPEC | 01-META-MODEL/ | 01-META-MODEL/ |
| ARTIFACT_META_MODEL | 01-META-MODEL/ | 01-META-MODEL/ |
| ARTIFACT_FAMILY_MODEL | 01-META-MODEL/ | 01-META-MODEL/ |
| REPOSITORY_STATE_MODEL | 01-META-MODEL/ | 01-META-MODEL/ |
| KERNEL_DEPENDENCY_MODEL | 01-META-MODEL/ | 01-META-MODEL/ |
| KERNEL_AUTHORITY_MODEL | 01-META-MODEL/ | 01-META-MODEL/ |
| KERNEL_DOCUMENT_REGISTRY | 00-CONSTITUTION/ | 00-CONSTITUTION/ |
| KERNEL_CHARTER | 00-CONSTITUTION/Charters/ | 00-CONSTITUTION/ |
| KERNEL_ROLE_MODEL | 00-CONSTITUTION/ | 00-CONSTITUTION/ |
| KERNEL_GOVERNANCE_MODEL | 02-GOVERNANCE/KERNEL_GOVERNANCE_MODEL.md | 02-GOVERNANCE/ |
| KERNEL_DECISION_MODEL | 05-EVIDENCE/KERNEL_DECISION_MODEL.md | 05-EVIDENCE/ |
| KERNEL_EVIDENCE_MODEL | 05-EVIDENCE/KERNEL_EVIDENCE_MODEL.md | 05-EVIDENCE/ |
| KERNEL_REVIEW_MODEL | 05-EVIDENCE/Reviews/KERNEL_REVIEW_MODEL.md | 05-EVIDENCE/ |
| KERNEL_AMENDMENT_MODEL | 02-GOVERNANCE/Amendments/KERNEL_AMENDMENT_MODEL.md | 02-GOVERNANCE/ |
| REPOSITORY_LIFECYCLE_MODEL | 01-META-MODEL/Lifecycles/REPOSITORY_LIFECYCLE_MODEL.md | 01-META-MODEL/ |
| CANONICAL_ISSUE_LEDGER | 05-EVIDENCE/CANONICAL_ISSUE_LEDGER.md | 05-EVIDENCE/ |
| CANONICAL_ARBITRATION_LEDGER | 05-EVIDENCE/CANONICAL_ARBITRATION_LEDGER.md | 05-EVIDENCE/ |
| CONSTITUTIONAL_EXECUTION_REPORT | 05-EVIDENCE/CONSTITUTIONAL_EXECUTION_REPORT.md | 05-EVIDENCE/ |
| PHASE_2_MASTER_PLAN | 03-PLANNING/PHASE_2_MASTER_PLAN.md | 03-PLANNING/ |
| KERNEL_PROCESS_MODEL | 07-WORKFLOW/KERNEL_PROCESS_MODEL.md | 07-WORKFLOW/ |
| CROSS_DOCUMENT_VALIDATOR | 03-STANDARDS/CROSS_DOCUMENT_VALIDATOR.md | 03-STANDARDS/ |
| UNSUPPORTED_MARKER_TRACKER | 03-STANDARDS/UNSUPPORTED_MARKER_TRACKER.md | 03-STANDARDS/ |
| SECTION_NAMING_STANDARD | 03-STANDARDS/SECTION_NAMING_STANDARD.md | 03-STANDARDS/ |
| RMM_v1.2_EXECUTION_PLAN | 03-STANDARDS/RMM_v1.2_EXECUTION_PLAN.md | 03-STANDARDS/ |
| OPERATIONAL_DOCUMENT_INVENTORY | 05-EVIDENCE/OPERATIONAL_DOCUMENT_INVENTORY.md | 05-EVIDENCE/ |

**NOTE:** `03-PLANNING/` is NOT listed in Constitution §10 directory structure. Constitution §10 assigns directory 03 to `03-STANDARDS/`. `PHASE_2_MASTER_PLAN.md` location at `03-PLANNING/` is a known documentation gap documented in the plan header.

---

## 12. Repository Navigation Rules

From KERNEL_STRUCTURE_SPEC:

| Rule | Statement | Source |
|------|-----------|--------|
| Rule 1 | Every artifact SHALL be stored in the directory matching its RMM Source of Truth. | KSS 3.1 |
| Rule 2 | Directory numbers are immutable. | KSS 8.1 |
| Rule 3 | No product-specific directory names. | KSS 8.2 |
| Rule 4 | Canonical directories contain only .md files. | KSS 8.3 |
| Rule 5 | Reserved directories (04, 08, 09) may contain only README.md. | KSS 8.4 |
| Rule 6 | Documents in 00-CONSTITUTION/ are supreme authority documents. | KSS 2.2 |
| Rule 7 | Documents in 01-META-MODEL/ are ontology and meta-model definitions. | KSS 2.3 |
| Rule 8 | RMM #15 Source of Truth is the canonical location for each entity type. | RMM property #15 |

---

## 13. Registry Invariants

Structural invariants derived from RMM and KDM:

| ID | Invariant | Source |
|----|-----------|--------|
| RI-01 | Every canonical document has a unique Identifier. | RMM #1 (Name) |
| RI-02 | Every canonical document has a Source of Truth path. | RMM #15 (SourceOfTruth) |
| RI-03 | The document dependency graph is acyclic. | KDM CAC-01: DAG verified |
| RI-04 | FROZEN documents may not be modified without Amendment. | RMM CONSTITUTION #7 |
| RI-05 | The Registry is complete — every canonical document appears exactly once. | This Registry (29 documents) |
| RI-06 | No canonical document depends on a non-canonical document. | KDM CAC-04 |
| RI-07 | The Constitution is the sole self-owning document. | RMM CONSTITUTION #4 |
| RI-08 | Directory numbers are immutable. | KSS 8.1 |

---

## 14. Normative References

The 10 authoritative inputs for this Registry:

| # | Document | Description |
|---|----------|-------------|
| 1 | RMM_v1.1.md | Repository Meta-Model v1.1, FROZEN. 79 entities, 10 matrices. |
| 2 | CONSTITUTION.md | Constitution of the Engineering Kernel. Supreme authority. |
| 3 | KERNEL_SCOPE_DEFINITION.md | Kernel Scope Definition. In-scope/out-of-scope boundaries. |
| 4 | KERNEL_STRUCTURE_SPEC.md | Kernel Structure Specification. Directory and naming rules. |
| 5 | DOCUMENT_STANDARD_SPEC.md | Document Standard Specification. 10-section document format. |
| 6 | ARTIFACT_META_MODEL.md | Artifact Meta-Model. Artifact definition and invariants. |
| 7 | ARTIFACT_FAMILY_MODEL.md | Artifact Family Model. Artifact classification families. |
| 8 | Repository_State_Model.md | Repository State Model. State definitions and transitions. |
| 9 | KERNEL_DEPENDENCY_MODEL.md | Kernel Dependency Model. Document-level dependency DAG. |
| 10 | KERNEL_AUTHORITY_MODEL.md | Kernel Authority Model. Authority extraction and chain. |

---

END OF DOCUMENT
