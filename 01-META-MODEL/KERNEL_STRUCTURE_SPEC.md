ENGINEERING KERNEL — KERNEL STRUCTURE SPECIFICATION
===================================================

Version: 1.0.0
Status: Approved
Date: 2026-06-26
Authority: MISSION-002
Source of Truth: 01-META-MODEL/
Classification: Kernel Core Document

------------------------------------------------------------------------------

TABLE OF CONTENTS
-----------------

1.  Document Purpose
2.  Directory Responsibilities
    2.1  00-CONSTITUTION
    2.2  01-META-MODEL
    2.3  02-GOVERNANCE
    2.4  03-STANDARDS
    2.5  04-PATTERNS
    2.6  05-EVIDENCE
    2.7  06-CONTRACTS
    2.8  07-WORKFLOW
    2.9  08-TEMPLATES
    2.10 09-TOOLS
    2.11 99-STATE
3.  Entity-to-Directory Mapping
4.  Naming Conventions
5.  Version Conventions
6.  Freeze Conventions
7.  File Organization Rules
8.  Validation Rules
9.  Normative References

------------------------------------------------------------------------------

1. DOCUMENT PURPOSE
-------------------

The Kernel Structure Specification defines the physical organization of the
Engineering Kernel repository. It maps RMM entities to their canonical storage
directories, establishes naming/version/freeze conventions, and provides rules
for file organization.

Every file in the repository must be locatable through this specification.
If a file's location cannot be justified by this spec, its placement is
non-compliant.

This document is derived directly from RMM property #15 (Source of Truth) and
the 11 directory structure entries defined at repository initialization.

------------------------------------------------------------------------------

2. DIRECTORY RESPONSIBILITIES
-----------------------------

2.1 00-CONSTITUTION — Supreme Governance
    RMM Source of Truth: 00-CONSTITUTION/
    Entities Assigned: CONSTITUTION, CHARTER, GOVERNANCE_BODY
    Purpose: Houses the supreme governance instrument and all bodies
             established by it. The Constitution is the root of all
             authority. No Kernel document may contradict it.
    Freeze Status: CONSTITUTION is Freezable=Yes; frozen by default.
    Permission: Human Modifiable=With Approval; AI Modifiable=No.

2.2 01-META-MODEL — Ontological Foundation
    RMM Source of Truth: 01-META-MODEL/
    Entities Assigned: REPOSITORY_META_MODEL, all Tier 1-20 entity
                      definitions, all matrices, all relationship graphs
    Purpose: Contains the complete ontology of the engineering universe.
             The RMM is the Source of Truth for what exists, how entities
             relate, and who may modify them.
    Freeze Status: RMM is Freezable=Yes; frozen at v1.1.
    Permission: Human Modifiable=With Approval; AI Modifiable=No.

2.3 02-GOVERNANCE — Authority Framework
    RMM Source of Truth: 02-GOVERNANCE/
    Entities Assigned: ROLE, ACTOR, SESSION, PERMISSION_MATRIX
    Purpose: Defines roles, actors, sessions, and the permissions that
             govern who can do what. Operationalizes the authority chain.
    Freeze Status: PERMISSION_MATRIX is Freezable=Yes.
    Permission: Role definitions Human Modifiable=With Approval.

2.4 03-STANDARDS — Lifecycle Rules
    RMM Source of Truth: 03-STANDARDS/
    Entities Assigned: LIFECYCLE, STATE, TRANSITION, APPROVAL, FREEZE
    Purpose: Defines lifecycle states, transitions between them, freeze
             mechanics, and the approval workflow required for changes.
    Freeze Status: LIFECYCLE and APPROVAL are Freezable=Yes.
    Permission: Standards Human Modifiable=With Approval.

2.5 04-PATTERNS — Reserved
    RMM Source of Truth: 04-PATTERNS/
    Entities Assigned: (none — reserved for future pattern definitions)
    Purpose: Reserved for design patterns, architectural patterns, and
             reusable structural templates that apply across products.
    Freeze Status: N/A (directory reserved, no entities assigned).
    Permission: N/A.

2.6 05-EVIDENCE — Process Artifacts
    RMM Source of Truth: 05-EVIDENCE/
    Entities Assigned: EVIDENCE, AUDIT_TRAIL, ARTIFACT, DOCUMENT
    Purpose: Defines evidence standards, audit trail structure, and the
             artifact framework. Process outputs are stored here.
    Freeze Status: EVIDENCE standards are Freezable=Yes.
    Permission: Evidence Human Modifiable=Yes; AI Modifiable=With Approval.

