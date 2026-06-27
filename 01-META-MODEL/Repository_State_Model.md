ENGINEERING KERNEL — REPOSITORY STATE MODEL
===========================================

Version: 1.0.0
Status: Approved
Date: 2026-06-26
Authority: MISSION-006
Source of Truth: Artifact Repository
Stability: Slow

------------------------------------------------------------------------------

TABLE OF CONTENTS
-----------------

1. Model Scope
2. State Taxonomy
   2.1 Artifact Lifecycle Track
   2.2 Document Lifecycle Track
3. State Definitions
   3.1 State: Defined
   3.2 State: Created
   3.3 State: Active
   3.4 State: Archived
   3.5 State: Destroyed
   3.6 State: Draft
   3.7 State: Review
   3.8 State: Approved
   3.9 State: Published
   3.10 State: Superseded
4. Cross-Cutting Invariants
5. Terminal State Summary
6. Prohibited Transition Summary
7. Validation Rule Summary
8. Normative References

------------------------------------------------------------------------------

1. MODEL SCOPE
--------------

RMM Basis: ENTITY.STATE properties 1-6; ENTITY.LIFECYCLE properties 1-7;
           ARTIFACT_META_MODEL.md Sections 3, 9, 10;
           ARTIFACT_FAMILY_MODEL.md Section 2.5, 3.5, 4.5, 5.5, 6.5, 7.5.

The Repository State Model defines every state that a repository entity
may occupy, every legal transition between states, every state invariant,
terminal states, and prohibited transitions.

This model applies to all entities whose Source of Truth is within the
Kernel repository per RMM property #15.

States not explicitly defined in the authoritative inputs are:

    UNSUPPORTED

------------------------------------------------------------------------------

2. STATE TAXONOMY
-----------------

The Repository State Model defines two lifecycle tracks derived from
the RMM and the Artifact Meta Model.

2.1 Artifact Lifecycle Track
    RMM Basis: Matrix 2 row 44; AMM Section 3.1.
    Sequence: Defined → Created → Active → Archived → Destroyed
    This track applies to all Artifact-family entities per AMM Section 1.

2.2 Document Lifecycle Track
    RMM Basis: Matrix 2 row 45; AMM Section 3.3.
    Sequence: Draft → Review → Approved → Published → Superseded → Archived
    This track applies to all Document-family entities per AFM Section 2.

2.3 Shared State
    The Archived state appears in both tracks. An entity in Archived
    from either track occupies the same canonical state.

2.4 State Mutability
    Per AMM Section 3.1 and Matrix 3, Artifact stability is Slow.
    Per AMM Section 3.3, Document stability varies by subtype.
    State changes are therefore infrequent and deliberate.

------------------------------------------------------------------------------

3. STATE DEFINITIONS
--------------------

Each state definition contains exactly nine fields:
Identifier, Purpose, Entry Conditions, Exit Conditions,
Allowed Transitions, Forbidden Transitions, Invariants,
Validation Rules, RMM References.

------------------------------------------------------------------------------

3.1 STATE: DEFINED
------------------

Identifier: DEFINED

Purpose: Concept established; not yet instantiated.
    RMM Basis: Matrix 2 row 44, AMM Section 3.1.
    Per RMM STATE property #2: A distinguishable condition that an entity
    can occupy at a point in time. Defined is the initial condition for
    artifact concepts.

Entry Conditions:
    EC-D-01  Entity concept has been identified                     AMM Section 3.1
    EC-D-02  Entity properties (1-15) are specified in RMM         RMM properties 1-15
    EC-D-03  Entity name is non-empty UPPER_SNAKE_CASE             AMM V-01, RMM #1
    Exit Conditions:
    XC-D-01  Entity is instantiated → transition to Created         AMM Section 3.1
    XC-D-02  Concept is abandoned → transition to Destroyed        AMM Section 3.1
    XC-D-03  Entity properties remain valid throughout transition  AMM Section 9.1

