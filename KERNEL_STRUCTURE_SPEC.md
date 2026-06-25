# KERNEL_STRUCTURE_SPEC

**Mission:** MISSION-002 — Engineering Kernel Structure
**Classification:** CANONICAL
**Authority:** PCS v1.0
**Derived exclusively from:** Frozen **RMM v1.1** (79 entities, 10 matrices; `RMM_v1.1.md`)
**Constraint:** Every rule traces to the RMM. No directory, path, or convention herein assumes any product or implementation technology. This document defines **only** directory responsibilities, artifact locations, naming conventions, version conventions, and freeze conventions — nothing else.

> **Substrate neutrality.** "Directory" in this spec denotes a *logical containment namespace*, not a filesystem. The structure is realizable on any substrate. No filesystem, datastore, serialization format, framework, runtime, vendor, or product is assumed or required. Forbidden tokens (non-exhaustive): any product name, `Radius1`, `SAS4`, `NestJS`, `React`, `PostgreSQL`, `Docker`. No path segment may encode any of these.

---

## 0. Derivation principle

The RMM assigns every entity a **Source of Truth** and a **Source-Type** (RMM Matrix 6). The Source-Types are the only five storage classes the kernel recognizes (RMM Matrix 6 legend):

| Source-Type | Meaning (RMM Matrix 6) | Canonical top-level root |
|---|---|---|
| **Ledger** | Authoritative governance record | `00-CONSTITUTION/`, `02-GOVERNANCE/` |
| **Registry** | Structural definitions | `01-META-MODEL/`, `03-STANDARDS/`, `06-CONTRACTS/` |
| **Vault** | Immutable evidence | `05-EVIDENCE/` |
| **Store** | Operational / transient state | `07-WORKFLOW/`, `99-STATE/` |
| **Repository** | Produced artifacts | *(unbound — see §6 Finding F-2)* |

The repository organization below is the union of the Source-of-Truth locations RMM Matrix 6 actually assigns. No location is introduced that the RMM does not reference.

---

## 1. Directory responsibilities

### 1.1 Canonical top-level directories

Each directory holds exactly the canonical Source-of-Truth of the RMM entities assigned to it by Matrix 6. The two-digit ordinal encodes authority/persistence order: `00` (supreme, most durable) → `99` (transient). This gradient is the RMM Source-Type authority order (Ledger ≻ Registry ≻ Vault ≻ Store), confirmed by Matrix 3 Stability (`00`/`02` host Static/Slow governance; `99` hosts Fast transient state).

| Dir | Source-Type | Responsibility (what it is the source of truth for) | RMM-assigned entities (Matrix 6) |
|---|---|---|---|
| `00-CONSTITUTION/` | Ledger | Supreme governance instruments and the kernel's root identity and immutable truths | Kernel, Constitution (`Constitution.md`), Charter (`/Charters/`), Role, Invariant, Actor |
| `01-META-MODEL/` | Registry | Canonical structural ontology — the entity definitions of the kernel | Domain, Subsystem, Module, Primitive, Resource, Layer, Tier, Slice, Topology, Boundary, Capability, Constraint, Concern, Lifecycle (`/Lifecycles/`), State |
| `02-GOVERNANCE/` | Ledger | Governance bodies, instruments, and proceedings (the **Governance Ledger**) | GovernanceBody (`/Bodies/`), Policy (`/Policies/`), Rule (`/Rules/`), Authorization (`/Authorizations/`), Exception, Amendment, Sanction, Precedent, Appeal, Veto, Dispute, Recusal, Escalation |
| `03-STANDARDS/` | Registry | Mandatory standards, advisory guidance, and operating environment specifications | Standard, Guideline (`/Guidelines/`), Environment |
| `05-EVIDENCE/` | Vault | Immutable evidentiary and attestation records (the **Evidence Vault**) | Decision, Certification (`/Certifications/`), Audit (`/Audits/`), Review (`/Reviews/`), TransparencyReport (`/TransparencyReports/`) |
| `06-CONTRACTS/` | Registry | Inter-entity contracts | Contract |
| `07-WORKFLOW/` | Store | Definitions of work units (locations only; this spec does **not** define any workflow) | Feature, Process, Workflow, Milestone |
| `99-STATE/` | Store | Transient session and runtime state | Task, Session, Participant, Context (`/Context/`), View (`/View/`) |

### 1.2 Owner-local registries

Four Registry-class entities are **not** stored at a fixed top-level path. Their canonical record lives under their owning entity's `META/<EntityType>/` subtree (RMM Matrix 6):

| Entity | Canonical location (RMM Matrix 6) |
|---|---|
| Component | `…/<owning Module>/META/Component/` |
| Assembly | `…/<owning Module>/META/Assembly/` |
| Channel | `…/<owning Module>/META/Channel/` |
| Interface | `…/<owning entity>/META/Interface/` |

