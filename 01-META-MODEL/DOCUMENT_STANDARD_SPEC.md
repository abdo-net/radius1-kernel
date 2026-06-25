ENGINEERING KERNEL — DOCUMENT STANDARD SPECIFICATION
====================================================

Version: 1.0.0
Status: Approved
Date: 2026-06-26
Authority: MISSION-003
Source of Truth: 01-META-MODEL/
Classification: CANONICAL

------------------------------------------------------------------------------

1. SCOPE
--------

This specification defines the universal structure that every Engineering
Kernel document SHALL follow. It applies to all artifacts stored within the
Kernel repository regardless of directory, tier, or classification.

This specification is derived from frozen RMM v1.1. No element exists in
this spec unless it is defined in the RMM.

------------------------------------------------------------------------------

2. NORMATIVE REFERENCES
-----------------------

Reference                        RMM Basis
-------------------------------  --------------------------------------------
Repository Meta Model v1.1       01-META-MODEL/RMM_v1.1.md
  - Entity: ARTIFACT             Properties 1-15, Matrix 2 row 44
  - Entity: DOCUMENT             Properties 1-15, Matrix 2 row 45
  - Entity: EVIDENCE             Properties 1-15, Matrix 2 row 41
  - Entity: AUDIT_TRAIL          Properties 1-15, Matrix 2 row (derived)
  - Entity: APPROVAL             Properties 1-15, Matrix 2 row 50
  - Entity: SIGNATURE            Properties 1-15, Matrix 2 row 54
  - Entity: LIFECYCLE            Properties 1-15, Matrix 2 row 65
  - Entity: STATE                Properties 1-15, Matrix 2 row 66
  - Entity: CONSTITUTION         Properties 1-15, Matrix 2 row 24
  - Matrix 2: Lifecycle Matrix   79 rows, 3 columns
  - Matrix 3: Stability          79 rows, 4 columns
  - Matrix 4: Versionability     79 rows, 4 columns
  - Matrix 5: Freeze             79 rows, 5 columns
  - Matrix 6: Source-of-Truth    79 rows, 5 columns
  - Matrix 7: Permissions        79 rows, 6 columns
Kernel Structure Spec            01-META-MODEL/KERNEL_STRUCTURE_SPEC.md

------------------------------------------------------------------------------

3. DOCUMENT SECTIONS
--------------------

Every Kernel document SHALL contain exactly the following ten sections in
the order specified. No additional sections are permitted at the top level.

    3.1  Document Header
    3.2  Metadata Block
    3.3  Classification
    3.4  Status
    3.5  Version
    3.6  Authority
    3.7  Dependencies
    3.8  Revision History
    3.9  Acceptance Block
    3.10 Canonical References

Each section is defined in the subsections below.

------------------------------------------------------------------------------

3.1 DOCUMENT HEADER
-------------------

RMM Basis: ENTITY.DOCUMENT properties 1-3; ENTITY.ARTIFACT properties 1-3.

Every document SHALL begin with a header block containing exactly these
seven fields in this order:

    Field             Required  Source
    ----------------  --------  --------------------------------------------
    Document Title    Yes       RMM #2 (Purpose) — "To carry structured..."
    Separator         Yes       Visual delimiter (80 '=' characters)
    Version           Yes       RMM #10 (Versionable) — see Section 3.5
    Status            Yes       RMM #5 (Lifecycle) — see Section 3.4
    Date              Yes       Temporal marker of last state change
    Authority         Yes       RMM #4 (Owner) — see Section 3.6
    Source of Truth   Yes       RMM #15 — canonical directory path
    Classification    Yes       See Section 3.3

Format: Each field on its own line. Key-value pairs separated by ": ".
The separator line (80 '=') appears after the title and before the first
field, and again after the last field before the table of contents.

Example:

    ENGINEERING KERNEL — DOCUMENT STANDARD SPECIFICATION
    ====================================================

    Version: 1.0.0
    Status: Approved
    Date: 2026-06-26
    Authority: MISSION-003
    Source of Truth: 01-META-MODEL/
    Classification: CANONICAL

    ------------------------------------------------------------------------------

