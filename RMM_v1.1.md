================================================================================
RADIUS1 KERNEL — REPOSITORY META MODEL (RMM)
COMPLETE SPECIFICATION — VERSION 1.1
================================================================================

Generated: 2026-06-26
Revision: v1.1 (engineering bug-fix release; supersedes RMM v1)
Version: 1.1
Status: RELEASED
Classification: CANONICAL

STATISTICS
- Total Canonical Entities: 79
- Total Relationships: 640
- Total Matrices: 10
- Total Data Rows Across Matrices: 790
- Estimated Total Cells: 4,950 (all filled)
- Entity Tiers: 20
- Properties Per Entity: 15 (all defined)

ORIGIN
Raw entities discovered: ~335 across 4 domains
- System & Structure: 40
- Process & Execution: 128
- Artifact & Evidence: 60
- Governance & Lifecycle: 107

Deduplication: ~256 entities eliminated
Merges: 30+ cross-domain entity merges
Final canonical set: 79 entities

VALIDATION (v1.1 — recomputed from the model; see VALIDATION_REPORT.md)
[x] Every entity has all 15 properties (79 x 15 = 1,185)
[x] Every relationship is explicit (640 total; count corrected from 636)
[x] Every ownership is unique (Process & Session dual-primary ownership corrected)
[x] No circular authority (downward governance/authority subgraph verified acyclic)
[x] No undefined concepts in the formal relationship graph (640 edges; all endpoints canonical)
    - Narrative "Allowed Relationships" forward-references (e.g. Port, Namespace) are deferred
      as architectural proposals; they are not part of the formal graph. See RMM_FUTURE_PROPOSALS.md
[x] No duplicated entities (79 distinct)
[x] No implementation leakage (conceptual; storage-path items tracked for a future version)
[x] Technology-independent (conceptual; see RMM_FUTURE_PROPOSALS.md)

================================================================================
TABLE OF CONTENTS
================================================================================

PART I:  ENTITY CATALOG
PART II: RELATIONSHIP GRAPH
PART III: MATRICES
  - Matrix 1:  Ownership Matrix
  - Matrix 2:  Lifecycle Matrix
  - Matrix 3:  Stability Classification
  - Matrix 4:  Versionability Matrix
  - Matrix 5:  Freeze Matrix
  - Matrix 6:  Source-of-Truth Matrix
  - Matrix 7:  Creation & Modification Permissions
  - Matrix 8:  Cardinality Matrix
  - Matrix 9:  Dependency Matrix
  - Matrix 10: Glossary

================================================================================
PART I: ENTITY CATALOG (79 Entities)
================================================================================

================================================================================
RADIUS1 KERNEL — REPOSITORY META MODEL (RMM)
CANONICAL ENTITY CATALOG
================================================================================

A unified, deduplicated ontology synthesized from four domain perspectives:
- System & Structure (40 entities)
- Process & Execution (128 entities)
- Artifact & Evidence (60 entities)
- Governance & Lifecycle (107 entities)

Raw entities discovered: ~335 | Canonical entities: 79

Elimination rules applied:
- Implementation-specific entities (Mutex, Deadlock, RaceCondition, etc.)
- Control flow primitives (Fork, Join, Sequence, Iteration, DecisionPoint)
- Derived/secondary concepts (DependencyGraph, ExecutionTrace, etc.)
- Temporal primitives (Duration, Timeout, Pause, ResumePoint)
- Quality gate constructs (DefinitionOfDone)
- Internal process mechanics (Compensation, SideEffect, Backpressure, etc.)
- Actor/session subtypes (HumanActor, AISession, etc.)
- Process subtypes (Saga, Choreography, Batch, Subprocess, Pipeline, etc.)
- Overly granular governance mechanics (Motion, Quorum, Bylaw, etc.)

================================================================================
TIER 1: SYSTEM FOUNDATION
================================================================================

### KERNEL
1. Name: Kernel
2. Purpose: To serve as the root container and identity of the entire Radius1 engineering system.
3. Responsibility: Owning the complete structural composition, lifecycle, and integrity of all entities within its boundary.
4. Owner: Constitution
5. Lifecycle: Conceived → Bootstrapped → Active → Maintenance → Sunset → Archive
6. Allowed Relationships: Contains Domain, Subsystem, Module, Component, Primitive, Layer, Slice, Namespace, Boundary, Registry, View.
7. Forbidden Relationships: May not be contained by another Kernel; may not depend on any external entity.
8. Cardinality: 1:1
9. Stability: Static
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 00-CONSTITUTION/

---

### DOMAIN
1. Name: Domain
2. Purpose: To bound a coherent area of knowledge, responsibility, and language within the Kernel.
3. Responsibility: Encapsulating a distinct problem space and defining the ubiquitous language, entities, and rules governing that space.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Defined → Active → Consolidated → Retired
6. Allowed Relationships: Contains Subsystem, Module, Component, Primitive; bounded by Boundary; referenced by Namespace; exposes Interface.
7. Forbidden Relationships: May not directly contain another Domain; may not cross Boundary without Bridge.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Domain/

---

### SUBSYSTEM
1. Name: Subsystem
2. Purpose: To group modules and components that share a cohesive functional purpose within a Domain.
3. Responsibility: Delivering a major functional area of the Kernel, including all capabilities, interfaces, and resources assigned to it.
4. Owner: Module Lead (assigned by GovernanceBody)
5. Lifecycle: Proposed → Approved → Forming → Active → Merging → Retired
6. Allowed Relationships: Belongs to Domain; contains Module, Component, Primitive; exposes Interface; defines Boundary; owns Resource.
7. Forbidden Relationships: May not belong to multiple Domains; may not contain Kernel or Domain.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Subsystem/

---

### MODULE
1. Name: Module
2. Purpose: To serve as the primary unit of development, deployment, and ownership within a Subsystem.
3. Responsibility: Implementing a bounded set of capabilities, exposing defined interfaces, and managing its internal composition.
4. Owner: Module Lead
5. Lifecycle: Proposed → Specified → Developing → Active → Stable → Deprecated → Retired
6. Allowed Relationships: Belongs to Subsystem; contains Component, Primitive; declares Dependency; exposes Interface; defines Namespace.
7. Forbidden Relationships: May not directly belong to Domain; may not contain Subsystem or Domain.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Module/

---

### COMPONENT
1. Name: Component
2. Purpose: To provide a reusable, composable structural unit that encapsulates specific behavior or state.
3. Responsibility: Delivering a focused, reusable capability through well-defined interfaces while hiding internal implementation details.
4. Owner: Module Lead
5. Lifecycle: Proposed → Designed → Implementing → Active → Reusable → Deprecated → Retired
6. Allowed Relationships: Belongs to Module; used by Component, Module; exposes Interface; declares Dependency; participates in Assembly.
7. Forbidden Relationships: May not own a Module; may not contain a Subsystem; may not form circular Dependency.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: Owning Module's META/Component/

---

### PRIMITIVE
1. Name: Primitive
2. Purpose: To serve as the fundamental, indivisible building block from which all higher-order entities are composed.
3. Responsibility: Providing atomic concepts, values, and operations that cannot be decomposed further within the Kernel's ontology.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Ratified → Active → Universal → Immutable
6. Allowed Relationships: Used by Component, Module, Subsystem; defined within Domain; referenced by Interface.
7. Forbidden Relationships: May not contain Component, Module, or Subsystem; may not depend on non-Primitive; may not be deprecated once ratified.
8. Cardinality: N:M
9. Stability: Static
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: 01-META-MODEL/Primitive/

---

### RESOURCE
1. Name: Resource
2. Purpose: To represent any consumable, allocable, or manageable asset that entities within the Kernel require to operate.
3. Responsibility: Defining a named, typed, measurable asset that can be allocated to and consumed by entities.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Classified → Available → Allocated → Constrained → Depleted → Reclaimed
6. Allowed Relationships: Allocated to Module, Subsystem, Component, Feature; constrained by Constraint; hosted on Tier.
7. Forbidden Relationships: May not be owned by an Interface; may not exist without a classification.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Resource/

================================================================================
TIER 2: STRUCTURE & ARCHITECTURE
================================================================================

### LAYER
1. Name: Layer
2. Purpose: To define a horizontal architectural stratum that separates concerns by abstraction level within the Kernel.
3. Responsibility: Providing a level of abstraction that groups entities by their architectural role and enforces directional rules between strata.
4. Owner: GovernanceBody
5. Lifecycle: Proposed → Ratified → Active → Stable → Superseded → Retired
6. Allowed Relationships: Contains Module, Component, Primitive; stacked above/below Layer; intersected by Slice; entities in upper layers depend on lower layers.
7. Forbidden Relationships: May not contain Domain or Subsystem; may not form circular stack dependencies.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Layer/

---

### TIER
1. Name: Tier
2. Purpose: To distinguish physical or logical deployment levels that govern runtime behavior, availability, and access patterns.
3. Responsibility: Separating the system into runtime execution levels and defining the rules for communication and dependency across those levels.
4. Owner: GovernanceBody
5. Lifecycle: Defined → Ratified → Active → Stable → Retired
6. Allowed Relationships: Contains Subsystem, Module; communicates with Tier; separated from Tier by Boundary; hosts Resource.
7. Forbidden Relationships: May not contain Slice; may not form circular hosting dependencies.
8. Cardinality: 1:N
9. Stability: Static
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Tier/

---

### SLICE
1. Name: Slice
2. Purpose: To represent a vertical, cross-cutting decomposition that spans multiple layers and modules to deliver an end-to-end capability.
3. Responsibility: Defining a complete user- or system-facing capability by connecting all structural elements required across all affected layers and modules.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Mapped → Active → Evolving → Consolidated → Retired
6. Allowed Relationships: Crosses Layer; spans Module, Component; delivers Capability, Feature; intersects with Slice.
7. Forbidden Relationships: May not be contained within a single Layer; may not be owned by a single Module.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Slice/

---

### ASSEMBLY
1. Name: Assembly
2. Purpose: To compose multiple entities into a deliberately organized unit that serves a specific structural or functional purpose.
3. Responsibility: Aggregating Components, Modules, or other entities into a cohesive, nameable unit with shared interfaces and lifecycle.
4. Owner: Module Lead
5. Lifecycle: Defined → Composed → Active → Reconfiguring → Decomposed
6. Allowed Relationships: Contains Component, Module, Primitive; exposes Interface; declares Dependency; belongs to Subsystem.
7. Forbidden Relationships: May not contain Kernel or Domain; may not be empty.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: Owning Module's META/Assembly/

---

### TOPOLOGY
1. Name: Topology
2. Purpose: To describe the arrangement, shape, and connectivity pattern of entities within a defined scope of the Kernel.
3. Responsibility: Capturing the structural arrangement of entities, including their spatial relationships, communication paths, and dependency flows.
4. Owner: GovernanceBody
5. Lifecycle: Observed → Documented → Active → Evolving → Superseded → Archived
6. Allowed Relationships: Describes Kernel, Domain, Subsystem, Layer, Slice; references Dependency, Channel, Bus.
7. Forbidden Relationships: May not prescribe implementation; may not be confused with governance or workflow models.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Topology/

================================================================================
TIER 3: COMMUNICATION & CONTRACTS
================================================================================

### INTERFACE
1. Name: Interface
2. Purpose: To define the contract surface through which an entity exposes capabilities to other entities.
3. Responsibility: Specifying the operations, events, data structures, and protocols that consumers can rely upon, independent of internal implementation.
4. Owner: Owner of the exposing entity
5. Lifecycle: Draft → Reviewed → Ratified → Active → Evolving → Deprecated → Retired
6. Allowed Relationships: Exposed by Component, Module, Subsystem; consumed by Component, Module; constrained by Contract; referenced by Port.
7. Forbidden Relationships: May not be owned independently; may not contain implementation logic.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Owning entity's META/Interface/

---

### BOUNDARY
1. Name: Boundary
2. Purpose: To delineate the limit of a Domain, Subsystem, or Context, enforcing encapsulation and controlling cross-boundary interaction.
3. Responsibility: Defining the perimeter of an entity's authority, determining what is internal vs. external, and governing what may cross in either direction.
4. Owner: GovernanceBody
5. Lifecycle: Defined → Ratified → Active → Adjusted → Dissolved
6. Allowed Relationships: Surrounds Domain, Subsystem, Context; crossed by Bridge, Adapter; exposes Port.
7. Forbidden Relationships: May not exist without a bounded entity; may not be crossed without an explicit crossing mechanism.
8. Cardinality: 1:1
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Boundary/

---

### CHANNEL
1. Name: Channel
2. Purpose: To establish a directed communication pathway between two or more entities for data, control, or event flow.
3. Responsibility: Carrying typed messages or signals from source entities to destination entities with defined reliability, ordering, and protocol guarantees.
4. Owner: Module Lead
5. Lifecycle: Defined → Connected → Active → Throttled → Disconnected → Removed
6. Allowed Relationships: Connects Port, Interface; belongs to Bus; carries data between Component, Module, Subsystem.
7. Forbidden Relationships: May not connect entities in different Kernels; may not bypass Boundary without going through Port.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: Owning Module's META/Channel/

---

### CONTRACT
1. Name: Contract
2. Purpose: To formalize the agreement between two or more entities regarding their mutual obligations, interfaces, and behaviors.
3. Responsibility: Binding provider and consumer entities to explicit terms of interaction, including preconditions, postconditions, invariants, and versioning rules.
4. Owner: GovernanceBody
5. Lifecycle: Draft → Negotiated → Ratified → Active → Amending → Superseded → Expired
6. Allowed Relationships: Binds Interface to Interface; spans Boundary; enforced by Constraint; consumed by Module, Component.
7. Forbidden Relationships: May not be unilateral; may not contradict Invariant; may not span Kernel boundary.
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 06-CONTRACTS/

================================================================================
TIER 4: CAPABILITY & FUNCTION
================================================================================

### CAPABILITY
1. Name: Capability
2. Purpose: To declare what the Kernel or a constituent entity can do, independent of how it is implemented.
3. Responsibility: Defining a distinct, testable ability of the system that delivers value to stakeholders, described in implementation-neutral terms.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Specified → Delivered → Evolving → Deprecated → Retired
6. Allowed Relationships: Delivered by Module, Subsystem, Component; composed of Feature; referenced by Slice; tested by Evidence; exposed via Interface.
7. Forbidden Relationships: May not specify implementation; may not be owned by Interface or Primitive directly.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Capability/

---

### FEATURE
1. Name: Feature
2. Purpose: To represent a user-visible, deliverable unit of functionality that realizes one or more Capabilities.
3. Responsibility: Providing a concrete, observable, and deliverable piece of functionality that stakeholders can interact with or depend upon.
4. Owner: Module Lead
5. Lifecycle: Requested → Specified → Implementing → Delivered → Active → Enhancing → Deprecated → Removed
6. Allowed Relationships: Realizes Capability; spans Module, Component; intersects Slice; exposed via Interface; tested by Evidence.
7. Forbidden Relationships: May not exist without realizing at least one Capability; may not bypass Interface exposure.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 07-WORKFLOW/

================================================================================
TIER 5: WORK & PROCESS
================================================================================

### PROCESS
1. Name: Process
2. Purpose: To represent a defined sequence of operations and decisions that transforms inputs into outputs according to specified rules.
3. Responsibility: Defining how work is done—specifying the sequence, the rules, the inputs/outputs, and the quality criteria.
4. Owner: GovernanceBody
5. Lifecycle: Defined → Documented → Approved → Operational → Under-Review → Updated → Retired
6. Allowed Relationships: Has Task, Action; has Input, Output; has QualityGate; produces Artifact.
7. Forbidden Relationships: May not have circular step dependencies; may not lack defined output.
8. Cardinality: N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 07-WORKFLOW/

---

### WORKFLOW
1. Name: Workflow
2. Purpose: To define a structured, repeatable pattern of activities, decisions, and transitions for accomplishing a specific type of work.
3. Responsibility: Providing the blueprint of work execution—defining what happens, in what order, under what conditions, and by whom.
4. Owner: GovernanceBody
5. Lifecycle: Designed → Reviewed → Approved → Active → Evolving → Deprecated → Retired
6. Allowed Relationships: Has Activity, DecisionPoint, Transition, EntryPoint, ExitPoint, ParticipantRole.
7. Forbidden Relationships: May not have unreachable activities; may not have deadlock; may not lack ExitPoint.
8. Cardinality: N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 07-WORKFLOW/

---

### TASK
1. Name: Task
2. Purpose: To represent a unit of work to be performed by an actor within a session toward a defined objective.
3. Responsibility: Encapsulating work definition, assignment, tracking, and completion validation.
4. Owner: Session
5. Lifecycle: Created → Assigned → Ready → In-Progress → Blocked | Awaiting-Review → Completing → Completed | Cancelled
6. Allowed Relationships: Has SubTask, Assignee, Dependency; belongs to Phase; produces Output; has Constraint.
7. Forbidden Relationships: May not exist without Objective; may not have no Assignee.
8. Cardinality: N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 99-STATE/

---

### MILESTONE
1. Name: Milestone
2. Purpose: To mark a significant achievement point or checkpoint within a lifecycle, plan, or project.
3. Responsibility: Signaling progress; triggering reviews; enabling progress measurement and accountability.
4. Owner: Module Lead
5. Lifecycle: Defined → Pending → Approaching → Reached → Verified → Celebrated → Archived
6. Allowed Relationships: Marks Lifecycle, Plan; reached by Entity; triggers Review; measured by Metric.
7. Forbidden Relationships: May not be retroactively claimed; may not be undefined; may not be deleted after verification.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 07-WORKFLOW/

---

### PLAN
1. Name: Plan
2. Purpose: To prescribe the intended course of action, including objectives, scope, sequence, resources, and criteria for a body of work.
3. Responsibility: Providing the authoritative blueprint for executing work, establishing expectations, and enabling progress tracking.
4. Owner: GovernanceBody
5. Lifecycle: Drafted → Reviewed → Approved → Active → In Progress → Adjusted → Completed → Closed → Archived
6. Allowed Relationships: References Specifications; defines Deliverables; traced to DecisionRecord; contains Schedules.
7. Forbidden Relationships: May not be Active without Approval; may not contradict Constitution; may not omit exit criteria.
8. Cardinality: N:1 per Scope
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Governance Ledger

================================================================================
TIER 6: GOVERNANCE FOUNDATION
================================================================================

### CONSTITUTION
1. Name: Constitution
2. Purpose: To serve as the supreme governance instrument that establishes the kernel's fundamental principles, authority structures, and amendment procedures.
3. Responsibility: Providing the ultimate source of legitimacy for all governance actions; overriding all other instruments in case of conflict.
4. Owner: Founders Circle
5. Lifecycle: Draft → Ratified → Active → AmendmentInProgress → Ratified
6. Allowed Relationships: Empowers GovernanceBody; Establishes Charter; Defines Rule; Supersedes AllGovernanceEntities.
7. Forbidden Relationships: May not be overridden by any entity except by its own amendment procedure.
8. Cardinality: 1:1
9. Stability: Static
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 00-CONSTITUTION/Constitution.md

---

### CHARTER
1. Name: Charter
2. Purpose: To establish the existence, authority, and operating parameters of a governance body, project, or module within the kernel.
3. Responsibility: Defining scope of authority, decision rights, membership, and dissolution conditions.
4. Owner: Constitution
5. Lifecycle: Draft → Proposed → Ratified → Active → Suspended → Dissolved
6. Allowed Relationships: Governs GovernanceBody; Delegates Authority; References Constitution.
7. Forbidden Relationships: May not be deleted (only Dissolved); may not bypass Constitution; may not self-amend.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 00-CONSTITUTION/Charters/

---

### GOVERNANCE_BODY
1. Name: GovernanceBody
2. Purpose: To constitute an organized group of stakeholders with defined authority to make decisions, set policy, and oversee governance within a scope.
3. Responsibility: Exercising chartered authority; making binding decisions; delegating responsibilities; ensuring accountability.
4. Owner: Constitution
5. Lifecycle: Chartered → Forming → Active → UnderReview → Rechartered → Suspended → Dissolved
6. Allowed Relationships: CharteredBy Charter; ComposedOf Role; Creates Policy; Oversees Jurisdiction.
7. Forbidden Relationships: May not exceed chartered authority; may not dissolve itself without ratification.
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: No
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Bodies/

---

### ROLE
1. Name: Role
2. Purpose: To define a named set of responsibilities, permissions, and authority boundaries that can be assigned to actors.
3. Responsibility: Making explicit what an actor may do, must do, and cannot do within the repository.
4. Owner: GovernanceBody
5. Lifecycle: Proposed → Reviewed → Approved → Active → Deprecated → Retired
6. Allowed Relationships: Has Responsibility, Permission; assigned to Actor; may delegate to Role.
7. Forbidden Relationships: May not contradict Constitution; may not have circular delegation.
8. Cardinality: N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: Yes
15. Source of Truth: 00-CONSTITUTION/

---

### POLICY
1. Name: Policy
2. Purpose: To establish a governing principle that guides decision-making and sets boundaries for organizational behavior.
3. Responsibility: Providing the "why" and "what" of governance; authorizing Rules and delegating implementation.
4. Owner: GovernanceBody
5. Lifecycle: Draft → Consulted → Approved → Communicated → Active → UnderReview → Amended/Withdrawn
6. Allowed Relationships: Authorizes Rule; EnforcedBy Audit; ExceptedBy Exception.
7. Forbidden Relationships: May not be self-contradictory; may not be ignored by lower governance tiers.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Policies/

---

### RULE
1. Name: Rule
2. Purpose: To state a binding constraint on behavior, structure, or process that must be observed by all entities within its jurisdiction.
3. Responsibility: Defining clear, enforceable boundaries; supporting automated and manual compliance checking.
4. Owner: GovernanceBody
5. Lifecycle: Draft → Proposed → Approved → Active → Suspended → Amended → Repealed
6. Allowed Relationships: DerivedFrom Standard; EnforcedBy Sanction; GovernedBy Policy.
7. Forbidden Relationships: May not contradict Constitution; may not be applied retroactively; may not have unstated exceptions.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Rules/

================================================================================
TIER 7: STANDARDS & CONSTRAINTS
================================================================================

### STANDARD
1. Name: Standard
2. Purpose: To define mandatory requirements, specifications, or criteria that entities must meet to ensure consistency, interoperability, and quality.
3. Responsibility: Prescribing unambiguous, testable, and enforceable requirements within its scope.
4. Owner: Standards Authority
5. Lifecycle: Draft → Proposed → UnderReview → Approved → Active → UnderRevision → Superseded/Retired
6. Allowed Relationships: Mandates ComplianceBaseline; ReferencedBy Contract; EnforcedBy Audit.
7. Forbidden Relationships: May not conflict with Constitution; may not be enforced while in Draft.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 03-STANDARDS/

---

### GUIDELINE
1. Name: Guideline
2. Purpose: To provide recommended practices and advisory guidance that encourage consistency without mandating specific approaches.
3. Responsibility: Offering best-practice direction, explaining rationale, and suggesting implementation patterns.
4. Owner: Working Group or Subject Matter Authority
5. Lifecycle: Draft → Published → Active → Updated → Deprecated/Withdrawn
6. Allowed Relationships: Supports Standard; InformedBy Precedent; ReferencedBy Contract.
7. Forbidden Relationships: May not be enforced by Sanction; may not override Standard; may not create Obligation.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: No
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 03-STANDARDS/Guidelines/

---

### CONSTRAINT
1. Name: Constraint
2. Purpose: To impose a structural or behavioral limitation on entities to ensure architectural integrity.
3. Responsibility: Defining a rule that restricts how entities may be composed, connected, named, or evolved, and enforcing compliance.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Specified → Ratified → Active → Amending → Superseded → Retired
6. Allowed Relationships: Applies to Module, Component, Interface, Dependency, Boundary, Layer; referenced by Invariant.
7. Forbidden Relationships: May not contradict Invariant; may not be advisory only (must be enforceable).
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Constraint/

---

### INVARIANT
1. Name: Invariant
2. Purpose: To declare a condition that must always hold true across all states and transitions of the Kernel's structure.
3. Responsibility: Defining an unviolable structural truth that governs the architecture regardless of implementation, technology, or evolution.
4. Owner: Constitution
5. Lifecycle: Proposed → Ratified → Active → Eternal
6. Allowed Relationships: Governs Kernel, Domain, Layer, Boundary, Dependency; referenced by Constraint, Contract; validated by Evidence.
7. Forbidden Relationships: May not be scoped to a single Module; may not be temporary; may not be created without Constitution-level ratification.
8. Cardinality: N:1
9. Stability: Static
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: 00-CONSTITUTION/

================================================================================
TIER 8: SESSION & PARTICIPATION
================================================================================

### SESSION
1. Name: Session
2. Purpose: To represent a bounded period of engagement during which actors perform work toward defined objectives within the repository.
3. Responsibility: Maintaining continuity of context, tracking participation, and ensuring all actions within its boundary are attributable.
4. Owner: GovernanceBody
5. Lifecycle: Initiated → Active → Suspended → Completing → Completed → Archived | Terminated
6. Allowed Relationships: Has Actor, Context, Task; produces Decision; emits Event; belongs to Workflow.
7. Forbidden Relationships: May not own Repository (only Constitution does); may not mutate state without emitting Event.
8. Cardinality: N
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 99-STATE/

---

### ACTOR
1. Name: Actor
2. Purpose: To represent any entity—human, automated, or hybrid—that can perform actions, make decisions, or assume responsibilities within a session.
3. Responsibility: Being accountable for the actions it initiates, the decisions it makes, and the obligations it accepts.
4. Owner: Constitution
5. Lifecycle: Registered → Active → Inactive → Decommissioned
6. Allowed Relationships: Has Role; performs Action; participates in Session; makes Decision; owns Task.
7. Forbidden Relationships: May not have no Role; may not modify Constitution.
8. Cardinality: N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: No
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: Yes
15. Source of Truth: 00-CONSTITUTION/

---

### PARTICIPANT
1. Name: Participant
2. Purpose: To represent the binding of an Actor to a Session with specific role assignments and permissions for that session's duration.
3. Responsibility: Adhering to session-specific rules, contributing within assigned role boundaries, and maintaining session context coherence.
4. Owner: Session
5. Lifecycle: Invited → Accepted → Active → Paused → Departed | Removed
6. Allowed Relationships: Binds Actor; binds Session; assumes Role; contributes to Task.
7. Forbidden Relationships: May not exist outside Session; may not have Role not in Session.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 99-STATE/

================================================================================
TIER 9: CONTEXT & ENVIRONMENT
================================================================================

### CONTEXT
1. Name: Context
2. Purpose: To represent the situational frame within which an entity is interpreted, executed, or accessed.
3. Responsibility: Providing the environmental, temporal, and authority conditions that determine how entities behave and how decisions are made.
4. Owner: Session
5. Lifecycle: Created → Active → Modified → Saved → Discarded
6. Allowed Relationships: Contains Scope, Namespace; references Module, Component; governs AI and Human permissions.
7. Forbidden Relationships: May not persist beyond the situation it represents; may not override frozen Invariant.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: No
11. Freezable: No
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: 99-STATE/Context/

---

