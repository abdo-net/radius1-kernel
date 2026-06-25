ENGINEERING KERNEL — KERNEL DEPENDENCY MODEL
============================================

Version: 1.0.0
Status: Approved
Date: 2026-06-26
Authority: MISSION-007
Source of Truth: Artifact Repository
Stability: Slow

------------------------------------------------------------------------------

TABLE OF CONTENTS
-----------------

1. Model Scope
2. Dependency Taxonomy
3. Document-Level Dependencies
   3.1 RMM_v1.1.md
   3.2 KERNEL_SCOPE_DEFINITION.md
   3.3 KERNEL_STRUCTURE_SPEC.md
   3.4 DOCUMENT_STANDARD_SPEC.md
   3.5 ARTIFACT_META_MODEL.md
   3.6 ARTIFACT_FAMILY_MODEL.md
   3.7 Repository_State_Model.md
4. Core Entity Dependencies
   4.1 CONSTITUTION
   4.2 CHARTER
   4.3 GOVERNANCE_BODY
   4.4 ARTIFACT
   4.5 DOCUMENT
   4.6 LIFECYCLE
   4.7 STATE
5. Cross-Artifact Dependency Constraints
6. Forbidden Dependencies
7. Validation Rules
8. Normative References

------------------------------------------------------------------------------

1. MODEL SCOPE
--------------

RMM Basis: Matrix 9 (Dependency Matrix); ENTITY properties 6-7
(Allowed/Forbidden Relationships); ARTIFACT_FAMILY_MODEL.md Sections
2.6-13.6; ARTIFACT_META_MODEL.md Section 8.

The Kernel Dependency Model defines every explicit dependency between
canonical Kernel artifacts. A dependency exists only if it is explicitly
stated in one of the authoritative input documents.

This model covers two dependency layers:
    Layer 1: Document-level — dependencies between the 7 canonical Kernel
             documents stored in 01-META-MODEL/.
    Layer 2: Entity-level — dependencies between the core RMM entities
             that constitute the Kernel's governance and artifact ontology.

Dependencies not explicitly stated in the authoritative inputs are:

    UNSUPPORTED

------------------------------------------------------------------------------

2. DEPENDENCY TAXONOMY
----------------------

RMM Basis: Matrix 9 (79 rows, 4 columns); AMM Section 8.1-8.3.

The Kernel Dependency Model recognizes five dependency types:

    Type              Definition                           Source
    ----------------  -----------------------------------  ------------------
    Depends On       Entity requires another to exist     Matrix 9 col 2
    Referenced By    Entity is required by another        Matrix 9 col 3
    Required Before  Entity must exist before another     Document creation
    Forbidden        Entity must NOT depend on another    RMM property #7
    Constraints      Rules governing dependency validity  AMM Section 8

Dependency notation:
    A → B         A depends on B (A requires B)
    A ← B         A is referenced by B (B requires A)
    A ⊸ B         A is forbidden from depending on B
    A ≺ B         A must exist before B (Required Before)

------------------------------------------------------------------------------

3. DOCUMENT-LEVEL DEPENDENCIES
------------------------------

RMM Basis: Document Normative References sections; DOCUMENT_STANDARD_SPEC
Section 3.7; Matrix 6 (Source-of-Truth Matrix).

The following dependencies are extracted from the explicit Normative
References sections of each Kernel document. Each entry is verbatim from
the source document.

------------------------------------------------------------------------------

3.1 RMM_v1.1.md
---------------

Identifier: REPOSITORY_META_MODEL
Source of Truth: 01-META-MODEL/RMM_v1.1.md

Depends On:
    (none — RMM is the root ontology; no upstream Kernel dependencies)

Referenced By:
    KERNEL_SCOPE_DEFINITION.md     KSD Section 15
    KERNEL_STRUCTURE_SPEC.md       KSS Section 9
    DOCUMENT_STANDARD_SPEC.md      DSS Section 2
    ARTIFACT_META_MODEL.md         AMM Section 2 (all sections)
    ARTIFACT_FAMILY_MODEL.md       AFM Section 2 (Normative References)
    Repository_State_Model.md      RSM Section 8

Required Before:
    All other Kernel documents         RMM is Source of Truth #1

Forbidden Dependencies:
    UNSUPPORTED (RMM does not declare forbidden dependencies at
    the document level)

