# ENGINEERING_RUNTIME_IMPLEMENTATION_SPEC.md

## ENGINEERING KERNEL — CONSUMER IMPLEMENTATION SPECIFICATION

> Operating-system specification for deterministic software engineering.
> Code-shaped, not prose: every subsystem below has interfaces, algorithms, a
> state machine, schemas, and failure/recovery. An implementation team can begin
> coding directly from Part III. Reference language: **TypeScript/Node** (non-binding,
> `KERNEL_SCOPE_DEFINITION.md` §3.2). Canonical storage: **git-committed JSON**.

---

# PART I: IDENTIFICATION

| Property | Value |
|----------|-------|
| Title | Engineering Runtime — Implementation Specification |
| Short | ENGINEERING_RUNTIME_IMPLEMENTATION_SPEC |
| Classification | DERIVED (specification of a separate consumer repository) |
| Owner | Engineering Kernel Architect (mission output; no RMM entity claims ownership) |
| Source of Truth | `05-EVIDENCE/ENGINEERING_RUNTIME_IMPLEMENTATION_SPEC.md` |
| Status | Active · Version 1.0.0 |
| Mission | ENGINEERING RUNTIME CONSTRUCTION DIRECTIVE (Implementation Phase) |
| Baseline Kernel HEAD | `96042489b39e9a589280483054349ac2d7da00bc` |
| Builds on | `ENGINEERING_RUNTIME_CONSTRUCTION_BLUEPRINT.md` (architecture); this adds executable detail |
| Placement (binding) | This spec lives in the Kernel repo as DERIVED design; the **code and all runtime content are built in a separate `engineering-runtime` repo** (§9.5). |

**Invariants carried from the agreed reviews (normative):** I-1 convergence on *constraints*, not code text · I-2 cold/warm (cross-model identity = reading only) · I-3 measured completeness + investigation fallback · I-4 execution validates the model · I-5 code authoritative for structure, model for intent · I-6 named validation authority · I-7 ontology-first · I-8 fixpoint reconstruction.

---

# PART II: SYSTEM-WIDE MODEL (shared by every subsystem)

## II.1 Process model — three processes, one mediation boundary

```
┌─ AI worker (any LLM) ─┐     stdin/stdout JSON-RPC     ┌─ Runtime (this software) ─┐
│ proposes / implements │  ←───────────────────────→   │ thinks / validates / freezes│
└───────────────────────┘                              └──────────────┬─────────────┘
                                                                       │ git
                                                          ┌────────────▼─────────────┐
                                                          │ <project>-runtime (memory)│
                                                          │ + project source (RO/scoped)│
                                                          └────────────────────────────┘
```

The AI is a **driven worker**, never an autonomous actor. It cannot touch the project repo directly; all reads/writes go through the Runtime (II.2). The Runtime is a normal program (CLI + library); it embeds no model. This is how "the AI works through the Runtime" becomes literal software.

## II.2 Mediation Protocol (the AI↔Runtime contract) — JSON-RPC over stdio

The Runtime drives a fixed loop. The AI may only respond to the *current required action*.

```ts
interface RuntimeRequest {                 // Runtime → AI
  session: string; mission: string; stage: Stage;
  action: "RECONSTRUCT_REASONING" | "PROPOSE_DECISION" | "IMPLEMENT_STEP" | "NONE";
  context: PackageView | ReconstructionView;   // the ONLY context the AI may use
  allowed_reads: string[];                      // globs; scoped to package closure
  deadline_ms: number;
}
interface AIResponse {                      // AI → Runtime
  proposals?: Proposal[];   // findings/decisions/edges (enter as HYPOTHESIS)
  patch?: UnifiedDiff;      // only in IMPLEMENT_STEP, only within allowed_reads
  notes?: string;          // discarded (temporary reasoning; "the AI forgets")
}
```

Rules enforced by the Runtime (not by AI goodwill):
- The AI cannot read a path outside `allowed_reads` → `runtime.read(path)` returns `E_SCOPE`.
- Any `patch` touching `forbidden_scope` is rejected pre-apply (`E_SCOPE`).
- `notes` are never persisted. Only validated, typed artifacts persist. ("Runtime records; AI forgets.")
- The AI cannot advance the stage; only the orchestrator does, and only through a gate.