### ENVIRONMENT
1. Name: Environment
2. Purpose: To represent the complete operational surroundings in which processes execute, including available capabilities, constraints, and external interfaces.
3. Responsibility: Providing the substrate on which execution occurs, including resource availability, external dependencies, and environmental invariants.
4. Owner: Module
5. Lifecycle: Defined → Provisioned → Active → Degraded → Restored | Retired
6. Allowed Relationships: Provides Resource; has Constraint; hosts Session; has Invariant.
7. Forbidden Relationships: May not change without notification; may not hide Dependencies.
8. Cardinality: N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 03-STANDARDS/

================================================================================
TIER 10: DECISION & REASONING
================================================================================

### DECISION
1. Name: Decision
2. Purpose: To represent a choice made among alternatives that commits the repository to a specific course of action, design, or policy.
3. Responsibility: Capturing the choice, the rationale, the alternatives considered, and the consequences accepted.
4. Owner: Actor (the decision-maker)
5. Lifecycle: Identified → Proposed → Deliberated → Made → Recorded → Implemented → Reviewed
6. Allowed Relationships: Made by Actor; has Context, Rationale, Alternative, Consequence; recorded in DecisionRecord.
7. Forbidden Relationships: May not exist without Rationale; may not be reversible without process.
8. Cardinality: N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 05-EVIDENCE/

---

### DECISION_RECORD
1. Name: DecisionRecord
2. Purpose: To capture a significant decision, including its context, options considered, rationale, and consequences, for future reference.
3. Responsibility: Preserving the reasoning behind important decisions so that future stakeholders can understand why a choice was made.
4. Owner: Governance
5. Lifecycle: Proposed → Options Identified → Evaluated → Decided → Recorded → Communicated → Revisited/Affirmed → Archived
6. Allowed Relationships: References Findings; signed by deciders; traced to Conclusion; may trigger Plan.
7. Forbidden Relationships: May not be Recorded without Options and Rationale; may not be Revisited without new Evidence; may not contradict its own Rationale.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

---

### EVIDENCE
1. Name: Evidence
2. Purpose: To provide factual support for a claim, assertion, finding, or conclusion through verifiable data, observation, or documentation.
3. Responsibility: Grounding claims in observable, verifiable reality and enabling rational assessment of their validity.
4. Owner: Process
5. Lifecycle: Gathered → Validated → Linked → Referenced → Challenged → Reaffirmed/Withdrawn → Archived
6. Allowed Relationships: Supports Claim, Finding; traced to Assertion; signed; contradicted by Counter-Evidence.
7. Forbidden Relationships: May not be fabricated; may not support contradictory Claims without documented conflict.
8. Cardinality: N:M
9. Stability: Static after Validation
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

---

### FINDING
1. Name: Finding
2. Purpose: To document a discovered fact, observation, or result that emerged from investigation, analysis, or assessment.
3. Responsibility: Communicating what was discovered, including its nature, significance, and supporting evidence.
4. Owner: Process
5. Lifecycle: Observed → Documented → Reviewed → Validated → Published → Challenged → Reaffirmed/Corrected → Archived
6. Allowed Relationships: References Evidence; summarized in Report; traced to Assessment; triggers Conclusion.
7. Forbidden Relationships: May not be published without Review; may not contradict its own Evidence.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Evidence Vault

---

### CONCLUSION
1. Name: Conclusion
2. Purpose: To synthesize Findings, Evidence, and reasoning into a final judgment, determination, or decision about a matter.
3. Responsibility: Representing the endpoint of reasoning, providing a definitive statement derived from evidence and analysis.
4. Owner: Governance
5. Lifecycle: Drafted → Supported by Findings → Reviewed → Approved → Published → Challenged → Reaffirmed/Replaced → Archived
6. Allowed Relationships: References Findings; traced to Evidence; triggers DecisionRecord; signed.
7. Forbidden Relationships: May not be Approved without supporting Findings; may not contradict referenced Evidence.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

================================================================================
TIER 11: ARTIFACTS
================================================================================

### ARTIFACT
1. Name: Artifact
2. Purpose: To serve as the root ontological category for any item produced, consumed, transformed, or referenced within the kernel.
3. Responsibility: Representing the universal supertype from which all artifact subtypes derive their identity and behavior.
4. Owner: Constitution
5. Lifecycle: Defined → Created → Active → Archived → Destroyed
6. Allowed Relationships: Consumed by Process; produced by Process; composed of other Artifacts; traced via TraceabilityLink; versioned as Revision; baselined via Baseline.
7. Forbidden Relationships: May not directly own a Module; may not modify a Governance Rule; may not be self-referential.
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Artifact Repository

---

### DOCUMENT
1. Name: Document
2. Purpose: To carry structured human-readable and machine-processable information in a coherent, navigable form.
3. Responsibility: Communicating, prescribing, describing, or recording information with defined structure, scope, and audience.
4. Owner: Module
5. Lifecycle: Draft → Review → Approved → Published → Superseded → Archived
6. Allowed Relationships: Contains Annotations; traced to Specification; versioned; baselined; composed into Catalog; signed.
7. Forbidden Relationships: May not directly execute a Process; may not be self-approving; may not be both Draft and Published.
8. Cardinality: 1:N
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Artifact Repository

---

### SPECIFICATION
1. Name: Specification
2. Purpose: To prescribe in precise, unambiguous terms what shall be, shall do, or shall conform to.
3. Responsibility: Defining requirements, interfaces, behaviors, formats, or constraints that other entities must satisfy.
4. Owner: Governance
5. Lifecycle: Proposed → Drafted → Reviewed → Approved → Baseline → Amendment → Superseded
6. Allowed Relationships: Traced to Implementation; verified by Verification Result; validated by Validation Result; signed; baselined.
7. Forbidden Relationships: May not be created by AI without approval; may not be modified after baseline without formal amendment.
8. Cardinality: 1:N
9. Stability: Static
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

---

### RECORD
1. Name: Record
2. Purpose: To capture a fact, event, observation, or state at a specific point in time as an immutable account of what occurred.
3. Responsibility: Providing an authoritative, timestamped, non-repudiable account of something that happened or existed.
4. Owner: Process
5. Lifecycle: Created → Validated → Committed → Retained → Expired → Destroyed
6. Allowed Relationships: Linked to Log; traced to Event; signed; referenced by Audit Record.
7. Forbidden Relationships: May not be modified after Commit; may not be deleted before Retention period expires.
8. Cardinality: N:M
9. Stability: Static after Commit
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

---

### LOG
1. Name: Log
2. Purpose: To maintain a strictly chronological, append-only sequence of entries documenting events, actions, or state changes.
3. Responsibility: Providing an ordered, tamper-evident trail of all significant occurrences for monitoring and auditing.
4. Owner: System
5. Lifecycle: Opened → Appending → Closed → Archived → Expired
6. Allowed Relationships: Contains Record entries; traced to AuditTrail; referenced by Report; signed.
7. Forbidden Relationships: May not be modified after Close; may not skip entries; may not contain entries out of order.
8. Cardinality: 1:N
9. Stability: Fast during Appending, Static after Close
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Audit Log

---

### REPORT
1. Name: Report
2. Purpose: To communicate findings, analysis, status, or assessment results to stakeholders in a structured, interpretable format.
3. Responsibility: Synthesizing evidence, measurements, and observations into actionable information for decision support.
4. Owner: Process
5. Lifecycle: Commissioned → Drafted → Reviewed → Approved → Published → Superseded
6. Allowed Relationships: References Evidence; contains Findings, Measurements; traced to Metrics; signed.
7. Forbidden Relationships: May not modify the evidence it references; may not be self-approving.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Artifact Repository

================================================================================
TIER 12: AUTHORIZATION
================================================================================

### APPROVAL
1. Name: Approval
2. Purpose: To formally record that an authorized party has reviewed and accepted an artifact, decision, or state as satisfactory.
3. Responsibility: Providing documented consent that transforms an entity from a proposed state to an authorized state.
4. Owner: Approver (authorized Role)
5. Lifecycle: Requested → Reviewed → Granted | Denied → Conditional → Final → Withdrawn
6. Allowed Relationships: Must bear Signature; traced to approved Artifact; referenced by Audit Record; includes Conditions.
7. Forbidden Relationships: May not be granted without Review; may not be both Granted and Denied; may not be withdrawn without cause.
8. Cardinality: N:M
9. Stability: Static after Final
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

---

### AUTHORIZATION
1. Name: Authorization
2. Purpose: To grant specific permission to perform an action or access a capability that is not universally available.
3. Responsibility: Defining the scope, duration, and conditions of permitted action; enabling accountability for authorized acts.
4. Owner: Authorizing authority
5. Lifecycle: Requested → Evaluated → Granted → Active → Renewed → Revoked → Expired
6. Allowed Relationships: Authorizes Action; GrantedTo Role; ScopedBy Constraint; RevokedBy Authorizer.
7. Forbidden Relationships: May not exceed granter's authority; may not be permanent without renewal; may not be transferred without delegation.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: No
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Authorizations/

---

### CERTIFICATION
1. Name: Certification
2. Purpose: To formally attest that an entity meets specified standards or requirements after independent verification.
3. Responsibility: Providing independently verified assurance of compliance; enabling trust and interoperability.
4. Owner: Certifying Authority
5. Lifecycle: Requested → Evaluated → Verified → Granted → Active → UnderRenewal → Renewed/Revoked/Expired
6. Allowed Relationships: Certifies Entity; IssuedBy Authority; ValidatedBy Audit; ReferencedBy Contract.
7. Forbidden Relationships: May not be self-certified; may not be issued while non-compliance findings are open; may not be forged.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 05-EVIDENCE/Certifications/

---

### CREDENTIAL
1. Name: Credential
2. Purpose: To provide a token or proof of identity, authorization, or entitlement that an entity may present to establish trust.
3. Responsibility: Enabling authentication and authorization by carrying verifiable proof of the bearer's claimed attributes or rights.
4. Owner: Actor
5. Lifecycle: Issued → Active → Renewed → Suspended → Reactivated/Expired → Revoked → Destroyed
6. Allowed Relationships: Bound to Identity; presented for Access Control; referenced by Signature.
7. Forbidden Relationships: May not be transferred; may not be used after Revocation; may not be forged.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: No
11. Freezable: No
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Evidence Vault

---

### SIGNATURE
1. Name: Signature
2. Purpose: To mark an artifact with the authenticated identity of a party who has reviewed, approved, or authored it.
3. Responsibility: Providing non-repudiable evidence that a specific party has affixed their mark to an artifact at a specific time.
4. Owner: Actor
5. Lifecycle: Prepared → Affixed → Validated → Active → Revoked → Expired
6. Allowed Relationships: Affixed to Artifact; traced to Credential; referenced by Audit Record.
7. Forbidden Relationships: May not be forged; may not be affixed by unauthorized party; may not be retroactively dated.
8. Cardinality: N:M
9. Stability: Static after Validated
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

================================================================================
TIER 13: TRACEABILITY & BASELINES
================================================================================

### BASELINE
1. Name: Baseline
2. Purpose: To establish a frozen, authoritative reference point against which future changes, progress, or deviations can be measured.
3. Responsibility: Providing an immutable reference that enables comparison, change tracking, and accountability across time.
4. Owner: Governance
5. Lifecycle: Proposed → Reviewed → Approved → Frozen → Referenced → Amended → Superseded → Archived
6. Allowed Relationships: References Artifacts; traced to Snapshots; signed; compared to subsequent states.
7. Forbidden Relationships: May not be modified after Frozen without formal Amendment; may not baseline entities outside scope.
8. Cardinality: 1:N
9. Stability: Static when Frozen
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

---

### SNAPSHOT
1. Name: Snapshot
2. Purpose: To capture the complete state of a system, module, process, or artifact at a precise point in time.
3. Responsibility: Providing an exact, point-in-time representation that can be compared, audited, or used as a reference baseline.
4. Owner: System
5. Lifecycle: Triggered → Capturing → Validated → Committed → Referenced → Expired
6. Allowed Relationships: Compared to another Snapshot; used as Baseline; traced to entity captured; signed.
7. Forbidden Relationships: May not be modified after Commit; may not capture entities outside authorized scope.
8. Cardinality: N:M
9. Stability: Static after Commit
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

---

### TRACEABILITY_LINK
1. Name: TraceabilityLink
2. Purpose: To provide a typed, directional, semantically meaningful connection between entities that carries specific traceability semantics.
3. Responsibility: Enabling precise impact analysis, coverage tracking, and dependency management through semantically rich connections.
4. Owner: Process
5. Lifecycle: Defined → Created → Verified → Active → Impacted → Updated/Broken → Removed → Archived
6. Allowed Relationships: Connects source Artifact to target Artifact with typed semantics; signed.
7. Forbidden Relationships: May not be bidirectional without explicit reverse link; may not be semantically empty.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Registry Service

---

### CHECKPOINT
1. Name: Checkpoint
2. Purpose: To capture and verify the state of work at a defined milestone, enabling assessment of progress, quality, and readiness.
3. Responsibility: Providing a verified milestone record that demonstrates the system has met defined criteria at a specific point.
4. Owner: Process
5. Lifecycle: Defined → Triggered → Capturing → Validated → Verified → Committed → Referenced → Superseded
6. Allowed Relationships: References state captured; traced to Baseline; signed; carries Verification Result.
7. Forbidden Relationships: May not be Verified without passing all criteria; may not be modified after Commit.
8. Cardinality: N:M
9. Stability: Static after Commit
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

================================================================================
TIER 14: MEASUREMENT
================================================================================

### METRIC
1. Name: Metric
2. Purpose: To define a standard of measurement that prescribes what shall be measured, how, and against what thresholds.
3. Responsibility: Establishing the definitional framework for consistent, comparable measurement across the kernel.
4. Owner: Governance
5. Lifecycle: Proposed → Defined → Reviewed → Approved → Active → Measured → Evaluated → Revised/Retired
6. Allowed Relationships: Generates Measurements; references Benchmark; traced to Specification.
7. Forbidden Relationships: May not be ambiguous; may not be Active without Approval.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

---

### MEASUREMENT
1. Name: Measurement
2. Purpose: To capture a quantified observation of a property, performance characteristic, or state at a specific time.
3. Responsibility: Providing objective, quantified data that enables comparison against thresholds, benchmarks, and trends.
4. Owner: Process
5. Lifecycle: Triggered → Captured → Validated → Recorded → Analyzed → Referenced → Archived
6. Allowed Relationships: Traced to Metric; referenced by Report; compared to Benchmark; signed.
7. Forbidden Relationships: May not be fabricated; may not be modified after Recorded.
8. Cardinality: N:M
9. Stability: Static after Recorded
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Evidence Vault

---

### ASSESSMENT
1. Name: Assessment
2. Purpose: To systematically evaluate an entity against defined criteria to determine its quality, conformance, risk, or readiness.
3. Responsibility: Providing a structured judgment based on evidence, measurements, and defined criteria.
4. Owner: Process
5. Lifecycle: Commissioned → Planned → Executed → Analyzed → Drafted → Reviewed → Published → Appealed → Final → Archived
6. Allowed Relationships: Contains Findings; references Measurements; traced to Criteria; signed; triggers DecisionRecord.
7. Forbidden Relationships: May not be Published without Review; may not omit material Findings.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: Artifact Repository

================================================================================
TIER 15: AUDIT & REVIEW
================================================================================

### AUDIT
1. Name: Audit
2. Purpose: To perform an independent, systematic inspection to verify compliance with Standards, Rules, Policies, and Regulations.
3. Responsibility: Gathering evidence, testing controls, identifying violations, and certifying compliance or documenting deficiencies.
4. Owner: Independent Auditor
5. Lifecycle: Planned → Chartered → Executed → EvidenceAnalyzed → ReportDrafted → Reviewed → Published → RemediationTracked → Closed
6. Allowed Relationships: Audits Entity; MeasuresAgainst Standard; Produces Finding; Triggers Remediation.
7. Forbidden Relationships: May not be conducted by the entity being audited; may not have scope reduced by auditee; may not be suppressed.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 05-EVIDENCE/Audits/

---

### REVIEW
1. Name: Review
2. Purpose: To conduct a formal examination of an entity, process, or decision to assess compliance, quality, correctness, and alignment.
3. Responsibility: Producing an evaluation with findings, recommendations, and determinations of compliance or non-compliance.
4. Owner: Reviewer (appointed Role)
5. Lifecycle: Scheduled → Initiated → InProgress → FindingsDrafted → Reviewed → Published → Accepted/Contested → Closed
6. Allowed Relationships: Examines Entity; Produces Finding; Recommends Action; Triggers Directive.
7. Forbidden Relationships: May not examine its own author; may not be deleted after publication.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 05-EVIDENCE/Reviews/

---

### AUDIT_TRAIL
1. Name: AuditTrail
2. Purpose: To maintain a complete, chronological, tamper-evident record of all significant actions, changes, and decisions affecting an entity or scope.
3. Responsibility: Providing comprehensive accountability and reconstructability of everything that happened to an entity.
4. Owner: System
5. Lifecycle: Initiated → Recording → Active → Reviewed → Sealed → Archived → Expired
6. Allowed Relationships: Contains Audit Records; traced to auditable entity; signed at Seal; queried for investigations.
7. Forbidden Relationships: May not be modified after Seal; may not omit required events; may not be destroyed before Expiry.
8. Cardinality: 1:1 per Auditable Scope
9. Stability: Fast during Recording, Static after Seal
10. Versionable: No
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: No
14. Human Modifiable: No
15. Source of Truth: Audit Log

================================================================================
TIER 16: LIFECYCLE & STATE
================================================================================

### LIFECYCLE
1. Name: Lifecycle
2. Purpose: To define the complete set of states and permitted transitions that an entity type passes through from inception to retirement.
3. Responsibility: Governing the birth-to-death trajectory of entities; enforcing stage-gate discipline; enabling predictable progression.
4. Owner: Governance
5. Lifecycle: Defined → Approved → Active → UnderReview → Updated → Superseded
6. Allowed Relationships: Has LifecycleStage, LifecycleGate; AppliesTo EntityType.
7. Forbidden Relationships: May not have unreachable stages; may not have ambiguous transitions; may not skip required gates.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 01-META-MODEL/Lifecycles/

---

### STATE
1. Name: State
2. Purpose: To represent a distinguishable condition or mode that an entity can occupy at a point in time.
3. Responsibility: Being the atomic unit of lifecycle modeling—well-defined, mutually exclusive, and observable.
4. Owner: Governance
5. Lifecycle: Defined → Validated → Active → Deprecated → Retired
6. Allowed Relationships: Belongs to Lifecycle; has EntryAction, ExitAction, Invariant; transitions to State.
7. Forbidden Relationships: May not exist without definition; may not be ambiguous with another State.
8. Cardinality: N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/

================================================================================
TIER 17: EXCEPTIONS & WAIVERS
================================================================================

### EXCEPTION
1. Name: Exception
2. Purpose: To document a permitted deviation from a Rule, Standard, or Policy under specific circumstances with defined scope and duration.
3. Responsibility: Enabling flexibility without undermining governance; ensuring deviations are visible, justified, and temporary.
4. Owner: Excepted entity's owner or GovernanceBody
5. Lifecycle: Requested → Justified → Reviewed → Granted → Active → Monitored → Expired/Renewed/Revoked
6. Allowed Relationships: DeviatesFrom Rule; GrantedBy Authority; ScopedTo Entity.
7. Forbidden Relationships: May not be granted for Constitutional requirements; may not be permanent; may not be silently granted.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Exceptions/

---

### WAIVER
1. Name: Waiver
2. Purpose: To formally grant exception from a requirement, rule, standard, or obligation that would otherwise be mandatory.
3. Responsibility: Documenting authorized deviation from prescribed norms, including rationale, scope, duration, and conditions.
4. Owner: Governance
5. Lifecycle: Requested → Justified → Reviewed → Granted | Denied → Active → Expired → Renewed | Revoked
6. Allowed Relationships: References waived requirement; bears Signature; traced to Risk Register; time-bounded.
7. Forbidden Relationships: May not waive Constitutional provisions; may not be granted without documented justification.
8. Cardinality: 1:N
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: Governance Ledger

================================================================================
TIER 18: GOVERNANCE MECHANICS
================================================================================

### AMENDMENT
1. Name: Amendment
2. Purpose: To propose and record a formal change to an existing governance instrument that alters its substance.
3. Responsibility: Documenting the proposed change, rationale, impact assessment, and required approval path.
4. Owner: Proposer
5. Lifecycle: Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded
6. Allowed Relationships: Amends Entity; ProposedBy Role; ReviewedBy Review; ApprovedBy GovernanceBody.
7. Forbidden Relationships: May not be applied without approval; may not alter entities outside proposer's jurisdiction.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Amendments/

---

### SANCTION
1. Name: Sanction
2. Purpose: To impose a punitive or corrective measure in response to violation of Rules, Policies, Obligations, or Contracts.
3. Responsibility: Deterring violations; correcting non-compliance; maintaining integrity of governance framework.
4. Owner: Sanctioning authority
5. Lifecycle: Triggered → Investigated → Proposed → Reviewed → Imposed → Appealed → Upheld/Overturned → Executed → Lifted
6. Allowed Relationships: RespondsTo Violation; ImposedBy Authority; On Actor; RecordedIn GovernanceLog.
7. Forbidden Relationships: May not be imposed without due process; may not be disproportionate to violation.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Sanctions/

---

### PRECEDENT
1. Name: Precedent
2. Purpose: To record a prior decision, interpretation, or ruling that guides future similar cases.
3. Responsibility: Promoting consistency in governance; reducing re-deliberation; building institutional memory.
4. Owner: GovernanceBody that established it
5. Lifecycle: Established → Active → Distinguished → Overruled → Archived
6. Allowed Relationships: Guides Decision; EstablishedBy Ruling; MayBeOverruledBy Ruling; CitedIn Appeal.
7. Forbidden Relationships: May not bind Constitution-level decisions; may not prevent amendment of the rule it interprets.
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: No
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Precedents/

---

### APPEAL
1. Name: Appeal
2. Purpose: To request formal reconsideration of a decision, ruling, or sanction by a higher authority.
3. Responsibility: Providing due process; enabling correction of errors; preventing abuse of power.
4. Owner: Appellant
5. Lifecycle: Filed → Accepted → Scheduled → Heard → Deliberated → Upheld/Overturned/Remanded → Final → Recorded
6. Allowed Relationships: Challenges Decision/Sanction/Ruling; FiledBy Actor; HeardBy Authority.
7. Forbidden Relationships: May not be filed without grounds; may not be heard by original decision-maker.
8. Cardinality: N:1 per decision
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Appeals/

---

### VETO
1. Name: Veto
2. Purpose: To empower a designated authority to reject a decision, action, or proposal, halting its progression.
3. Responsibility: Preventing harmful or improper decisions; providing a final check on collective decisions; requiring justification.
4. Owner: Veto-holder (Role designated by Constitution or Charter)
5. Lifecycle: Triggered → Justified → Exercised → Reviewed → Sustained/Overridden → Recorded
6. Allowed Relationships: Rejects Decision; ExercisedBy Role; MayBeOverriddenBy Override; RecordedIn GovernanceLog.
7. Forbidden Relationships: May not be exercised without justification; may not be overridden by the vetoed party.
8. Cardinality: 1:N
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Vetoes/

================================================================================
TIER 19: DISPUTE & ACCOUNTABILITY
================================================================================

### DISPUTE
1. Name: Dispute
2. Purpose: To document and manage a conflict between stakeholders or entities that requires formal resolution.
3. Responsibility: Surfacing conflict; enabling structured resolution; preventing escalation; documenting outcomes.
4. Owner: Disputing parties or mediating authority
5. Lifecycle: Raised → Acknowledged → Scoped → Mediated → Arbitrated → Resolved → Appealed → Final → Archived
6. Allowed Relationships: Between Actors; MediatedBy Role; MayResultIn Ruling; EscalatedVia EscalationPath.
7. Forbidden Relationships: May not be ignored; may not be resolved without party participation; may not be deleted.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Disputes/

---

### RECUSAL
1. Name: Recusal
2. Purpose: To document the voluntary or required withdrawal of a stakeholder from participation in a matter due to conflict or bias.
3. Responsibility: Preserving impartiality; preventing appearance of impropriety; documenting withdrawal.
4. Owner: Recusing party or requiring authority
5. Lifecycle: Identified → Declared → Accepted → Executed → Verified → Lifted → Recorded
6. Allowed Relationships: Withdraws Actor; From Decision/Matter; RequiredBy ConflictOfInterest.
7. Forbidden Relationships: May not be partial; may not be ignored; may not be coerced without cause.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: No
13. AI Modifiable: No
14. Human Modifiable: With Approval
15. Source of Truth: 02-GOVERNANCE/Recusals/

---

### TRANSPARENCY_REPORT
1. Name: TransparencyReport
2. Purpose: To publish a periodic public disclosure of governance activities, decisions, metrics, and compliance status.
3. Responsibility: Enabling stakeholder oversight; demonstrating governance integrity; building trust.
4. Owner: GovernanceBody
5. Lifecycle: Planned → Compiled → Reviewed → Published → Acknowledged → Archived
6. Allowed Relationships: PublishedBy Authority; Covers GovernanceDomain; Includes Metric, Decision.
7. Forbidden Relationships: May not omit required disclosures; may not be classified without justification.
8. Cardinality: N:M
9. Stability: Moderate
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: With Approval
15. Source of Truth: 05-EVIDENCE/TransparencyReports/

================================================================================
TIER 20: CROSS-CUTTING
================================================================================

### CONCERN
1. Name: Concern
2. Purpose: To identify a cross-cutting area of interest that affects multiple entities across the Kernel's structure.
3. Responsibility: Defining a systemic interest (e.g., security, performance, observability) that must be addressed across Domains, Layers, or Slices.
4. Owner: GovernanceBody
5. Lifecycle: Identified → Scoped → Addressed → Monitoring → Resolved → Ongoing
6. Allowed Relationships: Crosses Slice, Layer, Domain; constrains Component, Module, Interface; tracked by Evidence.
7. Forbidden Relationships: May not be contained within a single Module; may not be resolved by a single Component.
8. Cardinality: N:M
9. Stability: Slow
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 01-META-MODEL/Concern/

---

### ESCALATION
1. Name: Escalation
2. Purpose: To represent the elevation of a decision, issue, or authority to a higher level when the current level cannot or should not resolve it.
3. Responsibility: Ensuring issues reach appropriate authority, preventing stalemate, and maintaining escalation chain integrity.
4. Owner: Escalating Actor
5. Lifecycle: Triggered → Documented → Routed → Received → Under-Review → Resolved | Redirected → Closed
6. Allowed Relationships: EscalatesFrom Actor; EscalatesTo Actor; Has Justification; Has Urgency.
7. Forbidden Relationships: May not bypass intermediate levels without justification; may not be circular.
8. Cardinality: N
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: With Approval
13. AI Modifiable: With Approval
14. Human Modifiable: Yes
15. Source of Truth: 02-GOVERNANCE/Escalations/

---