Allowed Transitions:
    T-D-01  Defined → Created     (instantiation)                  AMM Section 3.1
    T-D-02  Defined → Destroyed   (abandonment)                    AMM Section 3.1

Forbidden Transitions:
    FT-D-01  Defined → Active      (skip Created)                   AMM Section 3.3
    FT-D-02  Defined → Archived    (skip Created and Active)        AMM Section 3.3
    FT-D-03  Defined → Approved    (Document track mismatch)        AMM Section 3.3
    FT-D-04  Defined → Published   (Document track mismatch)        AMM Section 3.3

Invariants:
    I-D-01  Entity in Defined SHALL have non-empty Entity Name      AMM 9.1, RMM #1
    I-D-02  Entity in Defined SHALL have non-empty Purpose          AMM 9.1, RMM #2
    I-D-03  Entity in Defined SHALL have specified Owner            AMM 9.3, RMM #4
    I-D-04  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-D-01  Entity Name is UPPER_SNAKE_CASE                         AMM V-01, RMM #1
    V-D-02  Purpose is non-empty                                    AMM V-02, RMM #2
    V-D-03  Responsibility is non-empty                             AMM V-03, RMM #3
    V-D-04  Owner is canonical RMM entity                           AMM V-04, RMM #4

RMM References:
    - Matrix 2 row 44 (Artifact lifecycle)
    - RMM STATE properties 1-3
    - RMM LIFECYCLE properties 1-3
    - AMM Sections 3.1, 9.1, 9.2, 9.3

------------------------------------------------------------------------------

3.2 STATE: CREATED
------------------

Identifier: CREATED

Purpose: Physical instance exists.
    RMM Basis: Matrix 2 row 44, AMM Section 3.1.
    The entity has been instantiated as a tangible artifact within the
    repository.

Entry Conditions:
    EC-C-01  Prior state was Defined                               AMM Section 3.1
    EC-C-02  Physical instance has been created                    AMM Section 3.1
    EC-C-03  Entity properties (1-15) are recorded                 RMM properties 1-15

Exit Conditions:
    XC-C-01  Instance is activated for use → transition to Active   AMM Section 3.1
    XC-C-02  Instance is abandoned → transition to Destroyed       AMM Section 3.1

Allowed Transitions:
    T-C-01  Created → Active        (activation)                   AMM Section 3.1
    T-C-02  Created → Destroyed     (abandonment)                  AMM Section 3.1

Forbidden Transitions:
    FT-C-01  Created → Archived     (skip Active)                  AMM Section 3.1
    FT-C-02  Created → Defined      (reverse flow)                 AMM Section 3.1
    FT-C-03  Created → Approved     (Document track mismatch)      AMM Section 3.3
    FT-C-04  Created → Published    (Document track mismatch)      AMM Section 3.3

Invariants:
    I-C-01  Entity in Created SHALL have non-empty Entity Name      AMM 9.1
    I-C-02  Entity in Created SHALL have one canonical Owner        AMM 9.3
    I-C-03  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-C-01  Cardinality is N:M per entity type                     AMM V-06, RMM #8
    V-C-02  Stability matches entity type (Slow for Artifact)      AMM V-07, RMM #9
    V-C-03  Versionable matches entity type (Yes for Artifact)     AMM V-08, RMM #10

RMM References:
    - Matrix 2 row 44 (Artifact lifecycle)
    - RMM STATE property #2
    - AMM Sections 3.1, 9.1, 9.2, 9.3

------------------------------------------------------------------------------

3.3 STATE: ACTIVE
-----------------

Identifier: ACTIVE

Purpose: In use; may be referenced by other entities.
    RMM Basis: Matrix 2 row 44, AMM Section 3.1.
    The entity is operational and available for consumption,
    transformation, or reference by other repository entities.

Entry Conditions:
    EC-A-01  Prior state was Created                               AMM Section 3.1
    EC-A-02  Instance is ready for use and reference               AMM Section 3.1
    EC-A-03  Entity integrity is validated                         AMM Section 9