## II.3 Object store & ID scheme (used by all subsystems)

Every persisted unit is a content-addressed JSON object in `<project>-runtime`:

```ts
type Id = `${Kind}:${string}`;   // node:Service/UsersService · truth:… · edge:… · plan:… · pkg:…
interface Obj { id: Id; $schema: string; version: string; commit: Sha; ts: IsoTime; }
interface Store {
  get<T extends Obj>(id: Id): T | null;
  put<T extends Obj>(o: T): Sha;          // writes file, returns commit-staged hash
  query(pred: Predicate): Id[];           // deterministic order: sort by id
  freeze(id: Id): void;                   // marks immutable; further put → E_IMMUTABLE
  commit(msg: string): Sha;               // git commit; the commit IS the save
}
```

Determinism law: every `query`/traversal returns results in **sorted id order**; no map-iteration order may leak into output (else cross-model divergence). Tested by `det-harness` (II.6).

## II.4 Global error taxonomy

| Code | Meaning | Default handling |
|------|---------|------------------|
| `E_SCOPE` | read/write outside allowed scope | reject; log; no state change |
| `E_GATE` | gate precondition unmet | block stage; emit `Finding(blocking)` |
| `E_FRESHNESS` | HEAD ≠ frozen snapshot in closure | HALT mission → `CONTRADICTION_RECOVERY` |
| `E_COVERAGE` | coverage < target | → `INVESTIGATION` sub-workflow |
| `E_IMMUTABLE` | write to frozen object | reject |
| `E_NONCONVERGENCE` | fixpoint exceeded max iters | block freeze; emit finding |
| `E_AUTHORITY` | promotion above authority ceiling | reject promotion; keep HYPOTHESIS |
| `E_ADAPTER` | parser failure on a source | mark region UNSUPPORTED; lower coverage |
| `E_CONTRADICTION` | model vs live code disagree | invalidate region; re-reconstruct |

Every error is a typed object, appended to `audit/audit.trail.jsonl`, and (if `blocking`) materialized as a `FINDING`.

## II.5 Determinism & recovery foundation

- **Idempotent stages.** Every stage is a pure function of (committed state, HEAD); re-running yields the same output. Crash recovery = re-run the current stage; no partial in-memory state is authoritative.
- **Write-ahead.** Each stage writes its outputs then advances the cursor (`state/cursor.json`) atomically (single commit). A crash leaves the cursor at the last completed stage.
- **Replayability.** `runtime replay <mission>` re-executes from the committed inputs and must reproduce byte-identical artifacts (the determinism test).

## II.6 Conformance harness (build-time gate)

`det-harness` runs the full pipeline twice on a fixture project and asserts byte-identical `model.frozen.json`, identical impact closures, identical handoff. Any non-determinism (map order, timestamps in hashed content, locale) fails CI. This is the executable proof of I-2.

---

# PART III: SUBSYSTEM SPECIFICATIONS

Each subsystem is specified with the 15 required facets. Trivial facets are stated compactly; hard logic (Store, Truth, Impact, Orchestrator, Coverage, Mediation) is expanded.

## S1 — Kernel Bridge