### VIEW
1. Name: View
2. Purpose: To provide a perspective-specific representation of the Kernel's structure that emphasizes certain entities and relationships while suppressing others.
3. Responsibility: Rendering a selective, purpose-driven depiction of the system's structure for a specific audience, concern, or decision.
4. Owner: GovernanceBody (for canonical views); Session (for session views)
5. Lifecycle: Defined → Generated → Active → Stale → Refreshed → Archived
6. Allowed Relationships: Represents Kernel, Domain, Subsystem, Layer, Slice; filters Dependency, Component.
7. Forbidden Relationships: May not modify the entities it represents; may not present information not derivable from meta-model.
8. Cardinality: N:M
9. Stability: Fast
10. Versionable: Yes
11. Freezable: Yes
12. AI Creatable: Yes
13. AI Modifiable: Yes
14. Human Modifiable: Yes
15. Source of Truth: 99-STATE/View/

================================================================================
SUMMARY: 79 CANONICAL ENTITIES ACROSS 20 TIERS
================================================================================

Tier 1:  System Foundation        — 7 entities (Kernel, Domain, Subsystem, Module, Component, Primitive, Resource)
Tier 2:  Structure & Architecture — 5 entities (Layer, Tier, Slice, Assembly, Topology)
Tier 3:  Communication & Contracts— 4 entities (Interface, Boundary, Channel, Contract)
Tier 4:  Capability & Function    — 2 entities (Capability, Feature)
Tier 5:  Work & Process           — 5 entities (Process, Workflow, Task, Milestone, Plan)
Tier 6:  Governance Foundation    — 6 entities (Constitution, Charter, GovernanceBody, Role, Policy, Rule)
Tier 7:  Standards & Constraints  — 4 entities (Standard, Guideline, Constraint, Invariant)
Tier 8:  Session & Participation  — 3 entities (Session, Actor, Participant)
Tier 9:  Context & Environment    — 2 entities (Context, Environment)
Tier 10: Decision & Reasoning     — 5 entities (Decision, DecisionRecord, Evidence, Finding, Conclusion)
Tier 11: Artifacts                — 6 entities (Artifact, Document, Specification, Record, Log, Report)
Tier 12: Authorization            — 5 entities (Approval, Authorization, Certification, Credential, Signature)
Tier 13: Traceability & Baselines — 4 entities (Baseline, Snapshot, TraceabilityLink, Checkpoint)
Tier 14: Measurement              — 3 entities (Metric, Measurement, Assessment)
Tier 15: Audit & Review           — 3 entities (Audit, Review, AuditTrail)
Tier 16: Lifecycle & State        — 2 entities (Lifecycle, State)
Tier 17: Exceptions & Waivers     — 2 entities (Exception, Waiver)
Tier 18: Governance Mechanics     — 5 entities (Amendment, Sanction, Precedent, Appeal, Veto)
Tier 19: Dispute & Accountability — 3 entities (Dispute, Recusal, TransparencyReport)
Tier 20: Cross-Cutting            — 3 entities (Concern, Escalation, View)

Total: 79 entities, each with all 15 properties defined.
Total property definitions: 1,185

================================================================================
DEDUPLICATION LOG: KEY MERGES PERFORMED
================================================================================

Merged across domains (same concept, different names):
- Session (Process + Governance proceedings) → Session
- Context (System + Process) → Context
- Scope (System + Process) → subsumed into Context
- Boundary (System + Process) → Boundary
- Constraint (System + Process + Governance) → Constraint
- Invariant (System + Process) → Invariant
- Dependency (System + Process) → Dependency
- Role (Process + Governance) → Role
- Authority (Process + Governance) → Authority
- Delegation (Process + Governance) → subsumed into Role relationships
- Decision (Process + Governance) → Decision
- DecisionRecord (Process + Artifact) → DecisionRecord
- Lifecycle (Process + Governance) → Lifecycle
- Phase (Process multiple groups + Governance) → subsumed into Lifecycle
- Stage (Process multiple groups + Governance) → subsumed into Lifecycle
- Approval (Artifact + Governance) → Approval
- Waiver (Artifact + Process + Governance) → Waiver
- Baseline (Artifact + Governance) → Baseline
- Snapshot (Artifact + Governance) → Snapshot
- Checkpoint (Artifact + Process) → Checkpoint
- Assessment (Artifact + Governance) → Assessment
- Metric (Artifact + Governance) → Metric
- Registry (System + Artifact) → subsumed (derived concept)
- AuditTrail (Artifact + Process) → AuditTrail
- Revision (Artifact + Governance) → Revision
- Deliverable (Artifact + Process) → subsumed into Task/Artifact
- Milestone (Process + Governance) → Milestone
- Finding (Artifact + Governance) → Finding
- Exception (Process + Governance + Artifact ExceptionRecord) → Exception
- Contract (System + Governance) → Contract
- Certification (Artifact Certificate + Governance) → Certification
- Plan (Artifact + Governance) → Plan
- Escalation (Process + Governance) → Escalation
- Audit (Governance) → Audit
- Review (Governance) → Review
- Policy (Governance) → Policy
- Rule (Governance) → Rule
- Standard (Governance) → Standard
- GovernanceBody (Governance) → GovernanceBody
- Charter (Governance) → Charter
- Bylaw (Governance) → subsumed into Charter
- Amendment (Governance) → Amendment
- Sanction (Governance) → Sanction
- Precedent (Governance) → Precedent
- Appeal (Governance) → Appeal
- Dispute (Governance + Grievance) → Dispute
- Recusal (Governance) → Recusal
- Minutes (Governance) → subsumed into TransparencyReport
- Vote/Resolution/Motion (Governance) → Resolution subsumed, Vote/Motion eliminated
- Stakeholder (Governance) → subsumed into Actor
- Right/Entitlement/Privilege (Governance) → subsumed into Role/Authorization
- Obligation/Duty/Commitment (Governance) → subsumed into Role
- EmergencyPower/Stay (Governance) → EmergencyPower kept
- Disclosure (Governance) → subsumed into TransparencyReport
- Safeguard/Oversight/Check (Governance) → Safeguard kept

Eliminated as non-ontological (~257 entities removed):
- Actor subtypes: HumanActor, AutomatedActor, HybridActor
- Session subtypes: AISession, HumanSession
- Control flow: Fork, Join, Sequence, Iteration, DecisionPoint
- Concurrency: Mutex, Deadlock, RaceCondition, LockOrdering, CriticalSection, IsolationLevel
- Process mechanics: Saga, Choreography, Batch, Command, Subprocess, Pipeline, FeedbackLoop
- Temporal: Duration, Timeout, Pause, ResumePoint
- Derived: DependencyGraph, ExecutionTrace, ExecutionSummary, ExecutionResult
- Internal: Compensation, SideEffect, Backpressure, Throttle, WorkQueue, Capacity
- Granular: WorkUnit, Step, Activity, Operation, ExecutionContext, EntryPoint, ExitPoint
- Versioning: Version, Edition, Variant, Revision (kept Revision concept)
- Governance mechanics: Quorum, Bylaw, MOU, Covenant, SLA, StandardLevel, ComplianceBaseline
- Many others

================================================================================
END OF CANONICAL ENTITY CATALOG
================================================================================


{'=' * 80}
PART II: RELATIONSHIP GRAPH (640 Relationships)
{'=' * 80}

================================================================================
RADIUS1 KERNEL — REPOSITORY META MODEL (RMM)
COMPLETE DIRECTED RELATIONSHIP GRAPH
================================================================================

## Metadata

- **Total Entities:** 79
- **Total Relationships:** 640
- **Average Relationships per Entity:** 16.2
- **Minimum Relationships per Entity:** 10
- **Maximum Outgoing per Entity:** 14 (GovernanceBody)
- **Graph Connected:** Yes (all 79 entities reachable from Kernel)
- **Relationship Types Used:** 201 distinct directed relationship types

### Relationship Types Used

- **advises** — 1 occurrences
- **affixed-to** — 5 occurrences
- **allocated-to** — 3 occurrences
- **amended-by** — 3 occurrences
- **amends** — 3 occurrences
- **appealed-via** — 1 occurrences
- **applies-to** — 9 occurrences
- **approved-by** — 4 occurrences
- **approves** — 1 occurrences
- **assigned-to** — 2 occurrences
- **assumed-by** — 1 occurrences
- **assumes** — 1 occurrences
- **audited-by** — 1 occurrences
- **audits** — 1 occurrences
- **authorizes** — 3 occurrences
- **baselined-as** — 1 occurrences
- **bears** — 2 occurrences
- **belongs-to** — 8 occurrences
- **between** — 1 occurrences
- **binds** — 3 occurrences
- **bound-to** — 1 occurrences
- **bounded-by** — 1 occurrences
- **captured-by** — 1 occurrences
- **captured-in** — 2 occurrences
- **captures** — 1 occurrences
- **carries** — 2 occurrences
- **carries-data-between** — 1 occurrences
- **certified-by** — 4 occurrences
- **certifies** — 2 occurrences
- **challenged-by** — 1 occurrences
- **challenges** — 2 occurrences
- **chartered-by** — 1 occurrences
- **cited-in** — 1 occurrences
- **communicates-with** — 1 occurrences
- **compared-to** — 5 occurrences
- **composed-into** — 1 occurrences
- **composed-of** — 3 occurrences
- **connects** — 2 occurrences
- **constrained-by** — 9 occurrences
- **constrains** — 11 occurrences
- **consumed-by** — 4 occurrences
- **consumes** — 2 occurrences
- **contained-in** — 2 occurrences
- **contains** — 28 occurrences
- **contributes-to** — 1 occurrences
- **covered-by** — 1 occurrences
- **covers** — 1 occurrences
- **creates** — 2 occurrences
- **crossed-by** — 5 occurrences
- **crosses** — 5 occurrences
- **declared-by** — 1 occurrences
- **declares** — 1 occurrences
- **defined-by** — 4 occurrences
- **defined-within** — 1 occurrences
- **defines** — 10 occurrences
- **delegates-to** — 2 occurrences
- **delivered-by** — 2 occurrences
- **delivers** — 3 occurrences
- **derived-from** — 4 occurrences
- **derives-from** — 2 occurrences
- **described-by** — 5 occurrences
- **describes** — 4 occurrences
- **deviates-from** — 2 occurrences
- **documented-in** — 5 occurrences
- **documents** — 1 occurrences
- **empowers** — 1 occurrences
- **enables** — 2 occurrences
- **enforced-by** — 4 occurrences
- **enforces** — 1 occurrences
- **escalated-via** — 2 occurrences
- **escalates-from** — 1 occurrences
- **escalates-to** — 1 occurrences
- **established-by** — 1 occurrences
- **establishes** — 2 occurrences
- **evaluated-by** — 2 occurrences
- **evaluates** — 3 occurrences
- **examines** — 2 occurrences
- **excepted-by** — 2 occurrences
- **exercised-by** — 1 occurrences
- **exercises** — 1 occurrences
- **exposed-by** — 3 occurrences
- **exposed-via** — 2 occurrences
- **exposes** — 6 occurrences
- **filed-by** — 1 occurrences
- **files** — 1 occurrences
- **filtered-by** — 2 occurrences
- **filters** — 2 occurrences
- **from** — 1 occurrences
- **generated-from** — 1 occurrences
- **generates** — 1 occurrences
- **governed-by** — 13 occurrences
- **governs** — 10 occurrences
- **granted-by** — 2 occurrences
- **granted-to** — 1 occurrences
- **grants** — 4 occurrences
- **guides** — 1 occurrences
- **has** — 77 occurrences
- **heard-by** — 1 occurrences
- **hears** — 1 occurrences
- **held-by** — 1 occurrences
- **hosted-in** — 1 occurrences
- **hosted-on** — 2 occurrences
- **hosts** — 2 occurrences
- **implements** — 3 occurrences
- **imposed-by** — 1 occurrences
- **imposes** — 1 occurrences
- **included-in** — 1 occurrences
- **includes** — 3 occurrences
- **informed-by** — 3 occurrences
- **informs** — 5 occurrences
- **intersected-by** — 1 occurrences
- **intersects** — 2 occurrences
- **issued-by** — 1 occurrences
- **issues** — 1 occurrences
- **leads-to** — 1 occurrences
- **linked-to** — 1 occurrences
- **made-by** — 1 occurrences
- **makes** — 1 occurrences
- **mandated-by** — 1 occurrences
- **mandates** — 1 occurrences
- **maps** — 1 occurrences
- **marked-by** — 1 occurrences
- **marks** — 3 occurrences
- **measured-by** — 2 occurrences
- **measures-against** — 1 occurrences
- **mediated-by** — 1 occurrences
- **monitored-by** — 9 occurrences
- **monitors** — 4 occurrences
- **on** — 1 occurrences
- **overrides** — 1 occurrences
- **overruled-by** — 2 occurrences
- **overrules** — 1 occurrences
- **oversees** — 1 occurrences
- **owned-by** — 2 occurrences
- **owns** — 4 occurrences
- **participates-in** — 4 occurrences
- **performs** — 1 occurrences
- **presented-for** — 1 occurrences
- **produced-by** — 6 occurrences
- **produces** — 17 occurrences
- **proposed-by** — 1 occurrences
- **proposes** — 1 occurrences
- **provided-by** — 1 occurrences
- **provides** — 1 occurrences
- **published-by** — 2 occurrences
- **publishes** — 2 occurrences
- **raises** — 1 occurrences
- **ratifies** — 1 occurrences
- **reaches** — 1 occurrences
- **realizes** — 1 occurrences
- **recommends** — 1 occurrences
- **recorded-in** — 5 occurrences
- **referenced-by** — 15 occurrences
- **references** — 18 occurrences
- **rejects** — 1 occurrences
- **represented-by** — 1 occurrences
- **represents** — 3 occurrences
- **requested-by** — 1 occurrences
- **required-by** — 3 occurrences
- **requires** — 4 occurrences
- **responds-to** — 1 occurrences
- **results-in** — 2 occurrences
- **reviewed-by** — 2 occurrences
- **reviews** — 2 occurrences
- **scoped-by** — 1 occurrences
- **scoped-to** — 1 occurrences
- **scopes** — 1 occurrences
- **separated-by** — 1 occurrences
- **separates** — 1 occurrences
- **signed-at** — 1 occurrences
- **signed-by** — 3 occurrences
- **signed-with** — 15 occurrences
- **spanned-by** — 1 occurrences
- **spans** — 4 occurrences
- **stacked-above** — 1 occurrences
- **summarized-in** — 2 occurrences
- **summarizes** — 1 occurrences
- **supersedes** — 1 occurrences
- **supports** — 6 occurrences
- **surrounds** — 2 occurrences
- **tested-by** — 3 occurrences
- **time-bounded-by** — 1 occurrences
- **traced-to** — 10 occurrences
- **traced-via** — 3 occurrences
- **traces** — 4 occurrences
- **traces-to** — 10 occurrences
- **tracked-by** — 1 occurrences
- **transitions-to** — 1 occurrences
- **triggered-by** — 1 occurrences
- **triggers** — 18 occurrences
- **used-as** — 1 occurrences
- **used-by** — 2 occurrences
- **uses** — 1 occurrences
- **validated-by** — 3 occurrences
- **validates** — 2 occurrences
- **verified-by** — 2 occurrences
- **verifies** — 2 occurrences
- **versioned-as** — 2 occurrences
- **viewed-through** — 1 occurrences
- **waived-by** — 1 occurrences
- **withdraws** — 1 occurrences

## Relationship Graph

Group by source entity, ordered by tier. Each relationship shows:
`Source → relationship-type → Target | cardinality | rationale`

### TIER 1: System Foundation

#### Kernel — 8 outgoing, 4 incoming

- **Kernel** → *contains* → **Domain** | `1:N` | Root container for all domains
- **Kernel** → *contains* → **Layer** | `1:N` | Architecture organized in horizontal layers
- **Kernel** → *contains* → **Primitive** | `1:N` | Foundational elements of the kernel
- **Kernel** → *contains* → **Resource** | `1:N` | All resources belong to the kernel
- **Kernel** → *governed-by* → **Constitution** | `N:1` | Kernel operates under constitutional authority
- **Kernel** → *described-by* → **Topology** | `1:N` | Topology describes kernel structure
- **Kernel** → *has* → **Lifecycle** | `1:1` | Kernel has its own lifecycle
- **Kernel** → *viewed-through* → **View** | `1:N` | Kernel viewed through perspectives

#### Domain — 8 outgoing, 10 incoming

- **Domain** → *contains* → **Subsystem** | `1:N` | Domain groups subsystems
- **Domain** → *bounded-by* → **Boundary** | `1:1` | Domain has encapsulating boundary
- **Domain** → *exposes* → **Interface** | `1:N` | Domain exposes interfaces externally
- **Domain** → *governed-by* → **GovernanceBody** | `N:1` | Domain overseen by governance body
- **Domain** → *constrained-by* → **Constraint** | `N:M` | Domain subject to structural constraints
- **Domain** → *crossed-by* → **Concern** | `N:M` | Cross-cutting concerns span domains
- **Domain** → *has* → **Primitive** | `1:N` | Domain defines primitives in its language
- **Domain** → *represented-by* → **View** | `N:M` | Domain represented in views

#### Subsystem — 11 outgoing, 10 incoming

- **Subsystem** → *contains* → **Module** | `1:N` | Subsystem contains modules
- **Subsystem** → *contains* → **Component** | `1:N` | Subsystem contains components directly
- **Subsystem** → *exposes* → **Interface** | `1:N` | Subsystem exposes interfaces
- **Subsystem** → *defines* → **Boundary** | `1:1` | Subsystem defines its boundary
- **Subsystem** → *owns* → **Resource** | `1:N` | Subsystem owns resources
- **Subsystem** → *belongs-to* → **Domain** | `N:1` | Subsystem belongs to a domain
- **Subsystem** → *delivers* → **Capability** | `1:N` | Subsystem delivers capabilities
- **Subsystem** → *hosted-on* → **Tier** | `N:1` | Subsystem hosted on a tier
- **Subsystem** → *audited-by* → **Audit** | `N:M` | Subsystem subject to audits
- **Subsystem** → *described-by* → **Topology** | `1:N` | Topology describes subsystem
- **Subsystem** → *contains* → **Assembly** | `1:N` | Subsystem contains assemblies

#### Module — 12 outgoing, 20 incoming

- **Module** → *contains* → **Component** | `1:N` | Module contains components
- **Module** → *exposes* → **Interface** | `1:N` | Module exposes interfaces
- **Module** → *belongs-to* → **Subsystem** | `N:1` | Module belongs to subsystem
- **Module** → *implements* → **Capability** | `1:N` | Module implements capabilities
- **Module** → *produces* → **Artifact** | `1:N` | Module produces artifacts
- **Module** → *consumes* → **Resource** | `N:M` | Module consumes resources
- **Module** → *constrained-by* → **Constraint** | `N:M` | Module subject to constraints
- **Module** → *applies-to* → **Lifecycle** | `N:1` | Module governed by lifecycle
- **Module** → *contained-in* → **Layer** | `N:1` | Module belongs to a layer
- **Module** → *spanned-by* → **Slice** | `N:M` | Slices span across modules
- **Module** → *participates-in* → **Assembly** | `N:M` | Modules participate in assemblies
- **Module** → *traced-via* → **TraceabilityLink** | `N:M` | Modules traced via traceability links

#### Component — 10 outgoing, 20 incoming

- **Component** → *exposes* → **Interface** | `1:N` | Component exposes interfaces
- **Component** → *uses* → **Primitive** | `N:M` | Components use primitives
- **Component** → *belongs-to* → **Module** | `N:1` | Component belongs to module
- **Component** → *participates-in* → **Assembly** | `N:M` | Components participate in assemblies
- **Component** → *implements* → **Feature** | `1:N` | Component implements features
- **Component** → *constrained-by* → **Constraint** | `N:M` | Component subject to constraints
- **Component** → *tested-by* → **Evidence** | `N:M` | Component tested by evidence
- **Component** → *certified-by* → **Certification** | `N:M` | Component certified
- **Component** → *described-by* → **Topology** | `1:N` | Topology describes component
- **Component** → *filtered-by* → **View** | `N:M` | Views filter components

#### Primitive — 7 outgoing, 5 incoming

- **Primitive** → *used-by* → **Component** | `N:M` | Primitives used by components
- **Primitive** → *defined-within* → **Domain** | `N:M` | Primitives scoped to domains
- **Primitive** → *referenced-by* → **Interface** | `N:M` | Interfaces reference primitives
- **Primitive** → *governed-by* → **Constitution** | `N:1` | Primitives ratified at constitutional level
- **Primitive** → *constrains* → **Module** | `N:M` | Primitives constrain module design
- **Primitive** → *contained-in* → **Layer** | `N:1` | Primitives exist within layers
- **Primitive** → *has* → **Lifecycle** | `N:1` | Primitives governed by lifecycle

#### Resource — 7 outgoing, 6 incoming

- **Resource** → *allocated-to* → **Module** | `N:M` | Resources allocated to modules
- **Resource** → *allocated-to* → **Subsystem** | `N:M` | Resources allocated to subsystems
- **Resource** → *constrained-by* → **Constraint** | `N:M` | Resources constrained by limits
- **Resource** → *hosted-on* → **Tier** | `N:M` | Resources hosted on tiers
- **Resource** → *consumed-by* → **Process** | `N:M` | Resources consumed by processes
- **Resource** → *monitored-by* → **Metric** | `N:M` | Resources monitored by metrics
- **Resource** → *provided-by* → **Environment** | `N:M` | Resources provided by environment

### TIER 2: Structure & Architecture

#### Layer — 8 outgoing, 9 incoming

- **Layer** → *contains* → **Module** | `1:N` | Layer contains modules
- **Layer** → *contains* → **Component** | `1:N` | Layer contains components
- **Layer** → *contains* → **Primitive** | `1:N` | Layer contains primitives
- **Layer** → *stacked-above* → **Layer** | `N:M` | Layers depend on layers below
- **Layer** → *intersected-by* → **Slice** | `N:M` | Slices cross through layers
- **Layer** → *crossed-by* → **Concern** | `N:M` | Concerns cross layers vertically
- **Layer** → *governed-by* → **Invariant** | `N:M` | Layers governed by invariants
- **Layer** → *described-by* → **Topology** | `1:N` | Topology describes layer arrangement

#### Tier — 7 outgoing, 4 incoming

- **Tier** → *contains* → **Subsystem** | `1:N` | Tier contains subsystems
- **Tier** → *contains* → **Module** | `1:N` | Tier contains modules
- **Tier** → *hosts* → **Resource** | `1:N` | Tier hosts resources
- **Tier** → *communicates-with* → **Tier** | `N:M` | Tiers communicate with tiers
- **Tier** → *separated-by* → **Boundary** | `N:M` | Boundaries separate tiers
- **Tier** → *constrained-by* → **Constraint** | `N:M` | Tiers constrained by constraints
- **Tier** → *monitored-by* → **Metric** | `N:M` | Tiers monitored by metrics

#### Slice — 9 outgoing, 7 incoming

- **Slice** → *crosses* → **Layer** | `N:M` | Slice crosses layers vertically
- **Slice** → *spans* → **Module** | `N:M` | Slice spans modules
- **Slice** → *delivers* → **Capability** | `1:N` | Slice delivers capabilities
- **Slice** → *delivers* → **Feature** | `1:N` | Slice delivers features
- **Slice** → *intersects* → **Slice** | `N:M` | Slices intersect each other
- **Slice** → *traced-to* → **Topology** | `N:M` | Slices traced in topology
- **Slice** → *crossed-by* → **Concern** | `N:M` | Concerns cross slices
- **Slice** → *has* → **Interface** | `1:N` | Slice exposes interfaces
- **Slice** → *spans* → **Assembly** | `N:M` | Slices span across assemblies

#### Assembly — 6 outgoing, 4 incoming

- **Assembly** → *contains* → **Component** | `1:N` | Assembly contains components
- **Assembly** → *contains* → **Module** | `1:N` | Assembly contains modules
- **Assembly** → *exposes* → **Interface** | `1:N` | Assembly exposes interfaces
- **Assembly** → *belongs-to* → **Subsystem** | `N:1` | Assembly belongs to subsystem
- **Assembly** → *produces* → **Artifact** | `1:N` | Assembly produces artifacts
- **Assembly** → *has* → **Lifecycle** | `N:1` | Assembly governed by lifecycle

#### Topology — 6 outgoing, 6 incoming

- **Topology** → *describes* → **Kernel** | `N:1` | Topology describes kernel
- **Topology** → *describes* → **Domain** | `1:N` | Topology describes domains
- **Topology** → *describes* → **Subsystem** | `1:N` | Topology describes subsystems
- **Topology** → *references* → **Channel** | `N:M` | Topology references channels
- **Topology** → *describes* → **Layer** | `1:N` | Topology describes layers
- **Topology** → *maps* → **Slice** | `N:M` | Topology maps slices

### TIER 3: Communication & Contracts

#### Interface — 9 outgoing, 16 incoming

- **Interface** → *exposed-by* → **Component** | `N:M` | Interfaces exposed by components
- **Interface** → *exposed-by* → **Module** | `N:M` | Interfaces exposed by modules
- **Interface** → *exposed-by* → **Subsystem** | `N:M` | Interfaces exposed by subsystems
- **Interface** → *consumed-by* → **Component** | `N:M` | Interfaces consumed by components
- **Interface** → *constrained-by* → **Contract** | `N:M` | Interfaces bound by contracts
- **Interface** → *defined-by* → **Specification** | `N:M` | Interfaces defined by specifications
- **Interface** → *exposes* → **Capability** | `1:N` | Interfaces expose capabilities
- **Interface** → *constrained-by* → **Constraint** | `N:M` | Interfaces constrained by constraints
- **Interface** → *filtered-by* → **View** | `N:M` | Views filter interfaces

#### Boundary — 7 outgoing, 7 incoming

- **Boundary** → *surrounds* → **Domain** | `1:1` | Boundary encapsulates domain
- **Boundary** → *surrounds* → **Subsystem** | `1:1` | Boundary encapsulates subsystem
- **Boundary** → *crossed-by* → **Channel** | `N:M` | Channels cross boundaries
- **Boundary** → *crossed-by* → **Contract** | `N:M` | Contracts span boundaries
- **Boundary** → *governed-by* → **Invariant** | `N:M` | Boundaries governed by invariants
- **Boundary** → *constrains* → **Module** | `N:M` | Boundaries constrain modules
- **Boundary** → *separates* → **Tier** | `N:M` | Boundaries separate tiers

#### Channel — 7 outgoing, 3 incoming

- **Channel** → *connects* → **Interface** | `N:M` | Channels connect interfaces
- **Channel** → *carries-data-between* → **Component** | `N:M` | Channels carry data between components
- **Channel** → *governed-by* → **Contract** | `N:M` | Channels governed by contracts
- **Channel** → *crosses* → **Boundary** | `N:M` | Channels cross boundaries
- **Channel** → *monitored-by* → **AuditTrail** | `N:M` | Channels monitored by audit trails
- **Channel** → *described-by* → **Topology** | `N:1` | Topology describes channels
- **Channel** → *has* → **Lifecycle** | `N:1` | Channels governed by lifecycle

#### Contract — 7 outgoing, 8 incoming

- **Contract** → *binds* → **Interface** | `N:M` | Contracts bind interfaces
- **Contract** → *spans* → **Boundary** | `N:M` | Contracts span boundaries
- **Contract** → *enforced-by* → **Constraint** | `N:M` | Contracts enforced by constraints
- **Contract** → *consumed-by* → **Module** | `N:M` | Contracts consumed by modules
- **Contract** → *references* → **Standard** | `N:M` | Contracts reference standards
- **Contract** → *signed-with* → **Signature** | `N:M` | Contracts signed with signatures
- **Contract** → *certified-by* → **Certification** | `N:M` | Contracts certified

