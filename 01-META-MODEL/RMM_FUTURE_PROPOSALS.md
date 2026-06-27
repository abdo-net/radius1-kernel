# RMM FUTURE PROPOSALS

## Version: v1.1 backlog
## Date: 2026-06-26

---

## Overview

This document catalogs **56 architectural proposals** deferred from the RMM v1.1 release. These proposals were classified as `FUTURE_PROPOSAL` by the Release Engineer following review by three independent review bodies (~140 total findings: 21 ACCEPT, ~40 REJECT, ~79 consolidated into the 56 distinct proposals below).

Proposals are organized by architectural category and reflect valid architectural improvements that were deferred due to scope, effort, or risk constraints in the v1.1 release cycle. Each proposal includes its triggering review findings, estimated engineering effort, priority, and cross-proposal dependencies.

| Category | Count | Theme | Avg Effort |
|----------|------:|-------|:----------:|
| A — New Entities | 15 | Close referential gaps; add missing structural concepts | High |
| B — Entity Restructuring | 12 | Merge duplicates; degrade misclassified entities; tag profiles | Medium-High |
| C — Property Schema Evolution | 7 | Disambiguate overloaded properties; add missing dimensions | Medium |
| D — Multi-Product Scalability | 4 | Kernel-to-Product multiplicity; extension mechanics | High |
| E — Technology Independence | 7 | Remove product/technology leakage; terminology cleanup | Low-Medium |
| F — Governance Enhancement | 6 | AI governance; actor taxonomy; rights/delegation frameworks | High |
| G — Meta-Model Infrastructure | 5 | Self-description; automated validation; profile system | Medium |
| **Total** | **56** | | |

---

## Category A: New Entities (15 proposals)

### A-01: Restore Stakeholder as Separate Entity from Actor

| Field | Content |
|-------|---------|
| **Description** | Reintroduce `Stakeholder` as a canonical entity distinct from `Actor`. Actor = participant in a process; Stakeholder = interest-holder with standing. Currently Stakeholder was subsumed into Actor per the dedup log, yet Matrix 1 uses `Stakeholder (●)` as primary owner of `Signature` and `Credential`, and `Stakeholder (○)` as secondary owner of 10 additional entities. |
| **Triggering Reviews** | Review-1 C2, C3; Review-2 C1, C2, m5, m6 |
| **Rationale for Deferral** | Requires reconciliation of 12+ ownership rows across Matrix 1; touches dedup log provenance chain. Cross-cuts with A-02 (Owner normalization). Too invasive for v1.1. |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | A-02, B-01 |

### A-02: Add Port, Bridge, Adapter, Bus Entities (Structural Adapters)

| Field | Content |
|-------|---------|
| **Description** | Add four canonical entities in Tier 3 (Communication & Contracts): `Port` — exposed connection surface of a Boundary/Interface; `Bridge` — cross-boundary connector; `Adapter` — interface translator; `Bus` — shared communication medium. All four are referenced in Allowed Relationships by Boundary, Interface, Channel, Topology, and Domain, but do not exist in the 79-entity catalog. |
| **Triggering Reviews** | Review-1 C3; Review-2 C3 |
| **Rationale for Deferral** | Requires defining ~30 new relationships and their inverses; introduces hexagonal-architecture lineage back into model. Needs relationship-graph capacity analysis first. |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | G-02 (validation suite must cover new edges) |

### A-03: Add Event Entity (Trigger/Capture Distinction)

| Field | Content |
|-------|---------|
| **Description** | Add `Event` as a canonical entity in Tier 11 (Artifacts), distinct from `Record`. Event = the trigger/occurrence; Record = the capture/persistence of evidence about the event. Session's Allowed Relationships references "emits Event" but Event is not a defined entity. |
| **Triggering Reviews** | Review-2 C3 |
| **Rationale for Deferral** | Semantic overlap with Record, Log, Snapshot needs boundary analysis. Requires clarification of event lifecycle (fired, handled, archived). |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | B-09 (Degrade Review/Audit/Assessment — affects Event placement) |

### A-04: Add LifecycleStage, LifecycleGate Entities

| Field | Content |
|-------|---------|
| **Description** | Add `LifecycleStage` and `LifecycleGate` as canonical sub-elements of `Lifecycle` in Tier 16. Lifecycle's Allowed Relationships references both, but neither exists. LifecycleStage = named phase within a lifecycle; LifecycleGate = approval checkpoint controlling stage transition. Also define `EntryAction` and `ExitAction` as properties of State. |
| **Triggering Reviews** | Review-1 C3; Review-2 C3, M4, F10 |
| **Rationale for Deferral** | Tied to broader lifecycle model restructuring (D-04). Adding sub-elements without template/instance separation would create technical debt. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | D-04 (LifecycleTemplate separation) |

### A-05: Add Annotation, Catalog Entities (Artifact Sub-elements)

| Field | Content |
|-------|---------|
| **Description** | Add `Annotation` and `Catalog` as canonical entities in Tier 11 (Artifacts). Document's Allowed Relationships references "Contains Annotations" and "composed into Catalog," but neither entity exists. Annotation = commentary/footnote attached to an artifact; Catalog = curated collection/index of artifacts. |
| **Triggering Reviews** | Review-2 C3 |
| **Rationale for Deferral** | Depends on B-06 (Document as Artifact subtype) resolution to determine correct placement in type hierarchy. |
| **Effort** | Low |
| **Priority** | P3 — Medium |
| **Dependencies** | B-06 |

### A-06: Add Product Entity (Multi-Product Governance)

| Field | Content |
|-------|---------|
| **Description** | Add `Product` as a canonical entity representing a deployable product instance governed by the kernel. Currently the kernel is a singleton (1:1 cardinality) bound to "Radius1." Multi-product governance requires Product as a scope container with 1:N relationship from Kernel to Product. |
| **Triggering Reviews** | Review-1 D5, H.1; Review-2 (Future Scalability 80) |
| **Rationale for Deferral** | Core architectural change affecting Kernel cardinality. Requires D-01 (Kernel 1:N) and D-02 (Product-Scope isolation) to be designed first. |
| **Effort** | High |
| **Priority** | P1 — Critical |
| **Dependencies** | D-01, D-02, E-01 |

### A-07: Add Namespace Entity (Naming Isolation)

| Field | Content |
|-------|---------|
| **Description** | Add `Namespace` as a canonical entity for name-isolation scoping. Referenced by Kernel ("Contains … Namespace … Registry") and Module ("defines Namespace") but not in the entity catalog. Essential for multi-product and multi-tenant scenarios. |
| **Triggering Reviews** | Review-1 C3 |
| **Rationale for Deferral** | Depends on A-06 (Product entity) for scoping semantics. Introduces naming-isolation concerns that cross-cut with Profile system (G-04). |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | A-06, G-04 |