1. **Responsibilities** Load + pin the Kernel; expose RMM entity definitions, validation rules (VS-1..5), read-order, and scope rules as a read-only typed API. Verify the pin on every boot.
2. **Lifecycle** `LOAD → VERIFY(hash) → INDEX → READY`. Re-verify on each `runtime boot`.
3. **Internal workflow** Read `kernel.lock` → `git ls-tree <kernel_commit>` → assert hash → parse `RMM_v1.1.md`, `KERNEL_VALIDATION_PROTOCOL.md`, `KERNEL_SCOPE_DEFINITION.md`, `KNOWLEDGE_INDEX_SPECIFICATION.md`, `KERNEL_DOCUMENT_REGISTRY.md §7` into in-memory tables.
4. **Algorithms** RMM parse → `Map<EntityName, EntitySpec{tier, owner, aiCreatable, lifecycle, forbidden[]}>`.
5. **State machine** see lifecycle; `READY` is terminal until version change.
6. **Persistence** none of its own; pin lives in `kernel.lock`.
7. **Storage format** `kernel.lock`: `{kernel_repo, kernel_commit, kernel_version, charter_id}`.
8. **Schemas** `kernel.lock.schema.json`.
9. **Interfaces** `entity(name): EntitySpec` · `canAICreate(name): boolean` · `validators(): ValidatorRef[]` · `readOrder(): string[]`.
10. **Contracts** Never writes to the Kernel repo (asserted: Kernel path mounted read-only).
11. **Validation** Boot fails (`E_GATE` at G-BOOT) if hash mismatches.
12. **Failure handling** Mismatch → abort with remediation (re-pin or update). Missing Kernel → abort.
13. **Recovery** Deterministic re-load; no state to repair.
14. **Update process** Kernel version bump = explicit `runtime pin <commit>` + re-run conformance; "must tolerate Kernel version changes" (§8).
15. **Integration** Source of all entity/validation semantics for S6/S7/S10/S12.

## S2 — Store / Persistence Layer (the engineering memory)

1. **Responsibilities** Durable, deterministic, git-backed object store; immutability of frozen objects; append-only audit.
2. **Lifecycle (object)** `Draft → Validated → Committed → (Frozen) → Superseded`.
3. **Internal workflow** `put` → schema-validate → write `<kind>/<id>.json` → stage. `commit` → `git commit`. `freeze` → set `frozen:true`, record in `frozen.index.json`.
4. **Algorithms** id sort for `query`; content hash = sha256 of canonical-JSON (sorted keys, no volatile fields) for change detection.
5. **State machine** object immutability enforced post-`freeze`.
6. **Persistence** the git repo itself.
7. **Storage format** one JSON file per object; JSONL for audit; directory = kind.
8. **Schemas** every object validates against its `$schema`.
9. **Interfaces** `Store` (II.3).
10. **Contracts** No external DB is authoritative; any DB is a rebuildable cache.
11. **Validation** reject malformed objects (`E_GATE`); reject writes to frozen (`E_IMMUTABLE`).
12. **Failure handling** write failure → roll back staged files (git restore); never leave half-objects.
13. **Recovery** `git reset` to last commit = consistent state; cursor points to last completed stage.
14. **Update process** new versions create new files (`@v2`), never mutate frozen.
15. **Integration** every other subsystem persists through S2.

## S3 — Adapter Framework (sources → observations)

1. **Responsibilities** Turn raw project sources into typed `Observation`s; one adapter per source kind, selected by the ontology.
2. **Lifecycle** `DETECT(files) → PARSE → EMIT(observations) → (E_ADAPTER → UNSUPPORTED region)`.
3. **Internal workflow** glob match → parse → map AST/spec nodes to ontology node-classes.
4. **Algorithms** pure parse functions; e.g. `ts-nest` adapter: walk decorators (`@Controller`,`@Injectable`) → emit `Controller`/`Service` observations with `source_ref=path#Lstart-Lend`.
5. **State machine** stateless per file.
6–8. **Persistence/format/schema** observations are transient inputs to engines; `observation.schema.json`.
9. **Interfaces** `interface Adapter { kind: string; detect(fs): File[]; parse(f): Observation[] }`.
10. **Contracts** Adapters emit only `DIRECT_OBSERVATION` truth-class, `source_authority:"CODE"`.
11. **Validation** every observation has a resolvable `source_ref`.
12. **Failure** parse error → emit `E_ADAPTER`, mark file UNSUPPORTED (counts against coverage, never fabricates).
13. **Recovery** re-parse on next run; deterministic.
14. **Update** new stack = new adapter behind the ontology, no engine change.
15. **Integration** feeds S5 reconstruction engines. Built-in set: `ts-nest`, `typeorm/prisma`, `sql-ddl`, `openapi`, `angular/react-router`, `rbac-config`, `markdown-adr`, `jest/vitest`.

## S4 — Ontology Engine (E00) — *ontology-first (I-7)*

