# RMM FUTURE PROPOSALS & FINDING DISPOSITION

**Purpose:** Per the release mandate, *every* review finding is classified as exactly one of
`ACCEPT` · `REJECT` · `FUTURE_PROPOSAL` · `ARCHITECT_DECISION_REQUIRED`.
`ACCEPT`ed findings were applied in `RMM_v1.1.md` (see `CHANGELOG_v1_to_v1.1.md`).
Everything else is recorded here. **None of these block the v1.1 release.**

**Authoritative base:** RMM v1. Reviews are *evidence only* and never override the RMM.

**Evidence order used to classify:**
1. Objective contradiction *inside* RMM (highest authority).
2. Consensus across ≥2 independent reviews.
3. Single-review findings.
When reviewers disagreed, or a finding would force an architecture change, the original RMM was kept and the finding was marked `FUTURE_PROPOSAL` or `ARCHITECT_DECISION_REQUIRED`. No architecture was redesigned inside v1.1.

**Reviews referenced:**
- **R1** = *Principal Architecture Review Board — Formal Engineering Review* (~140 findings: 35C/67M/34m)
- **R2** = *Engineering Review Report* (6C/10M/15m)
- **R3** = *RMM v1 Engineering Review* (5C/8 Major/minor) — archived at `05-EVIDENCE/Reviews/`

---

## 1. ACCEPTED — applied in v1.1

Objective, non-architectural defects. Detail in `CHANGELOG_v1_to_v1.1.md`.

| Finding (theme) | Sources | Action in v1.1 |
|---|---|---|
| Entity count 78 vs 79 | R1-m11, R2-C4, R3-D2 | Corrected to 79 |
| Relationship count / type-count / degree tables inconsistent | R1-m12/m13, R2-C5, R3-D1/D2/D7 | Recomputed: 640 edges, 201 types, all inline headers + Appendix A regenerated |
| `Concern` incoming = 0 vs actual 3 | R2-C6 (stat), R3-D1 | Corrected via Appendix A regen (Concern now 9/3/12) |
| `Governance Board` ≠ canonical `GovernanceBody` | R1-M11/M12, R2-C2, R3-C2 | Normalized 19 owner fields |
| `Stakeholder` subsumed-but-referenced | R1-C09, R2-C1(B), R3-C3 | Replaced with `Actor` per RMM dedup log |
| Process & Session dual-primary (self) ownership | R2-M1, R3 | Reduced to single primary owner |
| Path casing `01-META-Model` | R2-M6, R3-m2 | Normalized to `01-META-MODEL` |
| Self-contradicting validation/self-audit claims | R2-C4/C5, R3-D7 | Validation block rewritten to recomputed state |

---

## 2. REJECTED — not a defect

| Finding | Sources | Why rejected |
|---|---|---|
| **Signature is "orphaned" — no actor can create it** | R1-C10 | Misreading. The schema has no `Human Creatable` property; humans create by default. `Signature`'s `Human Modify = No` restricts *modification*, not creation. No defect. (Also: the proposed fix adds a property = schema change.) |
| **Constitution `Static` + `Versionable` is a contradiction** | R1-C22 | RMM documents this as intentional ("Static but Versionable — by design"). R2-m12 and R3 agree it is **not** a contradiction (amendment yields a new version). Consensus ⇒ keep. Changing `Stability` would also be an architecture change. |
| **`Concern` is a source-only node / missing reciprocals** | R2-C6 (graph claim) | False against the formal graph: `Domain/Layer/Slice → crossed-by → Concern` give it 3 incoming edges. Only the *Appendix A statistic* was wrong (fixed). |
| **Self-loops are cycles to remove** (`Layer→Layer`, `Lifecycle→Lifecycle`, `Role→Role`) | R1-M03 | By-design meta-level self-relations (instances relate to other instances of the same type). Not authority cycles; removing them changes the ontology. |
| **"119 circular dependencies" must be fixed now** | R1-M02 | The "cycles" are reciprocal forward/inverse verb pairs and structural containment reciprocity. The *authority* subgraph is verified acyclic. Treating containment-reciprocity as a defect requires splitting relationship semantics = architecture (see §3). |

---

## 3. FUTURE_PROPOSAL — real, but architectural (deferred to a future major version)

These are legitimate improvements that violate the v1.1 forbidden list (add/remove/merge/split/rename entities; change tiers/governance/lifecycle/ontology/schema/repository model). Kept out of the bug-fix release.