Exit Conditions:
    XC-A-01  Entity is no longer actively referenced               AMM Section 3.1
    XC-A-02  Retention policy triggers archival                   AMM Section 3.1
    XC-A-03  Entity is abandoned → transition to Destroyed        AMM Section 3.1

Allowed Transitions:
    T-A-01  Active → Archived       (retention/archival)           AMM Section 3.1
    T-A-02  Active → Destroyed      (abandonment)                  AMM Section 3.1

Forbidden Transitions:
    FT-A-01  Active → Defined       (reverse flow)                 AMM Section 3.1
    FT-A-02  Active → Created       (reverse flow)                 AMM Section 3.1
    FT-A-03  Active → Approved      (Document track mismatch)      AMM Section 3.3
    FT-A-04  Active → Draft         (Document track mismatch)      AMM Section 3.3

Invariants:
    I-A-01  Entity in Active SHALL be referenceable by other       AMM 9.2
            entities
    I-A-02  Entity in Active SHALL have valid Source of Truth      AMM 9.1, RMM #15
    I-A-03  Entity SHALL occupy exactly one state at any time       AMM 9.2
    I-A-04  Entity stability SHALL match entity type               AMM 9.4

Validation Rules:
    V-A-01  Freezable matches entity type (Yes for Artifact)       AMM V-09, RMM #11
    V-A-02  AI Modifiable matches entity type                      AMM V-12, RMM #13
    V-A-03  Human Modifiable matches entity type                   AMM V-13, RMM #14

RMM References:
    - Matrix 2 row 44 (Artifact lifecycle)
    - RMM STATE properties 1-3, RMM #15
    - AMM Sections 3.1, 9.1, 9.2, 9.3, 9.4

------------------------------------------------------------------------------

3.4 STATE: ARCHIVED
-------------------

Identifier: ARCHIVED

Purpose: Preserved for historical reference.
    RMM Basis: Matrix 2 row 44/45; AMM Sections 3.1, 3.3.
    This state is shared between the Artifact and Document lifecycle
    tracks. An Archived entity is retained but no longer active.

Entry Conditions:
    EC-AR-01  Prior state was Active (Artifact track)              AMM Section 3.1
    EC-AR-02  Prior state was Superseded (Document track)          AMM Section 3.3
    EC-AR-03  Entity is frozen per Freeze mechanism                AMM Section 3.4, Matrix 5
    EC-AR-04  Retention period is defined                          RMM LIFECYCLE property #5

Exit Conditions:
    XC-AR-01  Retention policy expires                            AMM Section 3.1
    XC-AR-02  Entity is permanently destroyed                     AMM Section 3.1

Allowed Transitions:
    T-AR-01  Archived → Destroyed   (permanent removal)            AMM Section 3.1

Forbidden Transitions:
    FT-AR-01  Archived → Active     (reactivation forbidden)       AMM Section 3.1
    FT-AR-02  Archived → Defined    (reverse flow)                 AMM Section 3.1
    FT-AR-03  Archived → Created    (reverse flow)                 AMM Section 3.1
    FT-AR-04  Archived → Draft      (Document track re-entry)      AMM Section 3.3

Invariants:
    I-AR-01  Entity in Archived SHALL be frozen                    AMM 9.6, Matrix 5
    I-AR-02  Entity in Archived SHALL NOT be modifiable            AMM 9.6, RMM #11
    I-AR-03  Entity SHALL occupy exactly one state at any time      AMM 9.2
    I-AR-04  Archived entity SHALL retain Source of Truth          AMM 9.1, RMM #15

Validation Rules:
    V-AR-01  Freezable is Yes                                       AMM V-09, RMM #11
    V-AR-02  Entity Owner remains canonical                        AMM V-04, RMM #4
    V-AR-03  Source of Truth remains valid                         AMM V-10, RMM #15