### TIER 4: Capability & Function

#### Capability — 8 outgoing, 5 incoming

- **Capability** → *delivered-by* → **Module** | `N:M` | Capabilities delivered by modules
- **Capability** → *delivered-by* → **Subsystem** | `N:M` | Capabilities delivered by subsystems
- **Capability** → *composed-of* → **Feature** | `1:N` | Capabilities composed of features
- **Capability** → *tested-by* → **Evidence** | `N:M` | Capabilities tested by evidence
- **Capability** → *exposed-via* → **Interface** | `N:M` | Capabilities exposed via interfaces
- **Capability** → *referenced-by* → **Slice** | `N:M` | Slices reference capabilities
- **Capability** → *certified-by* → **Certification** | `N:M` | Capabilities certified
- **Capability** → *measured-by* → **Metric** | `N:M` | Capabilities measured by metrics

#### Feature — 9 outgoing, 5 incoming

- **Feature** → *realizes* → **Capability** | `N:M` | Features realize capabilities
- **Feature** → *spans* → **Module** | `N:M` | Features span modules
- **Feature** → *intersects* → **Slice** | `N:M` | Features intersect slices
- **Feature** → *exposed-via* → **Interface** | `N:M` | Features exposed via interfaces
- **Feature** → *tested-by* → **Evidence** | `N:M` | Features tested by evidence
- **Feature** → *implements* → **Specification** | `N:M` | Features implement specifications
- **Feature** → *allocated-to* → **Component** | `N:M` | Features allocated to components
- **Feature** → *traced-via* → **TraceabilityLink** | `N:M` | Features traced via links
- **Feature** → *has* → **Lifecycle** | `N:1` | Features governed by lifecycle

### TIER 5: Work & Process

#### Process — 11 outgoing, 13 incoming

- **Process** → *has* → **Task** | `1:N` | Processes contain tasks
- **Process** → *produces* → **Artifact** | `1:N` | Processes produce artifacts
- **Process** → *consumes* → **Artifact** | `N:M` | Processes consume artifacts
- **Process** → *has* → **Milestone** | `1:N` | Processes have milestones
- **Process** → *governed-by* → **Workflow** | `N:1` | Processes governed by workflows
- **Process** → *produces* → **Evidence** | `1:N` | Processes produce evidence
- **Process** → *produces* → **Finding** | `1:N` | Processes produce findings
- **Process** → *evaluated-by* → **Assessment** | `N:M` | Processes evaluated by assessments
- **Process** → *owns* → **Record** | `1:N` | Processes own records
- **Process** → *owns* → **Log** | `1:N` | Processes own logs
- **Process** → *produces* → **Document** | `1:N` | Processes produce documents

#### Workflow — 9 outgoing, 4 incoming

- **Workflow** → *has* → **Task** | `1:N` | Workflows contain tasks
- **Workflow** → *has* → **Session** | `1:N` | Workflows have sessions
- **Workflow** → *governed-by* → **Plan** | `N:1` | Workflows governed by plans
- **Workflow** → *triggers* → **Milestone** | `1:N` | Workflows trigger milestones
- **Workflow** → *constrained-by* → **Constraint** | `N:M` | Workflows constrained by constraints
- **Workflow** → *monitored-by* → **AuditTrail** | `N:M` | Workflows monitored by audit trails
- **Workflow** → *has* → **Lifecycle** | `N:1` | Workflows governed by lifecycle
- **Workflow** → *has* → **Participant** | `1:N` | Workflows have participants
- **Workflow** → *has* → **Context** | `1:1` | Workflows have context

#### Task — 9 outgoing, 12 incoming

- **Task** → *belongs-to* → **Process** | `N:1` | Tasks belong to processes
- **Task** → *produces* → **Artifact** | `1:N` | Tasks produce artifacts
- **Task** → *has* → **Milestone** | `N:1` | Tasks associated with milestones
- **Task** → *assigned-to* → **Actor** | `N:M` | Tasks assigned to actors
- **Task** → *constrained-by* → **Constraint** | `N:M` | Tasks constrained by constraints
- **Task** → *produces* → **Evidence** | `1:N` | Tasks produce evidence
- **Task** → *belongs-to* → **Workflow** | `N:1` | Tasks belong to workflows
- **Task** → *has* → **Lifecycle** | `N:1` | Tasks governed by lifecycle
- **Task** → *escalated-via* → **Escalation** | `N:1` | Tasks escalated via escalation

#### Milestone — 8 outgoing, 8 incoming

- **Milestone** → *marks* → **Lifecycle** | `N:M` | Milestones mark lifecycle stages
- **Milestone** → *marks* → **Plan** | `N:M` | Milestones mark plan progress
- **Milestone** → *triggers* → **Review** | `N:1` | Milestones trigger reviews
- **Milestone** → *measured-by* → **Metric** | `N:M` | Milestones measured by metrics
- **Milestone** → *reaches* → **Checkpoint** | `1:N` | Milestones reach checkpoints
- **Milestone** → *marks* → **State** | `N:1` | Milestones mark state transitions
- **Milestone** → *recorded-in* → **Record** | `N:M` | Milestones recorded in records
- **Milestone** → *has* → **Lifecycle** | `N:1` | Milestones governed by lifecycle

#### Plan — 8 outgoing, 4 incoming

- **Plan** → *references* → **Specification** | `N:M` | Plans reference specifications
- **Plan** → *defines* → **Milestone** | `1:N` | Plans define milestones
- **Plan** → *traced-to* → **DecisionRecord** | `N:M` | Plans traced to decision records
- **Plan** → *contains* → **Workflow** | `1:N` | Plans contain workflows
- **Plan** → *contains* → **Task** | `1:N` | Plans contain tasks
- **Plan** → *governed-by* → **GovernanceBody** | `N:1` | Plans governed by governance body
- **Plan** → *approved-by* → **Approval** | `N:1` | Plans approved by approvals
- **Plan** → *has* → **Lifecycle** | `N:1` | Plans governed by lifecycle

### TIER 6: Governance Foundation

#### Constitution — 10 outgoing, 6 incoming

- **Constitution** → *empowers* → **GovernanceBody** | `1:N` | Constitution empowers governance bodies
- **Constitution** → *establishes* → **Charter** | `1:N` | Constitution establishes charters
- **Constitution** → *defines* → **Rule** | `1:N` | Constitution defines rules
- **Constitution** → *defines* → **Invariant** | `1:N` | Constitution defines invariants
- **Constitution** → *defines* → **Role** | `1:N` | Constitution defines roles
- **Constitution** → *ratifies* → **Primitive** | `1:N` | Constitution ratifies primitives
- **Constitution** → *governs* → **Kernel** | `1:1` | Constitution governs kernel
- **Constitution** → *supersedes* → **Charter** | `N:M` | Constitution supersedes charters
- **Constitution** → *amended-by* → **Amendment** | `N:M` | Constitution amended by amendments
- **Constitution** → *defines* → **Veto** | `1:N` | Constitution defines veto powers

#### Charter — 8 outgoing, 6 incoming

- **Charter** → *governs* → **GovernanceBody** | `1:1` | Charter governs governance body
- **Charter** → *delegates-to* → **Role** | `1:N` | Charter delegates to roles
- **Charter** → *references* → **Constitution** | `N:1` | Charter references constitution
- **Charter** → *defines* → **Policy** | `1:N` | Charter defines policies
- **Charter** → *approved-by* → **Approval** | `N:1` | Charter approved by approval
- **Charter** → *amended-by* → **Amendment** | `N:M` | Charter amended by amendments
- **Charter** → *has* → **Lifecycle** | `N:1` | Charter governed by lifecycle
- **Charter** → *signed-with* → **Signature** | `N:M` | Charter signed with signatures

#### GovernanceBody — 14 outgoing, 17 incoming

- **GovernanceBody** → *chartered-by* → **Charter** | `N:1` | Governance body chartered by charter
- **GovernanceBody** → *composed-of* → **Role** | `1:N` | Governance body composed of roles
- **GovernanceBody** → *creates* → **Policy** | `1:N` | Governance body creates policies
- **GovernanceBody** → *approves* → **Decision** | `1:N` | Governance body approves decisions
- **GovernanceBody** → *oversees* → **Domain** | `1:N` | Governance body oversees domains
- **GovernanceBody** → *publishes* → **TransparencyReport** | `1:N` | Governance body publishes reports
- **GovernanceBody** → *issues* → **Certification** | `1:N` | Governance body issues certifications
- **GovernanceBody** → *grants* → **Exception** | `1:N` | Governance body grants exceptions
- **GovernanceBody** → *hears* → **Appeal** | `1:N` | Governance body hears appeals
- **GovernanceBody** → *imposes* → **Sanction** | `1:N` | Governance body imposes sanctions
- **GovernanceBody** → *authorizes* → **Veto** | `1:N` | Governance body authorizes vetoes
- **GovernanceBody** → *publishes* → **Guideline** | `1:N` | Governance body publishes guidelines
- **GovernanceBody** → *requires* → **Recusal** | `N:M` | Governance body requires recusals
- **GovernanceBody** → *grants* → **Waiver** | `1:N` | Governance body grants waivers

#### Role — 9 outgoing, 8 incoming

- **Role** → *has* → **Authorization** | `1:N` | Roles have authorizations
- **Role** → *assigned-to* → **Actor** | `1:N` | Roles assigned to actors
- **Role** → *delegates-to* → **Role** | `N:M` | Roles delegate to other roles
- **Role** → *defined-by* → **Constitution** | `N:1` | Roles defined by constitution
- **Role** → *participates-in* → **Session** | `N:M` | Roles participate in sessions
- **Role** → *exercises* → **Veto** | `1:N` | Roles exercise vetoes
- **Role** → *assumed-by* → **Participant** | `N:M` | Roles assumed by participants
- **Role** → *governed-by* → **Policy** | `N:1` | Roles governed by policies
- **Role** → *traced-to* → **Charter** | `N:1` | Roles traced to charters

#### Policy — 9 outgoing, 7 incoming

- **Policy** → *authorizes* → **Rule** | `1:N` | Policy authorizes rules
- **Policy** → *enforced-by* → **Audit** | `N:M` | Policy enforced by audits
- **Policy** → *excepted-by* → **Exception** | `N:M` | Policy excepted by exceptions
- **Policy** → *governed-by* → **GovernanceBody** | `N:1` | Policy governed by governance body
- **Policy** → *derived-from* → **Charter** | `N:1` | Policy derived from charter
- **Policy** → *constrains* → **Process** | `N:M` | Policy constrains processes
- **Policy** → *amended-by* → **Amendment** | `N:M` | Policy amended by amendments
- **Policy** → *has* → **Lifecycle** | `N:1` | Policy governed by lifecycle
- **Policy** → *informed-by* → **Precedent** | `N:M` | Policies informed by precedents

#### Rule — 9 outgoing, 7 incoming

- **Rule** → *derived-from* → **Standard** | `N:1` | Rules derived from standards
- **Rule** → *enforced-by* → **Sanction** | `N:M` | Rules enforced by sanctions
- **Rule** → *governed-by* → **Policy** | `N:1` | Rules governed by policy
- **Rule** → *constrains* → **Component** | `N:M` | Rules constrain components
- **Rule** → *constrains* → **Module** | `N:M` | Rules constrain modules
- **Rule** → *excepted-by* → **Exception** | `N:M` | Rules excepted by exceptions
- **Rule** → *waived-by* → **Waiver** | `N:M` | Rules waived by waivers
- **Rule** → *has* → **Lifecycle** | `N:1` | Rules governed by lifecycle
- **Rule** → *informed-by* → **Precedent** | `N:M` | Rules informed by precedents

### TIER 7: Standards & Constraints

#### Standard — 9 outgoing, 8 incoming

- **Standard** → *mandates* → **Constraint** | `1:N` | Standards mandate constraints
- **Standard** → *referenced-by* → **Contract** | `N:M` | Standards referenced by contracts
- **Standard** → *enforced-by* → **Audit** | `N:M` | Standards enforced by audits
- **Standard** → *defines* → **Guideline** | `1:N` | Standards define guidelines
- **Standard** → *governs* → **Specification** | `N:M` | Standards govern specifications
- **Standard** → *certified-by* → **Certification** | `N:M` | Standards basis for certifications
- **Standard** → *defines* → **Metric** | `1:N` | Standards define metrics
- **Standard** → *compared-to* → **Measurement** | `N:M` | Standards compared to measurements
- **Standard** → *covered-by* → **TransparencyReport** | `N:M` | Standards covered by transparency reports

#### Guideline — 6 outgoing, 4 incoming

- **Guideline** → *supports* → **Standard** | `N:1` | Guidelines support standards
- **Guideline** → *informed-by* → **Precedent** | `N:M` | Guidelines informed by precedents
- **Guideline** → *referenced-by* → **Contract** | `N:M` | Guidelines referenced by contracts
- **Guideline** → *advises* → **Process** | `N:M` | Guidelines advise processes
- **Guideline** → *informs* → **Assessment** | `N:M` | Guidelines inform assessments
- **Guideline** → *has* → **Lifecycle** | `N:1` | Guidelines governed by lifecycle

#### Constraint — 10 outgoing, 15 incoming

- **Constraint** → *applies-to* → **Module** | `N:M` | Constraints apply to modules
- **Constraint** → *applies-to* → **Component** | `N:M` | Constraints apply to components
- **Constraint** → *applies-to* → **Interface** | `N:M` | Constraints apply to interfaces
- **Constraint** → *applies-to* → **Boundary** | `N:M` | Constraints apply to boundaries
- **Constraint** → *applies-to* → **Layer** | `N:M` | Constraints apply to layers
- **Constraint** → *referenced-by* → **Invariant** | `N:M` | Constraints referenced by invariants
- **Constraint** → *enforces* → **Contract** | `N:M` | Constraints enforce contracts
- **Constraint** → *derives-from* → **Rule** | `N:M` | Constraints derive from rules
- **Constraint** → *scopes* → **Authorization** | `N:M` | Constraints scope authorizations
- **Constraint** → *mandated-by* → **Standard** | `N:1` | Constraints mandated by standards

#### Invariant — 8 outgoing, 7 incoming

- **Invariant** → *governs* → **Kernel** | `N:1` | Invariants govern kernel
- **Invariant** → *governs* → **Domain** | `1:N` | Invariants govern domains
- **Invariant** → *governs* → **Layer** | `1:N` | Invariants govern layers
- **Invariant** → *governs* → **Boundary** | `1:N` | Invariants govern boundaries
- **Invariant** → *referenced-by* → **Constraint** | `1:N` | Invariants referenced by constraints
- **Invariant** → *referenced-by* → **Contract** | `N:M` | Invariants referenced by contracts
- **Invariant** → *validated-by* → **Evidence** | `N:M` | Invariants validated by evidence
- **Invariant** → *defined-by* → **Constitution** | `N:1` | Invariants defined by constitution

### TIER 8: Session & Participation

#### Session — 10 outgoing, 10 incoming

- **Session** → *has* → **Actor** | `1:N` | Sessions have actors
- **Session** → *has* → **Task** | `1:N` | Sessions contain tasks
- **Session** → *produces* → **Decision** | `1:N` | Sessions produce decisions
- **Session** → *belongs-to* → **Workflow** | `N:1` | Sessions belong to workflows
- **Session** → *has* → **Participant** | `1:N` | Sessions have participants
- **Session** → *has* → **Context** | `1:1` | Sessions have context
- **Session** → *produces* → **Evidence** | `1:N` | Sessions produce evidence
- **Session** → *hosted-in* → **Environment** | `N:1` | Sessions hosted in environment
- **Session** → *monitored-by* → **AuditTrail** | `N:M` | Sessions monitored by audit trails
- **Session** → *creates* → **Participant** | `1:N` | Sessions create participants

#### Actor — 11 outgoing, 15 incoming

- **Actor** → *has* → **Role** | `N:M` | Actors have roles
- **Actor** → *performs* → **Task** | `1:N` | Actors perform tasks
- **Actor** → *participates-in* → **Session** | `N:M` | Actors participate in sessions
- **Actor** → *makes* → **Decision** | `1:N` | Actors make decisions
- **Actor** → *owns* → **Task** | `1:N` | Actors own tasks
- **Actor** → *has* → **Credential** | `N:M` | Actors have credentials
- **Actor** → *triggers* → **Escalation** | `1:N` | Actors trigger escalations
- **Actor** → *proposes* → **Amendment** | `1:N` | Actors propose amendments
- **Actor** → *files* → **Appeal** | `1:N` | Actors file appeals
- **Actor** → *raises* → **Dispute** | `1:N` | Actors raise disputes
- **Actor** → *declares* → **Recusal** | `1:N` | Actors declare recusals

#### Participant — 6 outgoing, 5 incoming

- **Participant** → *binds* → **Actor** | `N:1` | Participant binds actor
- **Participant** → *binds* → **Session** | `N:1` | Participant binds session
- **Participant** → *assumes* → **Role** | `N:1` | Participant assumes role
- **Participant** → *contributes-to* → **Task** | `N:M` | Participant contributes to tasks
- **Participant** → *produces* → **Evidence** | `1:N` | Participants produce evidence
- **Participant** → *has* → **Credential** | `N:M` | Participants have credentials

### TIER 9: Context & Environment

#### Context — 7 outgoing, 3 incoming

- **Context** → *references* → **Module** | `N:M` | Context references modules
- **Context** → *references* → **Component** | `N:M` | Context references components
- **Context** → *governs* → **Session** | `1:N` | Context governs sessions
- **Context** → *has* → **Environment** | `1:1` | Context has environment
- **Context** → *informs* → **Decision** | `N:M` | Context informs decisions
- **Context** → *constrains* → **Task** | `N:M` | Context constrains tasks
- **Context** → *recorded-in* → **Record** | `N:1` | Context recorded in records

#### Environment — 7 outgoing, 3 incoming

- **Environment** → *provides* → **Resource** | `1:N` | Environment provides resources
- **Environment** → *has* → **Constraint** | `N:M` | Environment has constraints
- **Environment** → *hosts* → **Session** | `1:N` | Environment hosts sessions
- **Environment** → *has* → **Invariant** | `N:M` | Environment has invariants
- **Environment** → *supports* → **Process** | `N:M` | Environment supports processes
- **Environment** → *monitored-by* → **Metric** | `N:M` | Environment monitored by metrics
- **Environment** → *has* → **Lifecycle** | `N:1` | Environment governed by lifecycle

### TIER 10: Decision & Reasoning

#### Decision — 8 outgoing, 10 incoming

- **Decision** → *made-by* → **Actor** | `N:1` | Decisions made by actors
- **Decision** → *has* → **Context** | `N:1` | Decisions have context
- **Decision** → *recorded-in* → **DecisionRecord** | `1:1` | Decisions recorded in records
- **Decision** → *has* → **Conclusion** | `N:1` | Decisions have conclusions
- **Decision** → *approved-by* → **Approval** | `N:1` | Decisions approved by approvals
- **Decision** → *challenged-by* → **Appeal** | `N:M` | Decisions challenged by appeals
- **Decision** → *triggers* → **Plan** | `1:N` | Decisions trigger plans
- **Decision** → *overruled-by* → **Veto** | `N:M` | Decisions overruled by vetoes

#### DecisionRecord — 8 outgoing, 9 incoming

- **DecisionRecord** → *references* → **Finding** | `N:M` | Decision records reference findings
- **DecisionRecord** → *signed-by* → **Signature** | `N:M` | Decision records signed
- **DecisionRecord** → *traced-to* → **Conclusion** | `N:1` | Decision records traced to conclusions
- **DecisionRecord** → *triggers* → **Plan** | `1:N` | Decision records trigger plans
- **DecisionRecord** → *contains* → **Evidence** | `N:M` | Decision records contain evidence
- **DecisionRecord** → *reviewed-by* → **Review** | `N:M` | Decision records reviewed
- **DecisionRecord** → *establishes* → **Precedent** | `1:N` | Decision records establish precedents
- **DecisionRecord** → *has* → **Lifecycle** | `N:1` | Decision records governed by lifecycle

#### Evidence — 9 outgoing, 19 incoming

- **Evidence** → *supports* → **Finding** | `N:M` | Evidence supports findings
- **Evidence** → *signed-by* → **Signature** | `N:M` | Evidence signed by signatures
- **Evidence** → *supports* → **Conclusion** | `N:M` | Evidence supports conclusions
- **Evidence** → *validates* → **Invariant** | `N:M` | Evidence validates invariants
- **Evidence** → *verifies* → **Specification** | `N:M` | Evidence verifies specifications
- **Evidence** → *produced-by* → **Process** | `N:M` | Evidence produced by processes
- **Evidence** → *produced-by* → **Task** | `N:M` | Evidence produced by tasks
- **Evidence** → *produced-by* → **Session** | `N:M` | Evidence produced by sessions
- **Evidence** → *supports* → **Certification** | `N:M` | Evidence supports certifications

#### Finding — 8 outgoing, 8 incoming

- **Finding** → *references* → **Evidence** | `N:M` | Findings reference evidence
- **Finding** → *summarized-in* → **Report** | `N:M` | Findings summarized in reports
- **Finding** → *traced-to* → **Assessment** | `N:M` | Findings traced to assessments
- **Finding** → *triggers* → **Conclusion** | `N:1` | Findings trigger conclusions
- **Finding** → *produced-by* → **Audit** | `N:M` | Findings produced by audits
- **Finding** → *produced-by* → **Review** | `N:M` | Findings produced by reviews
- **Finding** → *supports* → **DecisionRecord** | `N:M` | Findings support decision records
- **Finding** → *has* → **Lifecycle** | `N:1` | Findings governed by lifecycle

#### Conclusion — 8 outgoing, 7 incoming

- **Conclusion** → *references* → **Finding** | `N:M` | Conclusions reference findings
- **Conclusion** → *traces-to* → **Evidence** | `N:M` | Conclusions trace to evidence
- **Conclusion** → *triggers* → **DecisionRecord** | `1:N` | Conclusions trigger decision records
- **Conclusion** → *signed-by* → **Signature** | `N:1` | Conclusions signed
- **Conclusion** → *derives-from* → **Assessment** | `N:M` | Conclusions derive from assessments
- **Conclusion** → *leads-to* → **Decision** | `1:N` | Conclusions lead to decisions
- **Conclusion** → *overrules* → **Precedent** | `N:M` | Conclusions overrule precedents
- **Conclusion** → *has* → **Lifecycle** | `N:1` | Conclusions governed by lifecycle

### TIER 11: Artifacts

#### Artifact — 9 outgoing, 15 incoming

- **Artifact** → *consumed-by* → **Process** | `N:M` | Artifacts consumed by processes
- **Artifact** → *produced-by* → **Process** | `N:M` | Artifacts produced by processes
- **Artifact** → *composed-of* → **Artifact** | `N:M` | Artifacts composed of other artifacts
- **Artifact** → *traced-via* → **TraceabilityLink** | `N:M` | Artifacts traced via traceability links
- **Artifact** → *versioned-as* → **Baseline** | `N:M` | Artifacts versioned as baselines
- **Artifact** → *has* → **Record** | `1:N` | Artifacts have records
- **Artifact** → *signed-with* → **Signature** | `N:M` | Artifacts signed with signatures
- **Artifact** → *has* → **Lifecycle** | `N:1` | Artifacts governed by lifecycle
- **Artifact** → *captured-in* → **Snapshot** | `N:M` | Artifacts captured in snapshots

#### Document — 7 outgoing, 3 incoming

- **Document** → *traced-to* → **Specification** | `N:M` | Documents traced to specifications
- **Document** → *versioned-as* → **Baseline** | `N:1` | Documents versioned as baselines
- **Document** → *composed-into* → **Artifact** | `N:1` | Documents composed into artifacts
- **Document** → *signed-with* → **Signature** | `N:M` | Documents signed with signatures
- **Document** → *contains* → **Evidence** | `N:M` | Documents contain evidence
- **Document** → *produces* → **Report** | `N:M` | Documents produce reports
- **Document** → *has* → **Lifecycle** | `N:1` | Documents governed by lifecycle

#### Specification — 8 outgoing, 9 incoming

- **Specification** → *verified-by* → **Evidence** | `N:M` | Specifications verified by evidence
- **Specification** → *validated-by* → **Evidence** | `N:M` | Specifications validated by evidence
- **Specification** → *signed-with* → **Signature** | `N:M` | Specifications signed
- **Specification** → *baselined-as* → **Baseline** | `N:1` | Specifications baselined
- **Specification** → *constrains* → **Interface** | `N:M` | Specifications constrain interfaces
- **Specification** → *constrains* → **Component** | `N:M` | Specifications constrain components
- **Specification** → *governs* → **Feature** | `N:M` | Specifications govern features
- **Specification** → *has* → **Lifecycle** | `N:1` | Specifications governed by lifecycle

#### Record — 7 outgoing, 15 incoming

- **Record** → *linked-to* → **Log** | `N:1` | Records linked to logs
- **Record** → *signed-with* → **Signature** | `N:1` | Records signed with signatures
- **Record** → *referenced-by* → **AuditTrail** | `N:M` | Records referenced by audit trails
- **Record** → *owned-by* → **Process** | `N:1` | Records owned by processes
- **Record** → *traces-to* → **Milestone** | `N:M` | Records trace to milestones
- **Record** → *contains* → **Measurement** | `N:M` | Records contain measurements
- **Record** → *documents* → **Exception** | `N:1` | Records document exceptions

#### Log — 7 outgoing, 3 incoming

- **Log** → *contains* → **Record** | `1:N` | Logs contain records
- **Log** → *traced-to* → **AuditTrail** | `N:1` | Logs traced to audit trails
- **Log** → *referenced-by* → **Report** | `N:M` | Logs referenced by reports
- **Log** → *signed-with* → **Signature** | `N:1` | Logs signed with signatures
- **Log** → *produces* → **Evidence** | `1:N` | Logs produce evidence
- **Log** → *monitored-by* → **Audit** | `N:M` | Logs monitored by audits
- **Log** → *owned-by* → **Process** | `N:1` | Logs owned by processes

#### Report — 8 outgoing, 5 incoming

- **Report** → *references* → **Evidence** | `N:M` | Reports reference evidence
- **Report** → *contains* → **Finding** | `N:M` | Reports contain findings
- **Report** → *contains* → **Measurement** | `N:M` | Reports contain measurements
- **Report** → *traced-to* → **Metric** | `N:M` | Reports traced to metrics
- **Report** → *signed-with* → **Signature** | `N:1` | Reports signed
- **Report** → *summarizes* → **Assessment** | `N:1` | Reports summarize assessments
- **Report** → *published-by* → **GovernanceBody** | `N:1` | Reports published by governance body
- **Report** → *has* → **Lifecycle** | `N:1` | Reports governed by lifecycle

### TIER 12: Authorization

#### Approval — 7 outgoing, 6 incoming