Dependency Constraints:
    DC-D-01  RMM must be frozen before documents referencing it
             are approved.                                         KSS Section 6.3

------------------------------------------------------------------------------

3.2 KERNEL_SCOPE_DEFINITION.md
------------------------------

Identifier: KERNEL_SCOPE_DEFINITION
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    KSD Normative References #1
    00-CONSTITUTION/               KSD Normative References #2
    01-META-MODEL/                 KSD Normative References #3
    02-GOVERNANCE/                 KSD Normative References #4

Referenced By:
    ARTIFACT_META_MODEL.md         AMM Normative References
    ARTIFACT_FAMILY_MODEL.md       AFM Normative References

Required Before:
    KERNEL_STRUCTURE_SPEC.md       KSS depends on scope being defined
    ARTIFACT_META_MODEL.md         AMM references KSD
    ARTIFACT_FAMILY_MODEL.md       AFM references KSD

Forbidden Dependencies:
    UNSUPPORTED (KSD does not declare forbidden document-level
    dependencies)

Dependency Constraints:
    DC-D-02  KSD must not reference entities outside RMM scope    KSD Section 3

------------------------------------------------------------------------------

3.3 KERNEL_STRUCTURE_SPEC.md
----------------------------

Identifier: KERNEL_STRUCTURE_SPEC
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    KSS Normative References #1

Referenced By:
    DOCUMENT_STANDARD_SPEC.md      DSS Normative References
    ARTIFACT_META_MODEL.md         AMM Section 2.3
    ARTIFACT_FAMILY_MODEL.md       AFM Normative References

Required Before:
    DOCUMENT_STANDARD_SPEC.md      DSS references KSS
    ARTIFACT_META_MODEL.md         AMM references KSS
    ARTIFACT_FAMILY_MODEL.md       AFM references KSS

Forbidden Dependencies:
    UNSUPPORTED (KSS does not declare forbidden document-level
    dependencies)

Dependency Constraints:
    DC-D-03  Directory assignments must match RMM Source of Truth   KSS Section 3

------------------------------------------------------------------------------

3.4 DOCUMENT_STANDARD_SPEC.md
-----------------------------

Identifier: DOCUMENT_STANDARD_SPEC
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    DSS Normative References
      - Entity: ARTIFACT           RMM properties 1-15, M2 row 44
      - Entity: DOCUMENT           RMM properties 1-15, M2 row 45
      - Entity: EVIDENCE           RMM properties 1-15, M2 row 41
      - Entity: AUDIT_TRAIL        RMM properties 1-15
      - Entity: APPROVAL           RMM properties 1-15, M2 row 50
      - Entity: SIGNATURE          RMM properties 1-15, M2 row 54
      - Entity: LIFECYCLE          RMM properties 1-15, M2 row 65
      - Entity: STATE              RMM properties 1-15, M2 row 66
      - Entity: CONSTITUTION       RMM properties 1-15, M2 row 24
      - Matrix 2 (Lifecycle)       79 rows, 3 columns
      - Matrix 3 (Stability)       79 rows, 4 columns
      - Matrix 4 (Versionability)  79 rows, 4 columns
      - Matrix 5 (Freeze)          79 rows, 5 columns
      - Matrix 6 (Source-of-Truth) 79 rows, 5 columns
      - Matrix 7 (Permissions)     79 rows, 6 columns
    KERNEL_STRUCTURE_SPEC.md       DSS Normative References

Referenced By:
    ARTIFACT_FAMILY_MODEL.md       AFM Normative References
    Repository_State_Model.md      RSM Section 8

Required Before:
    ARTIFACT_FAMILY_MODEL.md       AFM references DSS
    Repository_State_Model.md      RSM references DSS

Forbidden Dependencies:
    UNSUPPORTED (DSS does not declare forbidden document-level
    dependencies)

Dependency Constraints:
    DC-D-04  All 10 DSS sections must derive from RMM only       DSS Section 3

------------------------------------------------------------------------------

3.5 ARTIFACT_META_MODEL.md
--------------------------

Identifier: ARTIFACT_META_MODEL
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    AMM (cited throughout all sections)
    KERNEL_SCOPE_DEFINITION.md     AMM Section 1.4 (Scope Boundary)
    KERNEL_STRUCTURE_SPEC.md       AMM Section 2.3 (Naming)