1. **Responsibilities** Produce `ontology.json`: the node-classes, edge-types, and per-class coverage targets that exist in *this* project.
2. **Lifecycle** cold: `INFER(provisional) → RATIFY → ACTIVE`; warm: `READ(active)`.
3. **Internal workflow** cold: detect stack → select base profile (`profiles/*.json`) → AI proposes project-specific classes/edges as `HYPOTHESIS` → validation authority ratifies → freeze.
4. **Algorithms** profile-merge + AI-augment; warm = deterministic read.
5. **State machine** `PROVISIONAL → ACTIVE → EVOLVING`.
6–8. **Persistence/format/schema** `ontology/ontology.json`; `ontology.schema.json`.
9. **Interfaces** `ontology(): Ontology` · `coverageTarget(class): number`.
10. **Contracts** Every later engine is parameterized by the active ontology; engines may not hardcode classes.
11. **Validation** every node-class has a detector (adapter binding) or is marked unreconstructable.
12–13. **Failure/recovery** no profile match → `custom` profile, all classes provisional, coverage targets default low until ratified.
14. **Update** new class → EVOLVING + re-fixpoint.
15. **Integration** governs S3 selection and S5–S12 typing. This is what makes the Runtime universal, not CRUD-bound.

## S5 — Reconstruction Engine Framework (E01–E13)

1. **Responsibilities** Populate nodes/edges/findings per ontology. Two modes: **DETERMINISTIC** (E01 repo, E02 topology, E03 structural, E06 historical, E10 dependency, E11 traceability) and **REASONING** (E04 domain, E05 behavioral, E07 semantic, E09 reasoning, E13 risk).
2. **Lifecycle (per engine)** `INPUT(upstream artifacts) → COMPUTE → EMIT(typed objects) → DIFF(vs committed)`.
3. **Internal workflow** deterministic engines consume observations → emit nodes/edges tagged `CODE`/`DIRECT_OBSERVATION`. Reasoning engines drive the AI via Mediation (S13) → emit `HYPOTHESIS` tagged `MODEL`, never facts.
4. **Algorithms** per engine; e.g. E11 Traceability builds `TRACEABILITY_LINK` edges by matching typed endpoints (`Controller -exposes→ Endpoint`, `Endpoint -declared-in→ OpenAPI`) from edge-type rules in the ontology.
5. **State machine** each engine idempotent; emits a `delta` set.
6–8. **Persistence/format/schema** `model/nodes/*.json`, `model/edges/*.json`; `node.schema.json`, `edge.schema.json`.
9. **Interfaces** `interface Engine { id: EngineId; mode: "DET"|"REASON"; run(ctx): Delta }`.
10. **Contracts** Reasoning engines MUST emit `HYPOTHESIS`/`ASSUMPTION` only; promotion is S7's job. No engine writes a `VERIFIED_FACT`.
11. **Validation** every emitted edge non-empty-semantic; every node has truth ref.
12. **Failure** missing upstream → engine blocked (`E_GATE`); unparseable region → UNSUPPORTED.
13. **Recovery** re-run engine; deterministic engines reproduce exactly.
14. **Update** incremental: on warm resume, re-run only engines whose inputs changed (dirty-tracking by source hash).
15. **Integration** orchestrated by S11 under the fixpoint loop.

## S6 — Graph Service (+ Impact, E12)