**Rule D-1:** An entity whose RMM Source of Truth is `Owning … META/<EntityType>/` is co-located with its owner; it has no independent top-level directory. (Traces to RMM Matrix 6; the owner is the entity's Owner per RMM Matrix 1.)

### 1.3 Named logical stores → class roots

RMM Matrix 6 addresses some entities by a **named logical store** rather than a numbered path. Each named store resolves to the top-level root of its Source-Type (§0). This is a normalization of folder responsibility, not a new location.

| Logical store (RMM) | Source-Type | Resolves to | Entities |
|---|---|---|---|
| **Governance Ledger** | Ledger | `02-GOVERNANCE/` | Plan, DecisionRecord, Conclusion, Specification, Approval, Baseline, Metric, Waiver |
| **Evidence Vault** | Vault | `05-EVIDENCE/` | Evidence, Finding, Record, Credential, Signature, Snapshot, Checkpoint, Measurement |
| **Registry Service** | Registry | `01-META-MODEL/` | TraceabilityLink |
| **Audit Log** | Store | `05-EVIDENCE/` (append-only; see Finding F-3) | Log, AuditTrail |
| **Artifact Repository** | Repository | *unbound (Finding F-2)* | Artifact, Document, Report, Assessment |

**Rule D-2:** A named logical store is the canonical home for its assigned entities and resolves to the numbered root carrying the same RMM Source-Type. Where RMM v1.1 assigns no numbered root for a Source-Type, the binding is deferred to an RMM amendment (§6) and **not** invented here.

### 1.4 Boundary of the canonical structure

**Rule D-3:** The canonical kernel structure consists of **only** the locations RMM Matrix 6 assigns (§1.1–§1.3). Any directory present in a working tree that no RMM entity's Source of Truth references is **non-canonical** and outside this specification (see Findings F-1).

---

## 2. Artifact locations

**Rule A-1 (single source of truth).** Each entity instance has exactly one canonical location: the Source of Truth defined for its type in RMM Matrix 6, resolved through §1. No entity is canonically stored in two locations. (Traces to RMM validation property *"Every ownership is unique"* and Matrix 6.)

**Rule A-2 (placement by type, then owner).** An instance is placed under its type's canonical directory; for owner-local registries (§1.2) it is placed under its Owner's subtree, where Owner is the entity's RMM Matrix 1 Owner.

**Rule A-3 (derived views are not sources).** `Topology` and `View` are perspective/projection entities (RMM: *"may not present information not derivable from the meta-model"*). They are stored at their assigned locations (`01-META-MODEL/Topology/`, `99-STATE/View/`) but are **derived**, never an authority over the entities they depict. (Traces to the RMM definitions of Topology and View.)

**Rule A-4 (split records are intentional).** Where the RMM assigns an act and its record to different stores — e.g., `Decision` → `05-EVIDENCE/` (Vault) while `DecisionRecord` → Governance Ledger (`02-GOVERNANCE/`) — both locations are canonical for their respective entity. This spec locates them; it does not merge or relocate them. (Traces to RMM Matrix 6 rows for Decision and DecisionRecord.)

**Canonical placement (full enumeration):** the §1.1 / §1.2 / §1.3 tables together place all 79 entities. No entity is unplaced except those under the unbound Repository class (Finding F-2).

---

## 3. Naming conventions

**Rule N-1 (top-level directory).** `NN-DOMAIN` — a two-digit zero-padded ordinal, a hyphen, and the domain name in UPPERCASE. The ordinal set and names are exactly those of RMM Matrix 6 roots: `00-CONSTITUTION`, `01-META-MODEL`, `02-GOVERNANCE`, `03-STANDARDS`, `05-EVIDENCE`, `06-CONTRACTS`, `07-WORKFLOW`, `99-STATE`. (Traces to RMM Matrix 6 literal roots.)

**Rule N-2 (ordinal semantics).** Lower ordinal ⇒ higher authority and persistence; `99` is reserved for transient state. (Traces to Source-Type authority order §0 and RMM Matrix 3: `99-STATE` hosts Fast/transient entities, `00`/`02` host Static/Slow governance.)

**Rule N-3 (collection sub-directory).** A collection directory is named for the RMM **canonical entity name** it stores, as a path segment: `01-META-MODEL/Domain/`, `02-GOVERNANCE/Policy/`, `05-EVIDENCE/Audit/`. RMM v1.1 renders several of these segments as English plurals (e.g., `Policies`, `Charters`, `Audits`, `Vetoes`, `Reviews`, `Certifications`, `TransparencyReports`, `Guidelines`, `Lifecycles`, `Bodies`); these are equivalent renderings of the same entity-type segment (see Finding F-4). The canonical identifier is the entity name in the RMM Entity Catalog.

**Rule N-4 (owner-local segment).** Owner-local registries use `…/<owner>/META/<EntityType>/` (§1.2). The `META` segment is fixed; `<EntityType>` is the RMM entity name. (Traces to RMM Matrix 6.)

**Rule N-5 (instance identifier).** An instance is identified by its `<EntityType>` plus a stable, unique, monotonically assignable identifier. The identifier form is **format-neutral**; it must not encode a timestamp scheme, vendor, runtime, or product.

**Rule N-6 (format neutrality).** This specification does **not** mandate a file format or extension. The single literal filename appearing in RMM v1.1 (`Constitution.md`) is a non-normative example; canonical addressing is at directory + entity-identifier granularity. (Traces to RMM validation property *"Technology-independent."*)

**Rule N-7 (product/technology prohibition).** No path segment, directory name, or identifier may encode a product, brand, vendor, framework, datastore, or runtime. (Traces to the MISSION-002 acceptance criterion and RMM's technology-independence / no-product-leakage stance.) This holds even though RMM prose references a product name in entity *descriptions*: **no RMM Source-of-Truth path encodes a product, and none here may.**

---

## 4. Version conventions

Versionability is fixed per entity by **RMM Matrix 4** (66 `Yes`, 13 `No`).

**Rule V-1 (versionable entities).** An entity with `Versionable = Yes` carries an **ordered revision identifier**. Each transition through its Lifecycle (RMM Matrix 2) that alters substance produces a new, higher-ordered revision; prior revisions are retained, never overwritten. The identifier form is format-neutral; only monotonic ordering is required. (Traces to RMM Matrix 4 + Matrix 2.)

**Rule V-2 (non-versionable entities).** The following 13 entities are `Versionable = No` and have **no revision series** — a single canonical instance, write-once: **Primitive, Invariant, Participant, Context, Evidence, Record, Log, Credential, Signature, Snapshot, Checkpoint, Measurement, AuditTrail.** A change to such an entity is a new instance, not a revision. (Traces to RMM Matrix 4; reinforced by RMM Matrix 7 write-once for the evidentiary subset.)

**Rule V-3 (frozen reference points).** A versioned line is pinned for reference by a `Baseline` (the immutable reference point), and captured point-in-time by a `Snapshot` or verified by a `Checkpoint`. These reference entities are located per §1.3 / §1.1. (Traces to RMM definitions of Baseline, Snapshot, Checkpoint.)

**Rule V-4 (meta-model version line).** The kernel meta-model document set is itself versioned as an ordered `vMAJOR.MINOR` line. A `MINOR` increment preserves the entity set, tiers, and relationship graph (corrections only); a `MAJOR` increment changes entities, tiers, or relationships. (Traces to the established RMM release line `v1 → v1.1` and to `Kernel`/`Constitution` `Versionable = Yes` in Matrix 4. This spec states the convention; it does not modify the RMM.)

---

## 5. Freeze conventions

Freezability is fixed per entity by **RMM Matrix 5** (72 `Yes`, 7 `No`), with entity-specific freeze triggers in that matrix.

**Rule F-1 (freeze action).** Freezing converts the current revision of a freezable artifact into an immutable, attested reference. It is recorded as a `Baseline` in the Governance Ledger (`02-GOVERNANCE/`), bears a `Signature` in the Evidence Vault (`05-EVIDENCE/`), and references the frozen artifact(s) and, where applicable, a `Snapshot`/`Checkpoint`. (Traces to RMM definitions of Baseline, Signature, Snapshot, Checkpoint and their Matrix 6 Source-of-Truth.)

**Rule F-2 (triggers are RMM-defined).** The event that authorizes a freeze is the entity-specific **Freeze Trigger** in RMM Matrix 5 (e.g., ratification, publication, commitment). This spec references those triggers; it does **not** define any workflow or process to reach them.

**Rule F-3 (post-freeze change path).** After freeze, a frozen artifact may change **only** through the RMM-defined mechanism for its class: governance instruments via `Amendment` (`02-GOVERNANCE/Amendments/`); baselined definitions via formal amendment followed by a superseding `Baseline`. This spec locates these records; it does not redefine the mechanism. (Traces to RMM definitions of Amendment, Baseline, Constraint/Specification.)

**Rule F-4 (non-freezable entities).** These 7 entities are `Freezable = No` and **must remain mutable**; the structure must never place them under a frozen baseline: **GovernanceBody, Guideline, Actor, Context, Authorization, Credential, Precedent.** (Traces to RMM Matrix 5 rationales — e.g., a governance body must remain adaptable; a credential must remain revocable.)

**Rule F-5 (born-frozen entities).** **Primitive, Invariant, Signature** are fully immutable (RMM Matrix 7: AI-Create No, AI-Modify No, Human-Modify No). Their first committed instance is their only instance; no freeze action is required and no modification path exists. (Traces to RMM Matrix 7 + Matrix 4.)

**Rule F-6 (immutable stores).** Frozen evidentiary artifacts reside in write-once stores — the Evidence Vault (`05-EVIDENCE/`) and Audit Log — whose entities are non-modifiable by construction (RMM Matrix 7: Record, Log, Signature, Snapshot, Checkpoint, Measurement, AuditTrail = Human/AI Modify `No`). The structure must bind these artifacts to those stores and never to a mutable Store/Registry root. (Traces to RMM Matrix 7 + Matrix 6.)

---

## 6. Boundary validation (findings)

Per the allowed operation *"validate repository boundaries."* These are observations about RMM v1.1's own source-of-truth taxonomy. **No RMM modification and no invented binding is performed here.**

- **F-1 — Non-canonical directories.** A working tree may contain `04-PATTERNS/`, `08-TEMPLATES/`, `09-TOOLS/`. No RMM v1.1 entity assigns its Source of Truth to any of these, and the ordinal `04` is unused by Matrix 6. They are therefore **outside the canonical RMM-derived structure** (Rule D-3). This spec assigns them no responsibility, because none would trace to the RMM.
- **F-2 — Unbound Repository class.** The Source-Type **Repository** (`Artifact, Document, Report, Assessment`, via the *Artifact Repository* logical store) has **no numbered root** in RMM Matrix 6. A canonical top-level binding requires an RMM amendment; it is intentionally **not** invented here (doing so would fail the "every rule traces to RMM" criterion). Until amended, produced artifacts are addressed through the *Artifact Repository* logical store as a Repository-class content store.
- **F-3 — Audit Log type nuance.** The *Audit Log* store (`Log, AuditTrail`) carries Source-Type **Store** while residing in the audit/evidence domain. This spec binds it adjacent to `05-EVIDENCE/` for domain coherence and append-only immutability (Rule F-6), noting the Store/Vault type distinction in RMM Matrix 6.
- **F-4 — Collection-name pluralization variance.** RMM Matrix 6 renders some collection segments singular (`Domain`) and others plural (`Policies`, `Audits`). Rule N-3 treats both as equivalent renderings of the entity-type segment; the catalog entity name is canonical. (Observation only; no RMM change.)
- **F-5 — Product naming is confined to prose.** RMM entity *descriptions* reference a product name, but **no RMM Source-of-Truth path does**. Rule N-7 prohibits any such encoding in the structure. The structure therefore satisfies the MISSION-002 failure-avoidance condition: no folder depends on any product or implementation technology.

---

## Appendix — RMM traceability

| Rule(s) | RMM source |
|---|---|
| §0 Source-Types; §1.1–§1.3 directories & stores | Matrix 6 (Source-of-Truth) + its Source-Type legend |
| D-1 owner-local; D-2 logical stores; A-1, A-2, A-4 placement | Matrix 6; Matrix 1 (Ownership) |
| A-3 derived views | Entity definitions: Topology, View |
| N-1, N-2 directory naming & ordinal authority | Matrix 6 roots; Matrix 3 (Stability) |
| N-3, N-4 segment naming | Matrix 6 sub-paths; Entity Catalog names |
| N-6 format neutrality; N-7 no product/tech | Validation property "Technology-independent"; MISSION-002 acceptance criteria |
| V-1, V-2 versioning | Matrix 4 (Versionability); Matrix 2 (Lifecycle) |
| V-3 reference points | Entity definitions: Baseline, Snapshot, Checkpoint |
| V-4 meta-model version line | Release line v1→v1.1; Matrix 4 (Kernel/Constitution) |
| F-1, F-3 freeze records & change path | Entity definitions: Baseline, Signature, Amendment; Matrix 6 |
| F-2 triggers | Matrix 5 (Freeze Trigger column) |
| F-4 non-freezable (7) | Matrix 5 (`Freezable = No`) |
| F-5 born-frozen (3) | Matrix 7 (all-No); Matrix 4 |
| F-6 immutable stores | Matrix 7 (write-once); Matrix 6 |

**Acceptance check.** Every rule above cites an RMM matrix, entity definition, or validation property. No directory, path, or convention encodes a product or implementation technology. The canonical structure is exactly the set of RMM Matrix 6 source-of-truth locations, normalized by Source-Type — nothing added, nothing product-specific.

*End of KERNEL_STRUCTURE_SPEC.*
