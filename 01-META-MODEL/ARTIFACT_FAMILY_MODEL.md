ENGINEERING KERNEL — ARTIFACT FAMILY MODEL
==========================================

Version: 1.0.0
Status: Approved
Date: 2026-06-26
Authority: MISSION-005
Source of Truth: Artifact Repository
Stability: Slow

------------------------------------------------------------------------------

TABLE OF CONTENTS
-----------------

1. Root Artifact Family
2. Document Family
3. Evidence Family
4. Decision Family
5. Traceability Family
6. Authorization Family
7. Standards Family
8. Measurement Family
9. Oversight Family
10. Exception Family
11. Governance Mechanics Family
12. Accountability Family
13. Cross-Cutting Family

------------------------------------------------------------------------------

NORMATIVE REFERENCES
--------------------

| Reference                        | Location                                | RMM Basis
|----------------------------------|-----------------------------------------|-------------------------------
| Repository Meta Model v1.1       | 01-META-MODEL/RMM_v1.1.md              | All 79 entities, 10 matrices
| Kernel Scope Definition          | 01-META-MODEL/KERNEL_SCOPE_DEFINITION.md| Artifact definition
| Kernel Structure Spec            | 01-META-MODEL/KERNEL_STRUCTURE_SPEC.md  | Naming/version/freeze
| Document Standard Spec           | 01-META-MODEL/DOCUMENT_STANDARD_SPEC.md | Classification enum
| Artifact Meta Model              | 01-META-MODEL/ARTIFACT_META_MODEL.md    | Artifact invariants

------------------------------------------------------------------------------

CLASSIFICATION ENUMERATION
--------------------------

Per DOCUMENT_STANDARD_SPEC Section 3.3 (derived from RMM LIFECYCLE and STATE
entities), the following classification values apply to Artifact Families:

    CANONICAL — Supreme authority; frozen state
    NORMATIVE — Mandatory standards; approved
    DERIVED   — Computed from canonical sources
    DRAFT     — Work in progress; pre-approval

PROCEDURAL and INFORMATIONAL are RMM-defined classification values per
DOCUMENT_STANDARD_SPEC Section 3.3. The RMM defines no mapping between
classification values and entity types. Whether a specific classification
value applies to a specific Artifact Family is: UNSUPPORTED.

------------------------------------------------------------------------------

1. ROOT ARTIFACT FAMILY
-----------------------

RMM Basis: TIER 11; ENTITY.ARTIFACT properties 1-15; Matrix 2 row 44;
           Matrix 3 row 44; Matrix 4 row 44; Matrix 5 row 44;
           Matrix 7 row 44; Matrix 8 row 44; Matrix 9 row 44.

1.1 Name
    ARTIFACT

1.2 Purpose
    Per RMM property #2: To serve as the root ontological category for
    any item produced, consumed, transformed, or referenced within the
    kernel.

1.3 Classification
    CANONICAL — Root ontological category; changes propagate to all
    subtypes per Matrix 3 (Stability: Slow).

1.4 Authority
    Per RMM property #4: Owner is Process.
    Per Matrix 1 row 44: Constitution column carries ● marker.
    AI Creatable: Yes. AI Modifiable: With Approval. Human Modifiable: Yes.

1.5 Lifecycle
    Per Matrix 2 row 44: Defined → Created → Active → Archived → Destroyed

1.6 Relationships
    Per RMM property #6: Consumed by Process; produced by Process;
    composed of other Artifacts; traced via TraceabilityLink;
    versioned as Revision; baselined via Baseline.
    Per RMM property #7: May NOT own Module; may NOT modify Governance
    Rule; may NOT be directly self-referential.
    Per Matrix 8: Cardinality N:M.

1.7 Validation Rules
    V-AF-01  Entity Name is UPPER_SNAKE_CASE                 RMM #1
    V-AF-02  Purpose is non-empty                            RMM #2
    V-AF-03  Responsibility is non-empty                     RMM #3
    V-AF-04  Owner is Process                               RMM #4
    V-AF-05  Lifecycle is 5-state sequence                   RMM #5, M2R44
    V-AF-06  Cardinality is N:M                             RMM #8, M8R44
    V-AF-07  Stability is Slow                              RMM #9, M3R44
    V-AF-08  Versionable is Yes                             RMM #10, M4R44
    V-AF-09  Freezable is Yes                               RMM #11, M5R44
    V-AF-10  AI Creatable is Yes                            RMM #12, M7R44
    V-AF-11  AI Modifiable is With Approval                 RMM #13, M7R44
    V-AF-12  Human Modifiable is Yes                        RMM #14, M7R44

1.8 Constraints
    C-AF-01  Shall not own Module                           RMM #7
    C-AF-02  Shall not modify Governance Rule               RMM #7
    C-AF-03  Shall not be directly self-referential         RMM #7

------------------------------------------------------------------------------

2. DOCUMENT FAMILY
------------------

RMM Basis: TIER 11; ENTITIES: DOCUMENT, SPECIFICATION, RECORD, LOG, REPORT;
           Matrix 2 rows 45-49; Matrix 3 rows 45,46,47,48,49;
           Matrix 5 rows 45-49; Matrix 7 rows 45-49; Matrix 8 rows 45-49.

2.1 Family Definition
    Per RMM Matrix 9 row 44: ARTIFACT is Required By: Document,
    Specification, Record, Baseline, Snapshot. Per RMM Matrix 9 row 45:
    DOCUMENT Depends On: Module, Artifact. The Document Family comprises
    all artifact types in TIER 11.