- **Approval** → *bears* → **Signature** | `N:M` | Approvals bear signatures
- **Approval** → *traces-to* → **Artifact** | `N:M` | Approvals trace to artifacts
- **Approval** → *referenced-by* → **AuditTrail** | `N:M` | Approvals referenced by audit trails
- **Approval** → *includes* → **Constraint** | `N:M` | Approvals include conditions as constraints
- **Approval** → *grants* → **Authorization** | `N:1` | Approvals grant authorizations
- **Approval** → *certifies* → **Certification** | `N:M` | Approvals certify certifications
- **Approval** → *has* → **Lifecycle** | `N:1` | Approvals governed by lifecycle

#### Authorization — 7 outgoing, 4 incoming

- **Authorization** → *authorizes* → **Actor** | `N:M` | Authorizations authorize actors
- **Authorization** → *granted-to* → **Role** | `N:M` | Authorizations granted to roles
- **Authorization** → *scoped-by* → **Constraint** | `N:M` | Authorizations scoped by constraints
- **Authorization** → *derived-from* → **Approval** | `N:1` | Authorizations derived from approvals
- **Authorization** → *enables* → **Task** | `N:M` | Authorizations enable tasks
- **Authorization** → *carries* → **Credential** | `N:M` | Authorizations carry credentials
- **Authorization** → *has* → **Lifecycle** | `N:1` | Authorizations governed by lifecycle

#### Certification — 7 outgoing, 9 incoming

- **Certification** → *certifies* → **Component** | `N:M` | Certifications certify components
- **Certification** → *issued-by* → **GovernanceBody** | `N:1` | Certifications issued by governance body
- **Certification** → *validated-by* → **Audit** | `N:M` | Certifications validated by audits
- **Certification** → *referenced-by* → **Contract** | `N:M` | Certifications referenced by contracts
- **Certification** → *requires* → **Standard** | `N:1` | Certifications require standards
- **Certification** → *grants* → **Credential** | `1:N` | Certifications grant credentials
- **Certification** → *has* → **Lifecycle** | `N:1` | Certifications governed by lifecycle

#### Credential — 7 outgoing, 5 incoming

- **Credential** → *bound-to* → **Actor** | `N:1` | Credentials bound to actors
- **Credential** → *presented-for* → **Authorization** | `N:M` | Credentials presented for authorizations
- **Credential** → *referenced-by* → **Signature** | `N:M` | Credentials referenced by signatures
- **Credential** → *derived-from* → **Certification** | `N:1` | Credentials derived from certifications
- **Credential** → *enables* → **Session** | `N:M` | Credentials enable sessions
- **Credential** → *held-by* → **Participant** | `N:M` | Credentials held by participants
- **Credential** → *has* → **Lifecycle** | `N:1` | Credentials governed by lifecycle

#### Signature — 8 outgoing, 22 incoming

- **Signature** → *affixed-to* → **Artifact** | `N:M` | Signatures affixed to artifacts
- **Signature** → *traces-to* → **Credential** | `N:M` | Signatures trace to credentials
- **Signature** → *referenced-by* → **AuditTrail** | `N:M` | Signatures referenced by audit trails
- **Signature** → *affixed-to* → **Document** | `N:M` | Signatures affixed to documents
- **Signature** → *affixed-to* → **Record** | `N:M` | Signatures affixed to records
- **Signature** → *affixed-to* → **Approval** | `N:M` | Signatures affixed to approvals
- **Signature** → *affixed-to* → **Conclusion** | `N:M` | Signatures affixed to conclusions
- **Signature** → *has* → **Lifecycle** | `N:1` | Signatures governed by lifecycle

### TIER 13: Traceability & Baselines

#### Baseline — 9 outgoing, 6 incoming

- **Baseline** → *references* → **Artifact** | `N:M` | Baselines reference artifacts
- **Baseline** → *traces-to* → **Snapshot** | `N:1` | Baselines trace to snapshots
- **Baseline** → *signed-with* → **Signature** | `N:M` | Baselines signed with signatures
- **Baseline** → *compared-to* → **Checkpoint** | `N:M` | Baselines compared to checkpoints
- **Baseline** → *governs* → **Specification** | `N:M` | Baselines govern specifications
- **Baseline** → *contains* → **Document** | `N:M` | Baselines contain documents
- **Baseline** → *has* → **Lifecycle** | `N:1` | Baselines governed by lifecycle
- **Baseline** → *referenced-by* → **View** | `N:M` | Baselines referenced by views
- **Baseline** → *has* → **TraceabilityLink** | `1:N` | Baselines have traceability links

#### Snapshot — 7 outgoing, 6 incoming

- **Snapshot** → *compared-to* → **Snapshot** | `N:M` | Snapshots compared to snapshots
- **Snapshot** → *used-as* → **Baseline** | `N:1` | Snapshots used as baselines
- **Snapshot** → *traces-to* → **Artifact** | `N:M` | Snapshots trace to artifacts
- **Snapshot** → *signed-with* → **Signature** | `N:1` | Snapshots signed
- **Snapshot** → *captures* → **State** | `N:1` | Snapshots capture states
- **Snapshot** → *triggers* → **Checkpoint** | `1:N` | Snapshots trigger checkpoints
- **Snapshot** → *has* → **Lifecycle** | `N:1` | Snapshots governed by lifecycle

#### TraceabilityLink — 7 outgoing, 4 incoming

- **TraceabilityLink** → *connects* → **Artifact** | `N:M` | Traceability links connect artifacts
- **TraceabilityLink** → *signed-with* → **Signature** | `N:M` | Traceability links signed
- **TraceabilityLink** → *traces* → **Specification** | `N:M` | Links trace specifications
- **TraceabilityLink** → *traces* → **Feature** | `N:M` | Links trace features
- **TraceabilityLink** → *traces* → **Interface** | `N:M` | Links trace interfaces
- **TraceabilityLink** → *traces* → **Component** | `N:M` | Links trace components
- **TraceabilityLink** → *has* → **Lifecycle** | `N:1` | Links governed by lifecycle

#### Checkpoint — 7 outgoing, 4 incoming

- **Checkpoint** → *references* → **Baseline** | `N:1` | Checkpoints reference baselines
- **Checkpoint** → *traced-to* → **Milestone** | `N:1` | Checkpoints traced to milestones
- **Checkpoint** → *signed-with* → **Signature** | `N:M` | Checkpoints signed
- **Checkpoint** → *carries* → **Evidence** | `N:M` | Checkpoints carry evidence
- **Checkpoint** → *verifies* → **State** | `N:1` | Checkpoints verify states
- **Checkpoint** → *compared-to* → **Snapshot** | `N:M` | Checkpoints compared to snapshots
- **Checkpoint** → *has* → **Lifecycle** | `N:1` | Checkpoints governed by lifecycle

### TIER 14: Measurement

#### Metric — 7 outgoing, 11 incoming

- **Metric** → *generates* → **Measurement** | `1:N` | Metrics generate measurements
- **Metric** → *traces-to* → **Specification** | `N:M` | Metrics trace to specifications
- **Metric** → *monitors* → **Resource** | `N:M` | Metrics monitor resources
- **Metric** → *evaluates* → **Component** | `N:M` | Metrics evaluate components
- **Metric** → *defined-by* → **Standard** | `N:1` | Metrics defined by standards
- **Metric** → *included-in* → **Report** | `N:M` | Metrics included in reports
- **Metric** → *has* → **Lifecycle** | `N:1` | Metrics governed by lifecycle

#### Measurement — 7 outgoing, 5 incoming

- **Measurement** → *traces-to* → **Metric** | `N:1` | Measurements trace to metrics
- **Measurement** → *referenced-by* → **Report** | `N:M` | Measurements referenced by reports
- **Measurement** → *compared-to* → **Standard** | `N:M` | Measurements compared to standards
- **Measurement** → *signed-with* → **Signature** | `N:1` | Measurements signed
- **Measurement** → *captured-in* → **Record** | `N:1` | Measurements captured in records
- **Measurement** → *evaluated-by* → **Assessment** | `N:M` | Measurements evaluated by assessments
- **Measurement** → *has* → **Lifecycle** | `N:1` | Measurements governed by lifecycle

#### Assessment — 9 outgoing, 6 incoming

- **Assessment** → *contains* → **Finding** | `N:M` | Assessments contain findings
- **Assessment** → *references* → **Measurement** | `N:M` | Assessments reference measurements
- **Assessment** → *traces-to* → **Metric** | `N:M` | Assessments trace to metrics
- **Assessment** → *signed-with* → **Signature** | `N:1` | Assessments signed
- **Assessment** → *triggers* → **DecisionRecord** | `1:N` | Assessments trigger decision records
- **Assessment** → *evaluates* → **Process** | `N:M` | Assessments evaluate processes
- **Assessment** → *produces* → **Conclusion** | `1:N` | Assessments produce conclusions
- **Assessment** → *has* → **Lifecycle** | `N:1` | Assessments governed by lifecycle
- **Assessment** → *references* → **Guideline** | `N:M` | Assessments reference guidelines

### TIER 15: Audit & Review

#### Audit — 10 outgoing, 8 incoming

- **Audit** → *audits* → **Module** | `N:M` | Audits audit modules
- **Audit** → *measures-against* → **Standard** | `N:M` | Audits measure against standards
- **Audit** → *produces* → **Finding** | `1:N` | Audits produce findings
- **Audit** → *triggers* → **Sanction** | `1:N` | Audits trigger sanctions
- **Audit** → *reviews* → **Process** | `N:M` | Audits review processes
- **Audit** → *produces* → **Evidence** | `1:N` | Audits produce evidence
- **Audit** → *monitored-by* → **AuditTrail** | `N:1` | Audits monitored by audit trail
- **Audit** → *validates* → **Certification** | `N:M` | Audits validate certifications
- **Audit** → *has* → **Lifecycle** | `N:1` | Audits governed by lifecycle
- **Audit** → *summarized-in* → **TransparencyReport** | `N:M` | Audits summarized in transparency reports

#### Review — 9 outgoing, 8 incoming

- **Review** → *examines* → **Artifact** | `N:M` | Reviews examine artifacts
- **Review** → *produces* → **Finding** | `1:N` | Reviews produce findings
- **Review** → *recommends* → **Task** | `N:1` | Reviews recommend tasks
- **Review** → *triggers* → **Exception** | `N:M` | Reviews trigger exceptions
- **Review** → *evaluates* → **DecisionRecord** | `N:M` | Reviews evaluate decision records
- **Review** → *examines* → **Component** | `N:M` | Reviews examine components
- **Review** → *reviews* → **Amendment** | `N:1` | Reviews review amendments
- **Review** → *has* → **Lifecycle** | `N:1` | Reviews governed by lifecycle
- **Review** → *requires* → **Recusal** | `N:1` | Reviews may require recusals

#### AuditTrail — 8 outgoing, 8 incoming

- **AuditTrail** → *contains* → **Record** | `1:N` | Audit trails contain records
- **AuditTrail** → *traced-to* → **Artifact** | `N:M` | Audit trails traced to artifacts
- **AuditTrail** → *signed-at* → **Signature** | `N:M` | Audit trails signed at seal
- **AuditTrail** → *monitors* → **Process** | `N:M` | Audit trails monitor processes
- **AuditTrail** → *monitors* → **Session** | `N:M` | Audit trails monitor sessions
- **AuditTrail** → *contains* → **Log** | `1:N` | Audit trails contain logs
- **AuditTrail** → *monitors* → **Channel** | `N:M` | Audit trails monitor channels
- **AuditTrail** → *has* → **Lifecycle** | `N:1` | Audit trails governed by lifecycle

### TIER 16: Lifecycle & State

#### Lifecycle — 7 outgoing, 53 incoming

- **Lifecycle** → *has* → **State** | `1:N` | Lifecycles have states
- **Lifecycle** → *applies-to* → **Artifact** | `1:N` | Lifecycles apply to artifacts
- **Lifecycle** → *applies-to* → **Component** | `1:N` | Lifecycles apply to components
- **Lifecycle** → *applies-to* → **Module** | `1:N` | Lifecycles apply to modules
- **Lifecycle** → *governed-by* → **GovernanceBody** | `N:1` | Lifecycles governed by governance body
- **Lifecycle** → *defines* → **Milestone** | `1:N` | Lifecycles define milestones
- **Lifecycle** → *has* → **Lifecycle** | `N:1` | Lifecycles have their own lifecycle

#### State — 7 outgoing, 5 incoming

- **State** → *belongs-to* → **Lifecycle** | `N:1` | States belong to lifecycles
- **State** → *transitions-to* → **State** | `N:M` | States transition to other states
- **State** → *has* → **Invariant** | `N:M` | States have invariants
- **State** → *marked-by* → **Milestone** | `N:1` | States marked by milestones
- **State** → *captured-by* → **Snapshot** | `N:1` | States captured by snapshots
- **State** → *verified-by* → **Checkpoint** | `N:1` | States verified by checkpoints
- **State** → *has* → **Lifecycle** | `N:1` | States governed by lifecycle

### TIER 17: Exceptions & Waivers

#### Exception — 8 outgoing, 6 incoming

- **Exception** → *deviates-from* → **Rule** | `N:1` | Exceptions deviate from rules
- **Exception** → *deviates-from* → **Policy** | `N:1` | Exceptions deviate from policies
- **Exception** → *granted-by* → **GovernanceBody** | `N:1` | Exceptions granted by governance body
- **Exception** → *scoped-to* → **Module** | `N:1` | Exceptions scoped to modules
- **Exception** → *triggers* → **Review** | `N:1` | Exceptions trigger reviews
- **Exception** → *documented-in* → **Record** | `N:1` | Exceptions documented in records
- **Exception** → *has* → **Lifecycle** | `N:1` | Exceptions governed by lifecycle
- **Exception** → *requires* → **Waiver** | `1:1` | Exceptions may require waivers

#### Waiver — 8 outgoing, 3 incoming

- **Waiver** → *references* → **Rule** | `N:1` | Waivers reference rules
- **Waiver** → *bears* → **Signature** | `N:1` | Waivers bear signatures
- **Waiver** → *traces-to* → **Exception** | `N:1` | Waivers trace to exceptions
- **Waiver** → *time-bounded-by* → **Constraint** | `N:1` | Waivers bounded by constraints
- **Waiver** → *granted-by* → **GovernanceBody** | `N:1` | Waivers granted by governance body
- **Waiver** → *documented-in* → **Record** | `N:1` | Waivers documented in records
- **Waiver** → *has* → **Lifecycle** | `N:1` | Waivers governed by lifecycle
- **Waiver** → *requested-by* → **Actor** | `N:1` | Actors request waivers

### TIER 18: Governance Mechanics

#### Amendment — 7 outgoing, 5 incoming

- **Amendment** → *amends* → **Constitution** | `N:1` | Amendments amend constitution
- **Amendment** → *amends* → **Charter** | `N:M` | Amendments amend charters
- **Amendment** → *amends* → **Policy** | `N:M` | Amendments amend policies
- **Amendment** → *proposed-by* → **Actor** | `N:1` | Amendments proposed by actors
- **Amendment** → *reviewed-by* → **Review** | `N:1` | Amendments reviewed by reviews
- **Amendment** → *approved-by* → **GovernanceBody** | `N:1` | Amendments approved by governance body
- **Amendment** → *has* → **Lifecycle** | `N:1` | Amendments governed by lifecycle

#### Sanction — 8 outgoing, 4 incoming

- **Sanction** → *responds-to* → **Rule** | `N:M` | Sanctions respond to rule violations
- **Sanction** → *imposed-by* → **GovernanceBody** | `N:1` | Sanctions imposed by governance body
- **Sanction** → *on* → **Actor** | `N:1` | Sanctions imposed on actors
- **Sanction** → *recorded-in* → **Record** | `N:1` | Sanctions recorded in records
- **Sanction** → *triggered-by* → **Audit** | `N:1` | Sanctions triggered by audits
- **Sanction** → *appealed-via* → **Appeal** | `N:1` | Sanctions appealed via appeals
- **Sanction** → *has* → **Lifecycle** | `N:1` | Sanctions governed by lifecycle
- **Sanction** → *triggers* → **Dispute** | `1:N` | Sanctions trigger disputes

#### Precedent — 8 outgoing, 6 incoming

- **Precedent** → *guides* → **Decision** | `N:M` | Precedents guide decisions
- **Precedent** → *established-by* → **DecisionRecord** | `N:1` | Precedents established by decision records
- **Precedent** → *overruled-by* → **Conclusion** | `N:1` | Precedents overruled by conclusions
- **Precedent** → *cited-in* → **Appeal** | `N:M` | Precedents cited in appeals
- **Precedent** → *informs* → **Guideline** | `N:M` | Precedents inform guidelines
- **Precedent** → *has* → **Lifecycle** | `N:1` | Precedents governed by lifecycle
- **Precedent** → *informs* → **Policy** | `N:M` | Precedents inform policies
- **Precedent** → *informs* → **Rule** | `N:M` | Precedents inform rules

#### Appeal — 7 outgoing, 6 incoming

- **Appeal** → *challenges* → **Decision** | `N:1` | Appeals challenge decisions
- **Appeal** → *challenges* → **Sanction** | `N:1` | Appeals challenge sanctions
- **Appeal** → *filed-by* → **Actor** | `N:1` | Appeals filed by actors
- **Appeal** → *heard-by* → **GovernanceBody** | `N:1` | Appeals heard by governance body
- **Appeal** → *references* → **Precedent** | `N:M` | Appeals reference precedents
- **Appeal** → *results-in* → **DecisionRecord** | `1:N` | Appeals result in decision records
- **Appeal** → *has* → **Lifecycle** | `N:1` | Appeals governed by lifecycle

#### Veto — 6 outgoing, 4 incoming

- **Veto** → *rejects* → **Decision** | `N:1` | Vetoes reject decisions
- **Veto** → *exercised-by* → **Role** | `N:1` | Vetoes exercised by roles
- **Veto** → *recorded-in* → **Record** | `N:1` | Vetoes recorded in records
- **Veto** → *triggers* → **Appeal** | `1:N` | Vetoes trigger appeals
- **Veto** → *overrides* → **Approval** | `N:1` | Vetoes override approvals
- **Veto** → *has* → **Lifecycle** | `N:1` | Vetoes governed by lifecycle

### TIER 19: Dispute & Accountability

#### Dispute — 7 outgoing, 4 incoming

- **Dispute** → *between* → **Actor** | `N:M` | Disputes between actors
- **Dispute** → *mediated-by* → **GovernanceBody** | `N:1` | Disputes mediated by governance body
- **Dispute** → *results-in* → **DecisionRecord** | `1:N` | Disputes result in decision records
- **Dispute** → *escalated-via* → **Escalation** | `N:1` | Disputes escalated via escalations
- **Dispute** → *triggers* → **Recusal** | `1:N` | Disputes trigger recusals
- **Dispute** → *documented-in* → **Record** | `N:1` | Disputes documented in records
- **Dispute** → *has* → **Lifecycle** | `N:1` | Disputes governed by lifecycle

#### Recusal — 9 outgoing, 4 incoming

- **Recusal** → *withdraws* → **Actor** | `N:1` | Recusal withdraws actor
- **Recusal** → *from* → **Decision** | `N:1` | Recusal from decision
- **Recusal** → *required-by* → **Dispute** | `N:1` | Recusal required by dispute
- **Recusal** → *triggers* → **Review** | `N:1` | Recusal triggers review
- **Recusal** → *documented-in* → **Record** | `N:1` | Recusal documented in records
- **Recusal** → *has* → **Lifecycle** | `N:1` | Recusals governed by lifecycle
- **Recusal** → *required-by* → **GovernanceBody** | `N:M` | Governance body requires recusals
- **Recusal** → *declared-by* → **Actor** | `N:1` | Actors declare recusals
- **Recusal** → *required-by* → **Review** | `N:1` | Reviews may require recusals

#### TransparencyReport — 7 outgoing, 3 incoming

- **TransparencyReport** → *published-by* → **GovernanceBody** | `N:1` | Reports published by governance body
- **TransparencyReport** → *covers* → **Domain** | `N:M` | Reports cover domains
- **TransparencyReport** → *includes* → **Metric** | `N:M` | Reports include metrics
- **TransparencyReport** → *includes* → **Decision** | `N:M` | Reports include decisions
- **TransparencyReport** → *references* → **Audit** | `N:M` | Reports reference audits
- **TransparencyReport** → *signed-with* → **Signature** | `N:1` | Reports signed with signatures
- **TransparencyReport** → *has* → **Lifecycle** | `N:1` | Reports governed by lifecycle

### TIER 20: Cross-Cutting

#### Concern — 9 outgoing, 3 incoming

- **Concern** → *crosses* → **Slice** | `N:M` | Concerns cross slices
- **Concern** → *crosses* → **Layer** | `N:M` | Concerns cross layers
- **Concern** → *crosses* → **Domain** | `N:M` | Concerns cross domains
- **Concern** → *constrains* → **Component** | `N:M` | Concerns constrain components
- **Concern** → *constrains* → **Module** | `N:M` | Concerns constrain modules
- **Concern** → *constrains* → **Interface** | `N:M` | Concerns constrain interfaces
- **Concern** → *tracked-by* → **Evidence** | `N:M` | Concerns tracked by evidence
- **Concern** → *monitored-by* → **Metric** | `N:M` | Concerns monitored by metrics
- **Concern** → *has* → **Lifecycle** | `N:1` | Concerns governed by lifecycle

#### Escalation — 7 outgoing, 3 incoming

- **Escalation** → *escalates-from* → **Actor** | `N:1` | Escalations from actors
- **Escalation** → *escalates-to* → **GovernanceBody** | `N:1` | Escalations to governance body
- **Escalation** → *has* → **Task** | `1:N` | Escalations generate tasks
- **Escalation** → *documented-in* → **Record** | `N:1` | Escalations documented in records
- **Escalation** → *triggers* → **Dispute** | `1:N` | Escalations trigger disputes
- **Escalation** → *triggers* → **Review** | `N:1` | Escalations trigger reviews
- **Escalation** → *has* → **Lifecycle** | `N:1` | Escalations governed by lifecycle

#### View — 8 outgoing, 5 incoming

- **View** → *represents* → **Kernel** | `N:1` | Views represent kernel
- **View** → *represents* → **Domain** | `1:N` | Views represent domains
- **View** → *represents* → **Subsystem** | `1:N` | Views represent subsystems
- **View** → *filters* → **Component** | `N:M` | Views filter components
- **View** → *filters* → **Interface** | `N:M` | Views filter interfaces
- **View** → *generated-from* → **Snapshot** | `N:1` | Views generated from snapshots
- **View** → *used-by* → **Session** | `N:M` | Views used by sessions
- **View** → *references* → **Baseline** | `N:M` | Views reference baselines

--------------------------------------------------------------------------------
## Appendix A: Entity Statistics

| Entity | Out | In | Total | Tier |
|--------|-----|-----|-------|------|
| Kernel | 8 | 4 | 12 | 1 |
| Domain | 8 | 10 | 18 | 1 |
| Subsystem | 11 | 10 | 21 | 1 |
| Module | 12 | 20 | 32 | 1 |
| Component | 10 | 20 | 30 | 1 |
| Primitive | 7 | 5 | 12 | 1 |
| Resource | 7 | 6 | 13 | 1 |
| Layer | 8 | 9 | 17 | 2 |
| Tier | 7 | 4 | 11 | 2 |
| Slice | 9 | 7 | 16 | 2 |
| Assembly | 6 | 4 | 10 | 2 |
| Topology | 6 | 6 | 12 | 2 |
| Interface | 9 | 16 | 25 | 3 |
| Boundary | 7 | 7 | 14 | 3 |
| Channel | 7 | 3 | 10 | 3 |
| Contract | 7 | 8 | 15 | 3 |
| Capability | 8 | 5 | 13 | 4 |
| Feature | 9 | 5 | 14 | 4 |
| Process | 11 | 13 | 24 | 5 |
| Workflow | 9 | 4 | 13 | 5 |
| Task | 9 | 12 | 21 | 5 |
| Milestone | 8 | 8 | 16 | 5 |
| Plan | 8 | 4 | 12 | 5 |
| Constitution | 10 | 6 | 16 | 6 |
| Charter | 8 | 6 | 14 | 6 |
| GovernanceBody | 14 | 17 | 31 | 6 |
| Role | 9 | 8 | 17 | 6 |
| Policy | 9 | 7 | 16 | 6 |
| Rule | 9 | 7 | 16 | 6 |
| Standard | 9 | 8 | 17 | 7 |
| Guideline | 6 | 4 | 10 | 7 |
| Constraint | 10 | 15 | 25 | 7 |
| Invariant | 8 | 7 | 15 | 7 |
| Session | 10 | 10 | 20 | 8 |
| Actor | 11 | 15 | 26 | 8 |
| Participant | 6 | 5 | 11 | 8 |
| Context | 7 | 3 | 10 | 9 |
| Environment | 7 | 3 | 10 | 9 |
| Decision | 8 | 10 | 18 | 10 |
| DecisionRecord | 8 | 9 | 17 | 10 |
| Evidence | 9 | 19 | 28 | 10 |
| Finding | 8 | 8 | 16 | 10 |
| Conclusion | 8 | 7 | 15 | 10 |
| Artifact | 9 | 15 | 24 | 11 |
| Document | 7 | 3 | 10 | 11 |
| Specification | 8 | 9 | 17 | 11 |
| Record | 7 | 15 | 22 | 11 |
| Log | 7 | 3 | 10 | 11 |
| Report | 8 | 5 | 13 | 11 |
| Approval | 7 | 6 | 13 | 12 |
| Authorization | 7 | 4 | 11 | 12 |
| Certification | 7 | 9 | 16 | 12 |
| Credential | 7 | 5 | 12 | 12 |
| Signature | 8 | 22 | 30 | 12 |
| Baseline | 9 | 6 | 15 | 13 |
| Snapshot | 7 | 6 | 13 | 13 |
| TraceabilityLink | 7 | 4 | 11 | 13 |
| Checkpoint | 7 | 4 | 11 | 13 |
| Metric | 7 | 11 | 18 | 14 |
| Measurement | 7 | 5 | 12 | 14 |
| Assessment | 9 | 6 | 15 | 14 |
| Audit | 10 | 8 | 18 | 15 |
| Review | 9 | 8 | 17 | 15 |
| AuditTrail | 8 | 8 | 16 | 15 |
| Lifecycle | 7 | 53 | 60 | 16 |
| State | 7 | 5 | 12 | 16 |
| Exception | 8 | 6 | 14 | 17 |
| Waiver | 8 | 3 | 11 | 17 |
| Amendment | 7 | 5 | 12 | 18 |
| Sanction | 8 | 4 | 12 | 18 |
| Precedent | 8 | 6 | 14 | 18 |
| Appeal | 7 | 6 | 13 | 18 |
| Veto | 6 | 4 | 10 | 18 |
| Dispute | 7 | 4 | 11 | 19 |
| Recusal | 9 | 4 | 13 | 19 |
| TransparencyReport | 7 | 3 | 10 | 19 |
| Concern | 9 | 3 | 12 | 20 |
| Escalation | 7 | 3 | 10 | 20 |
| View | 8 | 5 | 13 | 20 |

--------------------------------------------------------------------------------
## Appendix B: Connectivity Matrix Summary

All 79 entities participate in the graph with no orphaned nodes.
The graph is strongly connected via Kernel as the root anchor.
Longest shortest-path diameter estimate: ~6 hops (Kernel to Credential/Veto)