### A-08: Add Extension, ExtensionSchema Entities (CRD-Like Extensibility)

| Field | Content |
|-------|---------|
| **Description** | Add `Extension` and `ExtensionSchema` as canonical entities enabling product-specific entity extensions without modifying the core kernel. ExtensionSchema defines the extension contract (names, types, constraints); Extension is an instance of product-specific metadata attached to a core entity. Inspired by Kubernetes CRD pattern. |
| **Triggering Reviews** | Review-1 (Future Scalability 7.5); Review-2 (Future Scalability 80) |
| **Rationale for Deferral** | Requires Meta-Meta-Model (G-01) to be in place first, as extensions are self-describing schema additions. High design complexity. |
| **Effort** | High |
| **Priority** | P3 — Medium |
| **Dependencies** | G-01, D-03 |

### A-09: Add EmergencyOverride Entity (Governance Emergency)

| Field | Content |
|-------|---------|
| **Description** | Add `EmergencyOverride` as a canonical entity in Tier 19 (Dispute & Accountability). The dedup log lists `EmergencyPower` as "kept" but it does not appear in the 79-entity catalog. EmergencyOverride represents a time-bounded, audited bypass of normal governance rules triggered by crisis conditions (security incident, safety hazard, compliance deadline). |
| **Triggering Reviews** | Review-1 D3 |
| **Rationale for Deferral** | Requires full delegation model (F-02) and Safeguard entity (A-12) to define override boundaries and constraints. Governance-sensitive design. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | A-12, F-02 |

### A-10: Add HumanFiduciary Entity (Human Accountability Anchor)

| Field | Content |
|-------|---------|
| **Description** | Add `HumanFiduciary` as a canonical entity representing a legally accountable human who holds ultimate responsibility for an AI-initiated action or automated decision. Provides the human-in-the-loop accountability anchor required by emerging AI governance regulations (EU AI Act, NIST AI RMF). |
| **Triggering Reviews** | Review-1 (Governance leakage C4); Review-2 (AI-readiness gap) |
| **Rationale for Deferral** | Emerging regulatory domain; standards not yet settled. Cross-cuts with F-04 (Actor subtypes) and F-05 (Provenance). |
| **Effort** | Medium |
| **Priority** | P4 — Research |
| **Dependencies** | F-04, F-05 |

### A-11: Add DecisionMechanism Entity (Vote, Consensus, Delegation)

| Field | Content |
|-------|---------|
| **Description** | Add `DecisionMechanism` as a canonical entity capturing the procedural mechanism by which a governance decision is reached: majority vote, supermajority, consensus, delegated authority, or automated rule-trigger. Currently encoded implicitly in GovernanceBody and Policy but not explicitly modeled. |
| **Triggering Reviews** | Review-1 C4 (Governance leakage); Review-2 M8 (Policy/Rule/Standard hierarchy) |
| **Rationale for Deferral** | Governance philosophy decision — model should not encode one specific mechanism. Requires Rights framework (F-01) to be defined first. |
| **Effort** | Medium-High |
| **Priority** | P3 — Medium |
| **Dependencies** | F-01, F-02 |

### A-12: Add Safeguard Entity (Checks and Balances)

| Field | Content |
|-------|---------|
| **Description** | Add `Safeguard` as a canonical entity representing a structural check or balance that prevents governance abuse: separation-of-duties constraints, dual-control requirements, cooling-off periods, or mandatory review thresholds. The dedup log lists `Safeguard` as "kept" but it does not appear in the catalog. |
| **Triggering Reviews** | Review-1 D3 |
| **Rationale for Deferral** | Requires DecisionMechanism (A-11) and Rights framework (F-01) to be defined before safeguard rules can be anchored. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | A-11, F-01 |

### A-13: Add Suspension Entity (Referenced in 3 Lifecycles but Undefined)

| Field | Content |
|-------|---------|
| **Description** | Add `Suspension` as a canonical entity. The state "Suspended" appears in lifecycle definitions for Charter, Exception, and Waiver, but `Suspension` itself is not a defined entity. Suspension = a governance act that temporarily halts an entity's normal operations pending review or appeal resolution. |
| **Triggering Reviews** | Review-1 C3 (undefined concepts); Review-2 (lifecycle state audit) |
| **Rationale for Deferral** | Needs governance-process restructuring (B-09) to determine whether Suspension is an entity, a lifecycle state, or an event type. |
| **Effort** | Low |
| **Priority** | P2 — High |
| **Dependencies** | B-09 |

### A-14: Add Override Entity (Veto Override Mechanism)

| Field | Content |
|-------|---------|
| **Description** | Add `Override` as a canonical entity. Referenced in Review-1 C3 as an unmodeled token appearing in governance clauses. Override = a formal mechanism by which a higher authority supersedes a lower authority's ruling (e.g., super-veto, constitutional override). Distinct from Veto (which blocks) and Appeal (which requests review). |
| **Triggering Reviews** | Review-1 C3 |
| **Rationale for Deferral** | Governance philosophy sensitive. Needs full Appeal/Veto lifecycle review first. Cross-cuts with A-09 (EmergencyOverride). |
| **Effort** | Low-Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | A-09 |

### A-15: Add Dependency as Canonical Entity (Currently Only Relationship Type)

| Field | Content |
|-------|---------|
| **Description** | Promote `Dependency` from a relationship type to a canonical entity (proposed Tier 13 — Structural Linkage). Currently `Constraint.Allowed Relationships` lists "Applies to … Dependency" and `Topology.Allowed Relationships` references Dependency — treating it as an entity target. The dedup log records Dependency as "kept" but it is absent from the catalog. As an entity, Dependency would carry typed, versioned, inspectable references between components (e.g., `Component A depends-on Component B: version-range, rationale, criticality`). |
| **Triggering Reviews** | Review-1 C3; Review-2 C3, M3, M5 |
| **Rationale for Deferral** | Significant graph expansion; requires dependency-cycle detection (G-02) to be operational before adding N dependency edges. Risks amplifying circular dependency problem (Review-1 C1). |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | G-02, B-01 |

---

## Category B: Entity Restructuring (12 proposals)

### B-01: Core vs Governance Profile Tagging

| Field | Content |
|-------|---------|
| **Description** | Introduce a `Profile` attribute on every entity marking it as `Core` (structural/engineering, mandatory for all consumers) or `Governance Profile` (optional overlay, opt-in). ~35–40 of 79 entities form a judicial apparatus (Veto, Appeal, Precedent, Recusal, Sanction, Dispute, TransparencyReport, etc.) fused at the same canonical altitude as structural primitives. This is the single largest threat to universal-kernel suitability. |
| **Triggering Reviews** | Review-1 C4; Review-2 (Reusability 78, Universal Kernel 75) |
| **Rationale for Deferral** | Tagging all 79 entities requires board-level decision on governance philosophy. Does not change any definitions (non-breaking), but classification decisions are politically sensitive. |
| **Effort** | Low (tagging only) |
| **Priority** | P1 — Critical |
| **Dependencies** | None — enabler for many others |