1. **Responsibilities** Maintain the four typed graphs (topology/semantic/knowledge/reasoning) and compute **impact closures** on demand.
2. **Lifecycle** graphs are views over committed nodes/edges; rebuilt deterministically.
3. **Internal workflow / Algorithm (Impact — the core)**:
```
function impact(target: NodeId): ImpactClosure {
  const visited = new Set(); const order: NodeId[] = []; const frontier = [target];
  while (frontier.length) {
    const n = frontier.shift();                  // BFS, ids pushed in sorted order
    if (visited.has(n)) continue; visited.add(n); order.push(n);
    for (const e of edges.outFrom(n).sort(byId)) // deterministic
       if (e.type ∈ ontology.impactPropagating) frontier.push(e.to);
  }
  const coverage = measuredCoverage(order);      // S8
  return { target, nodes: order, coverage, lower_bound: true };  // I-3: a lower bound
}
```
4. **State machine** none (pure over committed graph).
5–8. **Persistence/format/schema** `graphs/*.json`; impact materialized to `graphs/impact/<target>.json`; `coverage.schema.json` stamp attached.
9. **Interfaces** `impact(id): ImpactClosure` · `neighbors(id, type?)`.
10. **Contracts** Impact is always returned as a **lower bound** with coverage; never labeled "complete."
11. **Validation** closure references only existing nodes; coverage attached.
12. **Failure** missing edges → reflected as lower coverage, not silent omission.
13. **Recovery** recompute.
14. **Update** invalidate cached closures whose nodes changed.
15. **Integration** drives Planning (S9), Packaging (S10), and gates (S12). The `users.status` chain is one such closure (Part IV).

## S7 — Truth Engine (E15) — *epistemics + validation authority (I-5, I-6)*

1. **Responsibilities** Assign and transition the truth-class of every statement; enforce promotion authority; drive invalidation.
2. **Lifecycle (per fact)** `Observed → Documented → Validated → Published → (Challenged → Corrected) → Archived`.
3. **Internal workflow / Algorithm (promotion + invalidation)**:
```
promote(fact):
  if fact.class==DIRECT_OBSERVATION and confirmedByIndependentSources(fact)>=2: → VERIFIED_FACT
  if fact.derivedBy(rule) and allInputs(VERIFIED_FACT): → DERIVED_FACT
  if fact.fromAI: stay HYPOTHESIS/ASSUMPTION unless authority==HUMAN and ratified → VERIFIED/DECISION
  else if authority ceiling exceeded: raise E_AUTHORITY
invalidate(changedSource):
  for f in reverseClosure(changedSource): if f.invalidation_rule fires: f→CHALLENGED
```
4. **Algorithms** independent-source confirmation; reverse-closure walk; class lattice.
5. **State machine** the lifecycle above; `Challenged` blocks any execution gating on that fact.
6–8. **Persistence/format/schema** `truth/facts/*.json`, `truth/truth.ledger.json`; `truth.schema.json` (class, source_authority, evidence[], derivation, dependencies[], invalidation_rule, validated_by, lifecycle).
9. **Interfaces** `classify(stmt)` · `promote(id)` · `challenge(sourceRef)` · `gatingFacts(missionScope): TruthId[]`.
10. **Contracts** Only `{VERIFIED_FACT, ARCHITECTURAL_DECISION, BUSINESS_RULE, CONSTRAINT}` may gate execution. `ASSUMPTION`/`HYPOTHESIS` ride along as declared risks. Stratification: `source_authority=CODE` facts are revalidated against HEAD; `MODEL` facts trusted from the committed model.
11. **Validation** no `VERIFIED_FACT` without evidence; no promotion above ceiling (`E_AUTHORITY`); no fabrication — absent → `UNSUPPORTED`.
12. **Failure** ambiguous classification → lowest defensible class.
13. **Recovery** ledger is append-only; rebuild current classes by replay.
14. **Update** each session emits a truth-delta; only CHALLENGED facts in the mission closure are re-evaluated (bounded re-validation → the decay-economics answer).
15. **Integration** the spine of correctness; consulted by every gate.

## S8 — Coverage Engine (E14) — *measured completeness (I-3)*

1. **Responsibilities** Quantify how populated the model is per node-class and per impact closure; expose explicit blind spots.
2. **Internal workflow / Algorithm**:
```
coverage(class) = reconstructedNodes(class) / expectedNodes(class)   // expected from adapters' detect()
closureCoverage(order) = min over classes touched of coverage(class)
blindspots = classes where coverage < ontology.coverageTarget
```
3. **State machine** none.
6–8. **Persistence/format/schema** `model/model.coverage.json`.
9. **Interfaces** `coverage(): CoverageReport` · `meetsTargets(): boolean` · `blindspots(): Class[]`.
10. **Contracts** Coverage gates execution; a closure below target **must** trigger INVESTIGATION, never proceed silently.
11–13. **Validation/failure/recovery** deterministic recompute.
14. **Update** recompute on model delta.
15. **Integration** feeds G-COVERAGE (S12) and the lower-bound stamp on impact (S6).