### 3.1 Structural / multi-product
- **P-01 Add `Product` (and/or `Namespace`/`Tenant`) entity** between Kernel and Domain for multi-product scoping. *(R1-C04/C18, R1-M10)* — adds entities.
- **P-02 Add an `Extension`/CRD-style mechanism** for product-specific entities without constitutional amendment. *(R1-C05, R1-M20)* — adds entities + extensibility model.
- **P-03 `LifecycleTemplate` + `LifecycleInstance` split** to relieve the `Lifecycle` 53-incoming hub at scale. *(R1-C27)* — adds entities.
- **P-04 `EntitySchema` (meta-meta-model)** for self-description. *(R1-M19)* — adds a layer.

### 3.2 Restore / formalize referenced-but-undefined concepts
- **P-05 Decide promote-or-remove for narrative forward-references:** `Port, Bridge, Adapter, Bus, Namespace, Registry, Scope, Event, Dependency, LifecycleStage, LifecycleGate, EntityType, EntryAction, ExitAction`. *(R1-C08, R2-C3, R3-C3)* — add entities or edit declared relationships; **contested add-vs-remove** ⇒ also see §4.
- **P-06 `EmergencyOverride`, `HumanFiduciary`, `Vote`/`DecisionMechanism`** referenced by governance narrative / dedup log but absent. *(R1-C12/C13/C14)* — adds entities + governance mechanics.

### 3.3 Consolidation (merges / degrades)
- **P-07** Merge candidates: `Exception+Waiver`, `Approval+Authorization`, `Finding+Conclusion`, `Decision+DecisionRecord`. *(R1-C07/C25, R2-M-context, R3-m4)* — merges entities.
- **P-08** Degrade candidates: `Topology`, `TraceabilityLink`, `Concern`, `View`, `Measurement`, `Snapshot`, `Escalation`, `Review/Audit/Assessment`. *(R1-C06/C30/C31/C32/C33, R3-m4)* — removes/relevels entities.
- **P-09** Restructure Tier 11 as a type hierarchy (`Artifact` abstract → Document/Specification/Record/Log/Report). *(R1-C23)* — ontology change.