RMM References:
    - Matrix 2 rows 44, 45 (Artifact and Document lifecycles)
    - Matrix 5 row 44 (Freeze: Yes)
    - RMM STATE property #2, RMM LIFECYCLE properties 5, 7
    - AMM Sections 3.1, 3.3, 3.4, 9.1, 9.2, 9.6

------------------------------------------------------------------------------

3.5 STATE: DESTROYED
--------------------

Identifier: DESTROYED

Purpose: Permanently removed per retention policy.
    RMM Basis: Matrix 2 row 44, AMM Section 3.1.
    Terminal state. No further transitions, modifications, or references.

Entry Conditions:
    EC-DY-01  Prior state was Archived                             AMM Section 3.1
    EC-DY-02  Retention policy has expired                        AMM Section 3.1
    EC-DY-03  Prior state was Defined (abandoned concept)          AMM Section 3.1
    EC-DY-04  Prior state was Created (abandoned instance)        AMM Section 3.1
    EC-DY-05  Prior state was Active (abandoned active entity)    AMM Section 3.1

Exit Conditions:
    XC-DY-01  None. Destroyed is terminal.                        AMM Section 3.1

Allowed Transitions:
    None. Destroyed is a terminal state.

Forbidden Transitions:
    FT-DY-01  Destroyed → ANY       (all transitions prohibited)   AMM Section 3.1
    FT-DY-02  Destroyed → Defined   (terminal lock)                AMM Section 3.1
    FT-DY-03  Destroyed → Created   (terminal lock)                AMM Section 3.1
    FT-DY-04  Destroyed → Active    (terminal lock)                AMM Section 3.1
    FT-DY-05  Destroyed → Archived  (terminal lock)                AMM Section 3.1

Invariants:
    I-DY-01  Entity in Destroyed SHALL NOT be referenced            AMM 9.2, RMM #7
    I-DY-02  Entity in Destroyed SHALL NOT be modified             AMM 9.6, RMM #11
    I-DY-03  Entity in Destroyed SHALL have null Source of Truth   RMM #15
    I-DY-04  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-DY-01  Entity is not freezable in Destroyed state            AMM V-09
    V-DY-02  Entity is not versionable in Destroyed state          AMM V-08
    V-DY-03  Entity is not referenceable in Destroyed state        RMM #7

RMM References:
    - Matrix 2 row 44 (Artifact lifecycle terminal)
    - RMM STATE property #2
    - RMM LIFECYCLE property #5
    - AMM Sections 3.1, 9.2, 9.6

------------------------------------------------------------------------------

3.6 STATE: DRAFT
----------------

Identifier: DRAFT

Purpose: Initial creation; incomplete.
    RMM Basis: Matrix 2 row 45, AMM Section 3.3.
    The entity is under construction and not yet ready for review.

Entry Conditions:
    EC-DR-01  Entity creation has been initiated                   AMM Section 3.3
    EC-DR-02  Entity structure is partially complete               AMM Section 3.3
    EC-DR-03  Entity is not yet submitted for review              AMM Section 3.3

Exit Conditions:
    XC-DR-01  Entity is submitted for review → transition to Review AMM Section 3.3
    XC-DR-02  Entity is abandoned → transition to Archived        AMM Section 3.3

Allowed Transitions:
    T-DR-01  Draft → Review        (submission for review)        AMM Section 3.3
    T-DR-02  Draft → Archived      (abandonment)                  AMM Section 3.3

Forbidden Transitions:
    FT-DR-01  Draft → Approved     (skip Review)                  AMM Section 3.3
    FT-DR-02  Draft → Published    (skip Review and Approved)     AMM Section 3.3
    FT-DR-03  Draft → Defined      (Artifact track mismatch)      AMM Section 3.1
    FT-DR-04  Draft → Created      (Artifact track mismatch)      AMM Section 3.1

Invariants:
    I-DR-01  Entity in Draft SHALL have non-empty Entity Name       AMM 9.1
    I-DR-02  Entity in Draft SHALL have Owner specified            AMM 9.3
    I-DR-03  Entity SHALL occupy exactly one state at any time       AMM 9.2
    I-DR-04  Entity in Draft is modifiable                         AMM 9.6, Matrix 5

