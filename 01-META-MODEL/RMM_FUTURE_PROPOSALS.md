# RMM FUTURE PROPOSALS

## Version: v1.1 backlog
## Date: 2026-06-26

---

## Overview

This document catalogs architectural proposals deferred from the RMM v1.1 release. All items were reviewed, classified as architectural (not engineering defects), and postponed to future releases.

| Category | Count | Priority |
|----------|-------|----------|
| A: New Entities | 15 | v2.0 |
| B: Entity Restructuring | 12 | v1.2 / v2.0 |
| C: Property Schema Evolution | 7 | v2.0 |
| D: Multi-Product Scalability | 4 | v2.0 |
| E: Technology Independence | 7 | v1.2 |
| F: Governance Enhancement | 6 | v1.2 / v2.0 |
| G: Meta-Model Infrastructure | 5 | v2.0 |
| **Total** | **56** | |

---

## Category A: New Entities (15 proposals)

### A-01: Restore Stakeholder as Separate Entity
**Description:** Stakeholder was subsumed into Actor during deduplication. Stakeholder (interested party) and Actor (performing agent) are ontologically distinct. A CI/CD pipeline is an Actor but not a Stakeholder; a regulatory body is a Stakeholder but not an Actor.
**Triggering Reviews:** Entity & Abstraction; Relationship & Dependency; Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### A-02: Add Port Entity
**Description:** Port represents a named endpoint for communication. Referenced by Interface.Allowed Relationships and Boundary.Allowed Relationships but eliminated as non-canonical during deduplication.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v2.0
**Dependencies:** None

### A-03: Add Bridge Entity
**Description:** Bridge connects entities across boundaries. Referenced by Boundary.Allowed Relationships but eliminated during deduplication.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v2.0
**Dependencies:** A-02 (Port)

### A-04: Add Adapter Entity
**Description:** Adapter translates between incompatible interfaces. Referenced by Boundary.Allowed Relationships but eliminated during deduplication.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v2.0
**Dependencies:** None

### A-05: Add Bus Entity
**Description:** Bus is a shared communication medium for pub/sub patterns. Referenced by Channel.Allowed Relationships but eliminated during deduplication.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v2.0
**Dependencies:** A-02 (Port)

### A-06: Add Event Entity
**Description:** Event represents a discrete occurrence that triggers state changes or notifications. Referenced by Session.Allowed Relationships but eliminated during deduplication.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Medium
**Priority:** v1.2
**Dependencies:** None

### A-07: Add Dependency as Canonical Entity
**Description:** Dependency is referenced in Module.Allowed Relationships, Component.Forbidden, Constraint.Allowed Relationships, and Topology.Allowed Relationships. Currently exists only as a relationship type verb, not as a canonical entity.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Medium
**Priority:** v1.2
**Dependencies:** None

### A-08: Add Product Entity
**Description:** Product sits between Kernel and Domain in the containment hierarchy. Domain is a conceptual boundary; Product is a deployable unit. A product spans multiple domains. No multi-product governance is possible without this entity.
**Triggering Reviews:** Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### A-09: Add Namespace Entity
**Description:** Namespace provides naming isolation. Scope was subsumed into Context but Context is transient and provides no collision prevention. At 20 products, Module name collisions become inevitable without namespaces.
**Triggering Reviews:** Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** A-08 (Product)

### A-10: Add Extension Entity
**Description:** Extension provides a CRD-like mechanism for product-specific entity types. Without it, products needing "ML_Model", "Dataset", or "PCB_Layout" must map lossily to existing entities or amend the Constitution.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** None

### A-11: Add ExtensionSchema Entity
**Description:** ExtensionSchema validates extensions against the meta-model. Enables the Extension mechanism to self-validate.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** A-10 (Extension)

### A-12: Add EmergencyOverride Entity
**Description:** Deduplication log line 1712 states "EmergencyPower kept" but the entity does not appear in the final catalog. The Constitution TOC references Emergency Override.
**Triggering Reviews:** Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### A-13: Add HumanFiduciary Entity
**Description:** The Constitution TOC references Human Fiduciary but no such entity exists. No designated human accountability anchor for constitutional crises.
**Triggering Reviews:** Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### A-14: Add DecisionMechanism Entity
**Description:** GovernanceBody has 14 outgoing action relationships but no defined mechanism for how decisions are made (vote, consensus, delegation, fiat).
**Triggering Reviews:** Governance & Authority
**Effort:** Medium
**Priority:** v1.2
**Dependencies:** None