### B-02: Merge Exception + Waiver (Semantic Duplication)

| Field | Content |
|-------|---------|
| **Description** | Merge `Exception` and `Waiver` into a single entity. Exception = temporary deviation from a rule/standard; Waiver = formal exemption from a requirement. Both represent "permission to not comply" and have nearly identical lifecycles (Requested → Reviewed → Granted → Expired/Revoked). The dedup log treats them separately without clear disambiguation criteria. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, m4 overlap clusters); Review-2 (Deduplication discipline) |
| **Rationale for Deferral** | Requires policy impact analysis — downstream consumers may have built on the distinction. Non-breaking if Exception absorbs Waiver with a `type` attribute. |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | B-01 (governance profile tagging) |

### B-03: Merge Approval + Authorization (1:1 Chain)

| Field | Content |
|-------|---------|
| **Description** | Merge `Approval` and `Authorization` into a single entity or establish a strict 1:1 pairing. Both are governance-granted permissions in a chain: Approval = formal endorsement; Authorization = permission to act. In practice every Authorization requires an Approval, and every Approval intends to Authorize. The distinction creates a two-hop chain where one relationship would suffice. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, m4); Review-2 M8 (governance hierarchy) |
| **Rationale for Deferral** | Some governance frameworks separate approval (board vote) from authorization (operational permission). Need use-case analysis before collapsing. |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | B-01 |

### B-04: Merge Finding + Conclusion (State Transition, Not Independent)

| Field | Content |
|-------|---------|
| **Description** | Merge `Finding` and `Conclusion` into a single entity or convert Conclusion to a lifecycle state of Finding. The evidentiary chain (Evidence → Finding → Conclusion → Decision → DecisionRecord) treats Finding and Conclusion as independent, but in practice a Conclusion is simply a validated Finding endorsed by an authority. They are state transitions of the same underlying assessment result, not independently creatable concepts. |
| **Triggering Reviews** | Review-1 C5 (Lifecycle regress); Review-1 (Entity duplication 6.0) |
| **Rationale for Deferral** | The 5-step evidentiary chain is a deliberate design feature. Collapsing steps may weaken audit traceability. Needs governance review. |
| **Effort** | Low |
| **Priority** | P3 — Medium |
| **Dependencies** | B-05 |

### B-05: Merge Decision + DecisionRecord (1:1 Relationship)

| Field | Content |
|-------|---------|
| **Description** | Merge `Decision` and `DecisionRecord` into a single entity. Decision = the act of deciding; DecisionRecord = the formal documentation of that act. They have a 1:1 relationship by design — every Decision has exactly one DecisionRecord, and every DecisionRecord records exactly one Decision. Splitting them creates a split-brain source-of-truth (Decision lives in `05-EVIDENCE/`, DecisionRecord lives in `Governance Ledger`). |
| **Triggering Reviews** | Review-1 D3, m3; Review-2 M2 |
| **Rationale for Deferral** | Separation may be intentional for legal reasons (decision as mental act vs. record as durable evidence). Needs legal/governance counsel. |
| **Effort** | Low |
| **Priority** | P3 — Medium |
| **Dependencies** | B-01 |

### B-06: Document as Subtype of Artifact (Type Hierarchy Correction)

| Field | Content |
|-------|---------|
| **Description** | Establish `Document` as a subtype of `Artifact` in the type hierarchy. Currently Document and Artifact are sibling entities, but Document is a kind of Artifact (a documented artifact). Document's Allowed Relationships include "composed of other Artifacts" and "Contains Annotations" — behaviors that belong to Artifact. The self-reference contradiction in Artifact (Review-1 C5) is resolved by making Document the leaf node. |
| **Triggering Reviews** | Review-1 C5 (Artifact self-reference); Review-2 C3 (Annotation/Catalog references) |
| **Rationale for Deferral** | Type hierarchy changes affect graph traversal queries and inheritance semantics. Needs schema change coordination. |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | A-05 (Annotation/Catalog placement) |

### B-07: Degrade Measurement to Value Object

| Field | Content |
|-------|---------|
| **Description** | Convert `Measurement` from a full entity to a value object (or property collection) attached to `Metric`. Measurement has no independent lifecycle — it exists only as a recorded observation of a Metric at a point in time. It has no meaningful Allowed Relationships, no governance process, and no identity outside its Metric + timestamp context. |
| **Triggering Reviews** | Review-1 (Definition/instance pairs — Measurement/Metric); Review-2 M9 (cardinality "N") |
| **Rationale for Deferral** | Measurement participates in the write-once immutability pattern (Review-1 G.5). Degrading it requires confirming no downstream tooling depends on Measurement as a graph node. |
| **Effort** | Low-Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | G-02 (validate no graph-node consumers) |

### B-08: Degrade Escalation to Event Type

| Field | Content |
|-------|---------|
| **Description** | Convert `Escalation` from a full entity to an event type (or lifecycle state transition). Escalation is fundamentally an act of raising priority/authority level — an event that occurs within a governance process, not a persistent entity with its own lifecycle. Its lifecycle (Initiated → Reviewed → Resolved) describes an escalation process instance, not an enduring concept. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0); Review-2 M9 |
| **Rationale for Deferral** | Escalation has 7 incoming relationships in the graph; degrading it requires rerouting those edges. Needs dependency analysis. |
| **Effort** | Low-Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | A-03 (Event entity — Escalation may become an Event subtype) |

### B-09: Degrade Review, Audit, Assessment to Process Templates

| Field | Content |
|-------|---------|
| **Description** | Convert `Review`, `Audit`, and `Assessment` from independent entities to process templates or subtypes of a common `Evaluation` process. All three are "evaluate X against criteria" with thin semantic boundaries. Audit = formal evidence-based evaluation; Review = structured examination; Assessment = systematic appraisal. The distinctions are procedural, not ontological. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, m4); Review-2 M7 (Concern vs Constraint overlap context) |
| **Rationale for Deferral** | Each has distinct regulatory meaning (SOX audit vs. code review vs. risk assessment). Collapsing may violate compliance requirements. Needs domain expert review. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | B-01 |

### B-10: Degrade Topology, TraceabilityLink, Concern, View

