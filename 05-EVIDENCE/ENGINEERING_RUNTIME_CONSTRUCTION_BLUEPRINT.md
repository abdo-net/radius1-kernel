# ENGINEERING_RUNTIME_CONSTRUCTION_BLUEPRINT.md

## ENGINEERING KERNEL — CONSUMER BLUEPRINT (executable specification)

---

# PART I: IDENTIFICATION

| Property | Value |
|----------|-------|
| Title | Engineering Runtime — Construction Blueprint |
| Short | ENGINEERING_RUNTIME_CONSTRUCTION_BLUEPRINT |
| Classification | DERIVED (specification of a separate consumer repository) |
| Owner | Engineering Kernel Architect (mission output; no RMM entity claims ownership) |
| Source of Truth | `05-EVIDENCE/ENGINEERING_RUNTIME_CONSTRUCTION_BLUEPRINT.md` |
| Status | Active |
| Version | 1.0.0 |
| Mission | ENGINEERING RUNTIME CONSTRUCTION DIRECTIVE |
| Baseline Kernel HEAD | `96042489b39e9a589280483054349ac2d7da00bc` |
| Consumes | the frozen Kernel exactly as it exists (no Kernel/RMM/Constitution/Governance modification) |

**Placement rule (binding).** This file is the *specification of* the Engineering Runtime. The Runtime's *actual content* (code, state, graphs, packages, evidence) **must be created in a separate consumer repository** — `KERNEL_SCOPE_DEFINITION.md` §9.5 ("Product content in Kernel directories is a violation") forbids it from living in `radius1-kernel`. This document is a DERIVED design artifact (the same category as prior accepted determinations) and is the only part that resides in the Kernel repo. Everything Section 1 describes is built *elsewhere*.

**Reference technology (non-binding; §3.2 technology selection is out of Kernel scope).** Canonical artifacts are **JSON** (machine-readable, git-diffable) with optional Markdown human mirrors. Engines are specified as language-neutral artifact contracts; the reference implementation language is **TypeScript/Node**, replaceable without changing this blueprint. Schemas below are **JSON Schema (draft 2020-12)**, abbreviated.

**Design invariants baked in from the prior first-principles reviews (normative for the build):**
- **I-1 Goal.** Success = every compliant AI converges on the same *constraints + acceptance criteria* (the spec), **not** the same code text. The Runtime guarantees conformance, not textual identity.
- **I-2 Cold/Warm.** Cross-model identity is guaranteed for *reading* a committed model (warm), **not** for *first generation* (cold). Cold output is `PROVISIONAL` until ratified.
- **I-3 Measured completeness.** Impact/coverage is **measured with explicit blind spots**, never asserted complete. Below threshold, execution is blocked and an investigation sub-workflow is mandatory.
- **I-4 Execution validates the model.** A verification failure that reveals un-modeled impact **invalidates** the frozen model region and re-enters reconstruction (bounded).
- **I-5 Truth stratification.** **Code** is authoritative for structure/deps/API-shape; the **Model** is authoritative for intent/decision/invariant. Structural facts are a cache invalidated against HEAD.
- **I-6 Validation authority.** Only **ratified** reasoning becomes a `VERIFIED_FACT` that may autonomously gate execution. The autonomy/trust/human trilemma is resolved by configuration, with consequences stated.
- **I-7 Ontology-first.** The Runtime reconstructs the *project's ontology* before its model, so it is not bound to the CRUD-web shape.
- **I-8 Fixpoint.** Reconstruction iterates to stability before `FREEZE`.

---

# PART II: THE BLUEPRINT

## 1. Repository Structure

Two repositories. The Kernel is pinned, never written to.