### A-15: Add Safeguard Entity
**Description:** Deduplication log line 1714 states "Safeguard kept" but the entity does not appear in the final catalog. Safeguards provide checks and balances on governance actions.
**Triggering Reviews:** Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

---

## Category B: Entity Restructuring (12 proposals)

### B-01: Merge Exception and Waiver
**Description:** Exception and Waiver represent the same governance concept (permission to deviate) with 1:1 coupling, 6/7 matching lifecycle stages, same grantor (GovernanceBody).
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-02: Merge Approval and Authorization
**Description:** Approval and Authorization form a 1:1 chain. Approval is the act; Authorization is the result. The 1:1 relationship proves they are one concept.
**Triggering Reviews:** Entity & Abstraction; Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-03: Merge Finding and Conclusion
**Description:** Finding and Conclusion have 7/8 matching lifecycle stages. Finding "triggers" Conclusion (N:1) — a state transition, not a relationship between independent entities.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-04: Merge Decision and DecisionRecord
**Description:** Decision and DecisionRecord have a 1:1 "recorded-in" relationship. Decision has no persistence mechanism — it becomes a DecisionRecord.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v1.2
**Dependencies:** B-03 (Finding+Conclusion merge)

### B-05: Restructure Document as Subtype of Artifact
**Description:** Artifact is the "root ontological category" (supertype) but Document is modeled as a peer with "composed-into Artifact" (N:1) — ontological contradiction.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### B-06: Degrade Measurement to Value Object
**Description:** Measurement is a data point (metric_id, value, timestamp) with no independent existence. It always belongs to a Metric. Should be a value object, not a first-class entity.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-07: Degrade Escalation to Event Type
**Description:** Escalation's purpose uses the process verb "elevation." Its lifecycle reads like a workflow. Should be an event within the Process/Workflow hierarchy.
**Triggering Reviews:** Entity & Abstraction; Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-08: Degrade Review, Audit, Assessment to Process Templates
**Description:** All three are defined by process verbs (examine, perform, evaluate). They are ACTIVITIES — things DONE, not things that ARE.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### B-09: Eliminate Topology
**Description:** Topology has zero structural containment relationships. It is a read-only derivation of the containment graph, not a first-class entity.
**Triggering Reviews:** Entity & Abstraction; Scalability & Universality
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-10: Eliminate TraceabilityLink
**Description:** TraceabilityLink is relationship reification. The model already has "traced-to", "traced-via", "references" as relationship types.
**Triggering Reviews:** Entity & Abstraction
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-11: Degrade Concern to Attribute
**Description:** Concern has zero incoming relationships in a 636-relationship model — a definitive outlier. All outgoing relationships could be replaced by a "concerns" attribute.
**Triggering Reviews:** Entity & Abstraction; Relationship & Dependency
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### B-12: Eliminate or Restructure View
**Description:** View has dual ownership (GovernanceBody for canonical views; Session for session views). Views are query projections, not first-class ontological entities.
**Triggering Reviews:** Relationship & Dependency
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

---

## Category C: Property Schema Evolution (7 proposals)

### C-01: Remove Source of Truth Property
**Description:** Property #15 specifies numbered directory paths ("00-CONSTITUTION/", "99-STATE/"). An ontology describes WHAT IS, not WHERE it is stored. Should be moved to a separate Storage Mapping document.
**Triggering Reviews:** Leakage & Independence; Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### C-02: Remove AI/Human Permission Properties
**Description:** Properties #12-14 embed governance rules into the ontology. Changing AI policy would require modifying 79 entity definitions. Should be moved to Entity Access Policy in governance.
**Triggering Reviews:** Leakage & Independence; Governance & Authority
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** C-01

### C-03: Remove Versionable and Freezable Properties
**Description:** Properties #10-11 embed version control and immutability assumptions. These are implementation concerns, not ontological properties.
**Triggering Reviews:** Leakage & Independence
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** C-01