Referenced By:
    ARTIFACT_FAMILY_MODEL.md       AFM Normative References
    Repository_State_Model.md      RSM Section 8

Required Before:
    ARTIFACT_FAMILY_MODEL.md       AFM depends on AMM for invariants
    Repository_State_Model.md      RSM depends on AMM for state tracks

Forbidden Dependencies:
    AMM may not define: Document families, Templates, ADR, Evidence
    (as definition), Pattern, Contract, Workflow, Policy, Standard,
    Guideline, Repository structure, Products, AI behavior,
    Implementation, Technology.                          AMM Section 1.4

Dependency Constraints:
    DC-D-05  AMM must define ONLY what an Artifact IS; must not
             define governance, workflow, or implementation.      AMM Section 1.4

------------------------------------------------------------------------------

3.6 ARTIFACT_FAMILY_MODEL.md
----------------------------

Identifier: ARTIFACT_FAMILY_MODEL
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    AFM Normative References
    KERNEL_SCOPE_DEFINITION.md     AFM Normative References
    KERNEL_STRUCTURE_SPEC.md       AFM Normative References
    DOCUMENT_STANDARD_SPEC.md      AFM Normative References
    ARTIFACT_META_MODEL.md         AFM Normative References

Referenced By:
    Repository_State_Model.md      RSM Section 8

Required Before:
    Repository_State_Model.md      RSM depends on AFM for lifecycle data

Forbidden Dependencies:
    AFM may not define: Document templates, governance, workflow,
    implementation, products, repositories, or technology.       AFM Scope

Dependency Constraints:
    DC-D-06  AFM must classify only; must not describe
             implementation or create templates.                 AFM Objective

------------------------------------------------------------------------------

3.7 Repository_State_Model.md
-----------------------------

Identifier: REPOSITORY_STATE_MODEL
Source of Truth: 01-META-MODEL/

Depends On:
    RMM_v1.1.md                    RSM Section 8
      - Entity: STATE              RMM properties 1-15, M2 row 66
      - Entity: LIFECYCLE          RMM properties 1-15, M2 row 65
      - Matrix 2 (Lifecycle)       79 rows, 3 columns
      - Matrix 3 (Stability)       79 rows, 4 columns
      - Matrix 4 (Versionability)  79 rows, 4 columns
      - Matrix 5 (Freeze)          79 rows, 5 columns
      - Matrix 6 (Source-of-Truth) 79 rows, 5 columns
    ARTIFACT_META_MODEL.md         RSM Section 8 (Sections 3, 9, 10)
    ARTIFACT_FAMILY_MODEL.md       RSM Section 8 (Sections 2.5-7.5)
    DOCUMENT_STANDARD_SPEC.md      RSM Section 8 (Sections 3.4, 3.5)

Referenced By:
    (none — RSM is the terminal document in the dependency chain)

Required Before:
    UNSUPPORTED (no document requires RSM to exist before it)

Forbidden Dependencies:
    UNSUPPORTED (RSM does not declare forbidden document-level
    dependencies)

Dependency Constraints:
    DC-D-07  RSM must not invent states not in RMM Matrix 2       RSM Section 1

------------------------------------------------------------------------------

DOCUMENT DEPENDENCY SUMMARY
---------------------------

The document-level dependency graph is a Directed Acyclic Graph (DAG)
with RMM_v1.1.md as the root:

    RMM_v1.1.md
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

Total documents: 7
Total explicit document-to-document dependencies: 18
Root: RMM_v1.1.md (6 downstream dependents)
Leaf: Repository_State_Model.md (0 downstream dependents)

Cycles: None detected.

------------------------------------------------------------------------------

4. CORE ENTITY DEPENDENCIES
---------------------------

RMM Basis: Matrix 9 rows for CONSTITUTION, CHARTER, GOVERNANCE_BODY,
           ARTIFACT, DOCUMENT, LIFECYCLE, STATE; RMM properties 6-7.

The following dependencies are extracted from Matrix 9 (Dependency Matrix)
and RMM properties #6 (Allowed Relationships) and #7 (Forbidden
Relationships) for the core Kernel governance and artifact entities.

------------------------------------------------------------------------------

4.1 CONSTITUTION
----------------