| Field | Content |
|-------|---------|
| **Description** | Evaluate degrading four derived-view entities to read-only projections or relationship annotations rather than first-class entities: `Topology` = derived structural projection (not independently created); `TraceabilityLink` = typed relationship instance (belongs to a Baseline); `Concern` = cross-cutting topic tag (not an enforceable constraint); `View` = perspective-specific subset of the model. All are calculated/derived from base entities. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, D1 — Concern In=0); Review-2 C6 (Concern reciprocity) |
| **Rationale for Deferral** | These entities have inbound relationships that would need rerouting. Topology has governance-level ownership (Governance Board) suggesting it is treated as a controlled artifact. Needs usage audit. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | G-02 (graph consumer audit) |

### B-11: Merge Record + Snapshot + Checkpoint + Baseline

| Field | Content |
|-------|---------|
| **Description** | Merge `Record`, `Snapshot`, `Checkpoint`, and `Baseline` into a single entity (proposed `Baseline`) with a `type` attribute distinguishing capture intent. All four are point-in-time immutable captures of system state. Record = evidentiary capture; Snapshot = full state capture; Checkpoint = recoverable state marker; Baseline = approved reference state. The distinctions are usage-pattern variants of the same underlying concept. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, m4); Review-2 (Deduplication discipline) |
| **Rationale for Deferral** | Each has distinct immutability semantics and lifecycle states. Snapshot has `Committed → Expired`; Baseline has `Draft → Approved → Superseded`. Needs lifecycle-state compatibility analysis. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | B-01 |

### B-12: Merge Assembly vs Subsystem/Module

| Field | Content |
|-------|---------|
| **Description** | Resolve semantic overlap between `Assembly`, `Subsystem`, and `Module`. Assembly = "composition of deployable units"; Subsystem = "cohesive functional area"; Module = "deployable unit of code." Assembly participates-in relationships with Module while Module is-contained-by Subsystem — three levels of composition with thin disambiguation. Consider making Assembly a composition pattern (attribute on Subsystem) rather than a separate entity. |
| **Triggering Reviews** | Review-1 (Entity duplication 6.0, m4); Review-2 (Structural spine assessment) |
| **Rationale for Deferral** | Assembly may represent a runtime deployment grouping distinct from Subsystem's development-time grouping. Needs runtime modeling analysis. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | E-03 (runtime → operational terminology) |

---

## Category C: Property Schema Evolution (7 proposals)

### C-01: Remove Source of Truth as Entity Property (Move to Storage Mapping)

| Field | Content |
|-------|---------|
| **Description** | Remove the `SourceOfTruth` property from the per-entity 15-property schema. Replace with a storage-mapping matrix (deployment appendix) that maps entity types to storage classes (Ledger / Registry / Vault / Repository / Store) independently of entity definitions. The literal `NN-FOLDER/` paths (`00-CONSTITUTION/`, `01-META-MODEL/`, etc.) are baked into the ontology, contradicting the technology-independence claim. |
| **Triggering Reviews** | Review-1 D4; Review-2 F11 |
| **Rationale for Deferral** | Source-of-truth paths are actively used by downstream consumers. Removing requires migration of storage mapping to external configuration. Low risk but moderate coordination effort. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | G-05 |

### C-02: Remove AI/Human Permission Properties (Move to Governance Policy)

| Field | Content |
|-------|---------|
| **Description** | Remove `AI_Modify` and `Human_Modify` permission properties from the per-entity schema. Replace with a governance policy matrix that assigns modification rights by role class (HumanActor, AIAgent, HybridActor) rather than hardcoding per entity. Currently 22+ entities are AI-excluded, but the exclusion criteria are inconsistent. |
| **Triggering Reviews** | Review-1 D7 (verification miscount); Review-2 (AI-readiness gap) |
| **Rationale for Deferral** | AI governance landscape is evolving rapidly. Moving to policy enables flexible adaptation without entity-schema changes. Requires Rights framework (F-01) to be defined first. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | F-01, F-04 |

### C-03: Remove Versionable/Freezable Properties (Move to Governance Policy)

| Field | Content |
|-------|---------|
| **Description** | Remove `Versionable` and `Freezable` boolean properties from the per-entity schema. Replace with a governance policy matrix that determines versionability and freezability by entity Profile (Core vs Governance) and Stability classification (Static/Slow/Moderate/Fast). These are derivable policy decisions, not intrinsic entity attributes. |
| **Triggering Reviews** | Review-1 D7; Review-2 (Property Schema Discipline 88) |
| **Rationale for Deferral** | Current values are broadly correct; this is a schema simplification, not a bug fix. Deferring to avoid unnecessary churn in v1.1. |
| **Effort** | Low-Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | B-01, C-01 |

### C-04: Remove Cardinality as Entity Property (Redundant with Relationship Graph)

| Field | Content |
|-------|---------|
| **Description** | Remove the `Cardinality` property from the per-entity schema. Cardinality is inherently a property of a relationship (entity A to entity B), not an attribute of an entity in isolation. The current property conflates instance cardinality (how many X exist) with relationship cardinality (how many Y each X relates to). The relationship graph already encodes this information per edge. |
| **Triggering Reviews** | Review-1 D6; Review-2 M9, M10, F13 |
| **Rationale for Deferral** | Cardinality is heavily referenced in Matrix 8 and by downstream tools. Removing requires ensuring all cardinality semantics are recoverable from the relationship graph. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | C-05, G-02 |

### C-05: Split Cardinality into InstanceCardinality and RelationCardinality

| Field | Content |
|-------|---------|
| **Description** | If Cardinality is retained (alternative to C-04), split it into two distinct properties: `InstanceCardinality` (population scope: 1:1 singleton, N:1 per scope, N unbounded) and `RelationCardinality` (per-relationship multiplicity: 1:1, 1:N, N:M, N:1). Replace the boilerplate placeholder rationales in Matrix 8 ("One X contains many subordinate entities" copy-pasted across Interface, Guideline, DecisionRecord, Waiver) with entity-specific cardinality semantics. |
| **Triggering Reviews** | Review-1 D6; Review-2 M9, M10, F13, m14 |
| **Rationale for Deferral** | Either C-04 or C-05 must be chosen; doing both is contradictory. Decision deferred to v1.2 architectural review. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | C-04 (mutually exclusive — one must be rejected) |

### C-06: Add DefinitionLocation as 16th Property

| Field | Content |
|-------|---------|
| **Description** | Add `DefinitionLocation` as a 16th property to the entity schema, capturing where the canonical definition is stored (e.g., `01-META-MODEL/`, `02-GOVERNANCE/`). This separates *definition storage* from *governance authority* (Owner). Currently 14+ entities have catalog Owner = "Governance Board" but Matrix 1 primary owner = "Meta-Model" — two different semantics conflated under one property. |
| **Triggering Reviews** | Review-1 C2; Review-2 C2, F2 |
| **Rationale for Deferral** | Clean separation of concerns, but adds a schema-wide property change touching all 79 entities. Best done as part of a coordinated property-schema evolution batch. |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | B-01, C-01 |