Validation Rules:
    V-DR-01  Entity Name is UPPER_SNAKE_CASE                       AMM V-01
    V-DR-02  AI Creatable is Yes for Draft Document                AMM V-11
    V-DR-03  Human Modifiable is Yes for Draft Document            AMM V-13

RMM References:
    - Matrix 2 row 45 (Document lifecycle)
    - RMM STATE properties 1-3
    - AMM Sections 3.3, 9.1, 9.2, 9.3, 9.6

------------------------------------------------------------------------------

3.7 STATE: REVIEW
-----------------

Identifier: REVIEW

Purpose: Under peer or governance review.
    RMM Basis: Matrix 2 row 45, AMM Section 3.3.
    The entity is being examined by authorized reviewers.

Entry Conditions:
    EC-RV-01  Prior state was Draft                                AMM Section 3.3
    EC-RV-02  Entity is submitted for review                      AMM Section 3.3
    EC-RV-03  Reviewers are assigned                              RMM STATE property #6

Exit Conditions:
    XC-RV-01  Review completed satisfactorily → Approved          AMM Section 3.3
    XC-RV-02  Review requires rework → Draft                      AMM Section 3.3

Allowed Transitions:
    T-RV-01  Review → Approved     (review passed)                 AMM Section 3.3
    T-RV-02  Review → Draft        (rework required)              AMM Section 3.3

Forbidden Transitions:
    FT-RV-01  Review → Published   (skip Approved)                AMM Section 3.3
    FT-RV-02  Review → Superseded  (skip Approved and Published)  AMM Section 3.3
    FT-RV-03  Review → Destroyed   (no bypass)                    AMM Section 3.3
    FT-RV-04  Review → Active      (Artifact track mismatch)      AMM Section 3.1

Invariants:
    I-RV-01  Entity in Review SHALL have assigned reviewers        RMM STATE property #6
    I-RV-02  Entity in Review SHALL NOT be modified by author      AMM 9.6
    I-RV-03  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-RV-01  Reviewer assignment is non-empty                     RMM STATE property #6
    V-RV-02  Entity is not modifiable during Review                AMM V-12

RMM References:
    - Matrix 2 row 45 (Document lifecycle)
    - RMM STATE properties 1-3, 6
    - AMM Sections 3.3, 9.2, 9.6

------------------------------------------------------------------------------

3.8 STATE: APPROVED
-------------------

Identifier: APPROVED

Purpose: Review completed satisfactorily.
    RMM Basis: Matrix 2 row 45, AMM Section 3.3.
    The entity has passed review and is authorized for publication.

Entry Conditions:
    EC-AP-01  Prior state was Review                               AMM Section 3.3
    EC-AP-02  Review has been completed                           AMM Section 3.3
    EC-AP-03  Approval criteria are met                           RMM LIFECYCLE property #7

Exit Conditions:
    XC-AP-01  Entity is published → transition to Published       AMM Section 3.3
    XC-AP-02  Entity requires rework → transition to Draft        AMM Section 3.3

Allowed Transitions:
    T-AP-01  Approved → Published   (publication)                 AMM Section 3.3
    T-AP-02  Approved → Draft       (rework)                      AMM Section 3.3

Forbidden Transitions:
    FT-AP-01  Approved → Review    (reverse flow)                 AMM Section 3.3
    FT-AP-02  Approved → Archived  (skip Published)               AMM Section 3.3
    FT-AP-03  Approved → Destroyed (no bypass)                    AMM Section 3.3
    FT-AP-04  Approved → Active    (Artifact track mismatch)      AMM Section 3.1

Invariants:
    I-AP-01  Entity in Approved SHALL have Approval record         RMM LIFECYCLE property #7
    I-AP-02  Entity in Approved SHALL be freezable                 AMM 9.6, Matrix 5
    I-AP-03  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-AP-01  Approval record exists                               RMM LIFECYCLE property #7
    V-AP-02  Freezable is Yes for Approved Document               AMM V-09
    V-AP-03  Human Modifiable is With Approval                    AMM V-13