RMM Basis: Matrix 9 row 24; RMM property #6, property #7.

Depends On:
    Kernel (root)                  Matrix 9: "Kernel (root)"

Referenced By:
    Charter                        Matrix 9: "Required By: Charter"
    GovernanceBody                 Matrix 9: "Required By: GovernanceBody"
    Invariant                      Matrix 9: "Required By: Invariant"
    Role                           Matrix 9: "Required By: Role"
    Rule                           Matrix 9: "Required By: Rule"
    Policy                         Matrix 9: "Required By: Policy"
    Actor                          Matrix 9: "Required By: Actor"
    RMM property #6: Empowers GovernanceBody; Establishes Charter;
    Defines Rule; Supersedes AllGovernanceEntities.

Required Before:
    Charter                        Charter depends on Constitution
    GovernanceBody                 GovernanceBody is empowered by Constitution
    Invariant                      Invariant derives from Constitution
    Role                           Role is established by Constitution
    Rule                           Rule is defined by Constitution
    Policy                         Policy flows from Constitution
    Actor                          Actor references Constitution

Forbidden Dependencies:
    CONSTITUTION may not be overridden by any entity except by its
    own amendment procedure.                                       RMM #7

Dependency Constraints:
    DC-E-01  Constitution amendment requires its own procedure     RMM #7

------------------------------------------------------------------------------

4.2 CHARTER
-----------

RMM Basis: Matrix 9 row 25; RMM property #6, property #7.

Depends On:
    Constitution                   Matrix 9: "Depends On: Constitution"
    GovernanceBody                 Matrix 9: "Depends On: GovernanceBody"
    RMM property #6: Governs GovernanceBody; Delegates Authority;
    References Constitution.

Referenced By:
    GovernanceBody                 Matrix 9: "Required By: GovernanceBody"

Required Before:
    GovernanceBody                 GovernanceBody is chartered by Charter

Forbidden Dependencies:
    CHARTER may not be deleted (only Dissolved); may not bypass
    Constitution; may not self-amend.                              RMM #7

Dependency Constraints:
    DC-E-02  Charter dissolution requires ratification             RMM #7

------------------------------------------------------------------------------

4.3 GOVERNANCE_BODY
-------------------

RMM Basis: RMM property #6, property #7. Not in Matrix 9.

Depends On:
    Charter                        RMM property #6: "CharteredBy Charter"
    Role                           RMM property #6: "ComposedOf Role"

Referenced By:
    UNSUPPORTED (GOVERNANCE_BODY not found in Matrix 9 Required By
    column for explicit extraction)

Required Before:
    Policy                         GovernanceBody creates Policy
    Standard                       GovernanceBody defines Standard
    Rule                           GovernanceBody establishes Rule

Forbidden Dependencies:
    GOVERNANCE_BODY may not exceed chartered authority; may not
    dissolve itself without ratification.                          RMM #7

Dependency Constraints:
    DC-E-03  GovernanceBody authority is bounded by Charter        RMM #7

------------------------------------------------------------------------------

4.4 ARTIFACT
------------

RMM Basis: Matrix 9 row 44; RMM property #6, property #7.

Depends On:
    Process                        Matrix 9: "Depends On: Process"
    Task                           Matrix 9: "Depends On: Task"
    RMM property #6: Consumed by Process; produced by Process;
    composed of other Artifacts; traced via TraceabilityLink;
    versioned as Revision; baselined via Baseline.

Referenced By:
    Document                       Matrix 9: "Required By: Document"
    Specification                  Matrix 9: "Required By: Specification"
    Record                         Matrix 9: "Required By: Record"
    Baseline                       Matrix 9: "Required By: Baseline"
    Snapshot                       Matrix 9: "Required By: Snapshot"

Required Before:
    Document                       Document is a subtype of Artifact
    Specification                  Specification is a subtype of Artifact
    Record                         Record is a subtype of Artifact
    Baseline                       Baseline references artifacts
    Snapshot                       Snapshot captures artifacts

Forbidden Dependencies:
    ARTIFACT may not directly own a Module; may not modify a
    Governance Rule; may not be directly self-referential
    (recursive composition of distinct artifacts is permitted).    RMM #7

Dependency Constraints:
    DC-E-04  Artifact may not own Module                         RMM #7
    DC-E-05  Artifact may not modify Governance Rule             RMM #7