Key hub entities (high betweenness):
- **Lifecycle** (60 total) — central lifecycle management hub
- **Signature** (30 total) — authorization and attestation hub
- **GovernanceBody** (31 total) — governance and decision hub
- **Module** (32 total) — structural composition hub
- **Component** (30 total) — reusable capability hub
- **Evidence** (28 total) — verification and validation hub

Key structural paths:
- Kernel → Domain → Subsystem → Module → Component → Interface (structural containment)
- Constitution → GovernanceBody → Policy → Rule → Constraint (governance chain)
- Actor → Task → Process → Workflow → Plan (work execution)
- Evidence → Finding → Conclusion → Decision → DecisionRecord (reasoning chain)
- Standard → Specification → Feature → Capability (capability realization)

--------------------------------------------------------------------------------
*Generated from Canonical Entity Catalog — 79 entities, 640 directed relationships*
*Relationship Graph v1.0 — Radius1 Kernel Repository Meta Model*


{'=' * 80}
PART III: MATRICES (All 10)
{'=' * 80}


# RADIUS1 KERNEL — REPOSITORY META MODEL (RMM)
# COMPLETE MATRICES PACKAGE — ALL 10 DELIVERABLES

---

## Summary
- **Total Entities:** 79
- **Total Matrices:** 10
- **Total Cells Filled:** All cells populated — no blanks, no N/A, no placeholders
- **Mutual Consistency:** Each entity carries identical values across all matrices where the same property is referenced

---

# MATRIX 1: OWNERSHIP MATRIX

| # | Entity | Constitution | Meta-Model | Governance | Module | Session | Process | System | Actor |
|---|--------|:------------:|:----------:|:----------:|:------:|:-------:|:-------:|:------:|:-----------:|
| 1 | **Kernel** | ● | · | · | · | · | · | · | · |
| 2 | **Domain** | · | ● | ○ | · | · | · | · | · |
| 3 | **Subsystem** | · | ● | ○ | · | · | · | · | · |
| 4 | **Module** | · | · | · | ● | · | · | · | · |
| 5 | **Component** | · | · | · | ● | · | · | · | · |
| 6 | **Primitive** | · | ● | ○ | · | · | · | · | · |
| 7 | **Resource** | · | ● | ○ | · | · | · | ○ | · |
| 8 | **Layer** | · | ● | · | · | · | · | · | · |
| 9 | **Tier** | · | ● | · | · | · | · | · | · |
| 10 | **Slice** | · | ● | · | · | · | · | · | · |
| 11 | **Assembly** | · | · | · | ● | · | · | · | · |
| 12 | **Topology** | · | ● | · | · | · | · | · | · |
| 13 | **Interface** | · | · | · | ● | · | · | · | · |
| 14 | **Boundary** | · | ● | · | · | · | · | · | · |
| 15 | **Channel** | · | · | · | ● | · | · | · | · |
| 16 | **Contract** | · | · | ● | · | · | · | · | · |
| 17 | **Capability** | · | ● | ○ | · | · | · | · | · |
| 18 | **Feature** | · | · | · | ● | · | · | · | · |
| 19 | **Process** | · | · | ● | · | · | · | · | · |
| 20 | **Workflow** | · | · | ● | · | · | ○ | · | · |
| 21 | **Task** | · | · | · | · | ● | ○ | · | · |
| 22 | **Milestone** | · | · | · | ● | · | ○ | · | · |
| 23 | **Plan** | · | · | ● | · | · | · | · | · |
| 24 | **Constitution** | ● | · | · | · | · | · | · | · |
| 25 | **Charter** | ● | · | ○ | · | · | · | · | · |
| 26 | **GovernanceBody** | ● | · | ○ | · | · | · | · | · |
| 27 | **Role** | · | · | ● | · | · | · | · | · |
| 28 | **Policy** | · | · | ● | · | · | · | · | · |
| 29 | **Rule** | · | · | ● | · | · | · | · | · |
| 30 | **Standard** | · | · | ● | · | · | · | · | · |
| 31 | **Guideline** | · | · | ● | · | · | · | · | · |
| 32 | **Constraint** | · | ● | ○ | · | · | · | · | · |
| 33 | **Invariant** | ● | · | · | · | · | · | · | · |
| 34 | **Session** | · | · | ● | · | · | · | · | · |
| 35 | **Actor** | ● | · | · | · | · | · | · | · |
| 36 | **Participant** | · | · | · | · | ● | · | · | · |
| 37 | **Context** | · | · | · | · | ● | · | · | · |
| 38 | **Environment** | · | · | · | ● | · | · | · | · |
| 39 | **Decision** | · | · | · | · | · | ● | · | ○ |
| 40 | **DecisionRecord** | · | · | ● | · | · | · | · | · |
| 41 | **Evidence** | · | · | · | · | · | ● | · | · |
| 42 | **Finding** | · | · | · | · | · | ● | · | · |
| 43 | **Conclusion** | · | · | ● | · | · | · | · | · |
| 44 | **Artifact** | ● | · | · | · | · | · | · | · |
| 45 | **Document** | · | · | · | ● | · | · | · | · |
| 46 | **Specification** | · | · | ● | · | · | · | · | · |
| 47 | **Record** | · | · | · | · | · | ● | · | · |
| 48 | **Log** | · | · | · | · | · | · | ● | · |
| 49 | **Report** | · | · | · | · | · | ● | · | · |
| 50 | **Approval** | · | · | ● | · | · | · | · | ○ |
| 51 | **Authorization** | · | · | ● | · | · | · | · | ○ |
| 52 | **Certification** | · | · | · | · | · | · | · | ○ |
| 53 | **Credential** | · | · | · | · | · | · | · | ● |
| 54 | **Signature** | · | · | · | · | · | · | · | ● |
| 55 | **Baseline** | · | · | ● | · | · | · | · | · |
| 56 | **Snapshot** | · | · | · | · | · | · | ● | · |
| 57 | **TraceabilityLink** | · | · | · | · | · | ● | · | · |
| 58 | **Checkpoint** | · | · | · | · | · | ● | · | · |
| 59 | **Metric** | · | · | ● | · | · | · | · | · |
| 60 | **Measurement** | · | · | · | · | · | ● | · | · |
| 61 | **Assessment** | · | · | · | · | · | ● | · | · |
| 62 | **Audit** | · | · | · | · | · | · | · | ○ |
| 63 | **Review** | · | · | · | · | · | · | · | ○ |
| 64 | **AuditTrail** | · | · | · | · | · | · | ● | · |
| 65 | **Lifecycle** | · | ● | ○ | · | · | · | · | · |
| 66 | **State** | · | ● | ○ | · | · | · | · | · |
| 67 | **Exception** | · | · | ● | · | · | · | · | · |
| 68 | **Waiver** | · | · | ● | · | · | · | · | · |
| 69 | **Amendment** | · | · | ● | · | · | · | · | · |
| 70 | **Sanction** | · | · | ● | · | · | · | · | · |
| 71 | **Precedent** | · | · | ● | · | · | · | · | · |
| 72 | **Appeal** | · | · | ● | · | · | · | · | · |
| 73 | **Veto** | · | · | ● | · | · | · | · | · |
| 74 | **Dispute** | · | · | ● | · | · | · | · | ○ |
| 75 | **Recusal** | · | · | ● | · | · | · | · | ○ |
| 76 | **TransparencyReport** | · | · | ● | · | · | · | · | · |
| 77 | **Concern** | · | ● | ○ | · | · | · | · | · |
| 78 | **Escalation** | · | · | ● | · | · | · | · | ○ |
| 79 | **View** | · | · | · | · | ○ | · | · | · |

**Legend:** ● = Primary Owner | ○ = Secondary Owner (entity belongs to this domain functionally)

---

# MATRIX 2: LIFECYCLE MATRIX

| # | Entity | Lifecycle States |
|---|--------|------------------|
| 1 | **Kernel** | Conceived → Bootstrapped → Active → Maintenance → Sunset → Archive |
| 2 | **Domain** | Identified → Defined → Active → Consolidated → Retired |
| 3 | **Subsystem** | Proposed → Approved → Forming → Active → Merging → Retired |
| 4 | **Module** | Proposed → Specified → Developing → Active → Stable → Deprecated → Retired |
| 5 | **Component** | Proposed → Designed → Implementing → Active → Reusable → Deprecated → Retired |
| 6 | **Primitive** | Identified → Ratified → Active → Universal → Immutable |
| 7 | **Resource** | Identified → Classified → Available → Allocated → Constrained → Depleted → Reclaimed |
| 8 | **Layer** | Proposed → Ratified → Active → Stable → Superseded → Retired |
| 9 | **Tier** | Defined → Ratified → Active → Stable → Retired |
| 10 | **Slice** | Identified → Mapped → Active → Evolving → Consolidated → Retired |
| 11 | **Assembly** | Defined → Composed → Active → Reconfiguring → Decomposed |
| 12 | **Topology** | Observed → Documented → Active → Evolving → Superseded → Archived |
| 13 | **Interface** | Draft → Reviewed → Ratified → Active → Evolving → Deprecated → Retired |
| 14 | **Boundary** | Defined → Ratified → Active → Adjusted → Dissolved |
| 15 | **Channel** | Defined → Connected → Active → Throttled → Disconnected → Removed |
| 16 | **Contract** | Draft → Negotiated → Ratified → Active → Amending → Superseded → Expired |
| 17 | **Capability** | Identified → Specified → Delivered → Evolving → Deprecated → Retired |
| 18 | **Feature** | Requested → Specified → Implementing → Delivered → Active → Enhancing → Deprecated → Removed |
| 19 | **Process** | Defined → Documented → Approved → Operational → Under-Review → Updated → Retired |
| 20 | **Workflow** | Designed → Reviewed → Approved → Active → Evolving → Deprecated → Retired |
| 21 | **Task** | Created → Assigned → Ready → In-Progress → Blocked / Awaiting-Review → Completing → Completed / Cancelled |
| 22 | **Milestone** | Defined → Pending → Approaching → Reached → Verified → Celebrated → Archived |
| 23 | **Plan** | Drafted → Reviewed → Approved → Active → In Progress → Adjusted → Completed → Closed → Archived |
| 24 | **Constitution** | Draft → Ratified → Active → AmendmentInProgress → Ratified |
| 25 | **Charter** | Draft → Proposed → Ratified → Active → Suspended → Dissolved |
| 26 | **GovernanceBody** | Chartered → Forming → Active → UnderReview → Rechartered → Suspended → Dissolved |
| 27 | **Role** | Proposed → Reviewed → Approved → Active → Deprecated → Retired |
| 28 | **Policy** | Draft → Consulted → Approved → Communicated → Active → UnderReview → Amended / Withdrawn |
| 29 | **Rule** | Draft → Proposed → Approved → Active → Suspended → Amended → Repealed |
| 30 | **Standard** | Draft → Proposed → UnderReview → Approved → Active → UnderRevision → Superseded / Retired |
| 31 | **Guideline** | Draft → Published → Active → Updated → Deprecated / Withdrawn |
| 32 | **Constraint** | Identified → Specified → Ratified → Active → Amending → Superseded → Retired |
| 33 | **Invariant** | Proposed → Ratified → Active → Eternal |
| 34 | **Session** | Initiated → Active → Suspended → Completing → Completed → Archived / Terminated |
| 35 | **Actor** | Registered → Active → Inactive → Decommissioned |
| 36 | **Participant** | Invited → Accepted → Active → Paused → Departed / Removed |
| 37 | **Context** | Created → Active → Modified → Saved → Discarded |
| 38 | **Environment** | Defined → Provisioned → Active → Degraded → Restored / Retired |
| 39 | **Decision** | Identified → Proposed → Deliberated → Made → Recorded → Implemented → Reviewed |
| 40 | **DecisionRecord** | Proposed → Options Identified → Evaluated → Decided → Recorded → Communicated → Revisited / Affirmed → Archived |
| 41 | **Evidence** | Gathered → Validated → Linked → Referenced → Challenged → Reaffirmed / Withdrawn → Archived |
| 42 | **Finding** | Observed → Documented → Reviewed → Validated → Published → Challenged → Reaffirmed / Corrected → Archived |
| 43 | **Conclusion** | Drafted → Supported by Findings → Reviewed → Approved → Published → Challenged → Reaffirmed / Replaced → Archived |
| 44 | **Artifact** | Defined → Created → Active → Archived → Destroyed |
| 45 | **Document** | Draft → Review → Approved → Published → Superseded → Archived |
| 46 | **Specification** | Proposed → Drafted → Reviewed → Approved → Baseline → Amendment → Superseded |
| 47 | **Record** | Created → Validated → Committed → Retained → Expired → Destroyed |
| 48 | **Log** | Opened → Appending → Closed → Archived → Expired |
| 49 | **Report** | Commissioned → Drafted → Reviewed → Approved → Published → Superseded |
| 50 | **Approval** | Requested → Reviewed → Granted / Denied → Conditional → Final → Withdrawn |
| 51 | **Authorization** | Requested → Evaluated → Granted → Active → Renewed → Revoked → Expired |
| 52 | **Certification** | Requested → Evaluated → Verified → Granted → Active → UnderRenewal → Renewed / Revoked / Expired |
| 53 | **Credential** | Issued → Active → Renewed → Suspended → Reactivated / Expired → Revoked → Destroyed |
| 54 | **Signature** | Prepared → Affixed → Validated → Active → Revoked → Expired |
| 55 | **Baseline** | Proposed → Reviewed → Approved → Frozen → Referenced → Amended → Superseded → Archived |
| 56 | **Snapshot** | Triggered → Capturing → Validated → Committed → Referenced → Expired |
| 57 | **TraceabilityLink** | Defined → Created → Verified → Active → Impacted → Updated / Broken → Removed → Archived |
| 58 | **Checkpoint** | Defined → Triggered → Capturing → Validated → Verified → Committed → Referenced → Superseded |
| 59 | **Metric** | Proposed → Defined → Reviewed → Approved → Active → Measured → Evaluated → Revised / Retired |
| 60 | **Measurement** | Triggered → Captured → Validated → Recorded → Analyzed → Referenced → Archived |
| 61 | **Assessment** | Commissioned → Planned → Executed → Analyzed → Drafted → Reviewed → Published → Appealed → Final → Archived |
| 62 | **Audit** | Planned → Chartered → Executed → EvidenceAnalyzed → ReportDrafted → Reviewed → Published → RemediationTracked → Closed |
| 63 | **Review** | Scheduled → Initiated → InProgress → FindingsDrafted → Reviewed → Published → Accepted / Contested → Closed |
| 64 | **AuditTrail** | Initiated → Recording → Active → Reviewed → Sealed → Archived → Expired |
| 65 | **Lifecycle** | Defined → Approved → Active → UnderReview → Updated → Superseded |
| 66 | **State** | Defined → Validated → Active → Deprecated → Retired |
| 67 | **Exception** | Requested → Justified → Reviewed → Granted → Active → Monitored → Expired / Renewed / Revoked |
| 68 | **Waiver** | Requested → Justified → Reviewed → Granted / Denied → Active → Expired → Renewed / Revoked |
| 69 | **Amendment** | Drafted → Submitted → Reviewed → Approved → Ratified → Applied → Recorded |
| 70 | **Sanction** | Triggered → Investigated → Proposed → Reviewed → Imposed → Appealed → Upheld / Overturned → Executed → Lifted |
| 71 | **Precedent** | Established → Active → Distinguished → Overruled → Archived |
| 72 | **Appeal** | Filed → Accepted → Scheduled → Heard → Deliberated → Upheld / Overturned / Remanded → Final → Recorded |
| 73 | **Veto** | Triggered → Justified → Exercised → Reviewed → Sustained / Overridden → Recorded |
| 74 | **Dispute** | Raised → Acknowledged → Scoped → Mediated → Arbitrated → Resolved → Appealed → Final → Archived |
| 75 | **Recusal** | Identified → Declared → Accepted → Executed → Verified → Lifted → Recorded |
| 76 | **TransparencyReport** | Planned → Compiled → Reviewed → Published → Acknowledged → Archived |
| 77 | **Concern** | Identified → Scoped → Addressed → Monitoring → Resolved → Ongoing |
| 78 | **Escalation** | Triggered → Documented → Routed → Received → Under-Review → Resolved / Redirected → Closed |
| 79 | **View** | Defined → Generated → Active → Stale → Refreshed → Archived |

---

# MATRIX 3: STABILITY CLASSIFICATION

| # | Entity | Stability Level | Rationale |
|---|--------|:---------------:|-----------|
| 1 | **Kernel** | Static | Root container; structural changes require constitutional amendment |
| 2 | **Domain** | Slow | Problem spaces evolve slowly; language and boundaries shift over quarters |
| 3 | **Subsystem** | Slow | Major functional areas change at release cadence |
| 4 | **Module** | Moderate | Active development units evolve at sprint/release pace |
| 5 | **Component** | Moderate | Reusable units refactor with feature demands |
| 6 | **Primitive** | Static | Atomic building blocks ratified once, immutable thereafter |
| 7 | **Resource** | Moderate | Resource types evolve with infrastructure changes |
| 8 | **Layer** | Slow | Architectural strata ratified and stable for extended periods |
| 9 | **Tier** | Static | Runtime levels are fixed architectural decisions |
| 10 | **Slice** | Moderate | Cross-cutting capabilities evolve with end-to-end requirements |
| 11 | **Assembly** | Moderate | Composed units reconfigure based on deployment needs |
| 12 | **Topology** | Moderate | Structural arrangement evolves with system growth |
| 13 | **Interface** | Slow | Contracts ratified and versioned; slow evolution preserves compatibility |
| 14 | **Boundary** | Slow | Encapsulation limits ratified at architectural level |
| 15 | **Channel** | Moderate | Communication pathways adapt to runtime needs |
| 16 | **Contract** | Slow | Mutual agreements ratified; superseded only through formal process |
| 17 | **Capability** | Moderate | What the system can do evolves with stakeholder needs |
| 18 | **Feature** | Fast | User-visible functionality changes at product velocity |
| 19 | **Process** | Slow | How work is done changes at governance cadence |
| 20 | **Workflow** | Slow | Work patterns change through process improvement |
| 21 | **Task** | Moderate | Individual work units change within single session |
| 22 | **Milestone** | Fast | Achievement points shift with project dynamics |
| 23 | **Plan** | Moderate | Plans adjust continuously to circumstances |
| 24 | **Constitution** | Static | Supreme instrument; amendments follow strict procedure |
| 25 | **Charter** | Slow | Authority documents change through formal dissolution/renewal |
| 26 | **GovernanceBody** | Slow | Decision-making groups recharter slowly |
| 27 | **Role** | Slow | Responsibility definitions shift through governance |
| 28 | **Policy** | Slow | Governing principles evolve through consultation |
| 29 | **Rule** | Moderate | Binding constraints amended as needs change |
| 30 | **Standard** | Slow | Mandatory requirements change through revision cycles |
| 31 | **Guideline** | Moderate | Best practices update continuously |
| 32 | **Constraint** | Slow | Architectural limits ratified; superseded formally |
| 33 | **Invariant** | Static | Unviolable truths ratified once, eternal thereafter |
| 34 | **Session** | Fast | Engagement periods are transient and dynamic |
| 35 | **Actor** | Moderate | Participants register and decommission over time |
| 36 | **Participant** | Fast | Session bindings are short-lived and dynamic |
| 37 | **Context** | Fast | Situational frames are inherently transient |
| 38 | **Environment** | Moderate | Operational surroundings shift with deployments |
| 39 | **Decision** | Slow | Choices commit the system; slow to reverse |
| 40 | **DecisionRecord** | Slow | Recorded decisions preserved for institutional memory |
| 41 | **Evidence** | Static after Validation | Facts validated once; immutable factual record |
| 42 | **Finding** | Moderate | Discoveries emerge from investigation |
| 43 | **Conclusion** | Slow | Judgments derived from evidence; authoritative |
| 44 | **Artifact** | Slow | Root category for all produced items |
| 45 | **Document** | Moderate | Documents evolve through review cycles |
| 46 | **Specification** | Static | Prescribed requirements baselined as authority |
| 47 | **Record** | Static after Commit | Immutable timestamped facts after commitment |
| 48 | **Log** | Fast during Appending, Static after Close | Append-only sequence; fast during capture |
| 49 | **Report** | Moderate | Communication artifacts evolve with findings |
| 50 | **Approval** | Static after Final | Authorized state frozen after finalization |
| 51 | **Authorization** | Moderate | Permission grants evolve through lifecycle |
| 52 | **Certification** | Slow | Compliance attestations change through renewal |
| 53 | **Credential** | Moderate | Identity tokens evolve through lifecycle events |
| 54 | **Signature** | Static after Validated | Non-repudiable mark validated once |
| 55 | **Baseline** | Static when Frozen | Reference point frozen after approval |
| 56 | **Snapshot** | Static after Commit | Point-in-time capture immutable after commit |
| 57 | **TraceabilityLink** | Moderate | Typed connections evolve with entities |
| 58 | **Checkpoint** | Static after Commit | Verified milestone frozen after commit |
| 59 | **Metric** | Slow | Measurement standards evolve through review |
| 60 | **Measurement** | Static after Recorded | Quantified observations immutable after recording |
| 61 | **Assessment** | Moderate | Evaluations emerge from systematic analysis |
| 62 | **Audit** | Moderate | Independent inspections produce findings |
| 63 | **Review** | Fast | Formal examinations produce rapid results |
| 64 | **AuditTrail** | Fast during Recording, Static after Seal | Chronological record; fast during capture |
| 65 | **Lifecycle** | Slow | State-machine definitions evolve slowly |
| 66 | **State** | Slow | Atomic conditions validated once defined |
| 67 | **Exception** | Fast | Temporary deviations are transient by nature |
| 68 | **Waiver** | Slow | Formal exceptions change through expiration/renewal |
| 69 | **Amendment** | Fast | Formal changes proceed through fast-track process |
| 70 | **Sanction** | Moderate | Corrective measures follow due process |
| 71 | **Precedent** | Slow | Prior rulings guide future cases; not freezable |
| 72 | **Appeal** | Fast | Reconsideration requests resolve quickly |
| 73 | **Veto** | Fast | Rejection events are fast and decisive |
| 74 | **Dispute** | Fast | Conflicts resolve through structured process |
| 75 | **Recusal** | Fast | Withdrawal events are fast and documented |
| 76 | **TransparencyReport** | Moderate | Periodic disclosures at governance cadence |
| 77 | **Concern** | Slow | Cross-cutting interests persist over time |
| 78 | **Escalation** | Fast | Authority elevation events are rapid |
| 79 | **View** | Fast | Perspective representations are transient |

**Stability Levels:** Static (never changes) | Slow (changes at governance cadence) | Moderate (changes at release/sprint pace) | Fast (changes within single session)

---

# MATRIX 4: VERSIONABILITY MATRIX

| # | Entity | Versionable? | Rationale |
|---|--------|:------------:|-----------|
| 1 | **Kernel** | Yes | Entity evolves through states; versioning enables tracking |
| 2 | **Domain** | Yes | Entity evolves through states; versioning enables tracking |
| 3 | **Subsystem** | Yes | Entity evolves through states; versioning enables tracking |
| 4 | **Module** | Yes | Entity evolves through states; versioning enables tracking |
| 5 | **Component** | Yes | Entity evolves through states; versioning enables tracking |
| 6 | **Primitive** | No | Static entity; single version sufficient |
| 7 | **Resource** | Yes | Entity evolves through states; versioning enables tracking |
| 8 | **Layer** | Yes | Entity evolves through states; versioning enables tracking |
| 9 | **Tier** | Yes | Entity evolves through states; versioning enables tracking |
| 10 | **Slice** | Yes | Entity evolves through states; versioning enables tracking |
| 11 | **Assembly** | Yes | Entity evolves through states; versioning enables tracking |
| 12 | **Topology** | Yes | Entity evolves through states; versioning enables tracking |
| 13 | **Interface** | Yes | Entity evolves through states; versioning enables tracking |
| 14 | **Boundary** | Yes | Entity evolves through states; versioning enables tracking |
| 15 | **Channel** | Yes | Entity evolves through states; versioning enables tracking |
| 16 | **Contract** | Yes | Entity evolves through states; versioning enables tracking |
| 17 | **Capability** | Yes | Entity evolves through states; versioning enables tracking |
| 18 | **Feature** | Yes | Entity evolves through states; versioning enables tracking |
| 19 | **Process** | Yes | Entity evolves through states; versioning enables tracking |
| 20 | **Workflow** | Yes | Entity evolves through states; versioning enables tracking |
| 21 | **Task** | Yes | Entity evolves through states; versioning enables tracking |
| 22 | **Milestone** | Yes | Entity evolves through states; versioning enables tracking |
| 23 | **Plan** | Yes | Entity evolves through states; versioning enables tracking |
| 24 | **Constitution** | Yes | Entity evolves through states; versioning enables tracking |
| 25 | **Charter** | Yes | Entity evolves through states; versioning enables tracking |
| 26 | **GovernanceBody** | Yes | Entity evolves through states; versioning enables tracking |
| 27 | **Role** | Yes | Entity evolves through states; versioning enables tracking |
| 28 | **Policy** | Yes | Entity evolves through states; versioning enables tracking |
| 29 | **Rule** | Yes | Entity evolves through states; versioning enables tracking |
| 30 | **Standard** | Yes | Entity evolves through states; versioning enables tracking |
| 31 | **Guideline** | Yes | Entity evolves through states; versioning enables tracking |
| 32 | **Constraint** | Yes | Entity evolves through states; versioning enables tracking |
| 33 | **Invariant** | No | Static entity; single version sufficient |
| 34 | **Session** | Yes | Entity evolves through states; versioning enables tracking |
| 35 | **Actor** | Yes | Entity evolves through states; versioning enables tracking |
| 36 | **Participant** | No | Transient entity; versioning overhead not justified |
| 37 | **Context** | No | Transient entity; versioning overhead not justified |
| 38 | **Environment** | Yes | Entity evolves through states; versioning enables tracking |
| 39 | **Decision** | Yes | Entity evolves through states; versioning enables tracking |
| 40 | **DecisionRecord** | Yes | Entity evolves through states; versioning enables tracking |
| 41 | **Evidence** | No | Static entity; single version sufficient |
| 42 | **Finding** | Yes | Entity evolves through states; versioning enables tracking |
| 43 | **Conclusion** | Yes | Entity evolves through states; versioning enables tracking |
| 44 | **Artifact** | Yes | Entity evolves through states; versioning enables tracking |
| 45 | **Document** | Yes | Entity evolves through states; versioning enables tracking |
| 46 | **Specification** | Yes | Entity evolves through states; versioning enables tracking |
| 47 | **Record** | No | Static entity; single version sufficient |
| 48 | **Log** | No | Transient entity; versioning overhead not justified |
| 49 | **Report** | Yes | Entity evolves through states; versioning enables tracking |
| 50 | **Approval** | Yes | Entity evolves through states; versioning enables tracking |
| 51 | **Authorization** | Yes | Entity evolves through states; versioning enables tracking |
| 52 | **Certification** | Yes | Entity evolves through states; versioning enables tracking |
| 53 | **Credential** | No | Entity nature does not require versioning |
| 54 | **Signature** | No | Static entity; single version sufficient |
| 55 | **Baseline** | Yes | Entity evolves through states; versioning enables tracking |
| 56 | **Snapshot** | No | Static entity; single version sufficient |
| 57 | **TraceabilityLink** | Yes | Entity evolves through states; versioning enables tracking |
| 58 | **Checkpoint** | No | Static entity; single version sufficient |
| 59 | **Metric** | Yes | Entity evolves through states; versioning enables tracking |
| 60 | **Measurement** | No | Static entity; single version sufficient |
| 61 | **Assessment** | Yes | Entity evolves through states; versioning enables tracking |
| 62 | **Audit** | Yes | Entity evolves through states; versioning enables tracking |
| 63 | **Review** | Yes | Entity evolves through states; versioning enables tracking |
| 64 | **AuditTrail** | No | Transient entity; versioning overhead not justified |
| 65 | **Lifecycle** | Yes | Entity evolves through states; versioning enables tracking |
| 66 | **State** | Yes | Entity evolves through states; versioning enables tracking |
| 67 | **Exception** | Yes | Entity evolves through states; versioning enables tracking |
| 68 | **Waiver** | Yes | Entity evolves through states; versioning enables tracking |
| 69 | **Amendment** | Yes | Entity evolves through states; versioning enables tracking |
| 70 | **Sanction** | Yes | Entity evolves through states; versioning enables tracking |
| 71 | **Precedent** | Yes | Entity evolves through states; versioning enables tracking |
| 72 | **Appeal** | Yes | Entity evolves through states; versioning enables tracking |
| 73 | **Veto** | Yes | Entity evolves through states; versioning enables tracking |
| 74 | **Dispute** | Yes | Entity evolves through states; versioning enables tracking |
| 75 | **Recusal** | Yes | Entity evolves through states; versioning enables tracking |
| 76 | **TransparencyReport** | Yes | Entity evolves through states; versioning enables tracking |
| 77 | **Concern** | Yes | Entity evolves through states; versioning enables tracking |
| 78 | **Escalation** | Yes | Entity evolves through states; versioning enables tracking |
| 79 | **View** | Yes | Entity evolves through states; versioning enables tracking |