2.7 06-CONTRACTS — Interface Agreements
    RMM Source of Truth: 06-CONTRACTS/
    Entities Assigned: CONTRACT, INTERFACE, SERVICE_LEVEL
    Purpose: Defines contracts between entities, interface specifications,
             and service level definitions. Consumer-provider agreements.
    Freeze Status: CONTRACT is Freezable=Yes.
    Permission: Contracts Human Modifiable=With Approval.

2.8 07-WORKFLOW — Process Execution
    RMM Source of Truth: 07-WORKFLOW/
    Entities Assigned: WORKFLOW, PROCESS, TASK, ENGINEERING_WORK_ORDER,
                      ENGINEERING_CHANGE_ORDER
    Purpose: Defines workflows, processes, and the execution mechanics
             for engineering work orders and change orders.
    Freeze Status: WORKFLOW definitions Freezable=Yes.
    Permission: Workflows Human Modifiable=With Approval.

2.9 08-TEMPLATES — Reserved
    RMM Source of Truth: 08-TEMPLATES/
    Entities Assigned: (none — reserved for future template definitions)
    Purpose: Reserved for document templates, structural blueprints, and
             reusable formats for Kernel and product artifacts.
    Freeze Status: N/A (directory reserved, no entities assigned).
    Permission: N/A.

2.10 09-TOOLS — Reserved
    RMM Source of Truth: 09-TOOLS/
    Entities Assigned: (none — reserved for future tool configurations)
    Purpose: Reserved for tool configurations, validation scripts, and
             automation definitions that support Kernel operations.
    Freeze Status: N/A (directory reserved, no entities assigned).
    Permission: N/A.

2.11 99-STATE — Cross-Cutting Concerns
    RMM Source of Truth: 99-STATE/
    Entities Assigned: All cross-tier entities, global configuration,
                      shared utilities, system-wide invariants
    Purpose: Contains entities and definitions that span multiple tiers.
             Global state, cross-cutting patterns, and shared mechanisms.
    Freeze Status: Cross-cutting standards Freezable=Yes.
    Permission: Human Modifiable=With Approval.

------------------------------------------------------------------------------

3. ENTITY-TO-DIRECTORY MAPPING
------------------------------

The following table maps all 79 RMM entities to their canonical directories
based on RMM property #15 (Source of Truth):

Directory            Entity Count   Freezable Entities
-------------------  -------------  ----------------------------------------
00-CONSTITUTION/     3              CONSTITUTION, CHARTER, GOVERNANCE_BODY
01-META-MODEL/       20             REPOSITORY_META_MODEL, all entity defs
02-GOVERNANCE/       8              ROLE, ACTOR, SESSION, PERMISSION_MATRIX
03-STANDARDS/        10             LIFECYCLE, STATE, TRANSITION, APPROVAL
04-PATTERNS/         0              (reserved)
05-EVIDENCE/         12             EVIDENCE, AUDIT_TRAIL, ARTIFACT, DOCUMENT
06-CONTRACTS/        8              CONTRACT, INTERFACE, SERVICE_LEVEL
07-WORKFLOW/         10             WORKFLOW, PROCESS, TASK, EWO, ECO
08-TEMPLATES/        0              (reserved)
09-TOOLS/            0              (reserved)
99-STATE/            8              Cross-tier entities, global config

Module-Relative:     15             Product-specific entity extensions
Branded Storage:     15             Consumer namespace references

Total: 79 entities accounted for (64 directly assigned + 15 module-relative
       references that resolve to product-controlled storage).

------------------------------------------------------------------------------

4. NAMING CONVENTIONS
---------------------

4.1 Directory Names
    - Two-digit prefix (00-99)
    - Single-word uppercase descriptor
    - Format: NN-DESCRIPTOR/
    - Examples: 00-CONSTITUTION/, 01-META-MODEL/, 99-STATE/

4.2 File Names
    - UPPER_SNAKE_CASE for Kernel artifacts
    - Descriptive, self-documenting names
    - Format: DESCRIPTOR_TYPE.md
    - Examples: RMM_v1.1.md, KERNEL_SCOPE_DEFINITION.md

4.3 Entity Names
    - UPPER_SNAKE_CASE
    - Singular nouns
    - Self-describing without context
    - Examples: CONSTITUTION, GOVERNANCE_BODY, AUDIT_TRAIL

4.4 Version Identifiers
    - Semantic versioning: MAJOR.MINOR.PATCH
    - Pre-release tags not permitted for approved artifacts
    - Examples: v1.0.0, v1.1.0, v2.0.0

