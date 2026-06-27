# KERNEL_EXECUTION_RUNTIME_SPECIFICATION.md

## ENGINEERING KERNEL — EVIDENCE DOCUMENT

---

# PART I: DOCUMENT META-STRUCTURE

## Section A: Identification

| Property | Value |
|----------|-------|
| Title | Kernel Execution Runtime — Behavioral Specification (K-ERL) |
| Short | KERNEL_EXECUTION_RUNTIME_SPECIFICATION |
| Classification | DERIVED |
| Owner | Engineering Kernel Architect (mission output; no RMM entity claims ownership) |
| Source of Truth | `05-EVIDENCE/KERNEL_EXECUTION_RUNTIME_SPECIFICATION.md` |
| Status | Active |
| Version | 1.0.0 |
| Mission | PHASE 3 — KERNEL EXECUTION RUNTIME DIRECTIVE (K-ERD) |
| Baseline HEAD | `d2ce20d5c32f90289c656d13cce06233a4166511` |
| Frozen inputs (composed, never modified) | `KERNEL_RUNTIME_ARCHITECTURE.md`; `PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md`; `PHASE_3_EXECUTION_ARCHITECTURE.md`; `KERNEL_CONTROL_FLOW_ARCHITECTURE.md` (all under `ARCHITECTURE_FREEZE.md`) |
| Operational inputs (referenced) | `AI_EXECUTION_PROTOCOL.md`; `KERNEL_BOOT_PROTOCOL.md`; `KERNEL_VALIDATION_PROTOCOL.md`; `SKILL_MANIFEST_SPECIFICATION.md`; `99-STATE/README.md` |

## Section B: Purpose

This document specifies the **runtime behavior** requested by the Kernel Execution Runtime Directive (K-ERD): deterministic execution-state persistence, execution packaging, slice isolation, session resume, and conceptual enforcement checkpoints. It expresses these strictly as *behavior over the existing, already-frozen Kernel* — composing existing RMM entities, the frozen architecture stack, and the operational layer. It is the seven-fold output the directive requested (Runtime Model, Execution State Model, Execution Package Definition, Slice Isolation Model, Session Resume Protocol, Enforcement Checkpoints, Integration Map) plus runtime-only gaps.

## Section C: Authority Note and the One Determination That Governs This Document

**K-ERL is not, and is here expressly not presented as, a new architectural layer.** The directive states both "define ONLY: Kernel Execution Runtime Layer" and "Do NOT create new layers." Repository evidence resolves the tension cleanly: a runtime layer **already exists and is frozen** — `KERNEL_RUNTIME_ARCHITECTURE.md` occupies the "Kernel Runtime" position of the frozen stack (`ARCHITECTURE_FREEZE.md` §3: Repository → Boundary → **Kernel Runtime** → Execution Control → Mission Execution → Implementation[out of scope]). The directive's own target stack — "Architecture Layer → Execution Layer → AI Runtime" — maps onto that existing frozen stack, with "AI Runtime" being the Actor executing `AI_EXECUTION_PROTOCOL.md` EX-1..EX-7 *inside* the already-architected `CONTEXT`. This document therefore adds **no layer**; it specifies the operational *behavior* of layers that already exist.

Consequently this is a **DERIVED** specification. It has no authority to bind, to amend the frozen architecture, to create an RMM entity, or to issue a NORMATIVE runtime contract (which would require GovernanceBody Approval, currently within the `GAP-001`/`GOVERNANCE_WAIT` block). Its force is that of every prior closure/specification record in this engagement, revisable only by GovernanceBody.

---

# PART II: RUNTIME SPECIFICATION

## 0. Scope Discipline (what this document does and does not do)

| Does | Does not |
|---|---|
| Compose existing frozen architecture + RMM entities + operational layer into runtime behavior | Create a new architectural layer, entity, governance model, or methodology |
| Express state as a *runtime representation* of existing constructs | Modify RMM, Constitution, or any frozen/canonical artifact |
| Identify enforcement checkpoints conceptually | Design tools, write code, or specify an executable runtime |
| Mark runtime-only `[EVIDENCE BOUNDARY]` gaps | Invent mechanics where the repository is silent |

The executable runtime that would *perform* this behavior (a real state-persistence engine, a runtime boundary enforcer) is Product Implementation — permanently out of Kernel scope (`KERNEL_SCOPE_DEFINITION.md` §3.1, §3.3) — and belongs to a Kernel-consuming operational layer outside this repository (`EIP_EXECUTION_LAYER_DETERMINATION.md`). This document specifies *what the runtime must do*, expressed over the Kernel; it does not and cannot host the doer.

## 1. Runtime Model

The runtime is exactly the frozen Kernel Runtime Architecture, read operationally:

- An `ENVIRONMENT` (Tier 9, Owner: Module) **hosts** a `SESSION` (`KERNEL_RUNTIME_ARCHITECTURE.md` §1, §4; `ENVIRONMENT` Allowed: "hosts Session").
- A `SESSION` (Tier 8, Owner: GovernanceBody; Lifecycle Initiated→Active→Suspended→Completing→Completed→Archived|Terminated) **holds** a `CONTEXT` (Tier 9, Owner: Session).
- A `PARTICIPANT` (Tier 8) **binds** an `ACTOR`↔`SESSION` with role assignment (the AI worker is the Actor; `AI_EXECUTION_PROTOCOL.md` EX-2 AUTHORIZE performs this bind).
- The **"AI Runtime"** of the directive = the Actor executing EX-1..EX-7 *within* that `CONTEXT`. The runtime hosts; it does not itself execute (`KERNEL_RUNTIME_ARCHITECTURE.md` §1: "the substrate the EX-1..EX-7 phases execute within — it does not execute anything itself").

No element above is new; all are frozen RMM Tier 8/9/20 entities instantiated at `99-STATE/`.

## 2. Execution State Model

The directive's required state items map one-to-one onto existing constructs; the runtime representation is their persisted instance set in `99-STATE/` (Owner: Session — the directory canonically designated for "runtime state, session management, and operational context").

| Directive state item | Existing construct (runtime representation) |
|---|---|
| Session state persistence | `SESSION` lifecycle value + `CONTEXT` (Created→Active→Modified→Saved→Discarded, `99-STATE/README.md`) |
| Active mission tracking | `TASK` in In-Progress state (Owner: Session; SoT `99-STATE/`; Lifecycle Created→Assigned→Ready→In-Progress→…→Completed) bound to the active Mission Registry entry (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §2) |
| Active slice pointer | A reference to the current `SLICE` instance (RMM `SLICE`, SoT `01-META-MODEL/Slice/`) being executed |
| Last validated commit reference | The most recent `CHECKPOINT` in **Committed** state (`KERNEL_RUNTIME_ARCHITECTURE.md` §6; `CHECKPOINT` Forbidden: "may not be modified after Commit") |
| Checkpoint recovery state | `CHECKPOINT` lifecycle position (Defined→Triggered→Capturing→Validated→Verified→Committed→Referenced→Superseded) + `SNAPSHOT` (Owner: Kernel) |
| Execution history | `AUDIT_TRAIL` / Execution Ledger (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §7; AUDIT_TRAIL Forbidden: "may not be modified after Seal") |

**Critical, and the most actionable element of this entire specification:** persisting these as `99-STATE/` instances is **Session-owned, AI-Creatable runtime activity — not an amendment** — so it can be done *now*, under the existing canonical `99-STATE` definition, without GovernanceBody ratification. Per `99-STATE/README.md` ("persistent truths belong in their canonical source-of-truth locations"), this state record must be a **resume index that references canonical truths, not a duplication of them**.

`[EVIDENCE BOUNDARY]`: no such `99-STATE/` instance currently exists (the directory holds only its README); this specification defines the representation, it does not assert the instance is present.

## 3. Execution Package Definition

The "execution package" the AI receives is a **Session-scoped `VIEW`** (RMM `VIEW`, Tier 20: "a perspective-specific representation of kernel structure"; Forbidden: "may not modify the entities it represents") assembled per-mission from existing sources. It is a read-only projection, not a new artifact class:

| Package field | Source construct |
|---|---|
| Mission scope | `AI_EXECUTION_PROTOCOL.md` EX-2 AUTHORIZE (mission + authority binding) |
| Allowed files | EX-AO-01..05 (allowed operations) resolved through `KNOWLEDGE_INDEX_SPECIFICATION.md` §2 lookup |
| Forbidden files | EX-FO-01..06 (forbidden operations), incl. EX-FO-04 (architectural ops forbidden to execution) |
| Contracts | `CONTRACT` entity (SoT `06-CONTRACTS/`; "may not span Kernel boundary") |
| Validation rules | `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5 |
| Evidence requirements | `EVIDENCE`/`RECORD`/`AUDIT_TRAIL` entities; `SKILL_MANIFEST_SPECIFICATION.md` §3 outputs |
| Definition of Done | `[EVIDENCE BOUNDARY]` — **not defined in the repository** ("Definition of Done": 0 files). The nearest grounded equivalent is the conjunction of `TASK` terminal state **Completed** + EX-7 COMPLETE + all VS-1..VS-5 PASS + required `EVIDENCE` present. A first-class DoD concept would be a new definition → Approval/amendment-gated. |

The package is *compiled* (assembled) by the runtime and *executed* rather than re-interpreted — directly attacking interpretation drift. Compilation is a runtime/consumer behavior; the VIEW projection and its field sources are Kernel-side.

## 4. Slice Isolation Model

Single-slice, bounded, isolated execution is already expressible from existing constructs:

- **Single-slice only:** The Execution Controller processes one Ready `TASK`/Mission at a time; `PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §4 selects "the next Mission whose TASK state is Ready," and §15's Deterministic Execution Algorithm is strictly serial. The `SLICE` entity is the unit ("Crosses Layer; spans Module, Component; delivers Capability, Feature").
- **Bounded scope:** EX-FO-01..06 forbid operations outside the authorized scope; the execution package's allowed/forbidden file sets (§3) bound the slice.
- **No cross-module leakage:** `BOUNDARY` (Tier 3, AI Creatable/Modifiable: No) "may not be crossed without an explicit crossing mechanism"; `CONTRACT` "may not span Kernel boundary."
- **Strict dependency isolation:** `KERNEL_DEPENDENCY_MODEL.md` (CAC / no-cycle) + Dependency Resolver (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §5).
- **Locking:** The only literal lock the repository defines is the **Freeze lock** (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §8; `KERNEL_STRUCTURE_SPEC.md` §6.1/§6.4). `[EVIDENCE BOUNDARY]`: no per-slice mutual-exclusion lock beyond the Freeze lock and the serial single-Ready-Task selection rule is defined; runtime mutual exclusion at finer grain is a consumer-side enforcement behavior.