### C-07: Normalize Owner Field to Canonical Entity References

| Field | Content |
|-------|---------|
| **Description** | Restrict the `Owner` property to reference only canonical entities (or the `Role` entity with concrete role instances declared as instance data). Eliminate free-form owner descriptors: "Founders Circle", "Veto-holder (Role designated by Constitution)", "Sanctioning authority", "Independent Auditor", "Working Group or Subject Matter Authority", "Escalating Actor", etc. Map each to a controlled vocabulary class or explicit Role reference. |
| **Triggering Reviews** | Review-1 C2; Review-2 C2, M1, m13, F14 |
| **Rationale for Deferral** | Requires defining canonical Role instances and governance authority chains. Touches ~15 Owner fields and Matrix 1 column headers. Politically sensitive. |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | A-01 (Stakeholder restoration), B-01 |

---

## Category D: Multi-Product Scalability (4 proposals)

### D-01: Kernel Singleton → Kernel 1:N Product

| Field | Content |
|-------|---------|
| **Description** | Change `Kernel` cardinality from 1:1 singleton to 1:N with `Product`. Currently the kernel model assumes a single product ("the entire Radius1 engineering system"). Multi-product governance requires Kernel to be a shared meta-model across multiple Product instances, each with its own Constitution, GovernanceBody, and entity scope. |
| **Triggering Reviews** | Review-1 D5, H.1; Review-2 (Reusability 78, Universal Kernel 75) |
| **Rationale for Deferral** | Fundamental architectural change. Requires Product entity (A-06), Namespace (A-07), and Scope isolation (D-02) to be designed concurrently. Risk of destabilizing the structural spine. |
| **Effort** | High |
| **Priority** | P1 — Critical |
| **Dependencies** | A-06, A-07, D-02 |

### D-02: Product-Scope Isolation

| Field | Content |
|-------|---------|
| **Description** | Define scope-isolation semantics for multi-product deployment: each Product owns its Constitution, GovernanceBody, Policy set, and entity instances. Kernel entities (Tier 1–4, structural spine) are shared; Product-specific entities are isolated. Requires defining cross-product visibility rules, shared-standard propagation, and product-boundary enforcement. |
| **Triggering Reviews** | Review-1 D5; Review-2 (Future Scalability 80) |
| **Rationale for Deferral** | Depends on D-01 (Kernel 1:N). Also requires G-04 (Profile system) to define product-specific subsets. Governance-boundary design is complex. |
| **Effort** | High |
| **Priority** | P1 — Critical |
| **Dependencies** | D-01, G-04 |

### D-03: Extension Mechanism with Independent Versioning

| Field | Content |
|-------|---------|
| **Description** | Define the extension mechanics for product-specific entity additions without kernel modification: extension schema definition, extension validation, extension versioning (independent of kernel version), extension conflict resolution, and extension deprecation. Inspired by Kubernetes CRD evolution but adapted for governance-model extensions. |
| **Triggering Reviews** | Review-1 (Future Scalability 7.5); Review-2 (Future Scalability 80) |
| **Rationale for Deferral** | Requires A-08 (Extension/ExtensionSchema entities) and G-01 (Meta-Meta-Model) as prerequisites. Extension versioning is a research-level problem for ontologies. |
| **Effort** | High |
| **Priority** | P3 — Medium |
| **Dependencies** | A-08, G-01 |

### D-04: LifecycleTemplate + LifecycleInstance Separation

| Field | Content |
|-------|---------|
| **Description** | Separate `Lifecycle` into two concepts: `LifecycleTemplate` (the definitional pattern: states, transitions, gates, entry/exit actions) and `LifecycleInstance` (the runtime state machine executing a template for a specific entity). Currently Lifecycle conflates the pattern and the execution, causing the Lifecycle↔State 2-cycle (Review-1 C5) and infinite regress (Lifecycle has a Lifecycle). |
| **Triggering Reviews** | Review-1 C5; Review-2 M4 |
| **Rationale for Deferral** | Affects all 79 entities (each has `has Lifecycle`). Template/instance separation requires updating every entity's lifecycle reference. Wide blast radius. |
| **Effort** | High |
| **Priority** | P2 — High |
| **Dependencies** | A-04, G-02 |

---

## Category E: Technology Independence (7 proposals)

### E-01: Remove "Radius1" Product Naming

| Field | Content |
|-------|---------|
| **Description** | Replace all instances of "Radius1" in root-entity semantics with a parameterized system name. Kernel's purpose currently reads "the entire Radius1 engineering system." A universal kernel must not embed a product brand in its identity definition. The product name should be instance data, not ontology text. |
| **Triggering Reviews** | Review-1 D5; Review-2 (Domain leakage 6.0, Reusability 78) |
| **Rationale for Deferral** | Pure naming change, low risk. Deferred because it was flagged as "do not modify unless absolutely required" per the review mandate. Engineering team elected to batch all naming changes. |
| **Effort** | Low |
| **Priority** | P2 — High |
| **Dependencies** | A-06 (Product entity provides parameterization target) |

### E-02: Remove "Founders Circle" as Constitution Owner

| Field | Content |
|-------|---------|
| **Description** | Replace "Founders Circle" (a specific organizational group) as the Owner of `Constitution` with a canonical entity reference. Founders Circle is not a canonical entity; it is a free-form descriptor referencing a group of Actors. This creates an ownership circularity: Actor → owned-by → Constitution → owned-by → Founders Circle (= Actors). Replace with `GovernanceBody` or `Actor` as the constitutional owner. |
| **Triggering Reviews** | Review-1 C2 |
| **Rationale for Deferral** | Governance-sensitive naming decision. The Founders Circle may have specific legal meaning in the organizational structure. Requires organizational counsel. |
| **Effort** | Low |
| **Priority** | P2 — High |
| **Dependencies** | C-07 (Owner normalization) |

### E-03: Replace "Runtime" Terminology with "Operational"

| Field | Content |
|-------|---------|
| **Description** | Systematically replace "runtime" terminology with "operational" throughout the model. "Runtime" implies a specific execution-phase technology context; "operational" is technology-neutral and covers runtime, deployment, and execution phases. Environment entity description references "runtime surroundings." |
| **Triggering Reviews** | Review-1 (Technology leakage 5.5); Review-2 M5 |
| **Rationale for Deferral** | Terminology change with moderate documentation touchpoints. Low risk; batch with E-01 and E-04. |
| **Effort** | Low |
| **Priority** | P3 — Medium |
| **Dependencies** | None |