------------------------------------------------------------------------------

4.5 DOCUMENT
------------

RMM Basis: Matrix 9 row 45; RMM property #6, property #7.

Depends On:
    Module                         Matrix 9: "Depends On: Module"
    Artifact                       Matrix 9: "Depends On: Artifact"
    RMM property #6: Traced to Specification; versioned;
    baselined; signed.

Referenced By:
    Baseline                       Matrix 9: "Required By: Baseline"
    Review                         Matrix 9: "Required By: Review"
    Approval                       Matrix 9: "Required By: Approval"

Required Before:
    Baseline                       Baseline captures documents
    Review                         Reviews examine documents
    Approval                       Approvals authorize documents

Forbidden Dependencies:
    DOCUMENT may not directly execute a Process; may not be
    self-approving; may not be both Draft and Published.           RMM #7

Dependency Constraints:
    DC-E-06  Document may not execute Process                    RMM #7
    DC-E-07  Document may not be self-approving                  RMM #7
    DC-E-08  Document may not be both Draft and Published        RMM #7

------------------------------------------------------------------------------

4.6 LIFECYCLE
-------------

RMM Basis: Matrix 9 row 65; RMM property #6, property #7.

Depends On:
    Governance                     Matrix 9: "Depends On: Governance"
    State                          Matrix 9: "Depends On: State"
    RMM property #6: Has Stage, Gate; AppliesTo Entity.

Referenced By:
    Module                         Matrix 9: "Required By: Module"
    Component                      Matrix 9: "Required By: Component"
    Feature                        Matrix 9: "Required By: Feature"

Required Before:
    Module                         Module follows a lifecycle
    Component                      Component follows a lifecycle
    Feature                        Feature follows a lifecycle

Forbidden Dependencies:
    LIFECYCLE may not have unreachable stages; may not have
    ambiguous transitions; may not skip required gates.            RMM #7

Dependency Constraints:
    DC-E-09  Lifecycle must have all stages reachable             RMM #7
    DC-E-10  Lifecycle transitions must not be ambiguous          RMM #7

------------------------------------------------------------------------------

4.7 STATE
---------

RMM Basis: Matrix 9 row 66; RMM property #6, property #7.

Depends On:
    Lifecycle                      Matrix 9: "Depends On: Lifecycle"
    Invariant                      Matrix 9: "Depends On: Invariant"
    RMM property #6: Belongs to Lifecycle; has EntryAction,
    ExitAction, Invariant; transitions to State.

Referenced By:
    Lifecycle                      Matrix 9: "Required By: Lifecycle"

Required Before:
    Lifecycle                      Lifecycle contains states

Forbidden Dependencies:
    STATE may not exist without definition; may not be ambiguous
    with another State.                                            RMM #7

Dependency Constraints:
    DC-E-11  State must have explicit definition                  RMM #7
    DC-E-12  State must not be ambiguous with another State       RMM #7

------------------------------------------------------------------------------

ENTITY DEPENDENCY SUMMARY
-------------------------

Total core entities analyzed: 7
Total explicit entity-to-entity dependencies: 42
Total forbidden dependency rules: 12

------------------------------------------------------------------------------

5. CROSS-ARTIFACT DEPENDENCY CONSTRAINTS
----------------------------------------

RMM Basis: Matrix 9; AMM Section 8; RMM properties 6-7.