## S9 — Planning Engine (E16)

1. **Responsibilities** Derive an immutable `PLAN` from the impact closure: order, gates, acceptance criteria, rollback.
2. **Lifecycle** `Drafted → Validated → Frozen`.
3. **Algorithm** implementation order = topological sort of the impact sub-graph (Kahn's algorithm over dependency edges); acceptance criteria emitted as **machine-verifiable predicates** (I-1).
4–8. **Persistence/format/schema** `plans/<mission>.plan.frozen.json`; `plan.schema.json`.
9. **Interfaces** `plan(mission): Plan` · `freeze(planId)`.
10. **Contracts** no plan without exit/acceptance criteria (RMM `PLAN`); order must be a valid topo-sort or `E_GATE`.
11–13. **Validation/failure/recovery** cycle in graph → `E_GATE` (report cycle); recompute deterministically.
14. **Update** plan changes create new versions; frozen plans immutable.
15. **Integration** input to Packaging (S10); gated by G-PLAN-VALID.

## S10 — Packaging Engine (E17)

1. **Responsibilities** Freeze the plan + closure + scope + snapshot into the sole execution context.
2. **Lifecycle** `Assembled → Validated → Frozen(@HEAD)`.
3. **Algorithm** bind `repository_snapshot = HEAD`, `commit_hash = HEAD`; compute `forbidden_scope = all − allowed_scope`; attach gating truth + risks.
4–8. **Persistence/format/schema** `packages/<mission>.package.frozen.json`; `package.schema.json`.
9. **Interfaces** `package(plan): Package` · `view(pkg): PackageView` (what the AI sees).
10. **Contracts** `allowed_scope ∩ forbidden_scope = ∅`; snapshot must equal HEAD at freeze.
11–13. **Validation/failure/recovery** stale HEAD at freeze → re-snapshot; immutable after freeze.
14. **Update** new mission → new package.
15. **Integration** consumed by Execution Bridge (S14) and G-FRESHNESS.

## S11 — Orchestrator / Pipeline — *the mandatory state machine (I-8)*

1. **Responsibilities** Run the non-skippable sequence; enforce gates; run the fixpoint; manage cold/warm; handle contradiction recovery.
2. **State machine (mission)**:
```
DECLARED → (MODE-DETECT) → [COLD_BOOTSTRAP | WARM_RESUME]
 → RECONSTRUCTING ⟲(fixpoint E00..E13 until stable) → COVERAGE → TRUTH
 → [G:RECONSTRUCTION-COMPLETE]
 → PLANNED → [G:PLAN-VALID] → FROZEN(model,plan)
 → PACKAGED → [G:PACKAGE-VALID]
 → EXECUTING → VERIFYING → [verify-fail+unmodeled → CONTRADICTION_RECOVERY → RECONSTRUCTING]
 → LEARNING → UPDATING → HANDOFF → CLOSED
illegal transition → E_GATE
```
3. **Algorithm (fixpoint)**:
```
do { delta = runEngines(E00..E13) } while (delta.nonEmpty && iters++ < MAX);
if iters>=MAX: emit E_NONCONVERGENCE; block freeze
```
4. **Persistence** `state/cursor.json` (current stage), `state/mission.json`.
5–8. **Storage/schema** `pipeline/pipeline.json` (declarative transitions), `runtime.schema.json`, `mission.schema.json`.
9. **Interfaces** `next(): RuntimeRequest` (drives the AI loop) · `advance(result)` · `status()`.
10. **Contracts** `EXECUTING` is unreachable before `FROZEN(package)` — execution is late by construction.
11. **Validation** each transition guarded by its gate (S12).
12. **Failure** any gate fail blocks; mission → `BLOCKED` with reason.
13. **Recovery** resume from `cursor.json`; idempotent stage re-run.
14. **Update** pipeline edges are config; adding a stage = config + gate, no rewrite.
15. **Integration** the conductor of all subsystems.

## S12 — Gate / Validation Subsystem

1. **Responsibilities** Pure predicate gates between stages (the list in the blueprint §17), each returning `{pass, evidence, blocking}`.
2–5. Stateless predicates; registry in `pipeline/gates.json`.
6–8. evidence persisted as `EVIDENCE` objects.
9. **Interfaces** `interface Gate { id; check(ctx): GateResult }`.
10. **Contracts** Only G-COVERAGE and truth-promotion are waivable, and only by HUMAN authority, recorded as a `DECISION`.
11–13. deterministic; failure → `E_GATE` + blocking finding.
14. new gates registered declaratively.
15. delegates entity/structural checks to S1 (Kernel VS-1..5).

## S13 — Mediation Subsystem (AI driver + sandbox)

1. **Responsibilities** Implement II.2: drive the AI, scope its reads, reject out-of-scope patches, discard temporary reasoning.
2. **Lifecycle (per turn)** `BUILD_REQUEST → SEND → RECEIVE → VALIDATE → PERSIST(typed only)`.
3. **Algorithm** scope check = path ∈ allowed globs ∧ path ∉ forbidden; patch apply = `git apply --check` then stage.
4–8. transient; nothing but typed artifacts persists.
9. **Interfaces** `drive(req): AIResponse` (transport-agnostic: stdio/HTTP to any vendor).
10. **Contracts** vendor-neutral; identical request → any vendor → response validated identically. The AI cannot escalate scope or skip a stage.
11–13. invalid response (bad scope/patch) → `E_SCOPE`, request reissued; repeated failure → `BLOCKED`.
14. new vendor = new transport adapter, no protocol change.
15. the boundary that makes "AI works through the Runtime" real.

## S14 — Execution Bridge + Escape Hatch (I-4)

1. **Responsibilities** Apply implementation strictly from the frozen package; detect contradictions with live code.
2. **Lifecycle** `LOAD(pkg) → FRESHNESS → STEP* → VERIFY`.
3. **Algorithm** before each step: `G-FRESHNESS` (HEAD == pkg.commit within closure) else `E_FRESHNESS`. If live code contradicts a package fact mid-step → emit `E_CONTRADICTION` → HALT → `CONTRADICTION_RECOVERY`.
4–8. patches + evidence persisted; `evidence/<mission>/`.
9. **Interfaces** `executeStep(pkg, step)` · `verify(pkg): VerifyResult`.
10. **Contracts** no read/write outside package closure; a wrong package is *haltable*, not silently authoritative.
11–13. verify-fail revealing un-modeled impact ⇒ invalidate model region (S7.challenge) ⇒ re-reconstruct that region.
14. learning feeds back as truth-delta.
15. closes the loop: execution validates the model.

## S15 — Handoff / Session Subsystem (II + I-2)

1. **Responsibilities** Emit machine-readable session output so any vendor resumes with zero conversation history.
2. **Lifecycle** `OPEN → … → EMIT(handoff) → CLOSE`.
3. **Algorithm** handoff = diff of committed state since session start (knowledge/truth/impact deltas) + pointers to frozen model.
4–8. `handoff/<session>.handoff.json`; `handoff.schema.json`.
9. **Interfaces** `open()` · `handoff(): Handoff` · `resumeFrom(handoff)`.
10. **Contracts** next session reads handoff + frozen model only; warm reconstruction is a deterministic re-read ⇒ identical state across vendors (the reading guarantee).
11–13. missing/old handoff → fall back to full warm resume from frozen model.
14. append to audit.
15. integration point for multi-vendor continuation (Claude→Kimi→Gemini→…).

---

# PART IV: END-TO-END EXECUTION TRACE (`mission: modify users.status`)

```
boot → S1 verify Kernel pin OK → mode=WARM (model.frozen exists)
S15 open session ← reads last handoff
S11 WARM_RESUME → S3 adapters re-parse dirty files → S5 engines re-run dirty only
S11 fixpoint until model.stable
S8 coverage = 0.94 ≥ targets → S7 truth: gating facts = {users.status enum (VERIFIED/CODE), status-policy (BUSINESS_RULE)}
S6 impact("node:Column/users.status") → closure order:
   Column→Entity→Repository→Service→DTO→Validation→OpenAPI→Client→FrontendState
   →Permission→Route→Sidebar→Toolbar→Dialog→Grid→Filter→Search→Report→Statistic→Export→Test→Doc→Evidence
   coverage(closure)=0.91 lower_bound=true ; blindspots={Report:0.8}
G-COVERAGE: Report below target → S11 INVESTIGATION (bounded) → adapters deepen Report parsing → coverage 0.95
G-RECONSTRUCTION-COMPLETE pass
S9 plan: topo-order steps, acceptance = {AC1: OpenAPI regenerated, AC2: 0 broken refs in closure, AC3: tests green}
G-PLAN-VALID pass → FREEZE model+plan
S10 package @HEAD, allowed_scope=closure files, forbidden=rest → G-PACKAGE-VALID pass → FREEZE
S13/S14 EXECUTING: AI gets PackageView only; patches confined to scope; G-FRESHNESS each step
S14 VERIFY: AC1..3 → if a 21st artifact breaks → E_CONTRADICTION → invalidate → re-reconstruct (I-4)
S14 evidence emitted → S7 LEARN truth-delta → S11 UPDATE runtime → S15 HANDOFF → CLOSED
```

Every arrow is a function call across S1–S15; nothing depends on conversation memory.

---

# PART V: MODULE MANIFEST & BUILD SEQUENCE (code starts here)

```
engineering-runtime/
  package.json tsconfig.json kernel.lock
  src/
    kernel/        S1   store/      S2   adapters/   S3
    ontology/      S4   engines/    S5(E01..E13)
    graph/         S6(+impact)      truth/       S7(E15)
    coverage/      S8   planning/   S9   packaging/ S10
    pipeline/      S11(orchestrator)  gates/     S12
    mediation/     S13  execution/  S14  session/   S15
    cli/  index.ts  det-harness/
  spec/schemas/*.schema.json   profiles/*.json
```

Build order (each step shippable + tested by `det-harness`):
1. **S2 Store + S1 Kernel Bridge + schemas** (the substrate).
2. **S3 Adapters (ts-nest, sql-ddl, openapi) + S5 deterministic engines E01/E02/E03/E11** (real nodes/edges from a real repo).
3. **S6 Graph + Impact + S8 Coverage** (the `users.status` closure runs).
4. **S7 Truth + S12 Gates + S11 Orchestrator (fixpoint, gates)** (reconstruction completes deterministically).
5. **S4 Ontology + profiles** (universality).
6. **S5 reasoning engines + S13 Mediation** (AI driven, scoped, HYPOTHESIS-only).
7. **S9 Plan + S10 Package + S14 Execution + escape hatch**.
8. **S15 Handoff + S11 contradiction recovery + multi-vendor transport**.
9. First real `<project>-runtime`: cold bootstrap → ratify → warm → run `users.status` end-to-end.

A subsystem is "done" only when `det-harness` proves byte-identical reconstruction across two runs (and, for S15, across two vendor transports).

---

# PART VI: REVISION HISTORY

| Version | Date | Author | Change | Reference |
|---------|------|--------|--------|-----------|
| 1.0.0 | 2026-06-28 | Engineering Kernel Architect | Complete OS-grade implementation specification: system-wide process/mediation/store/error/determinism model + 15 fully-specified executable subsystems (S1–S15), each with responsibilities, lifecycle, workflow, algorithms, state machine, persistence, storage, schemas, interfaces, contracts, validation, failure handling, recovery, update, integration; concrete impact/truth/fixpoint/coverage algorithms; end-to-end execution trace; module manifest + 9-step build sequence + conformance harness. Bakes in invariants I-1..I-8. Code/content to be built in the separate engineering-runtime repo (§9.5); no Kernel/RMM/Constitution modification | ENGINEERING RUNTIME CONSTRUCTION DIRECTIVE (Implementation Phase) |

---

*End of ENGINEERING_RUNTIME_IMPLEMENTATION_SPEC.md*