### E-04: Redefine Channel Without Transport-Level Semantics

| Field | Content |
|-------|---------|
| **Description** | Redefine `Channel` to remove transport-level semantics: "reliability, ordering, and protocol guarantees" are implementation concerns, not meta-model concepts. Channel should be defined as a conceptual communication pathway between boundaries, with transport guarantees specified as deployment-configuration concerns outside the ontology. |
| **Triggering Reviews** | Review-1 D4; Review-2 (Technology Independence 90) |
| **Rationale for Deferral** | Requires A-02 (Port, Bridge, Adapter, Bus) to be defined first, as Channel's semantics will be redistributed across those entities. |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | A-02 |

### E-05: Remove Technology-Specific Lifecycle States

| Field | Content |
|-------|---------|
| **Description** | Audit and remove technology-specific lifecycle states that leaked into entity definitions: `Throttled` (performance/infra concept), `Bootstrapped` (startup concept), `Degraded` (health concept), and other operational-state vocabulary embedded in lifecycle definitions. Replace with technology-neutral governance states: `Active`, `Suspended`, `Archived`, `Deprecated`, `Retired`. |
| **Triggering Reviews** | Review-1 (Technology leakage 5.5); Review-2 (Technology Independence 90) |
| **Rationale for Deferral** | Requires inventory of all lifecycle states across 79 entities. Some technology-specific states may be defensible (e.g., `Degraded` for operational entities). Needs per-entity review. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | D-04 (LifecycleTemplate separation) |

### E-06: Remove Append-Only/Tamper-Evident from Entity Definitions

| Field | Content |
|-------|---------|
| **Description** | Remove "append-only" and "tamper-evident" as definitional properties of entities (Record, Log, Snapshot, Checkpoint, Measurement, AuditTrail, Signature). These are implementation/storage properties, not ontological attributes. An entity is defined by what it represents, not by how its storage backend behaves. Move these assertions to the storage-mapping appendix. |
| **Triggering Reviews** | Review-1 D4; Review-2 (Technology Independence 90) |
| **Rationale for Deferral** | Immutability semantics are load-bearing for the evidentiary chain (Review-1 G.5). Moving to storage layer must not weaken audit guarantees. Needs security review. |
| **Effort** | Low-Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | C-01, G-05 |

### E-07: Rename Tier Entity to Avoid Naming Collision with Tier Groupings

| Field | Content |
|-------|---------|
| **Description** | Rename the `Tier` entity (deployment level: Tier-1 through Tier-20) or rename the catalog's organizing axis from "Tier" to "Group" or "Stratum" to avoid naming collision. Currently `Tier` is both a canonical entity (representing a deployment level) and the catalog's organizing axis (TIER 1…20), confusing any tool that indexes by tier. |
| **Triggering Reviews** | Review-1 m1, D8 |
| **Rationale for Deferral** | Renaming is a breaking change for any tool referencing the Tier entity. Low priority since the collision is documentational, not semantic. |
| **Effort** | Low |
| **Priority** | P4 — Research |
| **Dependencies** | None |

---

## Category F: Governance Enhancement (6 proposals)

### F-01: Rights Framework (Right/Entitlement/Privilege as Entity or Property)

| Field | Content |
|-------|---------|
| **Description** | Introduce a `Right` entity (or property dimension) capturing the rights, entitlements, and privileges that Actor entities hold: access rights, decision rights, veto rights, delegation rights, creation rights, modification rights. Currently rights are implicit in the Owner property and permission matrices, not explicitly modeled. A Right would have type, scope, grantor, grantee, expiry, and conditions. |
| **Triggering Reviews** | Review-1 C4 (Governance leakage); Review-2 C2 (Owner ambiguity) |
| **Rationale for Deferral** | Rights frameworks are domain-specific (legal rights vs. technical permissions vs. governance entitlements). Needs governance philosophy alignment before design. |
| **Effort** | High |
| **Priority** | P2 — High |
| **Dependencies** | B-01, C-02, C-07 |

### F-02: Delegation Model (Entity or Relationship with Constraints)

| Field | Content |
|-------|---------|
| **Description** | Define a delegation model: whether `delegates-to` is a relationship type or `Delegation` is a first-class entity with constraints (max depth, revocation rules, scope limits, dual-control requirements). Currently `Role` entity mentions delegation but the model does not define delegation mechanics. The `no circular delegation` constraint on Role cannot be enforced without a defined delegation structure. |
| **Triggering Reviews** | Review-1 C1 (circular delegation constraint); Review-2 (Governance Integrity 70) |
| **Rationale for Deferral** | Delegation patterns vary significantly across governance frameworks (corporate vs. open-source vs. regulatory). Needs reference-model analysis. |
| **Effort** | Medium-High |
| **Priority** | P2 — High |
| **Dependencies** | F-01, G-02 |

### F-03: AI-Readiness Review (Reduce 22 AI-Excluded Entities)

| Field | Content |
|-------|---------|
| **Description** | Conduct a systematic review of the 22+ entities that exclude AI modification (Human_Modify: Yes, AI_Modify: No). For each, determine whether the exclusion is justified (e.g., Constitution, Veto require human judgment) or anachronistic (e.g., Evidence, Measurement could be AI-generated). Goal: reduce AI-exclusion count by reclassifying entities where AI participation is safe and beneficial. |
| **Triggering Reviews** | Review-1 D7; Review-2 (AI-readiness gap) |
| **Rationale for Deferral** | AI governance standards (EU AI Act, NIST AI RMF) are still evolving. Premature AI-inclusion may create compliance liability. Needs legal/ethical review. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | F-04, F-05 |

### F-04: Actor Subtypes (HumanActor, AIAgent, HybridActor)

| Field | Content |
|-------|---------|
| **Description** | Introduce Actor subtypes: `HumanActor` (natural person), `AIAgent` (autonomous system), `HybridActor` (human-AI team). Currently `Actor` is a unified entity with AI/Human permission properties. Subtyping enables differentiated governance treatment, accountability chains, and capability declarations. Also enables A-10 (HumanFiduciary) to reference HumanActor specifically. |
| **Triggering Reviews** | Review-1 C4; Review-2 C1 (Stakeholder/Actor separation context) |
| **Rationale for Deferral** | Actor is a central entity with many relationships. Subtyping affects all governance and process entities. Needs Actor-centric dependency analysis. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | B-01, F-03 |

### F-05: Provenance Entity (Human→AI→Artifact Chains)