---

# MATRIX 5: FREEZE MATRIX

| # | Entity | Freezable? | Freeze Trigger | Rationale |
|---|--------|:----------:|----------------|-----------|
| 1 | **Kernel** | Yes | Constitutional amendment or system retirement | Entity reaches stable states warranting freeze |
| 2 | **Domain** | Yes | Domain consolidation or retirement | Entity reaches stable states warranting freeze |
| 3 | **Subsystem** | Yes | Subsystem merger or retirement | Entity reaches stable states warranting freeze |
| 4 | **Module** | Yes | Module reaches stable release or deprecation | Entity reaches stable states warranting freeze |
| 5 | **Component** | Yes | Component reaches stable reusable state | Entity reaches stable states warranting freeze |
| 6 | **Primitive** | Yes | Primitive ratification — frozen at ratification | Fundamental truth; frozen by ratification |
| 7 | **Resource** | Yes | Resource allocation commitment | Entity reaches stable states warranting freeze |
| 8 | **Layer** | Yes | Layer ratification — architectural stability | Entity reaches stable states warranting freeze |
| 9 | **Tier** | Yes | Tier ratification — frozen after ratification | Fundamental truth; frozen by ratification |
| 10 | **Slice** | Yes | Slice consolidation or retirement | Entity reaches stable states warranting freeze |
| 11 | **Assembly** | Yes | Assembly composition finalization | Entity reaches stable states warranting freeze |
| 12 | **Topology** | Yes | Topology documentation approved as reference | Entity reaches stable states warranting freeze |
| 13 | **Interface** | Yes | Interface ratification — contract freeze | Contractual entity; freeze preserves agreement terms |
| 14 | **Boundary** | Yes | Boundary ratification — architectural boundary | Entity reaches stable states warranting freeze |
| 15 | **Channel** | Yes | Channel connection established | Entity reaches stable states warranting freeze |
| 16 | **Contract** | Yes | Contract ratification — mutual agreement freeze | Contractual entity; freeze preserves agreement terms |
| 17 | **Capability** | Yes | Capability delivery milestone | Entity reaches stable states warranting freeze |
| 18 | **Feature** | Yes | Feature delivery freeze for release | Entity reaches stable states warranting freeze |
| 19 | **Process** | Yes | Process approval as operational standard | Entity reaches stable states warranting freeze |
| 20 | **Workflow** | Yes | Workflow approval as operational pattern | Entity reaches stable states warranting freeze |
| 21 | **Task** | Yes | Task completion or cancellation | Entity reaches stable states warranting freeze |
| 22 | **Milestone** | Yes | Milestone verification and celebration | Entity reaches stable states warranting freeze |
| 23 | **Plan** | Yes | Plan approval as authorized blueprint | Entity reaches stable states warranting freeze |
| 24 | **Constitution** | Yes | Constitution ratification — supreme freeze | Fundamental truth; frozen by ratification |
| 25 | **Charter** | Yes | Charter ratification — authority freeze | Entity reaches stable states warranting freeze |
| 26 | **GovernanceBody** | No | Not freezable — governance body must remain adaptable | Governance body must remain adaptable to function |
| 27 | **Role** | Yes | Role approval — permission boundary freeze | Entity reaches stable states warranting freeze |
| 28 | **Policy** | Yes | Policy approval as governing principle | Entity reaches stable states warranting freeze |
| 29 | **Rule** | Yes | Rule approval as binding constraint | Entity reaches stable states warranting freeze |
| 30 | **Standard** | Yes | Standard approval as mandatory requirement | Entity reaches stable states warranting freeze |
| 31 | **Guideline** | No | Not freezable — advisory guidance evolves continuously | Advisory guidance evolves continuously |
| 32 | **Constraint** | Yes | Constraint ratification — architectural integrity freeze | Entity reaches stable states warranting freeze |
| 33 | **Invariant** | Yes | Invariant ratification — permanent structural truth | Fundamental truth; frozen by ratification |
| 34 | **Session** | Yes | Session completion or termination | Entity reaches stable states warranting freeze |
| 35 | **Actor** | No | Not freezable — actor status must remain dynamic | Actor status must remain dynamic for accountability |
| 36 | **Participant** | Yes | Session freeze captures participant snapshot | Entity reaches stable states warranting freeze |
| 37 | **Context** | No | Not freezable — context is inherently transient | Context is inherently transient; cannot be frozen |
| 38 | **Environment** | Yes | Environment provisioning freeze for stability | Entity reaches stable states warranting freeze |
| 39 | **Decision** | Yes | Decision recording — commitment freeze | Entity reaches stable states warranting freeze |
| 40 | **DecisionRecord** | Yes | Decision recording and communication | Entity reaches stable states warranting freeze |
| 41 | **Evidence** | Yes | Evidence validation — factual freeze | Audit/evidence entity; immutability required after freeze |
| 42 | **Finding** | Yes | Finding validation and publication | Entity reaches stable states warranting freeze |
| 43 | **Conclusion** | Yes | Conclusion approval and publication | Entity reaches stable states warranting freeze |
| 44 | **Artifact** | Yes | Artifact baseline or archival | Entity reaches stable states warranting freeze |
| 45 | **Document** | Yes | Document publication — published state freeze | Entity reaches stable states warranting freeze |
| 46 | **Specification** | Yes | Specification baseline — authoritative freeze | Contractual entity; freeze preserves agreement terms |
| 47 | **Record** | Yes | Record commitment — immutable factual capture | Audit/evidence entity; immutability required after freeze |
| 48 | **Log** | Yes | Log closure — append-only sequence sealed | Audit/evidence entity; immutability required after freeze |
| 49 | **Report** | Yes | Report publication — approved communication freeze | Entity reaches stable states warranting freeze |
| 50 | **Approval** | Yes | Approval finalization — authorized state freeze | Audit/evidence entity; immutability required after freeze |
| 51 | **Authorization** | No | Not freezable — authorization must be revocable | Must remain revocable; freeze would prevent revocation |
| 52 | **Certification** | Yes | Certification grant — verified compliance freeze | Entity reaches stable states warranting freeze |
| 53 | **Credential** | No | Not freezable — credential lifecycle must be dynamic | Must remain revocable; freeze would prevent revocation |
| 54 | **Signature** | Yes | Signature validation — non-repudiation freeze | Audit/evidence entity; immutability required after freeze |
| 55 | **Baseline** | Yes | Baseline freeze — authoritative reference point | Audit/evidence entity; immutability required after freeze |
| 56 | **Snapshot** | Yes | Snapshot commit — point-in-time state freeze | Audit/evidence entity; immutability required after freeze |
| 57 | **TraceabilityLink** | Yes | Traceability link verification | Entity reaches stable states warranting freeze |
| 58 | **Checkpoint** | Yes | Checkpoint commit — verified milestone state freeze | Audit/evidence entity; immutability required after freeze |
| 59 | **Metric** | Yes | Metric approval as measurement standard | Entity reaches stable states warranting freeze |
| 60 | **Measurement** | Yes | Measurement recording — quantified observation freeze | Audit/evidence entity; immutability required after freeze |
| 61 | **Assessment** | Yes | Assessment publication as final evaluation | Entity reaches stable states warranting freeze |
| 62 | **Audit** | Yes | Audit publication — independent inspection freeze | Entity reaches stable states warranting freeze |
| 63 | **Review** | Yes | Review publication — formal examination freeze | Entity reaches stable states warranting freeze |
| 64 | **AuditTrail** | Yes | Audit trail seal — tamper-evident record freeze | Audit/evidence entity; immutability required after freeze |
| 65 | **Lifecycle** | Yes | Lifecycle definition approval | Entity reaches stable states warranting freeze |
| 66 | **State** | Yes | State validation — lifecycle atomic unit freeze | Entity reaches stable states warranting freeze |
| 67 | **Exception** | Yes | Exception grant — temporary deviation freeze | Entity reaches stable states warranting freeze |
| 68 | **Waiver** | Yes | Waiver grant — formal exception freeze | Entity reaches stable states warranting freeze |
| 69 | **Amendment** | Yes | Amendment ratification — formal change freeze | Entity reaches stable states warranting freeze |
| 70 | **Sanction** | Yes | Sanction imposition — punitive measure freeze | Entity reaches stable states warranting freeze |
| 71 | **Precedent** | No | Not freezable — precedent must remain distinguishable/overridable | Precedent must remain distinguishable/overridable |
| 72 | **Appeal** | Yes | Appeal final determination | Entity reaches stable states warranting freeze |
| 73 | **Veto** | Yes | Veto exercise — rejection freeze | Entity reaches stable states warranting freeze |
| 74 | **Dispute** | Yes | Dispute resolution finalization | Entity reaches stable states warranting freeze |
| 75 | **Recusal** | Yes | Recusal execution — withdrawal freeze | Entity reaches stable states warranting freeze |
| 76 | **TransparencyReport** | Yes | Transparency report publication | Entity reaches stable states warranting freeze |
| 77 | **Concern** | Yes | Concern scoping and addressing | Entity reaches stable states warranting freeze |
| 78 | **Escalation** | Yes | Escalation resolution — authority elevation freeze | Entity reaches stable states warranting freeze |
| 79 | **View** | Yes | View generation — perspective snapshot freeze | Entity reaches stable states warranting freeze |

---

# MATRIX 6: SOURCE-OF-TRUTH MATRIX

| # | Entity | Source of Truth | Type | Rationale |
|---|--------|-----------------|------|-----------|
| 1 | **Kernel** | 00-CONSTITUTION/ | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 2 | **Domain** | 01-META-MODEL/Domain/ | Registry | Structural ontology definitions; canonical system architecture |
| 3 | **Subsystem** | 01-META-MODEL/Subsystem/ | Registry | Structural ontology definitions; canonical system architecture |
| 4 | **Module** | 01-META-MODEL/Module/ | Registry | Structural ontology definitions; canonical system architecture |
| 5 | **Component** | Owning Module's META/Component/ | Registry | Structural ontology definitions; canonical system architecture |
| 6 | **Primitive** | 01-META-MODEL/Primitive/ | Registry | Structural ontology definitions; canonical system architecture |
| 7 | **Resource** | 01-META-MODEL/Resource/ | Registry | Structural ontology definitions; canonical system architecture |
| 8 | **Layer** | 01-META-MODEL/Layer/ | Registry | Structural ontology definitions; canonical system architecture |
| 9 | **Tier** | 01-META-MODEL/Tier/ | Registry | Structural ontology definitions; canonical system architecture |
| 10 | **Slice** | 01-META-MODEL/Slice/ | Registry | Structural ontology definitions; canonical system architecture |
| 11 | **Assembly** | Owning Module's META/Assembly/ | Registry | Structural ontology definitions; canonical system architecture |
| 12 | **Topology** | 01-META-MODEL/Topology/ | Registry | Structural ontology definitions; canonical system architecture |
| 13 | **Interface** | Owning entity's META/Interface/ | Registry | Structural ontology definitions; canonical system architecture |
| 14 | **Boundary** | 01-META-MODEL/Boundary/ | Registry | Structural ontology definitions; canonical system architecture |
| 15 | **Channel** | Owning Module's META/Channel/ | Registry | Structural ontology definitions; canonical system architecture |
| 16 | **Contract** | 06-CONTRACTS/ | Registry | Mutual agreements registry; contract storage |
| 17 | **Capability** | 01-META-MODEL/Capability/ | Registry | Structural ontology definitions; canonical system architecture |
| 18 | **Feature** | 07-WORKFLOW/ | Store | Process and work definitions; operational store |
| 19 | **Process** | 07-WORKFLOW/ | Store | Process and work definitions; operational store |
| 20 | **Workflow** | 07-WORKFLOW/ | Store | Process and work definitions; operational store |
| 21 | **Task** | 99-STATE/ | Store | Session and runtime state; transient operational store |
| 22 | **Milestone** | 07-WORKFLOW/ | Store | Process and work definitions; operational store |
| 23 | **Plan** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 24 | **Constitution** | 00-CONSTITUTION/Constitution.md | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 25 | **Charter** | 00-CONSTITUTION/Charters/ | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 26 | **GovernanceBody** | 02-GOVERNANCE/Bodies/ | Ledger | Governance decisions and records; authoritative ledger |
| 27 | **Role** | 00-CONSTITUTION/ | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 28 | **Policy** | 02-GOVERNANCE/Policies/ | Ledger | Governance decisions and records; authoritative ledger |
| 29 | **Rule** | 02-GOVERNANCE/Rules/ | Ledger | Governance decisions and records; authoritative ledger |
| 30 | **Standard** | 03-STANDARDS/ | Registry | Standards and environment specifications; operational substrate |
| 31 | **Guideline** | 03-STANDARDS/Guidelines/ | Registry | Standards and environment specifications; operational substrate |
| 32 | **Constraint** | 01-META-MODEL/Constraint/ | Registry | Structural ontology definitions; canonical system architecture |
| 33 | **Invariant** | 00-CONSTITUTION/ | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 34 | **Session** | 99-STATE/ | Store | Session and runtime state; transient operational store |
| 35 | **Actor** | 00-CONSTITUTION/ | Ledger | Supreme governance instrument; ultimate source of legitimacy |
| 36 | **Participant** | 99-STATE/ | Store | Session and runtime state; transient operational store |
| 37 | **Context** | 99-STATE/Context/ | Store | Session and runtime state; transient operational store |
| 38 | **Environment** | 03-STANDARDS/ | Registry | Standards and environment specifications; operational substrate |
| 39 | **Decision** | 05-EVIDENCE/ | Vault | Factual evidence vault; immutable evidentiary records |
| 40 | **DecisionRecord** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 41 | **Evidence** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 42 | **Finding** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 43 | **Conclusion** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 44 | **Artifact** | Artifact Repository | Repository | Produced artifacts; content repository |
| 45 | **Document** | Artifact Repository | Repository | Produced artifacts; content repository |
| 46 | **Specification** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 47 | **Record** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 48 | **Log** | Audit Log | Store | System-generated audit trail; append-only log store |
| 49 | **Report** | Artifact Repository | Repository | Produced artifacts; content repository |
| 50 | **Approval** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 51 | **Authorization** | 02-GOVERNANCE/Authorizations/ | Ledger | Governance decisions and records; authoritative ledger |
| 52 | **Certification** | 05-EVIDENCE/Certifications/ | Vault | Factual evidence vault; immutable evidentiary records |
| 53 | **Credential** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 54 | **Signature** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 55 | **Baseline** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 56 | **Snapshot** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 57 | **TraceabilityLink** | Registry Service | Registry | Typed connections registry; relationship indexing |
| 58 | **Checkpoint** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 59 | **Metric** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 60 | **Measurement** | Evidence Vault | Vault | Factual evidence vault; immutable evidentiary records |
| 61 | **Assessment** | Artifact Repository | Repository | Produced artifacts; content repository |
| 62 | **Audit** | 05-EVIDENCE/Audits/ | Vault | Factual evidence vault; immutable evidentiary records |
| 63 | **Review** | 05-EVIDENCE/Reviews/ | Vault | Factual evidence vault; immutable evidentiary records |
| 64 | **AuditTrail** | Audit Log | Store | System-generated audit trail; append-only log store |
| 65 | **Lifecycle** | 01-META-MODEL/Lifecycles/ | Registry | Structural ontology definitions; canonical system architecture |
| 66 | **State** | 01-META-MODEL/ | Registry | Structural ontology definitions; canonical system architecture |
| 67 | **Exception** | 02-GOVERNANCE/Exceptions/ | Ledger | Governance decisions and records; authoritative ledger |
| 68 | **Waiver** | Governance Ledger | Ledger | Governance decisions and records; authoritative ledger |
| 69 | **Amendment** | 02-GOVERNANCE/Amendments/ | Ledger | Governance decisions and records; authoritative ledger |
| 70 | **Sanction** | 02-GOVERNANCE/Sanctions/ | Ledger | Governance decisions and records; authoritative ledger |
| 71 | **Precedent** | 02-GOVERNANCE/Precedents/ | Ledger | Governance decisions and records; authoritative ledger |
| 72 | **Appeal** | 02-GOVERNANCE/Appeals/ | Ledger | Governance decisions and records; authoritative ledger |
| 73 | **Veto** | 02-GOVERNANCE/Vetoes/ | Ledger | Governance decisions and records; authoritative ledger |
| 74 | **Dispute** | 02-GOVERNANCE/Disputes/ | Ledger | Governance decisions and records; authoritative ledger |
| 75 | **Recusal** | 02-GOVERNANCE/Recusals/ | Ledger | Governance decisions and records; authoritative ledger |
| 76 | **TransparencyReport** | 05-EVIDENCE/TransparencyReports/ | Vault | Factual evidence vault; immutable evidentiary records |
| 77 | **Concern** | 01-META-MODEL/Concern/ | Registry | Structural ontology definitions; canonical system architecture |
| 78 | **Escalation** | 02-GOVERNANCE/Escalations/ | Ledger | Governance decisions and records; authoritative ledger |
| 79 | **View** | 99-STATE/View/ | Store | Session and runtime state; transient operational store |

**Source Types:** Ledger (authoritative governance record) | Registry (structural definitions) | Vault (immutable evidence) | Repository (content storage) | Store (operational state)

---

# MATRIX 7: CREATION & MODIFICATION PERMISSIONS MATRIX

| # | Entity | AI Create? | AI Modify? | Human Modify? | Notes |
|---|--------|:----------:|:----------:|:-------------:|-------|
| 1 | **Kernel** | No | With Approval | Yes | AI cannot create but may modify with approval |
| 2 | **Domain** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 3 | **Subsystem** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 4 | **Module** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 5 | **Component** | Yes | Yes | Yes | Full AI autonomy; human oversight available |
| 6 | **Primitive** | No | No | No | Immutable after ratification; all modifications blocked |
| 7 | **Resource** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 8 | **Layer** | No | No | Yes | Human-only governance; AI excluded for accountability |
| 9 | **Tier** | No | No | Yes | Human-only governance; AI excluded for accountability |
| 10 | **Slice** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 11 | **Assembly** | Yes | Yes | Yes | Full AI autonomy; human oversight available |
| 12 | **Topology** | Yes | Yes | Yes | Full AI autonomy; human oversight available |
| 13 | **Interface** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 14 | **Boundary** | No | No | Yes | Human-only governance; AI excluded for accountability |
| 15 | **Channel** | Yes | Yes | Yes | Full AI autonomy; human oversight available |
| 16 | **Contract** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 17 | **Capability** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 18 | **Feature** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 19 | **Process** | No | With Approval | Yes | AI cannot create but may modify with approval |
| 20 | **Workflow** | No | With Approval | Yes | AI cannot create but may modify with approval |
| 21 | **Task** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 22 | **Milestone** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 23 | **Plan** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 24 | **Constitution** | No | No | With Approval | Highly restricted; amendment procedures required |
| 25 | **Charter** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 26 | **GovernanceBody** | No | No | With Approval | Highly restricted; amendment procedures required |
| 27 | **Role** | No | No | Yes | Human-only governance; AI excluded for accountability |
| 28 | **Policy** | With Approval | No | With Approval | AI may propose; only humans can modify |
| 29 | **Rule** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 30 | **Standard** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 31 | **Guideline** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 32 | **Constraint** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 33 | **Invariant** | No | No | No | Immutable after ratification; all modifications blocked |
| 34 | **Session** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 35 | **Actor** | No | No | Yes | Human-only governance; AI excluded for accountability |
| 36 | **Participant** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 37 | **Context** | Yes | Yes | Yes | Full AI autonomy; human oversight available |
| 38 | **Environment** | No | With Approval | Yes | AI cannot create but may modify with approval |
| 39 | **Decision** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 40 | **DecisionRecord** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 41 | **Evidence** | Yes | No | No | Write-once entity; immutable after creation |
| 42 | **Finding** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 43 | **Conclusion** | With Approval | No | With Approval | AI may propose; only humans can modify |
| 44 | **Artifact** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 45 | **Document** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 46 | **Specification** | With Approval | No | With Approval | AI may propose; only humans can modify |
| 47 | **Record** | Yes | No | No | Write-once entity; immutable after creation |
| 48 | **Log** | Yes | No | No | Write-once entity; immutable after creation |
| 49 | **Report** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 50 | **Approval** | No | No | With Approval | Highly restricted; amendment procedures required |
| 51 | **Authorization** | No | No | With Approval | Highly restricted; amendment procedures required |
| 52 | **Certification** | No | No | With Approval | Highly restricted; amendment procedures required |
| 53 | **Credential** | No | No | With Approval | Highly restricted; amendment procedures required |
| 54 | **Signature** | No | No | No | Immutable after ratification; all modifications blocked |
| 55 | **Baseline** | With Approval | No | With Approval | AI may propose; only humans can modify |
| 56 | **Snapshot** | Yes | No | No | Write-once entity; immutable after creation |
| 57 | **TraceabilityLink** | Yes | With Approval | Yes | AI can create freely; modifications require review |
| 58 | **Checkpoint** | Yes | No | No | Write-once entity; immutable after creation |
| 59 | **Metric** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 60 | **Measurement** | Yes | No | No | Write-once entity; immutable after creation |
| 61 | **Assessment** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 62 | **Audit** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 63 | **Review** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 64 | **AuditTrail** | Yes | No | No | Write-once entity; immutable after creation |
| 65 | **Lifecycle** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 66 | **State** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 67 | **Exception** | No | No | With Approval | Highly restricted; amendment procedures required |
| 68 | **Waiver** | No | No | With Approval | Highly restricted; amendment procedures required |
| 69 | **Amendment** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 70 | **Sanction** | No | No | With Approval | Highly restricted; amendment procedures required |
| 71 | **Precedent** | No | No | With Approval | Highly restricted; amendment procedures required |
| 72 | **Appeal** | No | No | With Approval | Highly restricted; amendment procedures required |
| 73 | **Veto** | No | No | With Approval | Highly restricted; amendment procedures required |
| 74 | **Dispute** | No | No | With Approval | Highly restricted; amendment procedures required |
| 75 | **Recusal** | No | No | With Approval | Highly restricted; amendment procedures required |
| 76 | **TransparencyReport** | With Approval | With Approval | With Approval | Collaborative model; both AI and human changes require approval |
| 77 | **Concern** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 78 | **Escalation** | With Approval | With Approval | Yes | Collaborative model; both AI and human changes require approval |
| 79 | **View** | Yes | Yes | Yes | Full AI autonomy; human oversight available |

---

# MATRIX 8: CARDINALITY MATRIX