RMM References:
    - Matrix 2 row 45 (Document lifecycle)
    - RMM STATE properties 1-3
    - RMM LIFECYCLE properties 5, 7
    - AMM Sections 3.3, 9.2, 9.6

------------------------------------------------------------------------------

3.9 STATE: PUBLISHED
--------------------

Identifier: PUBLISHED

Purpose: Approved and distributed.
    RMM Basis: Matrix 2 row 45, AMM Section 3.3.
    The entity has been approved and is available for consumption.

Entry Conditions:
    EC-PB-01  Prior state was Approved                             AMM Section 3.3
    EC-PB-02  Entity has been distributed                         AMM Section 3.3
    EC-PB-03  Entity is available for reference                   AMM Section 3.3

Exit Conditions:
    XC-PB-01  Entity is replaced → transition to Superseded       AMM Section 3.3
    XC-PB-02  Entity is retired → transition to Archived          AMM Section 3.3

Allowed Transitions:
    T-PB-01  Published → Superseded  (replaced)                   AMM Section 3.3
    T-PB-02  Published → Archived    (retirement)                 AMM Section 3.3

Forbidden Transitions:
    FT-PB-01  Published → Approved (reverse flow)                 AMM Section 3.3
    FT-PB-02  Published → Review   (reverse flow)                 AMM Section 3.3
    FT-PB-03  Published → Draft    (reverse flow)                 AMM Section 3.3
    FT-PB-04  Published → Active   (Artifact track mismatch)      AMM Section 3.1

Invariants:
    I-PB-01  Entity in Published SHALL be referenceable           AMM 9.2
    I-PB-02  Entity in Published SHALL be frozen                  AMM 9.6, Matrix 5
    I-PB-03  Entity SHALL occupy exactly one state at any time       AMM 9.2
    I-PB-04  Published entity SHALL retain version history        AMM 9.7, RMM #10

Validation Rules:
    V-PB-01  Versionable is Yes                                    AMM V-08
    V-PB-02  Freezable is Yes                                      AMM V-09
    V-PB-03  Entity is not modifiable without unfreeze            AMM 9.6

RMM References:
    - Matrix 2 row 45 (Document lifecycle)
    - RMM STATE property #2
    - AMM Sections 3.3, 9.2, 9.6, 9.7

------------------------------------------------------------------------------

3.10 STATE: SUPERSEDED
----------------------

Identifier: SUPERSEDED

Purpose: Replaced by newer version.
    RMM Basis: Matrix 2 row 45, AMM Section 3.3.
    The entity has been replaced by a newer version and is no longer
    the current reference.

Entry Conditions:
    EC-SP-01  Prior state was Published                            AMM Section 3.3
    EC-SP-02  Newer version has been published                   AMM Section 3.3
    EC-SP-03  Entity is no longer current reference              AMM Section 3.3

Exit Conditions:
    XC-SP-01  Entity is archived → transition to Archived         AMM Section 3.3

Allowed Transitions:
    T-SP-01  Superseded → Archived   (archival)                   AMM Section 3.3

Forbidden Transitions:
    FT-SP-01  Superseded → Published (reverse flow)               AMM Section 3.3
    FT-SP-02  Superseded → Approved  (reverse flow)               AMM Section 3.3
    FT-SP-03  Superseded → Active    (Artifact track mismatch)    AMM Section 3.1
    FT-SP-04  Superseded → Defined   (reverse flow)               AMM Section 3.3

Invariants:
    I-SP-01  Entity in Superseded SHALL have successor version     AMM 9.7, RMM #10
    I-SP-02  Entity in Superseded SHALL be frozen                  AMM 9.6, Matrix 5
    I-SP-03  Entity SHALL occupy exactly one state at any time       AMM 9.2