| Field | Content |
|-------|---------|
| **Description** | Add `Provenance` as a canonical entity capturing the full creation chain: which HumanActor initiated a request, which AIAgent processed it, which tools were used, and which Artifact was produced. Essential for AI governance audit trails, intellectual property attribution, and liability determination. Modeled after W3C PROV but adapted for the RMM entity set. |
| **Triggering Reviews** | Review-1 C4; Review-2 (AI-readiness gap) |
| **Rationale for Deferral** | Provenance standards (W3C PROV, DCMI) are mature but mapping to RMM entities requires design work. Cross-cuts with F-04 (Actor subtypes) and the evidentiary chain. |
| **Effort** | Medium |
| **Priority** | P3 — Medium |
| **Dependencies** | F-04, A-10 |

### F-06: AI Governance Cross-Cutting Concern

| Field | Content |
|-------|---------|
| **Description** | Define AI governance as a first-class cross-cutting concern in the RMM, with dedicated entities or properties for: AI capability declarations (what an AI agent can/cannot do), AI confidence scoring, AI human-oversight requirements, AI audit trails, and AI risk classification. Currently AI considerations are scattered across Human_Modify/AI_Modify properties and ad hoc entity descriptions. |
| **Triggering Reviews** | Review-1 C4; Review-2 (AI-readiness gap, Future Scalability 80) |
| **Rationale for Deferral** | AI governance is a rapidly evolving domain. Premature standardization risks obsolescence. Recommend monitoring NIST AI RMF v1.0 and EU AI Act implementing acts before design commitment. |
| **Effort** | High |
| **Priority** | P4 — Research |
| **Dependencies** | F-03, F-04, F-05, A-10 |

---

## Category G: Meta-Model Infrastructure (5 proposals)

### G-01: Meta-Meta-Model (EntitySchema for Self-Description)

| Field | Content |
|-------|---------|
| **Description** | Introduce a Meta-Meta-Model layer: an `EntitySchema` entity that describes the RMM's own entity definitions, enabling the model to describe itself. EntitySchema would define: entity name, property names/types, allowed relationships, forbidden relationships, lifecycle template reference, and profile classification. This enables automated validation, code generation, and self-consistency checking. |
| **Triggering Reviews** | Review-1 D2, D7; Review-2 (Property Schema Discipline 88, Internal Consistency 62) |
| **Rationale for Deferral** | Meta-meta-modeling adds significant complexity. The 15-property schema is already uniform and well-applied (Review-1 G.2). Defer until multi-product extensibility (D-03) requires schema-level abstraction. |
| **Effort** | High |
| **Priority** | P3 — Medium |
| **Dependencies** | G-02 |

### G-02: Automated Validation Suite (Cycle Check, Owner-Uniqueness Check)

| Field | Content |
|-------|---------|
| **Description** | Build and operationalize an automated validation suite that executes: (1) cycle detection on Matrix 9 (Dependency Matrix), (2) owner-uniqueness verification across all 79 entities, (3) referential-closure check (no dangling references to undefined entities), (4) count reconciliation (entity count, relationship count, type count), (5) reciprocal-relationship completeness check, (6) Matrix cross-consistency verification. Run on every model change. Attach output as Evidence. |
| **Triggering Reviews** | Review-1 C1, C2, C3, D1, D2, D7; Review-2 C4, C5, C6 |
| **Rationale for Deferral** | Tooling effort, not model effort. Requires engineering time separate from model amendment. The validation suite is a prerequisite for trusting any future model change. |
| **Effort** | Medium |
| **Priority** | P1 — Critical |
| **Dependencies** | None — enabler for all categories |

### G-03: Decision Rights Matrix (Matrix 11)

| Field | Content |
|-------|---------|
| **Description** | Create Matrix 11: Decision Rights Matrix. Map each entity type to the decision rights required to create, modify, approve, deprecate, and delete instances. Rows = entity types; columns = decision-right types (Create, Modify, Approve, Deprecate, Delete); cells = Role or Actor subtype required. Fills the governance gap between Matrix 1 (Ownership) and Matrix 7 (Permissions). |
| **Triggering Reviews** | Review-1 C2 (Owner ambiguity); Review-2 C2, F2 |
| **Rationale for Deferral** | Requires F-01 (Rights framework) and F-02 (Delegation model) to be defined first. Otherwise the matrix would be populated with placeholders. |
| **Effort** | Medium |
| **Priority** | P2 — High |
| **Dependencies** | F-01, F-02, C-07 |

### G-04: Profile System for Product-Specific Subsets

| Field | Content |
|-------|---------|
| **Description** | Define a Profile system that enables product-specific subsets of the RMM: a Profile declares which entities, relationships, and properties are included, excluded, or extended. Profiles are versioned independently of the kernel. Enables lightweight governance for small products (exclude judicial apparatus) and regulatory-heavy governance for enterprise products (include full apparatus). Complements B-01 (Core vs Governance tagging). |
| **Triggering Reviews** | Review-1 C4, H.1; Review-2 (Reusability 78, Universal Kernel 75) |
| **Rationale for Deferral** | Profile systems are design-pattern decisions with long-term consequences. Needs reference analysis (OSGi, OMG UML profiles, Kubernetes API groups) before commitment. |
| **Effort** | High |
| **Priority** | P3 — Medium |
| **Dependencies** | B-01, D-01, D-02 |

### G-05: Storage Abstraction (Demote Paths to Deployment Appendix)

| Field | Content |
|-------|---------|
| **Description** | Make the source-of-truth storage *classes* (Ledger / Registry / Vault / Repository / Store) normative, and demote the literal `NN-FOLDER/` paths and `.md` file extensions to a non-normative deployment-mapping appendix. The storage classes are the abstraction; the folder paths are one deployment of those classes. This enables the same RMM to be deployed on filesystems, databases, object stores, or document management systems without ontology changes. |
| **Triggering Reviews** | Review-1 D4; Review-2 F11, M5, M6 |
| **Rationale for Deferral** | Storage paths are actively used by current consumers. Demoting requires migration tooling and consumer notification. Low architectural risk but moderate operational coordination. |
| **Effort** | Low-Medium |
| **Priority** | P2 — High |
| **Dependencies** | C-01 |

---

## Priority Roadmap

### v1.2 (Next Release) — Foundation Hardening

Focus: Close integrity gaps and operationalize validation. All proposals in this bucket are P1–P2 priority with Low–Medium effort and no architectural redesign.

| ID | Proposal | Effort | Risk | Enabler For |
|----|----------|:------:|:----:|-------------|
| G-02 | Automated Validation Suite | Medium | Low | All categories |
| A-02 | Port, Bridge, Adapter, Bus Entities | Medium | Low | E-04 |
| A-15 | Dependency as Canonical Entity | Medium | Medium | Graph integrity |
| B-01 | Core vs Governance Profile Tagging | Low | Medium | B-02, B-03, B-09, F-01 |
| C-06 | DefinitionLocation as 16th Property | Medium | Low | C-07 |
| C-07 | Normalize Owner Field | Medium | Medium | G-03 |
| E-01 | Remove "Radius1" Product Naming | Low | Low | A-06 |
| E-02 | Remove "Founders Circle" as Owner | Low | Low | C-07 |
| A-13 | Suspension Entity | Low | Low | Lifecycle cleanup |
| C-01 | Remove Source of Truth from Entity Schema | Medium | Low | G-05 |
| G-05 | Storage Abstraction | Low-Medium | Low | C-01 |