No new entity is defined; isolation is the conjunction of `SLICE` + `BOUNDARY` + EX-FO + Dependency Resolver, enforced conceptually here and mechanically only by a consumer (§6, §7).

## 5. Session Resume Protocol

Deterministic resume from artifacts alone, with no conversational memory:

1. **Reconstruct state — boot:** `KERNEL_BOOT_PROTOCOL.md` mandatory load (FIRST CONSTITUTION → SECOND RMM → THIRD KERNEL_SCOPE_DEFINITION, or HALT) re-executed every session (`AI_EXECUTION_PROTOCOL.md` EX-1 BOOT). The full repository re-read *is* the persistence mechanism — the repository, not the conversation, is the memory (`SKILL_MANIFEST_SPECIFICATION.md` SM-LP).
2. **Read last execution checkpoint:** Resolve the most recent `CHECKPOINT` in **Committed** state and the `99-STATE/` resume index (§2); determine current `SESSION`/`TASK`/`SLICE` position via the Repository State Machine (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §14).
3. **Resume without conversation memory:** Re-enter EX-1..EX-7 at the phase implied by the recovered `TASK` state; no chat history is consulted or required.
4. **Validate consistency:** Run `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5 against the recovered state before resuming OPERATE (EX-4); any failure → EX-SC-07 HALT.

`[EVIDENCE BOUNDARY]` (runtime-only, pre-certified): **stale-state detection and the safe-resume trigger are undefined.** `KERNEL_RUNTIME_ARCHITECTURE.md` §11 records that `ENVIRONMENT.Degraded→Restored` is the sole recovery transition and specifies *no triggering procedure*; `PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §10 records that restart/resume/retry/**rollback** are not named mechanisms anywhere and that all lifecycles are forward-only. These are inherited, already-certified gaps (`KERNEL_CONTROL_FLOW_ARCHITECTURE.md` §11; `ARCHITECTURE_FREEZE.md` §6) — carried forward, not resolved here.

## 6. Enforcement Checkpoints (conceptual only — no tools, no code)

The enforcement points the directive asks for already exist as deterministic halt/validation points; this section *identifies* them, designing nothing:

| Enforcement need | Existing checkpoint (conceptual) |
|---|---|
| Validation must be enforced | EX-3 PRE-VALIDATE and EX-5 POST-VALIDATE; EX-VP-01..04 validation points; `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5 (PASS iff all stages pass; else FAIL/`[UNSUPPORTED]` — never silent pass) |
| Boundaries must be checked | `BOUNDARY` explicit-crossing-mechanism rule; EX-FO-04 (no architectural ops); the package's allowed/forbidden file sets (§3) |
| Evidence must be verified | EX-5 + `CERTIFICATION` entity; required `EVIDENCE` presence as completion precondition |
| Contract compliance must be validated | `CONTRACT` validation against its preconditions/postconditions/invariants (RMM CONTRACT #2/#3) |
| Halt on violation | `AI_EXECUTION_PROTOCOL.md` EX-SC-01..08 — every violation is a deterministic HALT, no further phase, best-effort EX-6 record (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §9, §11) |

All enforcement here is **conceptual identification**. *Mechanical* enforcement (a tool that runs these checks) is implementation → consumer-side (`KERNEL_OPERATIONAL_CAPABILITY_REVIEW.md` Areas 6, 10) — explicitly outside this document per the directive's §5.5 ("Do NOT design tools").

## 7. Integration Map (non-invasive)

Every K-ERL behavior is read/host/bind/consume against an existing artifact; none modifies one.

| K-ERL behavior | Governing existing artifact | Relationship |
|---|---|---|
| Runtime Model (§1) | `KERNEL_RUNTIME_ARCHITECTURE.md` (frozen) | Reads / composes — no modification |
| Execution State (§2) | `99-STATE/` + `CHECKPOINT`/`SNAPSHOT`/`TASK`/`AUDIT_TRAIL` | Instantiates Session-owned state — additive, not a definition change |
| Execution Package (§3) | `AI_EXECUTION_PROTOCOL.md` + `CONTRACT` + `KERNEL_VALIDATION_PROTOCOL.md` via a `VIEW` | Projects (VIEW "may not modify") |
| Slice Isolation (§4) | `SLICE` + `BOUNDARY` + Dependency Resolver + Freeze lock | Consumes rules — no modification |
| Session Resume (§5) | `KERNEL_BOOT_PROTOCOL.md` + Repository State Machine | Re-executes existing protocol |
| Enforcement (§6) | EX-VP / EX-SC / VS-1..VS-5 / CERTIFICATION | Identifies existing checkpoints |

Non-invasiveness is structural, not asserted: the runtime entities are owned by GovernanceBody/Session/Module and the dependency runs one way (`KERNEL` "may not depend on any external entity"; `KERNEL_RUNTIME_ARCHITECTURE.md` §10) — runtime behavior depends on the Kernel, never the reverse.

## 8. Runtime-Only Gaps (not architectural)

Strictly runtime-representation gaps, each already evidenced; none is an architectural gap and none is resolved here:

1. **Persisted `99-STATE/` instances do not yet exist** — the home is canonical and the representation is defined (§2), but no instance is committed. *Actionable now, no ratification* (Session-owned, AI-Creatable).
2. **Definition of Done is undefined** (§3) — 0 repository presence; runtime currently substitutes `TASK.Completed` + EX-7 + VS-pass + evidence-present. A first-class DoD is Approval/amendment-gated.
3. **Stale-state detection / safe-resume trigger undefined** (§5) — inherited from `KERNEL_RUNTIME_ARCHITECTURE.md` §11 / `PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §10; pre-certified standing gap.
4. **Rollback structurally absent** — all lifecycles forward-only (`PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §10, strong `[EVIDENCE BOUNDARY]`); "checkpoint recovery" means resume-from-last-Committed-Checkpoint, **not** state reversal.
5. **"Event" entity referenced but undefined** — `SESSION` Forbidden "may not mutate state without emitting Event," yet no `EVENT` entity exists in the 79-entity catalog (`KERNEL_RUNTIME_ARCHITECTURE.md` §3). Runtime state-mutation auditing currently relies on `AUDIT_TRAIL` in its place.

Resolving items 2–5 durably would require GovernanceBody ratification (new entity / NORMATIVE definition) and is therefore within the standing `GAP-001`/`GOVERNANCE_WAIT` block. Item 1 is not blocked.

## 9. Final Determination

The Kernel Execution Runtime Layer requested by K-ERD **already exists as frozen architecture**; what was missing was its **behavioral specification**, which this DERIVED document now provides — composed entirely from existing frozen layers, RMM entities, and the operational layer, introducing no new layer, entity, governance model, or methodology. The directive's six runtime capabilities all map onto existing constructs (Sections 1–6); the integration is structurally non-invasive (Section 7); the residual gaps are runtime-representation gaps, not architectural ones (Section 8).

**Single most actionable next step, unblocked by governance:** materialize the Execution State Model (§2) as a Session-owned `99-STATE/` resume index referencing canonical truths — the concrete artifact that turns "architecturally correct" into "deterministically resumable," achievable now without ratification. Everything requiring a new binding definition (Definition of Done, an Event entity, a NORMATIVE runtime contract, rollback/staleness mechanics) remains correctly behind the `GAP-001`/`GOVERNANCE_WAIT` boundary, and the executable runtime that performs this behavior remains correctly outside the Kernel in consumer space.

---

# PART III: REVISION HISTORY

| Version | Date | Author | Change | Reference |
|---------|------|--------|--------|-----------|
| 1.0.0 | 2026-06-27 | Engineering Kernel Architect | Initial behavioral specification of the Kernel Execution Runtime (K-ERL) over the already-frozen runtime/execution-control architecture; runtime model, state model, execution package, slice isolation, resume protocol, enforcement checkpoints, integration map, and runtime-only gaps — all composed from existing constructs; no new layer/entity/architecture | PHASE 3 — KERNEL EXECUTION RUNTIME DIRECTIVE (K-ERD) |

---

*End of KERNEL_EXECUTION_RUNTIME_SPECIFICATION.md*