### C-04: Remove Cardinality Property
**Description:** Property #8 uses relational patterns (1:1, 1:N, N:M). Cardinality is a relationship constraint, not an intrinsic entity property. Redundant with the Relationship Graph.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v2.0
**Dependencies:** C-01

### C-05: Add Mutability Property
**Description:** If Versionable and Freezable are removed, a single Mutability property with values [Mutable/Immutable/Versioned] could replace them more cleanly.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v2.0
**Dependencies:** C-03

### C-06: Add DefinitionLocation Property
**Description:** A 16th property specifying where the entity definition is authored/stored, distinct from Source of Truth which prescribes runtime storage.
**Triggering Reviews:** Scalability & Universality
**Effort:** Low
**Priority:** v2.0
**Dependencies:** C-01

### C-07: Split Cardinality into Instance and Relation Cardinality
**Description:** Current Cardinality conflates "how many instances of this entity" with "how many relationships of this type." These are distinct concepts.
**Triggering Reviews:** Leakage & Independence
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** C-04

---

## Category D: Multi-Product Scalability (4 proposals)

### D-01: Kernel Singleton to 1:N Product
**Description:** Kernel has cardinality 1:1. No "Product" entity exists. At 20 products, shared Kernel forces governance homogenization or independent Kernels fragment governance.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** A-08 (Product entity)

### D-02: Product-Scope Isolation
**Description:** Without namespaces, Product A's "Core" module and Product B's "Core" module collide. No collision prevention exists.
**Triggering Reviews:** Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** A-09 (Namespace)

### D-03: Extension Mechanism with Independent Versioning
**Description:** Products needing "ML_Model", "Dataset", or "PCB_Layout" must either map lossily to existing entities or amend the Constitution.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** A-10, A-11 (Extension, ExtensionSchema)

### D-04: LifecycleTemplate + LifecycleInstance Separation
**Description:** Lifecycle entity has 53 incoming relationships — a coupling bottleneck. Different products need different lifecycles.
**Triggering Reviews:** Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

---

## Category E: Technology Independence (7 proposals)

### E-01: Remove "Radius1" Product Naming
**Description:** Document title, headers, and Kernel definition repeatedly name "Radius1." A universal meta-model must be product-agnostic.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### E-02: Remove "Founders Circle" as Constitution Owner
**Description:** "Founders Circle" is a specific organizational title not defined as an entity. Not all organizations have founders or a "circle."
**Triggering Reviews:** Leakage & Independence; Governance & Authority
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### E-03: Replace "Runtime" Terminology
**Description:** "Runtime" appears in Tier, Environment, Channel, and Matrix 3 definitions. This is a software concept inapplicable to hardware or organizational systems.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### E-04: Redefine Channel Without Transport Semantics
**Description:** Channel is defined with "directed pathway", "typed messages", "reliability, ordering, protocol guarantees" — all network protocol characteristics.
**Triggering Reviews:** Leakage & Independence; Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### E-05: Remove Technology-Specific Lifecycle States
**Description:** States like "Bootstrapped", "Throttled", "Degraded", "Provisioned", "Committed", "Blocked", "Celebrated", "Enhancing" assume specific technologies.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v1.2
**Dependencies:** E-03

### E-06: Remove "Append-Only" and "Tamper-Evident" from Definitions
**Description:** Log and AuditTrail prescribe specific storage access patterns and cryptographic security properties. These describe HOW, not WHAT.
**Triggering Reviews:** Leakage & Independence
**Effort:** Low
**Priority:** v1.2
**Dependencies:** C-01

### E-07: Rename Tier Entity to Eliminate Naming Collision
**Description:** Entity "Tier" (deployment level) collides with catalog "Tier N" groupings (Tier 1 through Tier 20).
**Triggering Reviews:** Entity & Abstraction; Scalability & Universality
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

---

## Category F: Governance Enhancement (6 proposals)

### F-01: Rights Framework (Right/Entitlement/Privilege)
**Description:** Right/Entitlement/Privilege were subsumed into Role/Authorization. Neither captures "Actor A has the right to do B" as a first-class statement.
**Triggering Reviews:** Governance & Authority
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** None

### F-02: Delegation Model (Entity or Relationship)
**Description:** Delegation was subsumed into Role relationships. No tracking of delegation chains, duration, scope, or revocation.
**Triggering Reviews:** Governance & Authority
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** F-01