```
radius1-kernel/                      # FROZEN, pinned by hash; consumed read-only
  00-CONSTITUTION/ … 99-STATE/        # unchanged

engineering-runtime/                 # the Runtime engine (one repo, product-neutral)
  kernel.lock                         # { kernel_repo, kernel_commit, kernel_version, charter_id }
  package.json                        # reference impl (TS/Node)
  /spec/                              # this blueprint, vendored copy + JSON Schemas
    schemas/*.schema.json
  /engines/                           # reconstruction + planning + execution engines (code)
    e00-ontology/  e01-repository/ … e14-impact/  e15-truth/ e16-plan/ e17-package/
  /pipeline/                          # orchestrator + workflow definitions
    pipeline.json  gates.json
  /validators/                        # validation-gate implementations
  /adapters/                          # language/stack parsers (TS, SQL, OpenAPI, …) behind ontology
  /cli/                               # `runtime <command>` entrypoints
  /profiles/                          # ontology presets (crud-web, library, service, firmware, …)

<project>-runtime/                    # PER-PROJECT memory (one repo per software project)
  kernel.lock                         # pins the same Kernel version the project adopted
  runtime.lock                        # pins the engineering-runtime version used
  /state/                             # runtime + mission state (Section 3)
    runtime.json  mission.json  cursor.json
  /ontology/   ontology.json          # Section 4 (per-project node/edge taxonomy)
  /model/                             # the frozen Engineering Model (source of truth)
    nodes/*.json  edges/*.json  model.frozen.json  model.coverage.json
  /truth/      facts/*.json  truth.ledger.json     # Engineering Truth store (Section 6)
  /graphs/     topology.json semantic.json knowledge.json reasoning.json impact/*.json
  /plans/      <mission>.plan.frozen.json          # Section 7
  /packages/   <mission>.package.frozen.json       # Section 8
  /evidence/   <mission>/…                          # Section sessions output
  /decisions/  adr/*.json                           # ADRs / DECISION records
  /handoff/    <session>.handoff.json               # Section 11
  /audit/      audit.trail.jsonl                     # append-only
```

Three repos, three roles: **Kernel** = rules (frozen) · **engineering-runtime** = the engine (generic) · **`<project>-runtime`** = the memory (per project). No AI ever edits the project's *source* repo without first producing a frozen package in `<project>-runtime`.

## 2. Runtime Architecture

Layered, unidirectional (downstream depends on upstream; never the reverse):

```
Kernel (frozen rules)  ← read-only, hash-pinned
   ▲
Adapters (parsers)  →  Engines (E00–E17)  →  Pipeline Orchestrator  →  Gates/Validators
                                   │                    │
                                   ▼                    ▼
                          Engineering Model        Runtime State
                          (graphs + truth)         (state/ + handoff/)
```

- **Adapters** turn raw sources (code, SQL DDL, OpenAPI, config) into typed **observations**. Pure functions; deterministic.
- **Engines** consume observations + upstream engine outputs and emit model fragments. Each engine declares `mode ∈ {DETERMINISTIC, REASONING}`.
- **Orchestrator** runs the mandatory sequence (Section 16), enforces gates (Section 17), and forbids stage-skipping.
- **Model** and **State** are committed JSON in `<project>-runtime`; they *are* the memory. The Runtime is the *projection*; the Model is the source of truth (per I-5 stratification).

**Engine taxonomy.**

| ID | Engine | Mode | Output |
|----|--------|------|--------|
| E00 | Ontology | REASONING (cold) / DETERMINISTIC (warm) | `ontology.json` |
| E01 | Repository | DETERMINISTIC | structural nodes |
| E02 | Topology | DETERMINISTIC | `topology.json` |
| E03 | Structural (entities/db/services/dto/api/frontend…) | DETERMINISTIC | nodes + edges |
| E04 | Domain/Business | REASONING | business nodes, rules |
| E05 | Behavioral (workflows/state-machines/invariants) | REASONING | behavior nodes |
| E06 | Historical (ADR/decisions/findings/evidence) | DETERMINISTIC | decision/finding nodes |
| E07 | Semantic | REASONING→cached | `semantic.json` (typed meaning edges) |
| E08 | Knowledge | DETERMINISTIC | `knowledge.json` (join of E01–E07) |
| E09 | Reasoning | DETERMINISTIC over committed | `reasoning.json` |
| E10 | Dependency | DETERMINISTIC | dependency edges |
| E11 | Traceability | DETERMINISTIC | `TRACEABILITY_LINK` edges |
| E12 | Impact | DETERMINISTIC | `impact/<target>.json` |
| E13 | Risk/Regression | REASONING | risk nodes, regression predictions |
| E14 | Coverage/Completeness | DETERMINISTIC | `model.coverage.json` |
| E15 | Truth | DETERMINISTIC state machine + REASONING promotion | `truth.ledger.json` |
| E16 | Planning | DETERMINISTIC derive + REASONING fill | `*.plan.frozen.json` |
| E17 | Packaging | DETERMINISTIC | `*.package.frozen.json` |