**v1.2 target: 11 proposals** — expected 1 engineering cycle (3–4 weeks).

---

### v2.0 (Major Release) — Architectural Expansion

Focus: Multi-product support, entity model expansion, and governance framework formalization. These proposals are P1–P2 priority with High effort or architectural redesign scope.

| ID | Proposal | Effort | Risk | Prerequisite |
|----|----------|:------:|:----:|--------------|
| A-01 | Restore Stakeholder as Separate Entity | Medium | Medium | B-01, C-07 |
| A-04 | LifecycleStage, LifecycleGate Entities | Medium | Medium | D-04 |
| A-06 | Product Entity | High | High | D-01, D-02, E-01 |
| A-07 | Namespace Entity | Low-Medium | Low | A-06, G-04 |
| A-09 | EmergencyOverride Entity | Medium | Medium | A-12, F-02 |
| A-11 | DecisionMechanism Entity | Medium-High | High | F-01, F-02 |
| A-12 | Safeguard Entity | Medium | Medium | A-11, F-01 |
| A-14 | Override Entity | Low-Medium | Medium | A-09 |
| B-02 | Merge Exception + Waiver | Low-Medium | Medium | B-01 |
| B-03 | Merge Approval + Authorization | Low-Medium | Medium | B-01 |
| B-06 | Document as Subtype of Artifact | Low-Medium | Low | A-05 |
| C-02 | Remove AI/Human Permission Properties | Medium | Medium | F-01, F-04 |
| C-04 | Remove Cardinality as Entity Property | Medium | Medium | C-05, G-02 |
| C-05 | Split Cardinality into Instance/Relation | Medium | Medium | C-04 (alt) |
| D-01 | Kernel Singleton → Kernel 1:N Product | High | High | A-06, A-07, D-02 |
| D-02 | Product-Scope Isolation | High | High | D-01, G-04 |
| D-04 | LifecycleTemplate + LifecycleInstance Separation | High | High | A-04, G-02 |
| E-04 | Redefine Channel Without Transport Semantics | Low-Medium | Low | A-02 |
| E-05 | Remove Technology-Specific Lifecycle States | Medium | Low-Medium | D-04 |
| E-06 | Remove Append-Only/Tamper-Evident from Definitions | Low-Medium | Low | C-01, G-05 |
| F-01 | Rights Framework | High | High | B-01, C-02, C-07 |
| F-02 | Delegation Model | Medium-High | High | F-01, G-02 |
| F-03 | AI-Readiness Review | Medium | Medium | F-04, F-05 |
| F-04 | Actor Subtypes (HumanActor, AIAgent, HybridActor) | Medium | Medium | B-01, F-03 |
| F-05 | Provenance Entity | Medium | Medium | F-04, A-10 |
| G-03 | Decision Rights Matrix (Matrix 11) | Medium | Low | F-01, F-02, C-07 |
| G-04 | Profile System for Product-Specific Subsets | High | High | B-01, D-01, D-02 |

**v2.0 target: 28 proposals** — expected 2–3 engineering cycles (8–12 weeks).

---

### Future (Research) — Exploratory

Focus: Emerging domains and high-uncertainty proposals. These are P3–P4 priority, require external standard maturation, or have significant unknowns.

| ID | Proposal | Effort | Blocking Uncertainty | Research Trigger |
|----|----------|:------:|---------------------|-----------------|
| A-03 | Event Entity | Low-Medium | Semantic boundary with Record | Event sourcing pattern adoption |
| A-05 | Annotation, Catalog Entities | Low | Document hierarchy redesign | Knowledge management use cases |
| A-08 | Extension, ExtensionSchema Entities | High | Meta-Meta-Model design | CRD-style adoption demand |
| A-10 | HumanFiduciary Entity | Medium | AI regulation maturity | EU AI Act implementing acts (2027) |
| B-04 | Merge Finding + Conclusion | Low | Audit traceability impact | Governance process simplification |
| B-05 | Merge Decision + DecisionRecord | Low | Legal separation requirements | Legal counsel review |
| B-07 | Degrade Measurement to Value Object | Low-Medium | Downstream graph-node consumers | Tooling audit |
| B-08 | Degrade Escalation to Event Type | Low-Medium | Inbound relationship rerouting | Event model adoption |
| B-09 | Degrade Review/Audit/Assessment | Medium | Regulatory compliance requirements | Compliance framework review |
| B-10 | Degrade Topology/TraceabilityLink/Concern/View | Medium | Graph consumer dependency audit | Projection-tool adoption |
| B-11 | Merge Record + Snapshot + Checkpoint + Baseline | Medium | Lifecycle state compatibility | Storage model simplification |
| B-12 | Merge Assembly vs Subsystem/Module | Medium | Runtime vs development-time grouping | Deployment model analysis |
| D-03 | Extension Mechanism with Independent Versioning | High | Extension conflict resolution patterns | Multi-product deployment experience |
| E-03 | Replace "Runtime" with "Operational" | Low | Terminology coordination | Documentation batch cycle |
| E-07 | Rename Tier Entity | Low | Consumer impact assessment | Indexing tool feedback |
| F-06 | AI Governance Cross-Cutting Concern | High | AI governance standard maturity | NIST AI RMF v2.0, EU AI Act 2027 |
| G-01 | Meta-Meta-Model (EntitySchema) | High | Complexity/benefit tradeoff | Code generation demand |

**Future target: 17 proposals** — no committed timeline; activated by research triggers or downstream demand signals.

---

## Summary Statistics

| Metric | Value |
|--------|------:|
| Total Proposals | 56 |
| v1.2 Target | 11 |
| v2.0 Target | 28 |
| Future (Research) | 17 |
| P1 — Critical | 9 |
| P2 — High | 16 |
| P3 — Medium | 22 |
| P4 — Research | 9 |
| High Effort | 10 |
| Medium Effort | 31 |
| Low-Medium Effort | 11 |
| Low Effort | 4 |

---

*Document generated: 2026-06-26*
*Source reviews: RMM-v1-Engineering-Review.md (Principal Architecture Review Board), RMM_v1_Engineering_Review.md (Principal Architecture Review Board)*
*Classification: Release Engineering — FUTURE_PROPOSAL backlog*