The following constraints apply across all dependency types:

    CAC-01  No cyclic dependencies between Kernel documents.
            Verified: document dependency graph is a DAG
            with RMM as root.                                      Matrix 9

    CAC-02  If A depends on B and B depends on C, then A
            transitively depends on C. This transitive closure
            is: UNSUPPORTED (not explicitly computed in RMM).      RMM

    CAC-03  Forbidden dependencies (RMM property #7) are absolute.
            No exception mechanism exists at the document level.
            Per EXCEPTION entity: deviations require formal
            exception from GovernanceBody.                         RMM #7, M2R67

    CAC-04  All document-level dependencies must be explicitly
            stated in Normative References sections. Dependencies
            not stated in Normative References are:

                UNSUPPORTED

    CAC-05  Entity-level dependencies are derived from Matrix 9
            and RMM properties 6-7 only. Dependencies inferred
            from other sources are: UNSUPPORTED.

------------------------------------------------------------------------------

6. FORBIDDEN DEPENDENCIES
-------------------------

RMM Basis: RMM property #7 for all core entities; AMM Section 8.2;
           DOCUMENT_STANDARD_SPEC Section 3.7.2.

6.1 RMM-Level Forbidden Dependencies

    Entity          Forbidden Dependency                         Source
    --------------  -----------------------------------------  ---------
    CONSTITUTION    May not be overridden except by amendment  RMM #7
    CHARTER         May not be deleted; may not bypass         RMM #7
                    Constitution; may not self-amend
    GOVERNANCE_BODY May not exceed chartered authority;        RMM #7
                    may not dissolve itself without ratification
    ARTIFACT        May not own Module; may not modify         RMM #7
                    Governance Rule; may not be self-referential
    DOCUMENT        May not execute Process; may not be        RMM #7
                    self-approving; may not be Draft+Published
    LIFECYCLE       May not have unreachable stages; may not   RMM #7
                    skip required gates
    STATE           May not exist without definition; may not  RMM #7
                    be ambiguous

6.2 Document-Level Forbidden Dependencies

    Artifact        Forbidden Target                           Source
    --------------  -----------------------------------------  ---------
    All Kernel      Product-specific artifacts                 KSD Section 3
    documents
    All Kernel      Technology-specific implementations        KSD Section 3
    documents
    All Kernel      External product repositories              KSD Section 3
    documents
    AMM             Document families, Templates, ADR,         AMM Section 1.4
                    Evidence, Pattern, Contract, Workflow,
                    Policy, Standard, Guideline, Repository
                    structure, Products, AI behavior,
                    Implementation, Technology
    AFM             Same as AMM plus: implementation           AFM Objective
                    descriptions, templates

6.3 Forbidden Target Categories

    Category              Rationale
    --------------------  ------------------------------------------
    Product artifacts     KSD Section 3.1 — Kernel does not contain
                          product source code
    Technology names      KSD Section 3.2 — technology independence
    Infrastructure        KSD Section 3.3 — outside Kernel scope
    Business strategy     KSD Section 3.4 — outside Kernel scope
    External systems      KSD Section 7 — Kernel authority does not
                          extend to external systems

------------------------------------------------------------------------------

7. VALIDATION RULES
-------------------

RMM Basis: AMM Section 10; Matrix 9; RMM properties 6-7.

    Rule    Description                                         Source
    ------  --------------------------------------------------  -------------
    V-DM-01 Every dependency must cite its explicit source       This Model
    V-DM-02 No dependency may contradict RMM property #7         RMM #7
    V-DM-03 Document dependencies must appear in Normative       DSS Section 3.7
            References
    V-DM-04 Entity dependencies must appear in Matrix 9          Matrix 9
            or RMM property #6
    V-DM-05 No circular dependencies among Kernel documents      This Model
    V-DM-06 Forbidden dependencies are absolute                  RMM #7
    V-DM-07 Transitive dependencies are UNSUPPORTED              This Model
    V-DM-08 Inferred dependencies are UNSUPPORTED                This Model

------------------------------------------------------------------------------

8. NORMATIVE REFERENCES
-----------------------

Reference                        Location
-------------------------------  --------------------------------------------
Repository Meta Model v1.1       01-META-MODEL/RMM_v1.1.md
  - Matrix 9: Dependency Matrix  79 rows, 4 columns
  - RMM properties 6-7           Allowed/Forbidden Relationships
Artifact Meta Model              01-META-MODEL/ARTIFACT_META_MODEL.md
  - Section 8                    Artifact Relationships
Artifact Family Model            01-META-MODEL/ARTIFACT_FAMILY_MODEL.md
  - Sections 2.6-13.6            Family-level dependencies
Kernel Scope Definition          01-META-MODEL/KERNEL_SCOPE_DEFINITION.md
  - Section 3                    Out of Scope (forbidden targets)
Document Standard Spec           01-META-MODEL/DOCUMENT_STANDARD_SPEC.md
  - Section 3.7                  Dependencies section format
Repository State Model           01-META-MODEL/Repository_State_Model.md
  - Section 6                    Prohibited Transitions

------------------------------------------------------------------------------

END OF DOCUMENT