Reasoning engines never write `VERIFIED_FACT` directly — they emit `HYPOTHESIS`/`ASSUMPTION` to E15, which governs promotion (Section 6).

## 3. Runtime State Model

`state/runtime.json` (singleton, current cursor of the project):

```json
{
  "$schema":"spec/schemas/runtime.schema.json",
  "project_id":"string","kernel_commit":"sha","runtime_version":"semver",
  "mode":"COLD|WARM","model_frozen":"sha|null","model_coverage":0.0,
  "last_session":"session_id","open_decisions":["dec_id"],
  "pending_tasks":["task_id"],"active_mission":"mission_id|null",
  "head_at_freeze":"sha","drift":"NONE|STRUCTURAL|SEMANTIC"
}
```

`state/mission.json` (current mission):

```json
{ "mission_id":"string","title":"string","status":"DECLARED|RECONSTRUCTING|PLANNED|FROZEN|EXECUTING|VERIFYING|LEARNING|CLOSED|BLOCKED",
  "target":"e.g. users.status","allowed_scope":["glob"],"forbidden_scope":["glob"],
  "plan":"plan_id|null","package":"package_id|null","coverage":0.0,
  "blocked_reason":"string|null" }
```

State transitions are the pipeline (Section 16); illegal transitions are rejected by the orchestrator. State is **derived from committed artifacts** — never from conversation — satisfying session independence (Section… see 11).

## 4. Reconstruction Engines (and the ontology that parameterizes them)

**E00 Ontology (first, per I-7).** Output `ontology.json`:

```json
{ "profile":"crud-web|service|library|firmware|custom",
  "node_classes":[{"id":"Service","extends":"Component","detector":"adapter:ts/nest-service"}],
  "edge_types":[{"id":"exposes","from":"Controller","to":"Endpoint","semantic":"…"}],
  "coverage_targets":{"Service":0.95,"Permission":0.99} }
```

In **cold** mode E00 is REASONING (it infers what kinds of things exist) and its output is `PROVISIONAL` until ratified. In **warm** mode it is a deterministic read of the committed `ontology.json`. Every later engine is parameterized by it — this is what makes the Runtime universal rather than CRUD-web-bound.

**E01–E06** populate nodes/edges per ontology. Deterministic engines (E01/E02/E03/E06/E10/E11) extract from declarative sources via Adapters and tag every fact `source_authority:"CODE"`. Reasoning engines (E04/E05) tag `source_authority:"MODEL"` and emit at truth-class `HYPOTHESIS`.

**Fixpoint (I-8).** The orchestrator runs E00→E13 repeatedly until a full pass produces **zero** node/edge/fact deltas (`model.stable == true`). Only a stable model may be frozen. A max-iteration bound emits a `NON_CONVERGENCE` finding and blocks freeze.

## 5. Graph Builders

Four typed graphs, all over the same node set, all JSON, all `TRACEABILITY_LINK`-typed edges ("may not be semantically empty"):

- **Topology** (E02) — arrangement/connectivity (RMM `TOPOLOGY`; lifecycle Observed→Documented first).
- **Semantic** (E07) — typed meaning edges: `introduced-by-Decision`, `protects-Invariant`, `enforces-Rule`, `owned-by`, `governed-by-Contract`.
- **Knowledge** (E08) — deterministic join of structural + semantic + historical.
- **Reasoning** (E09) — `DECISION`/`FINDING`/`CONCLUSION` nodes linked to the objects they justify.
- **Impact** (E12) — *not stored whole*; computed on demand as the forward closure from a target node, materialized to `impact/<target>.json` with a coverage stamp.

Node/edge schema (`model/nodes/*.json`, `model/edges/*.json`):

```json
// node
{ "id":"node:Service/UsersService","class":"Service","name":"UsersService",
  "source_authority":"CODE|MODEL","source_ref":"path#L|adr:id","truth":"truth_id",
  "kernel_entity":"Component","extension_of":"RMM:Component (§9.7)" }
// edge
{ "id":"edge:…","type":"exposes","from":"node:…","to":"node:…",
  "semantic":"non-empty string","truth":"truth_id","directional":true }
```