### 3.4 Schema / property model
- **P-10** Move/abstract `Source of Truth` (property #15) — replace literal `NN-FOLDER/` paths with the existing storage *classes* (Ledger/Registry/Vault/Repository/Store) as normative, paths to an appendix. *(R1-C02, R3-D4)* — schema/repository-model change.
- **P-11** Move AI/Human permission properties (#12–#14) to a governance policy, or add a `Human Creatable` property. *(R1-C03/C26)* — schema change.
- **P-12** Split `Cardinality` into `InstanceCardinality` + `RelationCardinality`; replace generic Matrix-8 rationales. *(R2-M9/M10, R3-D6)* — schema change.
- **P-13** Disambiguate `Owner` (governance authority) vs definition-location; normalize free-form owner descriptors (`Module Lead`, `Founders Circle`, `Standards Authority`, …) to a controlled vocabulary or `Role` references. *(R1-C01, R2-C2, R3-C2)* — ownership-model change. *(Two unambiguous aliases already fixed in v1.1.)*
- **P-14** `Core` vs `Governance Profile` tagging so the judicial apparatus is an optional overlay. *(R3-C4/C5-context)* — adds schema dimension.

### 3.5 Naming / leakage / domain-independence
- **P-15** Remove product name `Radius1` from entity semantics; parameterize the system name. *(R1-C16, R3-D5)* — domain/rename change.
- **P-16** Replace `Founders Circle` with a self-referential / generic supreme-authority owner. *(R1-C17)* — governance change.
- **P-17** Replace runtime/SRE/IaC terminology (`runtime, provisioned, throttled, bootstrapped, append-only, tamper-evident`) with technology-neutral wording. *(R1-C15, R1-m04..m10)* — definition edits across many entities.
- **P-18** Generalize `Slice`, `Channel`, `Feature` away from SaaS/microservice/agile framing. *(R1-C19/C20/C24)* — definition/ontology edits.
- **P-19** Rename `Tier` entity (vs the catalog "Tier N" axis) to remove the naming collision. *(R1-C29, R3-m1)* — rename.

### 3.6 AI readiness
- **P-20** Reintroduce Actor subtypes (`HumanActor/AIAgent/HybridActor`), add a `Provenance` entity and an AI-native session/lifecycle. *(R1 §6, R1-C26)* — adds entities + lifecycle change.

### 3.7 Relationship coverage
- **P-21** Add missing relationships (e.g., `Constitution→Actor`, `Evidence→Artifact`, `Report→DecisionRecord`, `Standard→Rule`) and a documented reciprocal-relationship convention. *(R1-M01, R2-C6 convention)* — changes the graph.
- **P-22** Refile `Environment` source-of-truth out of `03-STANDARDS/`. *(R2-M5)* — repository-model change.

---

## 4. ARCHITECT_DECISION_REQUIRED — reviewers disagree, or RMM design intent conflicts

Kept exactly as authored in v1.1; an architect must rule.

| Item | Conflict |
|---|---|
| **A-01** Restore `Stakeholder` as a distinct entity (R1-C09, R2-C1-A) **vs** keep subsumed into `Actor` (RMM dedup log, applied in v1.1). | Review proposes overriding RMM's explicit dedup decision. RMM wins by evidence order #1; escalate only if the architect wants to revisit the merge. |
| **A-02** Structural dependency reciprocity in Matrix 9 (Module↔Component, Subsystem↔Module, etc.) is/ isn't a "circular dependency". | R1/R3 call it a defect; R2 does not. Resolution = split `contains` from `requires` (architecture). |
| **A-03** Forward-reference resolution (P-05): **promote** to entities (R1/R2) **vs** **remove** the references (R3 option). | Direct reviewer disagreement; either choice changes the model. |
| **A-04** Dedup-log "ghosts": `Authority, Revision, EmergencyPower, Safeguard, Dependency` logged "kept" but absent. Restore vs mark-eliminated. | R1 says restore; others imply remove/clean. Either changes entity set or rewrites provenance. |
| **A-05** `Invariant` full immutability vs Constitution amendability. | R1-C11 says make Invariant amendable (governance change); RMM design makes invariants `Eternal`. Single reviewer vs RMM intent. |
| **A-06** `Artifact` owned by `Constitution` ("category error", R1-C28). | Changing it is an ownership/governance decision; single reviewer; RMM intent is Artifact-as-root owned by the supreme instrument. |
| **A-07** Ownership model redesign into canonical tiers (R1-C01) vs add `DefinitionLocation` property (R2-C2) vs constrain `Owner` to entities (R3-C2). | Three incompatible redesigns; architect must choose (see P-13). |

---

## 5. Disposition index (per-review traceability)

**R1 (35 Critical):** C01→P-13/§4-A07; C02→P-10; C03→P-11; C04→P-01; C05→P-02; C06→P-08; C07→P-07; C08→P-05/A-03; C09→**ACCEPT**(ref)/A-01(entity); C10→**REJECT**; C11→A-05; C12→P-06; C13→P-06; C14→P-06; C15→P-17; C16→P-15; C17→P-16; C18→P-01; C19→P-18; C20→P-18; C21→P-08; C22→**REJECT**; C23→P-09; C24→P-18; C25→P-07; C26→P-11/P-20; C27→P-03; C28→A-06; C29→P-19; C30→P-08; C31→P-08; C32→P-08; C33→P-08; C34→P-21; C35→P-08. R1 Major M01→P-21; M02→**REJECT**/A-02; M03→**REJECT**; M09→P-10; M11/M12→**ACCEPT**; M18→P-02; M19→P-04; M20→P-02; (remaining M/m: terminology→P-17, or subsumed above). R1 minor m11/m12/m13→**ACCEPT**.

**R2 (6 Critical):** C1→**ACCEPT**(Actor)/A-01; C2→**ACCEPT**(alias)/P-13; C3→P-05/A-03; C4→**ACCEPT**; C5→**ACCEPT**; C6→**ACCEPT**(stat)/**REJECT**(graph claim). R2 Major: M1→**ACCEPT**; M5→P-22; M6→**ACCEPT**; M7/M8→P-08; M9/M10→P-12; M2/M3/M4→P-05/P-13. R2 minor: m1→**ACCEPT**; m12→**REJECT**(agrees not a defect); m13→P-13; others→P-12/P-13.

**R3 (5 Critical / 8 Major):** C1→A-02; C2→**ACCEPT**(aliases)/P-13; C3→**ACCEPT**(Stakeholder)/P-05; C4→P-14; C5→A-02/ontology; D1→**ACCEPT**; D2→**ACCEPT**; D3→A-04; D4→P-10; D5→P-15; D6→P-12; D7→**ACCEPT**; D8→P-19/A-02; minors→**ACCEPT**(m2)/P-08(m4)/P-05(m5).

---

*All architectural evolution above is reserved for a future major version. RMM v1.1 is a bug-fix release only.*