4.5 Status Labels
    - DRAFT, PROPOSED, APPROVED, ACTIVE, DEPRECATED, ARCHIVED
    - Single word, uppercase
    - No compound or qualified status values

------------------------------------------------------------------------------

5. VERSION CONVENTIONS
----------------------

5.1 Versionable Entities (RMM Property #10 = Yes)
    Count: 40 entities
    Behavior: Every change creates a new version. Version history is
              preserved. Rollback to any previous version is supported.
    Version Format: MAJOR.MINOR.PATCH
    Version Location: In document header and filename
    Examples: RMM_v1.1.md, KERNEL_SCOPE_DEFINITION_v1.0.0.md

5.2 Non-Versionable Entities (RMM Property #10 = No)
    Count: 39 entities
    Behavior: In-place updates only. No version history maintained.
              Changes overwrite previous content.
    Tracking: Change log entries document modifications
    Examples: Session logs, transient state files

5.3 Version Change Rules
    MAJOR: Breaking change to entity definition or contract
    MINOR: Non-breaking addition or clarification
    PATCH: Typo fix, formatting, non-substantive correction

------------------------------------------------------------------------------

6. FREEZE CONVENTIONS
---------------------

6.1 Freezable Entities (RMM Property #11 = Yes)
    Count: 28 entities
    Behavior: May be frozen to prevent modification. Requires APPROVAL
              entity to freeze and unfreeze.
    Freeze Default: Key foundational documents frozen upon approval.
    Unfreeze Process: Governance body approval → unfreeze → modify →
                      review → refreeze → new approval record.

6.2 Non-Freezable Entities (RMM Property #11 = No)
    Count: 51 entities
    Behavior: Always mutable. No freeze/unfreeze cycle.
    Examples: Session artifacts, work-in-progress documents,
              transient operational data.

6.3 Currently Frozen Artifacts
    - RMM v1.1 (01-META-MODEL/RMM_v1.1.md)
    - CONSTITUTION (00-CONSTITUTION/ — pending approval record)
    - PERMISSION_MATRIX (02-GOVERNANCE/ — pending initial creation)

6.4 Freeze Metadata
    A frozen artifact must include in its header:
        - Freeze date
    Freeze status must be recorded in 99-STATE/ or equivalent.

------------------------------------------------------------------------------

7. FILE ORGANIZATION RULES
--------------------------

7.1 One Concept Per File
    Each file contains one logical artifact. No monolithic files combining
    multiple independent entities.

7.2 Header Metadata
    Every file must begin with a header containing:
        - Document title
        - Version
        - Status
        - Date
        - Authority (mission/task/ECO that created it)
        - Source of Truth (directory path)
        - Classification (Kernel Core / Derived / Procedural)

7.3 Table of Contents
    Documents exceeding 100 lines must include a table of contents.

7.4 Cross-References
    References to other Kernel documents must use relative paths from
    repository root. Example: "See 01-META-MODEL/RMM_v1.1.md, Section 4.2"

7.5 No Orphaned Files
    Every file must be referenced by at least one of:
        - RMM entity Source of Truth
        - Another Kernel document's normative reference section
        - A directory README index

7.6 README Requirement
    Every directory must contain a README.md that indexes its contents.

------------------------------------------------------------------------------

8. VALIDATION RULES
-------------------

8.1 Structural Validation
    - Every file in 00-07, 99 must correspond to an RMM entity
    - Files in reserved directories (04, 08, 09) must be explicitly
      allowed by a governance decision
    - No file may exist in a directory without an associated entity

8.2 Naming Validation
    - All Kernel artifacts must use UPPER_SNAKE_CASE
    - No technology names in filenames
    - No product names in filenames
    - Version suffixes required for versionable entities

8.3 Metadata Validation
    - All 7 header fields must be present
    - Status must be a valid lifecycle state
    - Source of Truth must match actual directory path
    - Date must not be in the future

8.4 Cross-Reference Validation
    - All internal references must resolve to existing files
    - No dangling references to moved or deleted documents
    - External references must be in normative references section only

------------------------------------------------------------------------------

9. NORMATIVE REFERENCES
-----------------------

Reference                        Location
-------------------------------  --------------------------------------------
Repository Meta Model v1.1       01-META-MODEL/RMM_v1.1.md
Kernel Scope Definition          01-META-MODEL/KERNEL_SCOPE_DEFINITION.md
RMM Validation Report v2         01-META-MODEL/RMM_VALIDATION_REPORT_v2.md
Constitution TOC                 00-CONSTITUTION/README.md

------------------------------------------------------------------------------

END OF DOCUMENT