## 6. Engineering Truth Model

`truth/facts/<id>.json` — every node/edge/statement references exactly one truth record:

```json
{ "id":"truth:…","statement":"users.status is persisted as enum",
  "class":"DIRECT_OBSERVATION|VERIFIED_FACT|DERIVED_FACT|ARCHITECTURAL_DECISION|BUSINESS_RULE|CONSTRAINT|ASSUMPTION|HYPOTHESIS|UNSUPPORTED|REJECTED|SUPERSEDED",
  "source_authority":"CODE|MODEL","evidence":["evidence_ref"],"derivation":"rule_id|null",
  "confidence":"DISCRETE via class (no scalar)","commit":"sha","timestamp":"iso",
  "dependencies":["truth_id"],"invalidation_rule":"if source_ref@commit changes → CHALLENGED",
  "validated_by":"authority_id|null","lifecycle":"Observed|Validated|Published|Challenged|Corrected" }
```

**Class machine (E15).**
- Mechanical extraction → `DIRECT_OBSERVATION`.
- Confirmed by ≥2 independent deterministic sources, or ratified → `VERIFIED_FACT`.
- Computed from verified facts by a declared rule → `DERIVED_FACT`.
- AI inference → born `HYPOTHESIS` (or `ASSUMPTION` if it must be assumed to proceed); **never auto-promoted**. Searched-for-but-absent → `UNSUPPORTED` (explicit, per KI-LK-06 "returns `[UNSUPPORTED]`", no fabrication).
- Source change → reverse-closure walk sets dependents `CHALLENGED` until re-validated (I-4 invalidation; RMM `FINDING` Challenged→Corrected).

**Promotion / Validation Authority (I-6).** `runtime.json.validation_authority ∈ {SELF, PEER, HUMAN}`:
- `SELF` → fast, autonomous, **no class above `DERIVED_FACT`**; reasoning stays `HYPOTHESIS`/`ASSUMPTION` and can only inform, not gate.
- `HUMAN` → reasoning may be ratified to `VERIFIED_FACT`/`ARCHITECTURAL_DECISION`; autonomous throughput bounded by review. This is the GAP-001 ratification boundary surfaced operationally.
- Only `VERIFIED_FACT`/`ARCHITECTURAL_DECISION`/`BUSINESS_RULE`/`CONSTRAINT` may **gate execution**. `ASSUMPTION`/`HYPOTHESIS` are carried into the package as **declared risks**, never as facts.

## 7. Planning Engine (E16)

Produces an **immutable** `plans/<mission>.plan.frozen.json`:

```json
{ "id":"plan:…","mission":"mission_id","objective":"string",
  "affected_modules":[…],"affected_files":[…],"affected_apis":[…],"affected_contracts":[…],
  "affected_tests":[…],"affected_documentation":[…],
  "implementation_order":["step"],            // topological sort over dependency closure
  "validation_gates":["gate_id"],"rollback_point":"sha",
  "evidence_requirements":[…],"acceptance_criteria":[{ "id":"AC1","check":"machine-verifiable" }],
  "known_risks":["truth_id(ASSUMPTION/HYPOTHESIS)"],"coverage":0.0,"frozen":true,"frozen_at":"sha" }
```

Order is derived (topo-sort over the impact closure), never freely authored (RMM `PLAN`: "may not omit exit criteria"). Acceptance criteria are **machine-verifiable predicates** — this is the operational form of I-1 (convergence on the spec). The plan is `Drafted → validated (Section 9) → Frozen`; only frozen plans proceed.

## 8. Execution Package Model (E17)

`packages/<mission>.package.frozen.json` — the **only** engineering context allowed during implementation, a frozen engineering *mission*:

```json
{ "id":"pkg:…","mission":"mission_id","plan":"plan:…",
  "mission_statement":"string","allowed_scope":["glob"],"forbidden_scope":["glob"],
  "affected_components":["node_id"],"required_contracts":["contract_id"],
  "required_evidence":[…],"required_tests":[…],"required_validation":["gate_id"],
  "required_documentation":[…],"expected_deliverables":[…],"acceptance_criteria":[…],
  "known_risks":[…],"known_findings":["truth_id"],"known_decisions":["adr_id"],
  "required_patterns":["pattern_id"],"required_rules":["rule_id"],"required_invariants":["inv_id"],
  "repository_snapshot":"sha","commit_hash":"sha","coverage":0.0,
  "escape_hatch":"on contradiction with live code → HALT + emit CONTRADICTION finding → return to reconstruction" }
```