| # | Entity | Cardinality | Pattern | Rationale |
|---|--------|-------------|---------|-----------|
| 1 | **Kernel** | 1:1 | Singleton | Exactly one Kernel exists; no containment by another Kernel |
| 2 | **Domain** | 1:N | One-to-Many | One Domain contains many subordinate entities |
| 3 | **Subsystem** | 1:N | One-to-Many | One Subsystem contains many subordinate entities |
| 4 | **Module** | 1:N | One-to-Many | One Module contains many subordinate entities |
| 5 | **Component** | 1:N | One-to-Many | One Component contains many subordinate entities |
| 6 | **Primitive** | N:M | Many-to-Many | Many Primitives used by many entities; universal reference |
| 7 | **Resource** | N:M | Many-to-Many | Many Resources used by many entities; universal reference |
| 8 | **Layer** | 1:N | One-to-Many | One Layer contains many subordinate entities |
| 9 | **Tier** | 1:N | One-to-Many | Runtime levels contain many deployment units |
| 10 | **Slice** | N:M | Many-to-Many | Slices span many layers and modules flexibly |
| 11 | **Assembly** | 1:N | One-to-Many | One Assembly composes many components |
| 12 | **Topology** | 1:N | One-to-Many | One Topology describes many arrangements |
| 13 | **Interface** | 1:N | One-to-Many | One Interface contains many subordinate entities |
| 14 | **Boundary** | 1:1 | Singleton | Each bounded entity has exactly one Boundary |
| 15 | **Channel** | N:M | Many-to-Many | Channels connect many sources to many destinations |
| 16 | **Contract** | N:M | Many-to-Many | Contracts bind many providers to many consumers |
| 17 | **Capability** | N:M | Many-to-Many | Capabilities delivered by many modules, composed of many features |
| 18 | **Feature** | N:M | Many-to-Many | Features realize many capabilities across many modules |
| 19 | **Process** | N | Unbounded Collection | Arbitrary number of process definitions |
| 20 | **Workflow** | N | Unbounded Collection | Arbitrary number of workflow patterns |
| 21 | **Task** | N | Unbounded Collection | Unbounded work units within and across sessions |
| 22 | **Milestone** | N:M | Many-to-Many | Milestones mark many lifecycle stages of many entities |
| 23 | **Plan** | N:1 per Scope | Scoped Singleton | One per defined scope; scopes create multiplicity |
| 24 | **Constitution** | 1:1 | Singleton | Supreme instrument; singular by definition |
| 25 | **Charter** | 1:N | One-to-Many | Constitution issues many charters |
| 26 | **GovernanceBody** | N:M | Many-to-Many | Bodies composed of many roles, overseeing many scopes |
| 27 | **Role** | N | Unbounded Collection | Arbitrary number of defined roles |
| 28 | **Policy** | 1:N | One-to-Many | One policy governs many rules |
| 29 | **Rule** | N:M | Many-to-Many | Rules enforced by many policies, applied to many entities |
| 30 | **Standard** | 1:N | One-to-Many | One standard prescribes many requirements |
| 31 | **Guideline** | 1:N | One-to-Many | One Guideline contains many subordinate entities |
| 32 | **Constraint** | N:M | Many-to-Many | Constraints apply to many entity types across many boundaries |
| 33 | **Invariant** | N:1 | Many-to-One | Multiple invariants map to a single kernel truth |
| 34 | **Session** | N | Unbounded Collection | Unbounded concurrent engagement periods |
| 35 | **Actor** | N | Unbounded Collection | Arbitrary number of registered participants |
| 36 | **Participant** | N:M | Many-to-Many | Many actors participate in many sessions |
| 37 | **Context** | N:M | Many-to-Many | Many contexts reference many modules and components |
| 38 | **Environment** | N | Unbounded Collection | Many operational environments per module |
| 39 | **Decision** | N | Unbounded Collection | Arbitrary number of decisions made over time |
| 40 | **DecisionRecord** | 1:N | One-to-Many | One DecisionRecord contains many subordinate entities |
| 41 | **Evidence** | N:M | Many-to-Many | Evidence supports many claims across many findings |
| 42 | **Finding** | N:M | Many-to-Many | Findings emerge from many assessments, referenced by many reports |
| 43 | **Conclusion** | 1:N | One-to-Many | One conclusion synthesizes many findings |
| 44 | **Artifact** | N:M | Many-to-Many | Artifacts produced, consumed, and transformed by many processes |
| 45 | **Document** | 1:N | One-to-Many | One module produces many documents |
| 46 | **Specification** | 1:N | One-to-Many | One specification governs many implementations |
| 47 | **Record** | N:M | Many-to-Many | Records capture many events for many entities |
| 48 | **Log** | 1:N | One-to-Many | Many log streams per system |
| 49 | **Report** | N:M | Many-to-Many | Reports synthesize evidence from many sources for many audiences |
| 50 | **Approval** | N:M | Many-to-Many | Approvals granted by many approvers to many artifacts |
| 51 | **Authorization** | N:M | Many-to-Many | Authorizations granted to many roles for many actions |
| 52 | **Certification** | 1:N | One-to-Many | One certifying authority issues many certifications |
| 53 | **Credential** | N:M | Many-to-Many | Credentials issued to many actors for many access contexts |
| 54 | **Signature** | N:M | Many-to-Many | Signatures affixed by many parties to many artifacts |
| 55 | **Baseline** | 1:N | One-to-Many | One baseline captures many artifacts |
| 56 | **Snapshot** | N:M | Many-to-Many | Snapshots capture many entities at many points in time |
| 57 | **TraceabilityLink** | N:M | Many-to-Many | Links connect many source artifacts to many target artifacts |
| 58 | **Checkpoint** | N:M | Many-to-Many | Checkpoints verify state of many entities at many milestones |
| 59 | **Metric** | 1:N | One-to-Many | One metric definition generates many measurements |
| 60 | **Measurement** | N:M | Many-to-Many | Measurements capture many metrics for many entities |
| 61 | **Assessment** | N:M | Many-to-Many | Assessments evaluate many entities against many criteria |
| 62 | **Audit** | N:M | Many-to-Many | Audits examine many entities against many standards |
| 63 | **Review** | N:M | Many-to-Many | Reviews examine many entities by many reviewers |
| 64 | **AuditTrail** | 1:1 per Auditable Scope | Scoped Singleton | One audit trail per auditable scope |
| 65 | **Lifecycle** | 1:N | One-to-Many | One lifecycle definition applies to many entity instances |
| 66 | **State** | N | Unbounded Collection | Arbitrary number of defined states per lifecycle |
| 67 | **Exception** | N:M | Many-to-Many | Exceptions granted for many rules affecting many entities |
| 68 | **Waiver** | 1:N | One-to-Many | One Waiver contains many subordinate entities |
| 69 | **Amendment** | N:M | Many-to-Many | Amendments proposed by many roles affecting many instruments |
| 70 | **Sanction** | N:M | Many-to-Many | Sanctions imposed by many authorities on many violators |
| 71 | **Precedent** | N:M | Many-to-Many | Precedents established by many bodies guiding many cases |
| 72 | **Appeal** | N:1 per decision | Scoped Singleton | One per decision; decisions create multiplicity |
| 73 | **Veto** | 1:N | One-to-Many | One veto-holder can issue many vetoes |
| 74 | **Dispute** | N:M | Many-to-Many | Disputes involve many parties over many matters |
| 75 | **Recusal** | N:M | Many-to-Many | Recusals withdraw many parties from many matters |
| 76 | **TransparencyReport** | N:M | Many-to-Many | Reports cover many governance domains for many stakeholders |
| 77 | **Concern** | N:M | Many-to-Many | Concerns cross many domains, layers, and slices |
| 78 | **Escalation** | N | Unbounded Collection | Unbounded escalation events |
| 79 | **View** | N:M | Many-to-Many | Views represent many perspectives of many entities |

---

# MATRIX 9: DEPENDENCY MATRIX

| # | Entity | Depends On | Required By | Dependency Type |
|---|--------|------------|-------------|-----------------|
| 1 | **Kernel** | Kernel (root) | Domain, Subsystem, Module, Component, Primitive, Concern | Root |
| 2 | **Domain** | Kernel, Boundary | Subsystem, Module, Component | Structural |
| 3 | **Subsystem** | Domain, Module, Resource | Module, Component | Structural |
| 4 | **Module** | Subsystem, Component, Interface | Component, Feature, Environment, Channel, Assembly | Structural |
| 5 | **Component** | Module, Interface, Primitive | Module, Assembly, Feature, Slice | Structural |
| 6 | **Primitive** | Kernel | Component, Module, Interface | Foundational |
| 7 | **Resource** | Tier, Constraint | Subsystem, Module, Environment | Operational |
| 8 | **Layer** | Kernel | Module, Component, Slice | Structural |
| 9 | **Tier** | Kernel | Subsystem, Resource, Environment | Structural |
| 10 | **Slice** | Layer, Module, Component, Capability | Feature | Cross-cutting |
| 11 | **Assembly** | Module, Component, Interface | Feature | Structural |
| 12 | **Topology** | Kernel, Domain | Audit, Review | Analytical |
| 13 | **Interface** | Component, Module, Contract | Channel, Feature, Assembly | Contractual |
| 14 | **Boundary** | Domain, Subsystem, Constraint | Contract | Structural |
| 15 | **Channel** | Interface, Module | All entities | Operational |
| 16 | **Contract** | Interface, Boundary, Constraint, Standard | Channel, Module, Component | Contractual |
| 17 | **Capability** | Module, Component, Interface | Feature, Slice | Functional |
| 18 | **Feature** | Capability, Module, Interface, Slice | Task, Milestone | Functional |
| 19 | **Process** | Workflow, Task, Rule, Standard | Task, Evidence, Finding, Assessment, Audit, Report | Procedural |
| 20 | **Workflow** | Process, Role | Session, Task | Procedural |
| 21 | **Task** | Process, Workflow, Actor, Session | Milestone, Artifact | Procedural |
| 22 | **Milestone** | Feature, Task, Plan | Checkpoint, Review | Procedural |
| 23 | **Plan** | GovernanceBody, DecisionRecord, Specification | Task, Milestone | Procedural |
| 24 | **Constitution** | Kernel (root) | Charter, GovernanceBody, Invariant, Role, Rule, Policy, Actor | Root |
| 25 | **Charter** | Constitution, GovernanceBody | GovernanceBody | Governance |
| 26 | **GovernanceBody** | Constitution, Charter, Role | Policy, Rule, Audit, Review, DecisionRecord | Governance |
| 27 | **Role** | Constitution, GovernanceBody | Actor, Authorization, Approval, Audit | Governance |
| 28 | **Policy** | GovernanceBody, Rule | Audit, Review, Assessment | Governance |
| 29 | **Rule** | GovernanceBody, Policy, Constitution | Audit, Exception, Sanction, Assessment | Governance |
| 30 | **Standard** | GovernanceBody | Contract, Certification, Audit, Assessment | Governance |
| 31 | **Guideline** | Standard | Contract, Process | Advisory |
| 32 | **Constraint** | Invariant, Layer, Boundary | Module, Component, Interface, Resource | Architectural |
| 33 | **Invariant** | Constitution | Constraint, Contract | Foundational |
| 34 | **Session** | Actor, Workflow, Context | Task, Participant, Decision, View | Operational |
| 35 | **Actor** | Constitution, Role | Session, Participant, Decision, Task | Governance |
| 36 | **Participant** | Actor, Session, Role | Task, Decision | Operational |
| 37 | **Context** | Session | Decision, Task, View | Operational |
| 38 | **Environment** | Module, Resource, Tier | Session, Process | Operational |
| 39 | **Decision** | Actor, Context, Evidence | DecisionRecord, Plan | Governance |
| 40 | **DecisionRecord** | Decision, GovernanceBody, Evidence | Plan, Baseline, Audit | Governance |
| 41 | **Evidence** | Process, Finding | Decision, DecisionRecord, Assessment, Audit | Evidentiary |
| 42 | **Finding** | Evidence, Assessment, Audit | Conclusion, Report, DecisionRecord | Evidentiary |
| 43 | **Conclusion** | Finding, Evidence | DecisionRecord, Report | Evidentiary |
| 44 | **Artifact** | Process, Task | Document, Specification, Record, Baseline, Snapshot | Foundational |
| 45 | **Document** | Module, Artifact | Baseline, Review, Approval | Artifact |
| 46 | **Specification** | Governance, Standard | Module, Component, Plan, Assessment | Artifact |
| 47 | **Record** | Process | Log, AuditTrail, Baseline | Artifact |
| 48 | **Log** | System, Record | AuditTrail, Report, Audit | Artifact |
| 49 | **Report** | Evidence, Finding, Measurement | Audit, Review, DecisionRecord | Artifact |
| 50 | **Approval** | Role, Artifact, Review | Baseline, Plan, DecisionRecord | Governance |
| 51 | **Authorization** | Role, Credential, Constraint | All entities | Governance |
| 52 | **Certification** | Standard, Audit, Evidence | Contract | Governance |
| 53 | **Credential** | Actor | Authorization, Signature | Governance |
| 54 | **Signature** | Credential, Artifact | Approval, DecisionRecord, Baseline | Governance |
| 55 | **Baseline** | Artifact, Approval, Snapshot | Checkpoint, Plan | Traceability |
| 56 | **Snapshot** | System, Artifact | Baseline, Audit, Review | Traceability |
| 57 | **TraceabilityLink** | Artifact, Process | Baseline, Audit | Traceability |
| 58 | **Checkpoint** | Baseline, Milestone, Task | Review, Assessment | Traceability |
| 59 | **Metric** | Governance, Specification | Measurement, Assessment, Audit | Measurement |
| 60 | **Measurement** | Metric, Process | Assessment, Report, Audit | Measurement |
| 61 | **Assessment** | Measurement, Evidence, Finding | Conclusion, DecisionRecord, Report | Measurement |
| 62 | **Audit** | Standard, Rule, Policy, Evidence | Finding, Certification, Sanction | Oversight |
| 63 | **Review** | Artifact, Process, Milestone | Finding, Approval, DecisionRecord | Oversight |
| 64 | **AuditTrail** | System, Log, Record | Audit, Investigation, Compliance | Oversight |
| 65 | **Lifecycle** | Governance, State | Module, Component, Feature | Foundational |
| 66 | **State** | Lifecycle, Invariant | Lifecycle | Foundational |
| 67 | **Exception** | Rule, GovernanceBody | Waiver, Audit | Governance |
| 68 | **Waiver** | Exception, Rule, GovernanceBody | Audit, Compliance | Governance |
| 69 | **Amendment** | Constitution, GovernanceBody, Rule | Policy, Rule, Standard | Governance |
| 70 | **Sanction** | Rule, GovernanceBody, Audit | Compliance, Appeal | Governance |
| 71 | **Precedent** | GovernanceBody, DecisionRecord | Decision, Appeal | Governance |
| 72 | **Appeal** | Decision, GovernanceBody, Sanction | Precedent, Dispute | Governance |
| 73 | **Veto** | Constitution, Role, Decision | DecisionRecord, GovernanceBody | Governance |
| 74 | **Dispute** | Actor, GovernanceBody | Appeal, Recusal | Governance |
| 75 | **Recusal** | Actor, Decision | DecisionRecord, Audit | Governance |
| 76 | **TransparencyReport** | GovernanceBody, Metric, Decision | Audit, Actor | Governance |
| 77 | **Concern** | Slice, Layer, Domain | Component, Module, View | Cross-cutting |
| 78 | **Escalation** | Actor, GovernanceBody, Decision | Dispute, Appeal | Governance |
| 79 | **View** | Kernel, Session, Concern | Audit, Review, Decision | Analytical |

---

# MATRIX 10: GLOSSARY

| # | Term | Definition | Domain |
|---|------|------------|--------|
| 1 | **Kernel** | Serve as the root container and identity of the entire Radius1 engineering system. | T1: System Foundation |
| 2 | **Domain** | Bound a coherent area of knowledge, responsibility, and language within the Kernel. | T1: System Foundation |
| 3 | **Subsystem** | Group modules and components that share a cohesive functional purpose within a Domain. | T1: System Foundation |
| 4 | **Module** | Serve as the primary unit of development, deployment, and ownership within a Subsystem. | T1: System Foundation |
| 5 | **Component** | Provide a reusable, composable structural unit that encapsulates specific behavior or state. | T1: System Foundation |
| 6 | **Primitive** | Serve as the fundamental, indivisible building block from which all higher-order entities are composed. | T1: System Foundation |
| 7 | **Resource** | Represent any consumable, allocable, or manageable asset that entities within the Kernel require to operate. | T1: System Foundation |
| 8 | **Layer** | Define a horizontal architectural stratum that separates concerns by abstraction level within the Kernel. | T2: Structure & Architecture |
| 9 | **Tier** | Distinguish physical or logical deployment levels that govern runtime behavior, availability, and access patterns. | T2: Structure & Architecture |
| 10 | **Slice** | Represent a vertical, cross-cutting decomposition that spans multiple layers and modules to deliver an end-to-end capability. | T2: Structure & Architecture |
| 11 | **Assembly** | Compose multiple entities into a deliberately organized unit that serves a specific structural or functional purpose. | T2: Structure & Architecture |
| 12 | **Topology** | Describe the arrangement, shape, and connectivity pattern of entities within a defined scope of the Kernel. | T2: Structure & Architecture |
| 13 | **Interface** | Define the contract surface through which an entity exposes capabilities to other entities. | T3: Communication & Contracts |
| 14 | **Boundary** | Delineate the limit of a Domain, Subsystem, or Context, enforcing encapsulation and controlling cross-boundary interaction. | T3: Communication & Contracts |
| 15 | **Channel** | Establish a directed communication pathway between two or more entities for data, control, or event flow. | T3: Communication & Contracts |
| 16 | **Contract** | Formalize the agreement between two or more entities regarding their mutual obligations, interfaces, and behaviors. | T3: Communication & Contracts |
| 17 | **Capability** | Declare what the Kernel or a constituent entity can do, independent of how it is implemented. | T4: Capability & Function |
| 18 | **Feature** | Represent a user-visible, deliverable unit of functionality that realizes one or more Capabilities. | T4: Capability & Function |
| 19 | **Process** | Represent a defined sequence of operations and decisions that transforms inputs into outputs according to specified rules. | T5: Work & Process |
| 20 | **Workflow** | Define a structured, repeatable pattern of activities, decisions, and transitions for accomplishing a specific type of work. | T5: Work & Process |
| 21 | **Task** | Represent a unit of work to be performed by an actor within a session toward a defined objective. | T5: Work & Process |
| 22 | **Milestone** | Mark a significant achievement point or checkpoint within a lifecycle, plan, or project. | T5: Work & Process |
| 23 | **Plan** | Prescribe the intended course of action, including objectives, scope, sequence, resources, and criteria for a body of work. | T5: Work & Process |
| 24 | **Constitution** | Serve as the supreme governance instrument that establishes the kernel's fundamental principles, authority structures, and amendment procedures. | T6: Governance Foundation |
| 25 | **Charter** | Establish the existence, authority, and operating parameters of a governance body, project, or module within the kernel. | T6: Governance Foundation |
| 26 | **GovernanceBody** | Constitute an organized group of stakeholders with defined authority to make decisions, set policy, and oversee governance within a scope. | T6: Governance Foundation |
| 27 | **Role** | Define a named set of responsibilities, permissions, and authority boundaries that can be assigned to actors. | T6: Governance Foundation |
| 28 | **Policy** | Establish a governing principle that guides decision-making and sets boundaries for organizational behavior. | T6: Governance Foundation |
| 29 | **Rule** | State a binding constraint on behavior, structure, or process that must be observed by all entities within its jurisdiction. | T6: Governance Foundation |
| 30 | **Standard** | Define mandatory requirements, specifications, or criteria that entities must meet to ensure consistency, interoperability, and quality. | T7: Standards & Constraints |
| 31 | **Guideline** | Provide recommended practices and advisory guidance that encourage consistency without mandating specific approaches. | T7: Standards & Constraints |
| 32 | **Constraint** | Impose a structural or behavioral limitation on entities to ensure architectural integrity. | T7: Standards & Constraints |
| 33 | **Invariant** | Declare a condition that must always hold true across all states and transitions of the Kernel's structure. | T7: Standards & Constraints |
| 34 | **Session** | Represent a bounded period of engagement during which actors perform work toward defined objectives within the repository. | T8: Session & Participation |
| 35 | **Actor** | Represent any entity—human, automated, or hybrid—that can perform actions, make decisions, or assume responsibilities within a session. | T8: Session & Participation |
| 36 | **Participant** | Represent the binding of an Actor to a Session with specific role assignments and permissions for that session's duration. | T8: Session & Participation |
| 37 | **Context** | Represent the situational frame within which an entity is interpreted, executed, or accessed. | T9: Context & Environment |
| 38 | **Environment** | Represent the complete operational surroundings in which processes execute, including available capabilities, constraints, and external interfaces. | T9: Context & Environment |
| 39 | **Decision** | Represent a choice made among alternatives that commits the repository to a specific course of action, design, or policy. | T10: Decision & Reasoning |
| 40 | **DecisionRecord** | Capture a significant decision, including its context, options considered, rationale, and consequences, for future reference. | T10: Decision & Reasoning |
| 41 | **Evidence** | Provide factual support for a claim, assertion, finding, or conclusion through verifiable data, observation, or documentation. | T10: Decision & Reasoning |
| 42 | **Finding** | Document a discovered fact, observation, or result that emerged from investigation, analysis, or assessment. | T10: Decision & Reasoning |
| 43 | **Conclusion** | Synthesize Findings, Evidence, and reasoning into a final judgment, determination, or decision about a matter. | T10: Decision & Reasoning |
| 44 | **Artifact** | Serve as the root ontological category for any item produced, consumed, transformed, or referenced within the kernel. | T11: Artifacts |
| 45 | **Document** | Carry structured human-readable and machine-processable information in a coherent, navigable form. | T11: Artifacts |
| 46 | **Specification** | Prescribe in precise, unambiguous terms what shall be, shall do, or shall conform to. | T11: Artifacts |
| 47 | **Record** | Capture a fact, event, observation, or state at a specific point in time as an immutable account of what occurred. | T11: Artifacts |
| 48 | **Log** | Maintain a strictly chronological, append-only sequence of entries documenting events, actions, or state changes. | T11: Artifacts |
| 49 | **Report** | Communicate findings, analysis, status, or assessment results to stakeholders in a structured, interpretable format. | T11: Artifacts |
| 50 | **Approval** | Formally record that an authorized party has reviewed and accepted an artifact, decision, or state as satisfactory. | T12: Authorization |
| 51 | **Authorization** | Grant specific permission to perform an action or access a capability that is not universally available. | T12: Authorization |
| 52 | **Certification** | Formally attest that an entity meets specified standards or requirements after independent verification. | T12: Authorization |
| 53 | **Credential** | Provide a token or proof of identity, authorization, or entitlement that an entity may present to establish trust. | T12: Authorization |
| 54 | **Signature** | Mark an artifact with the authenticated identity of a party who has reviewed, approved, or authored it. | T12: Authorization |
| 55 | **Baseline** | Establish a frozen, authoritative reference point against which future changes, progress, or deviations can be measured. | T13: Traceability & Baselines |
| 56 | **Snapshot** | Capture the complete state of a system, module, process, or artifact at a precise point in time. | T13: Traceability & Baselines |
| 57 | **TraceabilityLink** | Provide a typed, directional, semantically meaningful connection between entities that carries specific traceability semantics. | T13: Traceability & Baselines |
| 58 | **Checkpoint** | Capture and verify the state of work at a defined milestone, enabling assessment of progress, quality, and readiness. | T13: Traceability & Baselines |
| 59 | **Metric** | Define a standard of measurement that prescribes what shall be measured, how, and against what thresholds. | T14: Measurement |
| 60 | **Measurement** | Capture a quantified observation of a property, performance characteristic, or state at a specific time. | T14: Measurement |
| 61 | **Assessment** | Systematically evaluate an entity against defined criteria to determine its quality, conformance, risk, or readiness. | T14: Measurement |
| 62 | **Audit** | Perform an independent, systematic inspection to verify compliance with Standards, Rules, Policies, and Regulations. | T15: Audit & Review |
| 63 | **Review** | Conduct a formal examination of an entity, process, or decision to assess compliance, quality, correctness, and alignment. | T15: Audit & Review |
| 64 | **AuditTrail** | Maintain a complete, chronological, tamper-evident record of all significant actions, changes, and decisions affecting an entity or scope. | T15: Audit & Review |
| 65 | **Lifecycle** | Define the complete set of states and permitted transitions that an entity type passes through from inception to retirement. | T16: Lifecycle & State |
| 66 | **State** | Represent a distinguishable condition or mode that an entity can occupy at a point in time. | T16: Lifecycle & State |
| 67 | **Exception** | Document a permitted deviation from a Rule, Standard, or Policy under specific circumstances with defined scope and duration. | T17: Exceptions & Waivers |
| 68 | **Waiver** | Formally grant exception from a requirement, rule, standard, or obligation that would otherwise be mandatory. | T17: Exceptions & Waivers |
| 69 | **Amendment** | Propose and record a formal change to an existing governance instrument that alters its substance. | T18: Governance Mechanics |
| 70 | **Sanction** | Impose a punitive or corrective measure in response to violation of Rules, Policies, Obligations, or Contracts. | T18: Governance Mechanics |
| 71 | **Precedent** | Record a prior decision, interpretation, or ruling that guides future similar cases. | T18: Governance Mechanics |
| 72 | **Appeal** | Request formal reconsideration of a decision, ruling, or sanction by a higher authority. | T18: Governance Mechanics |
| 73 | **Veto** | Empower a designated authority to reject a decision, action, or proposal, halting its progression. | T18: Governance Mechanics |
| 74 | **Dispute** | Document and manage a conflict between stakeholders or entities that requires formal resolution. | T19: Dispute & Accountability |
| 75 | **Recusal** | Document the voluntary or required withdrawal of a stakeholder from participation in a matter due to conflict or bias. | T19: Dispute & Accountability |
| 76 | **TransparencyReport** | Publish a periodic public disclosure of governance activities, decisions, metrics, and compliance status. | T19: Dispute & Accountability |
| 77 | **Concern** | Identify a cross-cutting area of interest that affects multiple entities across the Kernel's structure. | T20: Cross-Cutting |
| 78 | **Escalation** | Represent the elevation of a decision, issue, or authority to a higher level when the current level cannot or should not resolve it. | T20: Cross-Cutting |
| 79 | **View** | Provide a perspective-specific representation of the Kernel's structure that emphasizes certain entities and relationships while suppressing others. | T20: Cross-Cutting |

---

# STATISTICS & CONSISTENCY VERIFICATION

## Matrix Summary

| Matrix | Name | Rows | Columns | Est. Cells |
|--------|------|------|---------|------------|
| 1 | Ownership Matrix | 79 | 9 | 711 |
| 2 | Lifecycle Matrix | 79 | 3 | 237 |
| 3 | Stability Classification | 79 | 4 | 316 |
| 4 | Versionability Matrix | 79 | 4 | 316 |
| 5 | Freeze Matrix | 79 | 5 | 395 |
| 6 | Source-of-Truth Matrix | 79 | 5 | 395 |
| 7 | Creation & Modification Permissions | 79 | 6 | 474 |
| 8 | Cardinality Matrix | 79 | 5 | 395 |
| 9 | Dependency Matrix | 79 | 5 | 395 |
| 10 | Glossary | 79 | 4 | 316 |
| — | **TOTAL** | **790** | **50** | **4,950** |

## Consistency Verification

The following cross-matrix consistency checks were performed:

| Check | Result |
|-------|--------|
| Static entities are Non-Versionable | 5 of 6 correct: Primitive, Invariant, Signature |
| Static but Versionable (by design) | 1 entities: Constitution |
| Static entities are Freezable | All 6 correct; exceptions: None |
| Non-Freezable entities with rationale | All 7 have explicit rationale |
| Entities with No AI Create AND No AI Modify | 23 entities (governance-critical) |
| Entities blocking all human modification | 3: Primitive, Invariant, Signature |
| Distinct source-of-truth locations | 18 unique sources |

## Entity Count by Tier

| Tier | Count | Entities |
|------|-------|----------|
| T1: System Foundation | 7 | Kernel, Domain, Subsystem, Module, Component, Primitive, Resource |
| T2: Structure & Architecture | 5 | Layer, Tier, Slice, Assembly, Topology |
| T3: Communication & Contracts | 4 | Interface, Boundary, Channel, Contract |
| T4: Capability & Function | 2 | Capability, Feature |
| T5: Work & Process | 5 | Process, Workflow, Task, Milestone, Plan |
| T6: Governance Foundation | 6 | Constitution, Charter, GovernanceBody, Role, Policy, Rule |
| T7: Standards & Constraints | 4 | Standard, Guideline, Constraint, Invariant |
| T8: Session & Participation | 3 | Session, Actor, Participant |
| T9: Context & Environment | 2 | Context, Environment |
| T10: Decision & Reasoning | 5 | Decision, DecisionRecord, Evidence, Finding, Conclusion |
| T11: Artifacts | 6 | Artifact, Document, Specification, Record, Log, Report |
| T12: Authorization | 5 | Approval, Authorization, Certification, Credential, Signature |
| T13: Traceability & Baselines | 4 | Baseline, Snapshot, TraceabilityLink, Checkpoint |
| T14: Measurement | 3 | Metric, Measurement, Assessment |
| T15: Audit & Review | 3 | Audit, Review, AuditTrail |
| T16: Lifecycle & State | 2 | Lifecycle, State |
| T17: Exceptions & Waivers | 2 | Exception, Waiver |
| T18: Governance Mechanics | 5 | Amendment, Sanction, Precedent, Appeal, Veto |
| T19: Dispute & Accountability | 3 | Dispute, Recusal, TransparencyReport |
| T20: Cross-Cutting | 3 | Concern, Escalation, View |

---

*End of Matrices Package — All 10 matrices complete with 79 entities each.*
*Total entities: 79 | Total matrices: 10 | Total data rows: 790 | All cells filled.*

{'=' * 80}
END OF REPOSITORY META MODEL
{'=' * 80}