Validation Rules:
    V-SP-01  Successor version exists                             AMM 9.7
    V-SP-02  Freezable is Yes                                      AMM V-09
    V-SP-03  Entity is not modifiable without unfreeze            AMM 9.6

RMM References:
    - Matrix 2 row 45 (Document lifecycle)
    - RMM STATE property #2
    - AMM Sections 3.3, 9.2, 9.6, 9.7

------------------------------------------------------------------------------

4. CROSS-CUTTING INVARIANTS
---------------------------

RMM Basis: AMM Section 9; RMM STATE properties 6-7; RMM LIFECYCLE properties 6-7.

The following invariants apply to ALL states in the Repository State Model:

    CCI-01  Every entity SHALL occupy exactly one state at any
            time. No entity may occupy multiple states
            simultaneously.                                         AMM 9.2

    CCI-02  Every entity SHALL have exactly one canonical Owner
            (RMM property #4). Owner SHALL be a valid entity
            defined in RMM.                                         AMM 9.3

    CCI-03  No entity SHALL be directly self-referential.
            (Recursive composition of distinct artifacts is
            permitted.)                                             AMM 9.8, RMM #7

    CCI-04  Every state change SHALL leave a traceable record.
            UNSUPPORTED (RMM does not define traceability
            requirements for state changes).                        RMM STATE property #6

    CCI-05  State transitions SHALL follow the allowed paths
            defined in the entity's lifecycle. No skip
            transitions are permitted.                              RMM LIFECYCLE property #7

    CCI-06  Terminal states (Destroyed) SHALL have no exit
            transitions.                                            AMM Section 3.1

    CCI-07  Frozen entities (Archived, Published, Approved) SHALL
            not be modified without explicit unfreeze cycle.        AMM 9.6, Matrix 5

    CCI-08  Entity Source of Truth SHALL remain valid for all
            non-Destroyed states.                                   AMM 9.1, RMM #15

------------------------------------------------------------------------------

5. TERMINAL STATE SUMMARY
-------------------------

RMM Basis: AMM Section 3.1; Matrix 2 row 44.

The following states are terminal. No exit transitions are permitted.

    State      Track       RMM Basis
    ---------  ----------  -------------------------------
    Destroyed  Artifact    AMM Section 3.1, Matrix 2 row 44

Terminal state invariants:
    TS-01  Destroyed entity SHALL NOT be referenced            AMM 9.2
    TS-02  Destroyed entity SHALL NOT be modified             AMM 9.6
    TS-03  Destroyed entity SHALL have null Source of Truth   RMM #15

The following states are NOT terminal but have restricted exit:

    State      Exit Restriction                              RMM Basis
    ---------  --------------------------------------------- ------------------
    Archived   May only exit to Destroyed                    AMM Section 3.1
    Superseded May only exit to Archived                     AMM Section 3.3

------------------------------------------------------------------------------

6. PROHIBITED TRANSITION SUMMARY
--------------------------------

RMM Basis: AMM Sections 3.1, 3.3, 9.2; RMM LIFECYCLE property #7.

The following transitions are PROHIBITED for all entities:

    Prohibited Transition                    Rationale
    ---------------------------------------  ---------------------------
    ANY → Defined (reverse from Created+)    AMM Section 3.1
    ANY → Created (reverse from Active+)     AMM Section 3.1
    Destroyed → ANY (terminal lock)          AMM Section 3.1
    Active → Defined (reverse flow)          AMM Section 3.1
    Archived → Active (reactivation)         AMM Section 3.1

The following transitions are PROHIBITED within the Artifact track:

    Prohibited Transition                    Rationale
    ---------------------------------------  ---------------------------
    Defined → Active (skip Created)          AMM Section 3.1
    Defined → Archived (skip Created, Active) AMM Section 3.1
    Created → Archived (skip Active)         AMM Section 3.1

The following transitions are PROHIBITED within the Document track:

    Prohibited Transition                    Rationale
    ---------------------------------------  ---------------------------
    Draft → Approved (skip Review)           AMM Section 3.3
    Draft → Published (skip Review, Approved) AMM Section 3.3
    Review → Published (skip Approved)       AMM Section 3.3
    Review → Superseded (skip Approved,
                         Published)           AMM Section 3.3
    Approved → Review (reverse flow)         AMM Section 3.3
    Approved → Archived (skip Published)     AMM Section 3.3
    Published → Approved (reverse flow)      AMM Section 3.3
    Published → Review (reverse flow)        AMM Section 3.3
    Published → Draft (reverse flow)         AMM Section 3.3
    Superseded → Published (reverse flow)    AMM Section 3.3
    Superseded → Approved (reverse flow)     AMM Section 3.3

The following cross-track transitions are PROHIBITED:

    Prohibited Transition                    Rationale
    ---------------------------------------  ---------------------------
    Artifact track → Document track          Track mismatch            AMM Sections 3.1, 3.3
    Document track → Artifact track          Track mismatch            AMM Sections 3.1, 3.3

Entity-specific state transitions that deviate from these canonical
sequences are: UNSUPPORTED (not defined in RMM).

------------------------------------------------------------------------------

7. VALIDATION RULE SUMMARY
--------------------------

RMM Basis: AMM Section 10; RMM STATE properties 1-6.

Structural Validation:

    Rule    Description                                         Source
    ------  --------------------------------------------------  -------------
    V-01    Entity Name is non-empty and UPPER_SNAKE_CASE       AMM V-01
    V-02    Purpose is non-empty                                AMM V-02
    V-03    Responsibility is non-empty                         AMM V-03
    V-04    Owner is canonical RMM entity                       AMM V-04
    V-05    Lifecycle matches entity track                      AMM V-05
    V-06    Cardinality matches entity type                     AMM V-06
    V-07    Stability matches entity type                       AMM V-07
    V-08    Versionable matches entity type                     AMM V-08
    V-09    Freezable matches entity type                       AMM V-09
    V-10    Source of Truth is valid for non-Destroyed          AMM V-10

Permission Validation:

    Rule    Description                                         Source
    ------  --------------------------------------------------  -------------
    V-11    AI Creatable matches entity type                    AMM V-11
    V-12    AI Modifiable matches entity type                   AMM V-12
    V-13    Human Modifiable matches entity type                AMM V-13

State Validation:

    Rule    Description                                         Source
    ------  --------------------------------------------------  -------------
    V-14    Entity occupies exactly one state at any time       AMM V-17
    V-15    Terminal state (Destroyed) has no exit              AMM V-18
    V-16    State transition follows allowed path               AMM V-19
    V-17    Frozen state (Archived, Published, Approved)
            is not modifiable without unfreeze                  AMM 9.6

------------------------------------------------------------------------------

8. NORMATIVE REFERENCES
-----------------------

Reference                        Location
-------------------------------  --------------------------------------------
Repository Meta Model v1.1       01-META-MODEL/RMM_v1.1.md
  - Entity: STATE                Properties 1-15, Matrix 2 row 66
  - Entity: LIFECYCLE            Properties 1-15, Matrix 2 row 65
  - Matrix 2: Lifecycle Matrix   79 rows, 3 columns
  - Matrix 3: Stability          79 rows, 4 columns
  - Matrix 4: Versionability     79 rows, 4 columns
  - Matrix 5: Freeze             79 rows, 5 columns
  - Matrix 6: Source-of-Truth    79 rows, 5 columns
Artifact Meta Model              01-META-MODEL/ARTIFACT_META_MODEL.md
  - Sections 3, 9, 10
Artifact Family Model            01-META-MODEL/ARTIFACT_FAMILY_MODEL.md
  - Sections 2.5, 3.5, 4.5, 5.5, 6.5, 7.5
Document Standard Spec           01-META-MODEL/DOCUMENT_STANDARD_SPEC.md
  - Sections 3.4, 3.5

------------------------------------------------------------------------------

END OF DOCUMENT