**Freshness + escape hatch (I-3/I-4).** Execution aborts if live `HEAD ≠ commit_hash` within the impact closure. The package **scopes** repository reading to its `affected_components` + closure (it does not pretend to replace the repo). If, during implementation, live code contradicts the package, the AI must **halt and raise a `CONTRADICTION` finding**, not silently follow a stale package nor read freely outside scope.

## 9. Validation Pipeline

Validators are pure predicates returning `{pass, evidence, blocking}`. They run at the gates of Section 17. Categories:
- **Structural** — schema-valid artifacts; every node/edge has a truth ref; no semantically-empty edge.
- **Truth** — no `VERIFIED_FACT` lacking evidence; no fact promoted above authority ceiling; no `CHALLENGED` fact gating execution.
- **Coverage** — `model.coverage.json ≥ ontology.coverage_targets` per class, else block (I-3).
- **Plan** — acceptance criteria machine-checkable; order is a valid topo-sort; rollback point set.
- **Package** — snapshot hash matches HEAD; scope non-empty; forbidden∩allowed = ∅.
- **Post-execution** — acceptance criteria satisfied; no regression outside `affected_components`; required evidence present.

Bridges to Kernel: validators delegate to `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5 semantics (completeness/integrity) — referenced, never modified.

## 10. Runtime Persistence

The committed JSON in `<project>-runtime` **is** the persistence; git is the database. Rules:
- All model/truth/graph/plan/package artifacts are content-addressed and committed; the commit is the deliverable (code is a *consequence*).
- `model.frozen.json` and `*.frozen.json` are immutable (RMM `SNAPSHOT` "may not be modified after Commit"); revisions create new versions.
- `audit/audit.trail.jsonl` is append-only.
- No external DB is required; a graph DB may be a *cache* rebuilt from JSON, never the source of truth.

## 11. Handoff Model (session independence)

End of session writes `handoff/<session>.handoff.json`:

```json
{ "session_id":"…","next_starts_from":"this file","mode":"WARM",
  "runtime_state":"state/runtime.json@sha","mission_state":"state/mission.json@sha",
  "knowledge_delta":["node_id|edge_id"],"truth_delta":["truth_id"],"impact_delta":["target"],
  "open_decisions":["adr_id"],"pending_tasks":["task_id"],
  "evidence_bundle":"evidence/<mission>/","execution_summary":"…","model_frozen":"sha" }