### F-03: AI-Readiness Review
**Description:** 22 entities (28% of the model) block AI from both creating and modifying. Every governance action requires human initiation.
**Triggering Reviews:** Governance & Authority
**Effort:** Medium
**Priority:** v1.2
**Dependencies:** None

### F-04: Actor Subtypes (HumanActor, AIAgent, HybridActor)
**Description:** Actor subtypes were eliminated during deduplication. AI governance requires distinguishing human, AI, and hybrid actors.
**Triggering Reviews:** Scalability & Universality
**Effort:** Low
**Priority:** v1.2
**Dependencies:** None

### F-05: Provenance Entity
**Description:** No entity tracks human→AI→artifact creation chains. In an AI-primary development model, provenance is essential for accountability.
**Triggering Reviews:** Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** F-04

### F-06: AI Governance Cross-Cutting Concern
**Description:** AI governance should be a first-class concern like Security, Performance, and Observability — not an afterthought.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** F-04, F-05

---

## Category G: Meta-Model Infrastructure (5 proposals)

### G-01: Meta-Meta-Model (EntitySchema)
**Description:** All 79 entities share 15 properties but there is no EntitySchema entity that formally models these properties.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** A-10 (Extension)

### G-02: Automated Validation Suite
**Description:** A computational validation suite that checks: cycle detection, owner-uniqueness, dangling reference detection, cross-matrix consistency.
**Triggering Reviews:** Validation process
**Effort:** High
**Priority:** v1.2
**Dependencies:** None

### G-03: Decision Rights Matrix (Matrix 11)
**Description:** The Constitution TOC references a Decision Rights Matrix. It is not present. Decision rights are only inferable by traversing ownership chains.
**Triggering Reviews:** Governance & Authority
**Effort:** Medium
**Priority:** v1.2
**Dependencies:** None

### G-04: Profile System for Product-Specific Subsets
**Description:** A mechanism to define product-specific subsets of the RMM (e.g., "SaaS Profile", "Hardware Profile") without modifying the kernel.
**Triggering Reviews:** Scalability & Universality
**Effort:** High
**Priority:** v2.0
**Dependencies:** A-10 (Extension), D-01 (Product)

### G-05: Storage Abstraction
**Description:** Demote Source-of-Truth paths from entity properties to a deployment-specific Storage Mapping document.
**Triggering Reviews:** Leakage & Independence; Scalability & Universality
**Effort:** Medium
**Priority:** v2.0
**Dependencies:** C-01

---

## Priority Roadmap

### v1.2 (Next Release) — Low Risk, High Value
- A-01: Restore Stakeholder
- A-12: Add EmergencyOverride
- A-13: Add HumanFiduciary
- A-14: Add DecisionMechanism
- A-15: Add Safeguard
- B-01 through B-04: Entity merges (Exception+Waiver, Approval+Auth, Finding+Conclusion, Decision+DR)
- B-06 through B-07: Degrades (Measurement, Escalation)
- B-09 through B-11: Eliminations (Topology, TraceabilityLink, Concern)
- E-01 through E-03: Naming fixes (Radius1, Founders Circle, runtime)
- E-05 through E-06: Lifecycle state cleanup
- E-07: Tier rename
- F-03 through F-04: AI readiness
- G-02: Validation suite
- G-03: Decision Rights Matrix

### v2.0 (Major Release) — Architecture Redesign
- A-02 through A-07: Structural entities (Port, Bridge, Adapter, Bus, Event, Dependency)
- A-08 through A-11: Multi-product (Product, Namespace, Extension, ExtensionSchema)
- B-05: Document-Artifact hierarchy
- B-08: Review/Audit/Assessment degradation
- B-12: View restructuring
- C-01 through C-07: Property schema evolution
- D-01 through D-04: Multi-product scalability
- E-04: Channel redefinition
- F-01 through F-02: Rights and Delegation
- F-05 through F-06: AI governance
- G-01: Meta-Meta-Model
- G-04: Profile system
- G-05: Storage abstraction

### Future (Research)
- Cross-product governance federation
- AI-native lifecycle models (continuous agent sessions)
- Automated ontology evolution
- Real-time compliance monitoring

---

*End of Future Proposals Document*