2.2 Members

    Name           Purpose (RMM #2)                                     RMM Row
    -------------  ---------------------------------------------------  ---------
    DOCUMENT       Carry structured human/machine info                  M2R45
    SPECIFICATION  Prescribe in precise terms what shall be             M2R46
    RECORD         Capture fact, event, observation at point in time    M2R47
    LOG            Maintain chronological append-only sequence          M2R48
    REPORT         Communicate findings, analysis, status               M2R49

2.3 Classification
    NORMATIVE — All members are produced artifacts subject to review
    and approval per their lifecycles.

    DOCUMENT:       NORMATIVE (Draft→Review→Approved→Published)
    SPECIFICATION:  NORMATIVE (Proposed→Drafted→Reviewed→Approved→Baseline)
    RECORD:         INFORMATIONAL (Created→Validated→Committed→Retained)
    LOG:            NORMATIVE (Opened→Appending→Closed→Archived)
    REPORT:         DERIVED   (Commissioned→Drafted→Reviewed→Approved)

2.4 Authority
    Per RMM property #4 and Matrix 7:

    Member         Owner       AI-C    AI-M    H-M     Source
    -------------  ----------  ------  ------  ------  ----------
    DOCUMENT       Module      Yes     W/Appr  Yes     RMM #4,M7R45
    SPECIFICATION  GovernanceBody W/Appr  No      W/Appr  RMM #4,M7R46
    RECORD         Process     Yes     No      No      RMM #4,M7R47
    LOG            Kernel      Yes     No      No      RMM #4,M7R48
    REPORT         Process     Yes     W/Appr  Yes     RMM #4,M7R49

2.5 Lifecycle
    Per Matrix 2:

    DOCUMENT:       Draft → Review → Approved → Published → Superseded → Archived
    SPECIFICATION:  Proposed → Drafted → Reviewed → Approved → Baseline →
                    Amendment → Superseded
    RECORD:         Created → Validated → Committed → Retained → Expired → Destroyed
    LOG:            Opened → Appending → Closed → Archived → Expired
    REPORT:         Commissioned → Drafted → Reviewed → Approved → Published →
                    Superseded

2.6 Relationships
    Per Matrix 9:

    DOCUMENT:       Depends On: Module, Artifact. Required By: Baseline,
                    Review, Approval.
    SPECIFICATION:  Depends On: GovernanceBody, Standard. Required By: Module,
                    Component, Plan, Assessment.
    RECORD:         Depends On: Process. Required By: Log, AuditTrail, Baseline.
    LOG:            Depends On: Kernel, Record. Required By: AuditTrail,
                    Report, Audit.
    REPORT:         Depends On: Evidence, Finding, Measurement. Required By:
                    Audit, Review, DecisionRecord.

2.7 Validation Rules
    V-DF-01  All members have UPPER_SNAKE_CASE names             RMM #1
    V-DF-02  All members have defined lifecycles                  M2R45-49
    V-DF-03  All members are Freezable=Yes except where noted     M5R45-49
    V-DF-04  DOCUMENT Owner is Module                             RMM #4,M1R45
    V-DF-05  SPECIFICATION AI Modifiable is No                    M7R46
    V-DF-06  RECORD Human Modifiable is No                        M7R47
    V-DF-07  LOG Human Modifiable is No                           M7R48

2.8 Constraints
    C-DF-01  DOCUMENT may not execute Process                     RMM #7
    C-DF-02  DOCUMENT may not be self-approving                   RMM #7
    C-DF-03  DOCUMENT may not be both Draft and Published         RMM #7
    C-DF-04  SPECIFICATION may not be modified after baseline
             without formal amendment                            RMM #7

------------------------------------------------------------------------------

3. EVIDENCE FAMILY
------------------

RMM Basis: TIER 10; ENTITIES: EVIDENCE, FINDING, CONCLUSION;
           Matrix 2 rows 41-43; Matrix 3 rows 41-43;
           Matrix 5 rows 41-43; Matrix 7 rows 41-43; Matrix 8 rows 41-43.

3.1 Family Definition
    Per RMM Matrix 9 row 41: EVIDENCE is Required By: Decision,
    DecisionRecord, Assessment, Audit. Per RMM Matrix 9 row 42: FINDING
    is Required By: Conclusion, Report, DecisionRecord. Per Matrix 9
    row 43: CONCLUSION is Required By: DecisionRecord, Report. The
    Evidence Family captures the evidentiary chain from raw evidence
    through findings to conclusions.

3.2 Members

    Name       Purpose (RMM #2)                                     RMM Row
    ---------  ---------------------------------------------------  ---------
    EVIDENCE   Provide factual support for claims                   M2R41
    FINDING    Document discovered facts, observations, results     M2R42
    CONCLUSION Synthesize findings, evidence, reasoning into judgment M2R43

3.3 Classification
    DERIVED — Evidence is gathered and validated; Findings are
    documented from evidence; Conclusions are synthesized from findings.

    EVIDENCE:   DERIVED (Gathered → Validated → Linked → Referenced)
    FINDING:    DERIVED (Observed → Documented → Reviewed → Validated)
    CONCLUSION: DERIVED (Drafted → Supported → Reviewed → Approved)

3.4 Authority
    Per RMM property #4 and Matrix 7:

    Member      Owner       AI-C    AI-M    H-M     Source
    ----------  ----------  ------  ------  ------  ----------
    EVIDENCE    Process     Yes     No      No      RMM #4,M7R41
    FINDING     Process     Yes     W/Appr  Yes     RMM #4,M7R42
    CONCLUSION  GovernanceBody W/Appr  No      W/Appr  RMM #4,M7R43

3.5 Lifecycle
    Per Matrix 2:

    EVIDENCE:   Gathered → Validated → Linked → Referenced → Challenged →
                Reaffirmed/Withdrawn → Archived
    FINDING:    Observed → Documented → Reviewed → Validated → Published →
                Challenged → Reaffirmed/Corrected → Archived
    CONCLUSION: Drafted → Supported by Findings → Reviewed → Approved →
                Published → Challenged → Reaffirmed/Corrected → Archived

3.6 Relationships
    Per Matrix 9:

    EVIDENCE:   Depends On: Process, Finding. Required By: Decision,
                DecisionRecord, Assessment, Audit.
    FINDING:    Depends On: Evidence, Assessment, Audit. Required By:
                Conclusion, Report, DecisionRecord.
    CONCLUSION: Depends On: Finding, Evidence. Required By:
                DecisionRecord, Report.

3.7 Validation Rules
    V-EF-01  EVIDENCE Human Modifiable is No                      M7R41
    V-EF-02  EVIDENCE AI Modifiable is No                         M7R41
    V-EF-03  EVIDENCE Stability: Static after Validation          M3R41
    V-EF-04  FINDING Stability: Moderate                          M3R42
    V-EF-05  CONCLUSION Stability: Slow                          M3R43

3.8 Constraints
    C-EF-01  EVIDENCE may not be fabricated                       RMM #7
    C-EF-02  UNSUPPORTED (RMM property #7 for EVIDENCE does not mention contradictions)

------------------------------------------------------------------------------

4. DECISION FAMILY
------------------

RMM Basis: TIER 10; ENTITIES: DECISION, DECISION_RECORD;
           Matrix 2 rows 39-40; Matrix 3 rows 39-40;
           Matrix 5 rows 39-40; Matrix 7 rows 39-40; Matrix 8 rows 39-40.

4.1 Family Definition
    Per RMM Matrix 9 row 39: DECISION is Required By: DecisionRecord,
    Plan. Per Matrix 9 row 40: DECISION_RECORD is Required By: Plan,
    Baseline, Audit. The Decision Family captures decision-making and
    its formal record.

4.2 Members

    Name            Purpose (RMM #2)                                  RMM Row
    --------------  ------------------------------------------------  ---------
    DECISION        Represent a choice among alternatives              M2R39
    DECISION_RECORD Capture significant decision with context          M2R40

4.3 Classification
    CANONICAL — Decisions commit the organization; Decision Records
    are permanent governance artifacts.

4.4 Authority
    Per RMM property #4 and Matrix 7:

    Member          Owner       AI-C      AI-M      H-M       Source
    --------------  ----------  --------  --------  --------  ----------
    DECISION        Actor       W/Appr    W/Appr    Yes       RMM #4,M7R39
    DECISION_RECORD GovernanceBody W/Appr    W/Appr    W/Appr    RMM #4,M7R40

4.5 Lifecycle
    Per Matrix 2:

    DECISION:        Identified → Proposed → Deliberated → Made → Recorded →
                     Implemented → Reviewed → Retired
    DECISION_RECORD: Proposed → Options Identified → Evaluated → Decided →
                     Recorded → Communicated → Archived

4.6 Relationships
    Per Matrix 9:

    DECISION:        Depends On: Actor, Context, Evidence. Required By:
                     DecisionRecord, Plan.
    DECISION_RECORD: Depends On: Decision, GovernanceBody, Evidence.
                     Required By: Plan, Baseline, Audit.

4.7 Validation Rules
    V-DNF-01  DECISION Stability: Slow                            M3R39
    V-DNF-02  DECISION_RECORD Stability: Slow                     M3R40
    V-DNF-03  DECISION_RECORD Freezable: Yes                      M5R40

4.8 Constraints
    C-DNF-01  DECISION may not be reversible without process       RMM #7
    C-DNF-02  UNSUPPORTED (RMM property #7 for DECISION_RECORD does not mention destruction)

------------------------------------------------------------------------------

5. TRACEABILITY FAMILY
----------------------

RMM Basis: TIER 13; ENTITIES: BASELINE, SNAPSHOT, CHECKPOINT,
           TRACEABILITY_LINK; Matrix 2 rows 55-58; Matrix 3 rows 55-58;
           Matrix 5 rows 55-58; Matrix 7 rows 55-58; Matrix 8 rows 55-58.

5.1 Family Definition
    Per RMM Matrix 9 row 55: BASELINE Depends On: Artifact, Approval,
    Snapshot. Per Matrix 9 row 56: SNAPSHOT Depends On: System, Artifact.
    Per Matrix 9 row 57: TRACEABILITY_LINK Depends On: Artifact, Process.
    The Traceability Family captures reference points and connections
    between artifacts.

5.2 Members

    Name             Purpose (RMM #2)                                  RMM Row
    ---------------  ------------------------------------------------  ---------
    BASELINE         Establish frozen, authoritative reference point    M2R55
    SNAPSHOT         Capture complete state of system/module/process  M2R56
    CHECKPOINT       Capture and verify state at defined milestone    M2R58
    TRACEABILITY_LINK Typed, directional connection between entities  M2R57

5.3 Classification
    NORMATIVE — Baselines are frozen reference points; Snapshots are
    committed state captures; Checkpoints are verified milestones;
    TraceabilityLinks are typed semantic connections.

5.4 Authority
    Per RMM property #4 and Matrix 7:

    Member           Owner       AI-C      AI-M      H-M       Source
    ---------------  ----------  --------  --------  --------  ----------
    BASELINE         GovernanceBody W/Appr    No        W/Appr    RMM #4,M7R55
    SNAPSHOT         Kernel      Yes       No        No        RMM #4,M7R56
    CHECKPOINT       Process     Yes       No        No        RMM #4,M7R58
    TRACEABILITY_LINK Process    Yes       W/Appr    Yes       RMM #4,M7R57

5.5 Lifecycle
    Per Matrix 2:

    BASELINE:         Proposed → Reviewed → Approved → Frozen → Referenced →
                      Amended → Superseded → Archived
    SNAPSHOT:         Triggered → Capturing → Validated → Committed →
                      Referenced → Expired
    CHECKPOINT:       Defined → Triggered → Capturing → Validated →
                      Verified → Committed → Reviewed
    TRACEABILITY_LINK: Defined → Created → Verified → Active → Impacted →
                      Updated/Broken → Removed → Archived

5.6 Relationships
    Per Matrix 9:

    BASELINE:         Depends On: Artifact, Approval, Snapshot. Required By:
                      Checkpoint, Plan.
    SNAPSHOT:         Depends On: System, Artifact. Required By: Baseline,
                      Audit, Review.
    CHECKPOINT:       Depends On: Baseline, Milestone, Task. Required By:
                      Review, Assessment.
    TRACEABILITY_LINK: Depends On: Artifact, Process. Required By: Baseline,
                      Audit.

5.7 Validation Rules
    V-TF-01  BASELINE Freezable: Yes                                  M5R55
    V-TF-02  SNAPSHOT Freezable: Yes                                 M5R56
    V-TF-03  TRACEABILITY_LINK may not be bidirectional without       RMM #7
             explicit reverse link
    V-TF-04  TRACEABILITY_LINK may not be semantically empty           RMM #7

5.8 Constraints
    C-TF-01  BASELINE shall not be modified after Frozen state         RMM #7
    C-TF-02  UNSUPPORTED (RMM property #7 for TRACEABILITY_LINK does not mention circular references)

------------------------------------------------------------------------------

6. AUTHORIZATION FAMILY
-----------------------

RMM Basis: TIER 12; ENTITIES: AUTHORIZATION, CERTIFICATION, CREDENTIAL,
           SIGNATURE, APPROVAL; Matrix 2 rows 50-54; Matrix 3 rows 50-54;
           Matrix 5 rows 50-54; Matrix 7 rows 50-54; Matrix 8 rows 50-54.

6.1 Family Definition
    Per RMM Matrix 9 row 50: APPROVAL Depends On: Role, Artifact, Review.
    Per Matrix 9 row 51: AUTHORIZATION Depends On: Role, Credential,
    Constraint. Per Matrix 9 row 52: CERTIFICATION Depends On: Standard,
    Audit, Evidence. The Authorization Family captures permission-granting
    and attestation mechanisms.

6.2 Members

    Name            Purpose (RMM #2)                                  RMM Row
    --------------  ------------------------------------------------  ---------
    APPROVAL        Formally record authorized party acceptance       M2R50
    AUTHORIZATION   Grant specific permission for action or access    M2R51
    CERTIFICATION   Formally attest entity meets standards            M2R52
    CREDENTIAL      Provide token or proof of identity/authorization  M2R53
    SIGNATURE       Mark artifact with authenticated identity         M2R54

6.3 Classification
    CANONICAL — Authorization artifacts govern access and permission;
    they are frozen after finalization.

    APPROVAL:       CANONICAL (Static after Final)
    AUTHORIZATION:  NORMATIVE (Granted → Active → Renewed → Revoked)
    CERTIFICATION:  NORMATIVE (Granted → Active → UnderRenewal → Revoked)
    CREDENTIAL:     NORMATIVE (Issued → Active → Renewed → Revoked)
    SIGNATURE:      CANONICAL (Static after Validated)

6.4 Authority
    Per RMM property #4 and Matrix 7:

    Member          Owner       AI-C      AI-M      H-M       Source
    --------------  ----------  --------  --------  --------  ----------
    APPROVAL        Role        No        No        W/Appr    RMM #4,M7R50
    AUTHORIZATION   GovernanceBody No        No        W/Appr    RMM #4,M7R51
    CERTIFICATION   GovernanceBody No        No        W/Appr    RMM #4,M7R52
    CREDENTIAL      Actor       No        No        W/Appr    RMM #4,M7R53
    SIGNATURE       Actor       No        No        No        RMM #4,M7R54

6.5 Lifecycle
    Per Matrix 2:

    APPROVAL:       Requested → Reviewed → Granted/Denied → Conditional →
                    Final → Withdrawn
    AUTHORIZATION:  Requested → Evaluated → Granted → Active → Renewed →
                    Revoked → Expired
    CERTIFICATION:  Requested → Evaluated → Verified → Granted → Active →
                    UnderRenewal → Revoked
    CREDENTIAL:     Issued → Active → Renewed → Suspended →
                    Reactivated/Expired → Revoked
    SIGNATURE:      Prepared → Affixed → Validated → Active → Revoked →
                    Expired

6.6 Relationships
    Per Matrix 9:

    APPROVAL:       Depends On: Role, Artifact, Review. Required By:
                    Baseline, Plan, DecisionRecord.
    AUTHORIZATION:  Depends On: Role, Credential, Constraint. Required By:
                    All entities.
    CERTIFICATION:  Depends On: Standard, Audit, Evidence. Required By:
                    Contract.
    CREDENTIAL:     Depends On: Actor. Required By: Authorization, Signature.
    SIGNATURE:      Depends On: Credential, Artifact. Required By: Approval,
                    DecisionRecord, Baseline.

6.7 Validation Rules
    V-AUF-01  APPROVAL AI Creatable: No                             M7R50
    V-AUF-02  SIGNATURE Human Modifiable: No                        M7R54
    V-AUF-03  APPROVAL Stability: Static after Final                M3R50
    V-AUF-04  SIGNATURE Stability: Static after Validated           M3R54
    V-AUF-05  AUTHORIZATION Freezable: No                           M5R51
    V-AUF-06  CREDENTIAL Freezable: No                              M5R53

6.8 Constraints
    C-AUF-01  APPROVAL may not be granted without Review             RMM #7
    C-AUF-02  APPROVAL may not be both Granted and Denied            RMM #7
    C-AUF-03  SIGNATURE may not be forged; may not be affixed by unauthorized party; may not be retroactively dated       RMM #7

------------------------------------------------------------------------------

7. STANDARDS FAMILY
-------------------

RMM Basis: TIER 6 (POLICY, RULE); TIER 7 (STANDARD, GUIDELINE, CONSTRAINT);
           plus INVARIANT (T7). Matrix 2 rows 28-32; Matrix 3 rows 28-32;
           Matrix 5 rows 28-32; Matrix 7 rows 28-32; Matrix 8 rows 28-32.

7.1 Family Definition
    Per RMM Matrix 9 row 30: STANDARD Depends On: GovernanceBody. Required
    By: Contract, Certification, Audit, Assessment. Per Matrix 9 row 31:
    GUIDELINE Depends On: Standard. Required By: Contract, Process. The
    Standards Family captures mandatory requirements, advisory guidance,
    and structural limitations.

7.2 Members

    Name        Purpose (RMM #2)                                     RMM Row
    ----------  ---------------------------------------------------  ---------
    POLICY      Establish governing principle for decisions          M2R28
    RULE        State binding constraint on behavior/structure       M2R29
    STANDARD    Define mandatory requirements/criteria               M2R30
    GUIDELINE   Provide recommended practices and advisory guidance  M2R31
    CONSTRAINT  Impose structural or behavioral limitation           M2R32
    INVARIANT   Declare condition that must always hold true         T7

7.3 Classification
    NORMATIVE — Standards, Rules, Policies, and Constraints are
    mandatory. Guidelines are advisory. Invariants are foundational.

    POLICY:     NORMATIVE
    RULE:       NORMATIVE
    STANDARD:   NORMATIVE
    GUIDELINE:  NORMATIVE ( advisory per RMM; not binding )
    CONSTRAINT: NORMATIVE
    INVARIANT:  CANONICAL (Proposed → Ratified → Active → Eternal)

7.4 Authority
    Per RMM property #4 and Matrix 7:

    Member      Owner           AI-C      AI-M      H-M       Source
    ----------  --------------  --------  --------  --------  ----------
    POLICY      GovernanceBody  W/Appr    No        W/Appr    RMM #4,M7R28
    RULE        GovernanceBody  W/Appr    W/Appr    W/Appr    RMM #4,M7R29
    STANDARD    GovernanceBody  W/Appr    W/Appr    W/Appr    RMM #4,M7R30
    GUIDELINE   GovernanceBody  Yes       W/Appr    Yes       RMM #4,M7R31
    CONSTRAINT  GovernanceBody  W/Appr    W/Appr    Yes       RMM #4,M7R32
    INVARIANT   Constitution    No        No        No        RMM #4,M7R33

7.5 Lifecycle
    Per Matrix 2:

    POLICY:     Draft → Consulted → Approved → Communicated → Active →
                UnderReview → Amended → Retired
    RULE:       Draft → Proposed → Approved → Active → Suspended →
                Amended → Repealed
    STANDARD:   Draft → Proposed → UnderReview → Approved → Active →
                UnderRevision → Superseded/Retired
    GUIDELINE:  Draft → Published → Active → Updated → Deprecated/Withdrawn
    CONSTRAINT: Identified → Specified → Ratified → Active → Amending →
                Superseded → Retired
    INVARIANT:  Proposed → Ratified → Active → Eternal

7.6 Relationships
    Per Matrix 9:

    POLICY:     Depends On: GovernanceBody, Rule. Required By: Audit,
                Review, Assessment.
    RULE:       Depends On: GovernanceBody, Policy, Constitution. Required
                By: Audit, Exception, Sanction, Assessment.
    STANDARD:   Depends On: GovernanceBody. Required By: Contract,
                Certification, Audit, Assessment.
    GUIDELINE:  Depends On: Standard. Required By: Contract, Process.
    CONSTRAINT: Depends On: Invariant, Layer, Boundary. Required By:
                Module, Component, Interface, Resource.
    INVARIANT:  Depends On: Constitution. Required By: Constraint, Contract.

7.7 Validation Rules
    V-SF-01  INVARIANT AI Creatable: No                             M7R33
    V-SF-02  INVARIANT AI Modifiable: No                            M7R33
    V-SF-03  INVARIANT Human Modifiable: No                         M7R33
    V-SF-04  INVARIANT Stability: Static                            M3R33
    V-SF-05  INVARIANT Freezable: Yes                               M5R33
    V-SF-06  GUIDELINE Freezable: No                                M5R31
    V-SF-07  STANDARD Freezable: Yes                                M5R30

7.8 Constraints
    C-SF-01  RULE may not contradict Constitution                    RMM #7
    C-SF-02  CONSTRAINT may not contradict Invariant; may not be advisory only (must be enforceable)  RMM #7
    C-SF-03  INVARIANT may not be temporary                         RMM #7

------------------------------------------------------------------------------

8. MEASUREMENT FAMILY
---------------------

RMM Basis: TIER 14; ENTITIES: MEASUREMENT, ASSESSMENT;
           Matrix 2 rows 60-61; Matrix 3 rows 60-61;
           Matrix 5 rows 60-61; Matrix 7 rows 60-61; Matrix 8 rows 60-61.

8.1 Family Definition
    Per RMM Matrix 9 row 59: METRIC Depends On: Governance,
    Specification. Required By: Measurement, Assessment, Audit. Per
    Matrix 9 row 60: MEASUREMENT Depends On: Metric, Process. Required
    By: Assessment, Report, Audit. Per Matrix 9 row 61: ASSESSMENT
    Depends On: Measurement, Evidence, Finding. The Measurement Family
    captures quantified observations and systematic evaluations.

8.2 Members

    Name         Purpose (RMM #2)                                    RMM Row
    -----------  --------------------------------------------------  ---------
    MEASUREMENT  Capture quantified observation of property          M2R60
    ASSESSMENT   Systematically evaluate against defined criteria    M2R61

8.3 Classification
    DERIVED — Measurements are captured observations; Assessments are
    evaluations derived from measurements and evidence.

8.4 Authority
    Per RMM property #4 and Matrix 7:

    Member       Owner       AI-C      AI-M      H-M       Source
    -----------  ----------  --------  --------  --------  ----------
    MEASUREMENT  Process     Yes       No        No        RMM #4,M7R60
    ASSESSMENT   Process     W/Appr    W/Appr    Yes       RMM #4,M7R61

8.5 Lifecycle
    Per Matrix 2:

    MEASUREMENT: Triggered → Captured → Validated → Recorded → Analyzed →
                 Referenced → Archived
    ASSESSMENT:  Commissioned → Planned → Executed → Analyzed → Drafted →
                 Reviewed → Published → Appealed → Final → Archived

8.6 Relationships
    Per Matrix 9:

    MEASUREMENT: Depends On: Metric, Process. Required By: Assessment,
                 Report, Audit.
    ASSESSMENT:  Depends On: Measurement, Evidence, Finding. Required By:
                 Conclusion, DecisionRecord, Report.

8.7 Validation Rules
    V-MF-01  MEASUREMENT Human Modifiable is No                       M7R60
    V-MF-02  MEASUREMENT AI Modifiable is No                          M7R60
    V-MF-03  MEASUREMENT Stability: Static after Recorded           M3R60

8.8 Constraints
    C-MF-01  MEASUREMENT may not be retroactively altered            RMM #7
    C-MF-02  UNSUPPORTED (RMM property #7 for ASSESSMENT does not mandate basis)

------------------------------------------------------------------------------

9. OVERSIGHT FAMILY
-------------------

RMM Basis: TIER 15; ENTITIES: AUDIT, AUDIT_TRAIL, REVIEW;
           Matrix 2 rows 62-64; Matrix 3 rows 62-64;
           Matrix 5 rows 62-64; Matrix 7 rows 62-64; Matrix 8 rows 62-64.

9.1 Family Definition
    Per RMM Matrix 9 row 62: AUDIT Depends On: Standard, Rule, Policy,
    Evidence. Required By: Finding, Certification, Sanction. Per Matrix
    9 row 63: REVIEW Depends On: Artifact, Process, Milestone. Required
    By: Finding, Approval, DecisionRecord. The Oversight Family captures
    independent inspection, audit trail maintenance, and formal examination.

9.2 Members

    Name       Purpose (RMM #2)                                     RMM Row
    ---------  ---------------------------------------------------  ---------
    AUDIT      Perform independent, systematic compliance inspection M2R62
    AUDIT_TRAIL Maintain tamper-evident record of actions           M2R64
    REVIEW     Conduct formal examination of entity/process         M2R63

9.3 Classification
    NORMATIVE — Audits and Reviews are formal governance processes;
    Audit Trails are evidentiary records.

    AUDIT:       NORMATIVE
    AUDIT_TRAIL: CANONICAL (Initiated → Recording → Active → Reviewed →
                 Sealed → Archived → Expired)
    REVIEW:      NORMATIVE

9.4 Authority
    Per RMM property #4 and Matrix 7:

    Member       Owner       AI-C      AI-M      H-M       Source
    ---------    ----------  --------  --------  --------  ----------
    AUDIT        GovernanceBody W/Appr    W/Appr    W/Appr    RMM #4,M7R62
    AUDIT_TRAIL  Kernel      Yes       No        No        RMM #4,M7R64
    REVIEW       GovernanceBody W/Appr    W/Appr    W/Appr    RMM #4,M7R63

9.5 Lifecycle
    Per Matrix 2:

    AUDIT:       Planned → Chartered → Executed → EvidenceAnalyzed →
                 ReportDrafted → Reviewed → Published → RemediationTracked →
                 Closed
    AUDIT_TRAIL: Initiated → Recording → Active → Reviewed → Sealed →
                 Archived → Expired
    REVIEW:      Scheduled → Initiated → InProgress → FindingsDrafted →
                 Reviewed → Published → Accepted/Contested → Closed

9.6 Relationships
    Per Matrix 9:

    AUDIT:       Depends On: Standard, Rule, Policy, Evidence. Required
                 By: Finding, Certification, Sanction.
    AUDIT_TRAIL: Depends On: System, Log, Record. Required By: Audit,
                 Investigation, Compliance.
    REVIEW:      Depends On: Artifact, Process, Milestone. Required By:
                 Finding, Approval, DecisionRecord.

9.7 Validation Rules
    V-OF-01  AUDIT_TRAIL AI Creatable: Yes                          M7R64
    V-OF-02  AUDIT_TRAIL AI Modifiable: No                          M7R64
    V-OF-03  AUDIT_TRAIL Human Modifiable: No                       M7R64
    V-OF-04  AUDIT_TRAIL Stability: Static after Seal               M3R64
    V-OF-05  AUDIT_TRAIL Freezable: Yes                             M5R64

9.8 Constraints
    C-OF-01  AUDIT_TRAIL may not be modified after Seal              RMM #7
    C-OF-02  AUDIT_TRAIL may not omit required events                RMM #7
    C-OF-03  UNSUPPORTED (RMM property #7 for AUDIT_TRAIL does not mention destruction)

------------------------------------------------------------------------------

10. EXCEPTION FAMILY
--------------------

RMM Basis: TIER 17; ENTITIES: EXCEPTION, WAIVER;
            Matrix 2 rows 67-68; Matrix 3 rows 67-68;
            Matrix 5 rows 67-68; Matrix 7 rows 67-68; Matrix 8 rows 67-68.

10.1 Family Definition
    Per RMM Matrix 9 row 67: EXCEPTION Depends On: Rule, GovernanceBody.
    Required By: Waiver, Audit. Per Matrix 9 row 68: WAIVER Depends On:
    Exception, Rule, GovernanceBody. The Exception Family captures
    permitted deviations and formal exemptions.

10.2 Members

    Name      Purpose (RMM #2)                                      RMM Row
    --------  ----------------------------------------------------  ---------
    EXCEPTION Document permitted deviation from Rule/Standard       M2R67
    WAIVER    Formally grant exception from requirement/rule        M2R68

10.3 Classification
    DRAFT — Exceptions and Waivers are temporary; they expire or are
    revoked. Their pre-approval state is DRAFT.

10.4 Authority
    Per RMM property #4 and Matrix 7:

    Member    Owner           AI-C      AI-M      H-M       Source
    --------  --------------  --------  --------  --------  ----------
    EXCEPTION GovernanceBody  No        No        W/Appr    RMM #4,M7R67
    WAIVER    GovernanceBody  No        No        W/Appr    RMM #4,M7R68

10.5 Lifecycle
    Per Matrix 2:

    EXCEPTION: Requested → Justified → Reviewed → Granted → Active →
               Monitored → Expired/Revoked
    WAIVER:    Requested → Justified → Reviewed → Granted/Denied →
               Active → Expired/Revoked

10.6 Relationships
    Per Matrix 9:

    EXCEPTION: Depends On: Rule, GovernanceBody. Required By: Waiver, Audit.
    WAIVER:    Depends On: Exception, Rule, GovernanceBody. Required By:
               Audit, Compliance.

10.7 Validation Rules
    V-EXF-01  EXCEPTION AI Creatable: No                            M7R67
    V-EXF-02  WAIVER AI Creatable: No                               M7R68
    V-EXF-03  EXCEPTION Freezable: Yes                              M5R67
    V-EXF-04  WAIVER Freezable: Yes                                 M5R68

10.8 Constraints
    C-EXF-01  EXCEPTION must reference the Rule being excepted       RMM #7
    C-EXF-02  UNSUPPORTED (RMM property #7 for WAIVER does not mention self-granting)

------------------------------------------------------------------------------

11. GOVERNANCE MECHANICS FAMILY
-------------------------------

RMM Basis: TIER 18; ENTITIES: AMENDMENT, SANCTION, PRECEDENT, APPEAL,
           VETO; Matrix 2 rows 69-73; Matrix 3 rows 69-73;
           Matrix 5 rows 69-73; Matrix 7 rows 69-73; Matrix 8 rows 69-73.

11.1 Family Definition
    Per RMM Matrix 9 row 69: AMENDMENT Depends On: Constitution,
    GovernanceBody, Rule. Per Matrix 9 row 70: SANCTION Depends On:
    Rule, GovernanceBody, Audit. The Governance Mechanics Family captures
    formal change, punitive measures, prior decisions, reconsideration,
    and rejection authority.

11.2 Members

    Name      Purpose (RMM #2)                                      RMM Row
    --------  ----------------------------------------------------  ---------
    AMENDMENT Propose and record formal change to governance        M2R69
    SANCTION  Impose punitive/corrective measure for violation      M2R70
    PRECEDENT Record prior decision that guides future decisions    M2R71
    APPEAL    Request reconsideration of decision/ruling            M2R72
    VETO      Empower authority to reject decision/action           M2R73

11.3 Classification
    CANONICAL — All members are governance-critical with restricted
    modification permissions.

11.4 Authority
    Per RMM property #4 and Matrix 7:

    Member    Owner           AI-C      AI-M      H-M       Source
    --------  --------------  --------  --------  --------  ----------
    AMENDMENT Actor           W/Appr    W/Appr    W/Appr    RMM #4,M7R69
    SANCTION  GovernanceBody  No        No        W/Appr    RMM #4,M7R70
    PRECEDENT GovernanceBody  No        No        W/Appr    RMM #4,M7R71
    APPEAL    Actor           No        No        W/Appr    RMM #4,M7R72
    VETO      Role            No        No        W/Appr    RMM #4,M7R73

11.5 Lifecycle
    Per Matrix 2:

    AMENDMENT: Drafted → Submitted → Reviewed → Approved → Ratified →
               Applied → Recorded
    SANCTION:  Triggered → Investigated → Proposed → Reviewed → Imposed →
               Appealed → Upheld/Overturned → Executed → Lifted
    PRECEDENT: Established → Active → Distinguished → Overruled → Archived
    APPEAL:    Filed → Accepted → Scheduled → Heard → Deliberated →
               Upheld/Overturned/Remanded → Final → Recorded
    VETO:      Triggered → Justified → Exercised → Reviewed →
               Sustained/Overridden → Recorded

11.6 Relationships
    Per Matrix 9:

    AMENDMENT: Depends On: Constitution, GovernanceBody, Rule. Required
               By: Policy, Rule, Standard.
    SANCTION:  Depends On: Rule, GovernanceBody, Audit. Required By:
               Compliance, Appeal.
    PRECEDENT: Depends On: GovernanceBody, DecisionRecord. Required By:
               Decision, Appeal.
    APPEAL:    Depends On: Decision, GovernanceBody, Sanction. Required
               By: Precedent, Dispute.
    VETO:      Depends On: Constitution, Role, Decision. Required By:
               DecisionRecord, GovernanceBody.

11.7 Validation Rules
    V-GMF-01  SANCTION AI Creatable: No                            M7R70
    V-GMF-02  PRECEDENT AI Creatable: No                           M7R71
    V-GMF-03  APPEAL AI Creatable: No                              M7R72
    V-GMF-04  VETO AI Creatable: No                                M7R73
    V-GMF-05  PRECEDENT Freezable: No                              M5R71

11.8 Constraints
    C-GMF-01  SANCTION may not be imposed without due process       RMM #7
    C-GMF-02  VETO may not be overridden by the vetoed party        RMM #7
    C-GMF-03  APPEAL may not be filed without grounds               RMM #7

------------------------------------------------------------------------------

12. ACCOUNTABILITY FAMILY
-------------------------

RMM Basis: TIER 19; ENTITIES: DISPUTE, RECUSAL, TRANSPARENCY_REPORT;
           Matrix 2 rows 74-76; Matrix 3 rows 74-76;
           Matrix 5 rows 74-76; Matrix 7 rows 74-76; Matrix 8 rows 74-76.

12.1 Family Definition
    Per RMM Matrix 9 row 74: DISPUTE Depends On: Actor, GovernanceBody.
    Required By: Appeal, Recusal. The Accountability Family captures
    conflict documentation, stakeholder withdrawal, and public disclosure.

12.2 Members

    Name               Purpose (RMM #2)                                RMM Row
    -----------------  ----------------------------------------------  ---------
    DISPUTE            Document and manage conflict between parties    M2R74
    RECUSAL            Document voluntary/required withdrawal          M2R75
    TRANSPARENCY_REPORT Publish periodic public disclosure of activity M2R76

12.3 Classification
    DERIVED — Disputes and Recusals document events; Transparency
    Reports compile and publish information.

12.4 Authority
    Per RMM property #4 and Matrix 7:

    Name               Owner           AI-C      AI-M      H-M       Source
    -----------------  --------------  --------  --------  --------  ----------
    DISPUTE            Actor           No        No        W/Appr    RMM #4,M7R74
    RECUSAL            Actor           No        No        W/Appr    RMM #4,M7R75
    TRANSPARENCY_REPORT GovernanceBody  W/Appr    W/Appr    W/Appr    RMM #4,M7R76

12.5 Lifecycle
    Per Matrix 2:

    DISPUTE:           Raised → Acknowledged → Scoped → Mediated →
                       Arbitrated → Resolved → Appealed → Final → Archived
    RECUSAL:           Identified → Declared → Accepted → Executed →
                       Verified → Lifted → Recorded
    TRANSPARENCY_REPORT: Planned → Compiled → Reviewed → Published →
                       Acknowledged → Archived

12.6 Relationships
    Per Matrix 9:

    DISPUTE:           Depends On: Actor, GovernanceBody. Required By:
                       Appeal, Recusal.
    RECUSAL:           Depends On: Actor, Decision. Required By:
                       DecisionRecord, Audit.
    TRANSPARENCY_REPORT: Depends On: GovernanceBody, Metric, Decision.
                       Required By: Audit, Stakeholder.

12.7 Validation Rules
    V-ACF-01  DISPUTE AI Creatable: No                             M7R74
    V-ACF-02  RECUSAL AI Creatable: No                             M7R75
    V-ACF-03  DISPUTE Stability: Fast                              M3R74
    V-ACF-04  RECUSAL Stability: Fast                              M3R75

12.8 Constraints
    C-ACF-01  RECUSAL may not be partial                           RMM #7
    C-ACF-02  UNSUPPORTED (RMM property #7 for TRANSPARENCY_REPORT does not mention schedule)

------------------------------------------------------------------------------

13. CROSS-CUTTING FAMILY
------------------------

RMM Basis: TIER 20; ENTITY: ESCALATION; Matrix 2 row 78;
           Matrix 3 row 78; Matrix 5 row 78; Matrix 7 row 78;
           Matrix 8 row 78.

13.1 Family Definition
    Per RMM Matrix 9 row 78: ESCALATION Depends On: Actor,
    GovernanceBody, Decision. Required By: Dispute, Appeal. The
    Cross-Cutting Family contains a single entity that operates across
    multiple governance and dispute processes.

13.2 Members

    Name       Purpose (RMM #2)                                     RMM Row
    ---------  ---------------------------------------------------  ---------
    ESCALATION Elevate decision/issue/authority to higher level      M2R78

13.3 Classification
    DRAFT — Escalation is transient; each instance is raised,
    processed, and resolved.

13.4 Authority
    Per RMM property #4 and Matrix 7:

    Member     Owner       AI-C      AI-M      H-M       Source
    ---------  ----------  --------  --------  --------  ----------
    ESCALATION Actor       W/Appr    W/Appr    Yes       RMM #4,M7R78

13.5 Lifecycle
    Per Matrix 2:
    ESCALATION: Triggered → Documented → Routed → Received →
                Under-Review → Resolved/Redirected → Closed

13.6 Relationships
    Per Matrix 9:
    ESCALATION: Depends On: Actor, GovernanceBody, Decision. Required
                By: Dispute, Appeal.

13.7 Validation Rules
    V-CCF-01  ESCALATION Stability: Fast                            M3R78
    V-CCF-02  ESCALATION Freezable: Yes                             M5R78

13.8 Constraints
    C-CCF-01  ESCALATION may not bypass intermediate levels without justification; may not be circular   RMM #7

------------------------------------------------------------------------------

FAMILY MEMBERSHIP SUMMARY
-------------------------

| # | Family                  | Tier | Members                                                    | Count |
|---|------------------------|------|------------------------------------------------------------|-------|
| 1 | Root Artifact          | T11  | ARTIFACT                                                   | 1     |
| 2 | Document               | T11  | DOCUMENT, SPECIFICATION, RECORD, LOG, REPORT              | 5     |
| 3 | Evidence               | T10  | EVIDENCE, FINDING, CONCLUSION                             | 3     |
| 4 | Decision               | T10  | DECISION, DECISION_RECORD                                 | 2     |
| 5 | Traceability           | T13  | BASELINE, SNAPSHOT, CHECKPOINT, TRACEABILITY_LINK         | 4     |
| 6 | Authorization          | T12  | APPROVAL, AUTHORIZATION, CERTIFICATION, CREDENTIAL, SIGNATURE | 5  |
| 7 | Standards              | T6/7 | STANDARD, GUIDELINE, POLICY, RULE, CONSTRAINT, INVARIANT  | 6     |
| 8 | Measurement            | T14  | MEASUREMENT, ASSESSMENT                                   | 2     |
| 9 | Oversight              | T15  | AUDIT, AUDIT_TRAIL, REVIEW                                | 3     |
| 10| Exception              | T17  | EXCEPTION, WAIVER                                         | 2     |
| 11| Governance Mechanics   | T18  | AMENDMENT, SANCTION, PRECEDENT, APPEAL, VETO              | 5     |
| 12| Accountability         | T19  | DISPUTE, RECUSAL, TRANSPARENCY_REPORT                     | 3     |
| 13| Cross-Cutting          | T20  | ESCALATION                                                | 1     |
|---|------------------------|------|------------------------------------------------------------|-------|
|   | TOTAL                  |      |                                                            | 42    |

------------------------------------------------------------------------------

END OF DOCUMENT