```

Any vendor (Claude/Kimi/xAI/Gemini/ChatGPT) begins by reading the latest handoff + frozen model — **never** conversation history. Because warm reconstruction is a deterministic re-read of identical committed artifacts under the identical pinned Kernel grammar, all vendors reconstruct the **same** engineering state (I-2, reading guarantee).

## 12. Update Model

`UPDATE` stage commits the deltas: advance/append truth records, extend topology toward `Evolving`, add edges, write evidence, record `DECISION`s, append audit, bump `runtime.json`. Updates are **incremental and scoped to the mission's impact closure** (bounded re-validation, answering the decay-economics gap): only `CHALLENGED` facts in the closure are re-evaluated, not the whole model.

## 13. Workflow Definitions

`pipeline/pipeline.json` defines the mandatory mission workflow as an explicit state machine (RMM `WORKFLOW`: "may not have deadlock; may not lack ExitPoint"). States = Section 16 stages; each edge declares `precondition` (a gate, Section 17). Sub-workflows:
- **COLD_BOOTSTRAP** — full reconstruction → mark `PROVISIONAL` → request ratification.
- **WARM_RESUME** — read frozen model → freshness-check vs HEAD → invalidate stale CODE facts → re-extract only those.
- **INVESTIGATION** (escape hatch) — triggered by coverage<threshold or a `CONTRADICTION`; bounded deep-dive that emits new observations, returns to fixpoint.
- **CONTRADICTION_RECOVERY** — verification revealed un-modeled impact → invalidate model region → re-enter reconstruction at E-level of the contradiction.

## 14. Runtime File Specifications

Every file above has a JSON Schema in `engineering-runtime/spec/schemas/`. Canonical set: `runtime.schema.json`, `mission.schema.json`, `ontology.schema.json`, `node.schema.json`, `edge.schema.json`, `truth.schema.json`, `plan.schema.json`, `package.schema.json`, `handoff.schema.json`, `coverage.schema.json`, `gate.schema.json`. All artifacts carry `$schema`, `version`, `commit`, `timestamp`. Markdown mirrors (optional) are generated, never authoritative.

## 15. Data Schemas

The normative schemas are Sections 3, 5, 6, 7, 8, 11 above (runtime/mission state, node/edge, truth, plan, package, handoff). Cross-cutting required fields on every record: `id`, `$schema`, `version`, `commit`, `timestamp`, and (for facts/nodes/edges) `truth`/`source_authority`. IDs are namespaced (`node:`, `edge:`, `truth:`, `plan:`, `pkg:`, `adr:`, `task:`).

## 16. Execution Sequence

The mandatory, non-skippable pipeline (orchestrator-enforced):

```
BOOT → MODE-DETECT(cold|warm)
  → [cold: COLD_BOOTSTRAP] | [warm: WARM_RESUME]
  → E00 Ontology → E01 Repository → E02 Topology → E03 Structural
  → E04 Domain/Business → E05 Behavioral → E06 Historical
  → E07 Semantic → E08 Knowledge → E09 Reasoning
  → E10 Dependency → E11 Traceability → E12 Impact
  → E13 Risk/Regression → [fixpoint: repeat E00–E13 until stable]
  → E14 Coverage → E15 Truth-Verification
  → GATE:RECONSTRUCTION-COMPLETE
  → E16 Plan → GATE:PLAN-VALID → FREEZE-MODEL → FREEZE-PLAN
  → E17 Package → GATE:PACKAGE-VALID → FREEZE-PACKAGE
  → IMPLEMENT (only from package; escape-hatch armed)
  → VERIFY → [fail+un-modeled: CONTRADICTION_RECOVERY] 
  → EVIDENCE → LEARN → UPDATE-RUNTIME → HANDOFF → CLOSE
```

`IMPLEMENT` is structurally unreachable before `FREEZE-PACKAGE` — execution is late by construction, not by discipline (RMM/`AI_EXECUTION_PROTOCOL.md`: "a phase SHALL NOT be skipped").

## 17. Validation Gates

| Gate | Precondition to pass | On fail |
|------|----------------------|---------|
| G-BOOT | `kernel.lock` hash matches pinned Kernel; runtime/project locks present | abort |
| G-FIXPOINT | `model.stable == true` within max iterations | NON_CONVERGENCE finding; block |
| G-COVERAGE | coverage ≥ ontology targets per class | INVESTIGATION sub-workflow |
| G-TRUTH | no fact above authority ceiling; no CHALLENGED fact gating; no fabrication | block + flag |
| G-RECONSTRUCTION-COMPLETE | G-FIXPOINT ∧ G-COVERAGE ∧ G-TRUTH | block |
| G-PLAN-VALID | acceptance criteria machine-checkable; valid topo order; rollback set | block |
| G-PACKAGE-VALID | snapshot==HEAD; scope sane; forbidden∩allowed=∅ | block / re-snapshot |
| G-FRESHNESS (exec-time) | HEAD == package.commit_hash within closure | HALT + CONTRADICTION |
| G-POST | acceptance criteria met; no out-of-scope regression; evidence present | fail mission; LEARN |

No gate may be waived except `G-COVERAGE` and truth-promotion, and only by the configured **HUMAN** validation authority (recorded as a `DECISION`).

## 18. Integration with the Existing Kernel

The Runtime **consumes** the Kernel; it adds no layer to it and modifies nothing in it.

- **Pinning.** `kernel.lock` records the Kernel commit (`96042489…`) + version + Charter id (§8 Consumer Model: "Consumers reference specific Kernel versions"; "must tolerate Kernel version changes").
- **Entity mapping (§9.7 product extensions; every Runtime object references a base Kernel entity, lives in consumer space, and "must not claim to be part of Kernel"):**

| Runtime object | Kernel entity (consumed, unchanged) | AI Creatable |
|---|---|---|
| topology graph | `TOPOLOGY` (Observed→Documented) | Yes |
| nodes composite | `ASSEMBLY` | Yes |
| all edges | `TRACEABILITY_LINK` (typed, non-empty) | Yes |
| truth facts | `FINDING` (Observed→Validated→Published→Challenged→Corrected) | Yes |
| derived facts | `CONCLUSION` | With Approval |
| ADRs / decisions | `DECISION` / `DECISION_RECORD` | With Approval |
| invariants / rules | `INVARIANT` / `RULE` / `POLICY` / `CONSTRAINT` | (existing) |
| plan | `PLAN` (Freezable) | With Approval |
| frozen package / snapshot | `SNAPSHOT` / `ASSEMBLY` | Kernel/Yes |
| session state | `SESSION` / `CONTEXT` (`99-STATE/` semantics) | (existing) |
| evidence | `EVIDENCE` | Yes |

- **Buildable today vs. gated.** All AI-Creatable:Yes objects (TOPOLOGY, ASSEMBLY, TRACEABILITY_LINK, FINDING, EVIDENCE) are buildable immediately. `DECISION`/`CONCLUSION`/`PLAN` as *binding* and any `VERIFIED_FACT` promotion route through the configured validation authority (the GAP-001/governance boundary), exactly as Section 6 specifies.
- **Discipline bridges.** Determinism inherits from `KNOWLEDGE_INDEX_SPECIFICATION.md` (KI-IX-04 completeness, KI-LK-06 no-fabrication), `KERNEL_DOCUMENT_REGISTRY.md` §7 read order, and `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5 — all referenced, none modified. Reference-isolation (SAS4 etc.) uses `KERNEL_SCOPE_DEFINITION.md` §9.3 Technology Bridge + `04-PATTERNS/`: a reference enters only as an abstract pattern node born `HYPOTHESIS`, never as copied content (§9.5).