------------------------------------------------------------------------------

3.2 METADATA BLOCK
------------------

RMM Basis: ENTITY.ARTIFACT properties 1-15; ENTITY.DOCUMENT properties 1-15.

The Metadata Block is a machine-parseable representation of the document's
RMM-derived attributes. It appears immediately after the Document Header
and before the Table of Contents.

Required fields:

    Field             RMM Source                Format
    ----------------  ------------------------  ------------------------------
    Entity Type       Property #1 (Name)        UPPER_SNAKE_CASE entity name
    Entity Purpose    Property #2 (Purpose)     Single sentence
    Entity Owner      Property #4 (Owner)       Canonical owner entity
    Lifecycle         Property #5 (Lifecycle)   State1 → State2 → ...
    Cardinality       Property #8 (Cardinality) 1:1, 1:N, N:M, or N
    Stability         Property #9 (Stability)   Static, Slow, Moderate, Fast
    Versionable       Property #10              Yes / No
    Freezable         Property #11              Yes / No
    AI Creatable      Property #12              Yes / No / With Approval
    AI Modifiable     Property #13              Yes / No / With Approval
    Human Modifiable  Property #14              Yes / No / With Approval
    Source of Truth   Property #15              Directory path

The Metadata Block is enclosed in a delimited region for automated
extraction. Format: Three backticks (```) above and below the block.

Example:

    ```metadata
    Entity Type: DOCUMENT
    Entity Purpose: To carry structured human-readable and machine-processable
                    information in a coherent, navigable form.
    Entity Owner: Module
    Lifecycle: Draft → Review → Approved → Published → Superseded → Archived
    Cardinality: 1:N
    Stability: Moderate
    Versionable: Yes
    Freezable: Yes
    AI Creatable: Yes
    AI Modifiable: With Approval
    Human Modifiable: Yes
    Source of Truth: Artifact Repository
    ```

------------------------------------------------------------------------------

3.3 CLASSIFICATION
------------------

RMM Basis: ENTITY.LIFECYCLE property #5; ENTITY.STATE property #2.

Every document SHALL have exactly one classification value from the
following enumerated set. No other values are permitted.

    Value          Definition                          Source
    -------------  ----------------------------------  ------------------------
    CANONICAL      Supreme authority; frozen state     CONSTITUTION, CHARTER
    NORMATIVE      Mandatory standards; approved       STANDARD, SPECIFICATION
    DERIVED        Computed from canonical sources     ASSESSMENT, REPORT
    PROCEDURAL     Execution instructions              WORKFLOW, PROCESS, TASK
    INFORMATIONAL  Reference material                  GUIDELINE, RECORD
    DRAFT          Work in progress; pre-approval      STATE: Draft

Classification determines:
    - Which lifecycle states are valid (Section 3.4)
    - Which modification permissions apply (Matrix 7)
    - Whether the document is freezable (Matrix 5)
    - Whether the document requires an Acceptance Block (Section 3.9)

Rules:
    - CANONICAL documents: Human Modifiable = With Approval (RMM #14)
    - NORMATIVE documents: AI Modifiable = With Approval (RMM #13)
    - DRAFT documents: AI Creatable = Yes, AI Modifiable = Yes (RMM #12, #13)
    - CANONICAL and NORMATIVE documents require an Acceptance Block
    - DRAFT and INFORMATIONAL documents do not require an Acceptance Block

------------------------------------------------------------------------------

3.4 STATUS
----------

RMM Basis: ENTITY.LIFECYCLE property #5; ENTITY.STATE properties 1-6;
           Matrix 2 (Lifecycle Matrix) rows 44, 45.

Every document SHALL have exactly one status value. The valid status set
is determined by the document's entity type lifecycle as defined in RMM
Matrix 2.

For DOCUMENT entities (Matrix 2, row 45):

    Status        Definition                                Next Valid States
    ------------  ----------------------------------------  ------------------
    Draft         Initial creation; incomplete              Review, Archived
    Review        Under peer or governance review           Approved, Draft
    Approved      Review completed satisfactorily           Published, Draft
    Published     Approved and distributed                  Superseded, Archived
    Superseded    Replaced by newer version                 Archived
    Archived      Retained for reference; no longer active  (terminal)

For ARTIFACT entities (Matrix 2, row 44):

    Status        Definition                                Next Valid States
    ------------  ----------------------------------------  ------------------
    Defined       Concept established; not yet instantiated Created, Destroyed
    Created       Physical instance exists                  Active, Destroyed
    Active        In use; may be referenced                 Archived, Destroyed
    Archived      Preserved for historical reference        Destroyed
    Destroyed     Permanently removed per retention policy  (terminal)

Rules:
    - A document SHALL NOT skip states. Transitions must follow the
      RMM-defined paths.
    - A frozen document (Matrix 5, Freezable=Yes) must have Status
      Approved, Published, or terminal state.
    - Status changes require an Authority entry in the Revision History
      (Section 3.8).

------------------------------------------------------------------------------

3.5 VERSION
-----------

RMM Basis: ENTITY.DOCUMENT property #10 (Versionable=Yes); ENTITY.ARTIFACT
           property #10 (Versionable=Yes); Matrix 4 (Versionability Matrix).

Every Kernel document SHALL carry a version identifier. Versioning rules
are determined by the RMM Versionable property and the entity lifecycle.

Format: Semantic versioning per KERNEL_STRUCTURE_SPEC.md Section 5.
    MAJOR.MINOR.PATCH

    Component    When to Increment
    -----------  -----------------------------------------------------------
    MAJOR        Breaking change to entity definition, contract, or schema
    MINOR        Non-breaking addition, clarification, or expansion
    PATCH        Typographical correction, formatting, non-substantive fix

Rules:
    - Versionable=Yes entities (Matrix 4): Every change creates a new
      version. Version history is preserved.
    - Versionable=No entities (Matrix 4: EVIDENCE, SIGNATURE, PRIMITIVE,
      INVARIANT): No version identifier required. Changes overwrite.
    - The version SHALL appear in the Document Header (Section 3.1).
    - The version SHALL appear in the filename for versionable entities
      per KERNEL_STRUCTURE_SPEC.md Section 4.2.
    - A version change SHALL trigger a Revision History entry
      (Section 3.8).

------------------------------------------------------------------------------

3.6 AUTHORITY
-------------

RMM Basis: ENTITY.DOCUMENT property #4 (Owner); ENTITY.APPROVAL properties
           1-6; ENTITY.ROLE properties 1-6; authority chain:
           CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR.

The Authority field identifies the governing entity responsible for the
document's content, accuracy, and lifecycle management.

Format: One of the following canonical values derived from RMM #4:

    Value              RMM Owner Source             Meaning
    -----------------  ---------------------------  ------------------------
    Constitution       Property #4 = Constitution   Supreme authority
    Charter            Property #4 = Charter        Chartered body
    GovernanceBody     Property #4 = GovernanceBody  Elected or appointed body
    Role               Property #4 = Role             Named responsibility set
    Actor              Property #4 = Actor            Individual actor
    Session            Property #4 = Session          Bounded work period
    Task               Property #4 = Task             Specific work unit
    Process            Property #4 = Process          Defined procedure
    Module             Property #4 = Module           Development unit

    Additionally, mission and work order identifiers are valid:
    - MISSION-NNN  (per WORKFLOW entity)
    - EWO-NNN      (per ENGINEERING_WORK_ORDER entity)
    - ECO-NNN      (per ENGINEERING_CHANGE_ORDER entity)
    - TASK-NNNN    (per TASK entity)

Rules:
    - The Authority SHALL match the RMM Owner property for the document's
      entity type.
    - Authority changes require an Approval entity (RMM Matrix 2, row 50).
    - The authority chain must be traceable: Authority → Role →
      GovernanceBody → Charter → Constitution.

------------------------------------------------------------------------------

3.7 DEPENDENCIES
----------------

RMM Basis: ENTITY.DOCUMENT property #6 (Allowed Relationships);
           ENTITY.DOCUMENT property #7 (Forbidden Relationships);
           Matrix 9 (Dependency Matrix).

The Dependencies section lists all documents, entities, and external
references upon which this document depends.

Required subsections:

    3.7.1 Allowed Dependencies
          Documents that this document explicitly references, requires,
          or builds upon. Format: relative path from repository root.

    3.7.2 Forbidden Dependencies
          Documents, technologies, or entities that this document
          explicitly must NOT reference per RMM property #7.

    3.7.3 Dependency Type
          Classification of each dependency per Matrix 9:
              - Normative: Required for correctness; document is invalid
                without this dependency.
              - Informative: Helpful context; document is valid without it.
              - Structural: Defines document structure or schema.

Format:

    Dependencies
    ------------

    3.7.1 Allowed Dependencies
    | Reference                               | Type        | Required |
    |-----------------------------------------|-------------|----------|
    | 01-META-MODEL/RMM_v1.1.md              | Normative   | Yes      |
    | 01-META-MODEL/KERNEL_STRUCTURE_SPEC.md   | Structural  | Yes      |

    3.7.2 Forbidden Dependencies
    | Reference           | Rationale                                    |
    |---------------------|----------------------------------------------|
    | Product-specific    | RMM #7: May not depend on external product    |
    | Technology-specific | RMM #7: Technology independence required      |

Rules:
    - All internal references SHALL use relative paths.
    - Forbidden Dependencies SHALL be explicit — if not listed, the
      assumption is no restriction.
    - Technology names SHALL NOT appear in Allowed Dependencies except
      within Forbidden Dependencies as examples of what is excluded.

------------------------------------------------------------------------------

3.8 REVISION HISTORY
--------------------

RMM Basis: ENTITY.DOCUMENT property #10 (Versionable=Yes);
           ENTITY.AUDIT_TRAIL properties 1-6;
           ENTITY.APPROVAL properties 1-6.

The Revision History is a chronological record of all changes to the
document. It is the human-readable form of the audit trail.

Required columns:

    Column        Source                          Format
    ------------  ------------------------------  ------------------------
    Version       RMM #10                         MAJOR.MINOR.PATCH
    Date          Temporal marker                 YYYY-MM-DD
    Author        RMM #4 (Owner)                  Actor identifier
    Change Type   RMM #5 (Lifecycle transition)   Added/Modified/Removed/
                                                  Corrected/Refactored
    Authority     RMM #4                          MISSION/EWO/ECO/Task
    Description   RMM #3 (Responsibility)         Brief change summary

Format:

    REVISION HISTORY
    ----------------

    | Version | Date       | Author      | Change Type | Authority  | Description                    |
    |---------|------------|-------------|-------------|------------|--------------------------------|
    | 1.0.0   | 2026-06-26 | Governance  | Added       | MISSION-003| Initial document standard spec |

Rules:
    - Every version change SHALL have a corresponding Revision History entry.
    - The Date SHALL NOT be in the future.
    - The Author SHALL be a valid Actor (RMM #35).
    - Frozen documents: Revision History is append-only.
    - Change Type SHALL be one of: Added, Modified, Removed, Corrected,
      Refactored, Superseded.

------------------------------------------------------------------------------

3.9 ACCEPTANCE BLOCK
--------------------

RMM Basis: ENTITY.APPROVAL properties 1-6 (Matrix 2, row 50);
           ENTITY.SIGNATURE properties 1-6 (Matrix 2, row 54);
           ENTITY.BASELINE properties 1-6 (Matrix 2, row 55).

The Acceptance Block records formal authorization that the document has
been reviewed and accepted. It is required for CANONICAL and NORMATIVE
classifications (Section 3.3). It is optional for DERIVED, PROCEDURAL,
and INFORMATIONAL. It is prohibited for DRAFT.

Required fields:

    Field         RMM Source                    Format
    ------------  ----------------------------  ------------------------
    Status        APPROVAL property #5          Granted / Denied /
                                                Conditional / Withdrawn
    Approver      APPROVAL property #4 (Owner)  Role name or Actor ID
    Date          Temporal marker               YYYY-MM-DD
    Method        SIGNATURE property #2         Signature type
    Conditions    APPROVAL property #6          Optional constraints

Format:

    ACCEPTANCE
    ----------

    | Status  | Approver         | Date       | Method    | Conditions |
    |---------|------------------|------------|-----------|------------|
    | Granted | GovernanceBody   | 2026-06-26 | Signature | None       |

Rules:
    - Status = Granted: Document is authorized for its declared Status.
    - Status = Denied: Document must return to Draft state.
    - Status = Conditional: Document is approved with listed Conditions.
    - Status = Withdrawn: Previous approval revoked; document Status
      reverts to Draft.
    - Method = Signature: Non-repudiable mark per RMM SIGNATURE entity.
    - Method = Record: Logged approval without cryptographic signature.
    - Method = Automated: System-generated approval per defined rule.
    - Once Status reaches Granted, the Acceptance Block is frozen.
      Changes require a new Approval cycle.

------------------------------------------------------------------------------

3.10 CANONICAL REFERENCES
-------------------------

RMM Basis: ENTITY.DOCUMENT property #15 (Source of Truth);
           Matrix 6 (Source-of-Truth Matrix, 79 rows, 5 columns).

The Canonical References section lists all documents that are the
authoritative sources for definitions, rules, or constraints referenced
within this document.

Format:

    CANONICAL REFERENCES
    --------------------

    | Reference                        | Location                     |
    |----------------------------------|------------------------------|
    | Repository Meta Model v1.1       | 01-META-MODEL/RMM_v1.1.md   |
    | Kernel Structure Spec            | 01-META-MODEL/...           |

Rules:
    - Every reference SHALL resolve to a file at the listed location.
    - References SHALL use relative paths from repository root.
    - References to RMM entities SHALL include the entity name and
      the Matrix rows/columns that support the reference.
    - References to external sources (non-Kernel) SHALL be marked
      [EXTERNAL] and are informational only.
    - Canonical References are normative — the referenced document's
      definitions govern this document.

------------------------------------------------------------------------------

4. COMPLIANCE VERIFICATION
--------------------------

A document is compliant with this specification if and only if:

    [ ] All 10 sections (3.1-3.10) are present in order
    [ ] Document Header contains all 7 required fields
    [ ] Metadata Block contains all 12 required fields
    [ ] Classification is a valid enumerated value (Section 3.3)
    [ ] Status is valid per the entity's lifecycle (Matrix 2)
    [ ] Version follows semantic versioning format (Section 3.5)
    [ ] Authority is a canonical value from RMM #4 (Section 3.6)
    [ ] Dependencies lists all Allowed and Forbidden references
    [ ] Revision History has an entry for the current version
    [ ] Acceptance Block is present if required by Classification
    [ ] Canonical References resolves all listed paths
    [ ] No technology names appear in normative content
    [ ] No product-specific references appear in normative content

A non-compliant document SHALL NOT be Approved or Published.

------------------------------------------------------------------------------

5. ENTITY MAPPING
-----------------

This specification maps to the following RMM entities:

    Spec Section    RMM Entity    RMM Properties    Matrix Rows
    --------------  ------------  ----------------  -------------
    3.1 Header      DOCUMENT      1, 2, 3           45
    3.2 Metadata    ARTIFACT      1-15              44
    3.3 Classify    LIFECYCLE     5                 65
    3.4 Status      STATE         1, 5, 6           66
    3.5 Version     DOCUMENT      10                45
    3.6 Authority   APPROVAL      4, 5, 6           50
    3.7 Depends     DOCUMENT      6, 7              45
    3.8 Revision    AUDIT_TRAIL   1-6               (derived)
    3.9 Acceptance  SIGNATURE     1-6               54
    3.10 Canonical  DOCUMENT      15                45

------------------------------------------------------------------------------

END OF DOCUMENT