---

# PART III: BUILD ORDER (so implementation begins immediately)

1. Scaffold `engineering-runtime` repo + `spec/schemas/*` (Section 14/15) + `kernel.lock`.
2. Implement Adapters + E01/E02/E03/E06/E10/E11 (deterministic core) and the JSON model store (Sections 4/5/10).
3. Implement E15 Truth + E14 Coverage + the gate engine (Sections 6/9/17).
4. Implement E00 Ontology + profiles (Section 4) and the fixpoint orchestrator (Sections 2/16).
5. Implement E04/E05/E07/E09/E13 (reasoning engines emitting HYPOTHESIS) + validation-authority promotion.
6. Implement E16 Plan + E17 Package + freshness/escape-hatch (Sections 7/8).
7. Implement IMPLEMENT/VERIFY/LEARN/UPDATE/HANDOFF + CONTRADICTION_RECOVERY (Sections 11/12/13/16).
8. Stand up the first `<project>-runtime` (cold bootstrap), ratify, freeze, and run a real mission (`users.status`) end-to-end.

This blueprint is directly implementable: every engine has a typed input/output, every artifact a schema, every transition a gate, and every Runtime object a Kernel entity it extends without modifying.

---

# PART IV: REVISION HISTORY

| Version | Date | Author | Change | Reference |
|---------|------|--------|--------|-----------|
| 1.0.0 | 2026-06-28 | Engineering Kernel Architect | Complete executable construction blueprint for the Engineering Runtime as a separate consumer repository (three-repo model: frozen Kernel · generic engine · per-project memory); all 18 required sections (repo structure, architecture, state, engines E00–E17, graph builders, truth model, planning, execution package, validation pipeline, persistence, handoff, update, workflows, file specs, data schemas, execution sequence, gates, Kernel integration); baked in the agreed first-principles invariants I-1..I-8 (constraint-convergence not code-identity; cold/warm; measured completeness + investigation fallback; execution-as-validator; truth stratification; named validation authority; ontology-first; fixpoint); maps every Runtime object to an existing RMM entity as a §9.7 extension; no Kernel/RMM/Constitution/Governance modification | ENGINEERING RUNTIME CONSTRUCTION DIRECTIVE |

---

*End of ENGINEERING_RUNTIME_CONSTRUCTION_BLUEPRINT.md*
