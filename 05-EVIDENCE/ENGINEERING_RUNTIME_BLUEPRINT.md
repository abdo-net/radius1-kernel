# ENGINEERING_RUNTIME_BLUEPRINT.md

## ENGINEERING KERNEL — EVIDENCE DOCUMENT

---

# PART I: DOCUMENT META-STRUCTURE

## Section A: Identification

| Property | Value |
|----------|-------|
| Title | Operational Engineering Runtime — Evaluation & Blueprint |
| Short | ENGINEERING_RUNTIME_BLUEPRINT |
| Classification | DERIVED |
| Owner | Engineering Kernel Architect (mission output; no RMM entity claims ownership) |
| Source of Truth | `05-EVIDENCE/ENGINEERING_RUNTIME_BLUEPRINT.md` |
| Status | Active |
| Version | 1.0.0 |
| Mission | OPERATIONAL ENGINEERING RUNTIME — EVALUATION & BLUEPRINT |
| Baseline HEAD | `a3ea5f7772957356014491f6b76b237c8cdc5c47` |
| Consumes (prior determinations, accepted as repository facts) | `ENGINEERING_INTELLIGENCE_DETERMINATION.md` (knowledge graph), `ENGINEERING_REASONING_DETERMINATION.md` (reasoning/intent), `ENGINEERING_COGNITIVE_DETERMINATION.md` (mandatory pipeline), `ENGINEERING_SYSTEM_RECONSTRUCTION_DETERMINATION.md` (TOPOLOGY/reconstruction), `EIP_EXECUTION_LAYER_DETERMINATION.md` (consumer execution layer), `KERNEL_OPERATIONAL_CAPABILITY_REVIEW.md` (gap inventory) |

## Section B: Purpose

This document answers the mission's single explicit question: **can the proposed operational Engineering Runtime be implemented entirely on top of the existing Kernel without violating any constitutional boundary?** It evaluates first; because the evidence proves it can, it produces the complete **operational Runtime blueprint**. Unlike the six prior determinations — which each determined that the *Kernel-side grammar* for a capability already exists and that a *consumer engine* would execute it — this document specifies that consumer engine concretely, as a single coherent per-project Runtime. It creates no entity, no architectural layer, modifies no frozen/canonical/constitutional artifact, and implements nothing in this repository.

## Section C: Authority Note and Scope of Novelty

DERIVED; binding force identical to prior determinations. **Honest scope note (as in the reconstruction determination):** the *contents* of the Runtime — knowledge graph, topology, reasoning/intent, impact closure, mandatory pipeline, reference-isolation, cross-session/model determinism — were all already determined in the six prior documents and are integrated here by reference, not re-derived. This document's two genuinely new contributions are: **(1)** the *constitutional placement* finding — the Runtime is a Consumer artifact that **must live outside `radius1-kernel`**, which is the actual question asked; and **(2)** the **Engineering Truth** epistemic model, which the mission calls "the most important missing capability," grounded here in the frozen `FINDING` lifecycle. Everything else is the assembly of already-determined parts into one operational specification.

---

# PART II: EVALUATION

## 1. Executive Evaluation

**Yes — the Runtime can be implemented entirely on top of the existing Kernel without violating any constitutional boundary, provided it is built as a Consumer, in space the Kernel does not own.** The mission's own framing is already the constitutionally correct one and matches the repository's Consumer Model exactly:

- *"The Kernel defines the rules. The Runtime executes them."* — this is `KERNEL_SCOPE_DEFINITION.md` §8 (Consumer Model: voluntary adoption, version pinning, "Extensions must not modify Kernel artifacts") and §9.7 (Product-Specific Extensions: "Must reference base Kernel entity; stored in **product-controlled space**; must not claim to be part of Kernel").
- *"The Kernel remains global. Each project owns its own Runtime."* — this is precisely §9.5: **"Product content in Kernel directories is a violation."** The per-project `runtime/` therefore *cannot* live inside this repository; it lives in the product's own space (§3.1: "Products maintain their own repositories"). Placed there, it violates nothing — placed here, it would violate §9.5 on contact.

So the constitutional answer is not merely "yes, it is allowed"; it is "yes, **and the Consumer/Kernel split the mission proposes is the only constitutionally valid placement** — the Kernel was explicitly built to be consumed exactly this way." Nothing in the Constitution, the frozen RMM, or the Architecture Freeze obstructs a Runtime that *reads, references, and version-pins* the Kernel and *never modifies* it. The two prohibitions that matter (`§9.5` no product content in Kernel; `§8` extensions must not modify Kernel artifacts) are satisfied by construction the moment the Runtime is a separate, downstream artifact.

The three-way split is unchanged from every prior determination: **Kernel = the immutable rules/grammar (this repository); Runtime = the consumer engine + per-project memory that executes them; Governance = ratification for anything that must become *binding* on the Kernel.** No new architectural layer is created — the Runtime is downstream of the existing stack, not inserted into it.

## 2. The Mandatory Pipeline Is Already a Repository Fact

Every stage of the proposed pipeline maps to a primitive or prior determination; the Runtime *composes and enforces* them, it does not invent them.

| Pipeline stage (mission) | Existing construct / prior determination |
|---|---|
| Load Kernel · Bootstrap | `KERNEL_BOOT_PROTOCOL.md`; `AI_EXECUTION_PROTOCOL.md` EX-1 |
| Reconstruct Project · Build System Model · Build Topology | `TOPOLOGY` (Observed → Documented first) — `ENGINEERING_SYSTEM_RECONSTRUCTION_DETERMINATION.md` |
| Build Knowledge Graph · Build Semantic Relationships | `TRACEABILITY_LINK` typed edges — `ENGINEERING_INTELLIGENCE_DETERMINATION.md` |
| Build Reasoning Graph | Tier-10 `DECISION`/`FINDING`/`CONCLUSION` + intent primitives — `ENGINEERING_REASONING_DETERMINATION.md` |
| Build Impact Graph | forward `TRACEABILITY_LINK` closure ("precise impact analysis") |
| Verify Repository State | `KERNEL_VALIDATION_PROTOCOL.md` VS-1..VS-5; EX-3 |
| Generate · Validate · Freeze Plan | `PLAN` (Freezable; "may not omit exit criteria") + Freeze lock |
| Generate Blueprint · SDD · Tasks | `SPECIFICATION`/`DOCUMENT` artifacts; `TASK` (Tier with terminal Completed) |
| Implement | EX-4 OPERATE, single-slice isolation (`KERNEL_EXECUTION_RUNTIME_SPECIFICATION.md` §4) |
| Regression Verification · Evidence Generation | EX-5; `CERTIFICATION`; `EVIDENCE` (`05-EVIDENCE/` semantics) |
| Update Project Runtime · Close Session | `CHECKPOINT`/`SNAPSHOT` + commit; EX-7; `TASK` terminal |

The non-skippability the mission demands ("The AI should never decide to skip these steps. The Runtime should require them") is already a repository rule: `AI_EXECUTION_PROTOCOL.md` states verbatim **"A phase SHALL NOT be skipped,"** and `PROCESS`/`WORKFLOW` are by definition "a defined sequence... according to specified rules" that "may not have deadlock; may not lack ExitPoint." The Runtime's job is to *bind the AI to this sequence operationally* — the grammar that makes a sequence mandatory is already frozen.

## 3. Engineering Truth — the New Capability — Is Grounded in the Frozen `FINDING` Lifecycle

The mission names this the most important missing capability: distinguish **Observation / Verified Fact / Derived Fact / Hypothesis**, admit only Verified Facts to permanent memory, and **auto-invalidate** dependent knowledge when a source changes. The decisive finding is that the frozen RMM **already encodes this exact epistemic ladder** in the `FINDING` entity:

> `FINDING` Lifecycle: **Observed → Documented → Reviewed → Validated → Published → Challenged → Reaffirmed/Corrected → Archived**
> Forbidden: "may not be published without Review; **may not contradict its own Evidence**." · Owner: Process · **AI Creatable: Yes** · SoT: Evidence Vault.

| Engineering-Truth tier (mission) | Existing RMM grounding |
|---|---|
| **Observation** | `FINDING` in state *Observed* / *Documented* (not yet validated) |
| **Hypothesis** | `FINDING` *Observed* awaiting Review — provisional, not admissible to permanent knowledge |
| **Verified Fact** | `FINDING` advanced to *Validated* / *Published* — "may not be published without Review" is the verification gate |
| **Derived Fact** | `CONCLUSION` — "synthesize Findings, Evidence, and reasoning into a final judgment"; "may not contradict referenced Evidence" |
| **Source / Evidence / Verification** | `EVIDENCE` (Tier 11): "factual support... through verifiable data, observation, or documentation"; `FINDING` "References Evidence" |
| **Invalidation when source changes** | `FINDING` *Challenged → Corrected* transition + "may not contradict its own Evidence"; reverse `TRACEABILITY_LINK` traversal locates every dependent `FINDING`/`CONCLUSION` |
| **Commit / Timestamp** | repository commit + `SNAPSHOT`/`RECORD` ("a fact... at a specific point in time as an immutable account") |

So "only Verified Facts may enter permanent Runtime knowledge" becomes a precise, evidence-backed rule: **only `FINDING`s in `Validated`/`Published` state are written to permanent project memory; `Observed`/`Documented` findings remain provisional.** Automatic invalidation is the *Challenged → Corrected* lifecycle driven by the reverse closure of the typed edge graph: when a source node's commit changes, every `FINDING` reachable by a `derived-from` / `verified-by` edge is moved to *Challenged* until re-validated. `[EVIDENCE BOUNDARY]`: a numeric **Confidence** field is *not* a first-class RMM attribute — the four discrete lifecycle states carry verification status, and `ASSESSMENT`/`METRIC` (Tier 14/15) can quantify where a consumer needs a scalar; a continuous confidence score is therefore a **consumer-side annotation**, not a Kernel guarantee.

## 4. Why This Is a Runtime and Not Another Specification

The mission's insistence that "the primary output of every engineering session should NOT be code... it should be Updated Project Runtime" is the operational restatement of **repository-as-memory** (`SKILL_MANIFEST_SPECIFICATION.md` SM-LP: the repository, not the conversation, is the memory). The Kernel already establishes that persisted artifacts are the memory and conversations are disposable; the Runtime simply relocates *that same principle* into per-project consumer space so each product accumulates its own persisted `TOPOLOGY`, typed graph, validated `FINDING`s, and frozen `PLAN`s. Code is then a *consequence* of the committed Runtime state, exactly as the mission requires — and exactly as `KERNEL_BOOT_PROTOCOL.md` already treats the Kernel's own state.

---

# PART III: OPERATIONAL RUNTIME BLUEPRINT

(Produced because §1–§4 prove the capability exists within the current architecture. Parts already derived in prior determinations are integrated by reference, not repeated.)

## A. Placement and Structure (the constitutional core)

The Runtime is a **Consumer artifact in product-controlled space**, version-pinned to a Kernel release (§8). It must not reside in `radius1-kernel` (§9.5). A conformant layout:

```
radius1-kernel/                      ← THIS repo, immutable, version-pinned by consumers
  00-CONSTITUTION / 01-META-MODEL / … (unchanged)

radius1/                             ← product repo (Consumer space, §3.1/§9.5/§9.7)
  runtime/
    kernel.lock        # pinned Kernel version + commit (the §8 version pin)
    state/             # current mission, session state  (RMM: SESSION/CONTEXT, 99-STATE semantics)
    topology/          # reconstructed system graph       (RMM: TOPOLOGY, Observed→Documented)
    knowledge/         # nodes + typed edges               (RMM: TRACEABILITY_LINK)
    reasoning/         # decisions, findings, conclusions  (RMM: Tier 10)
    truth/             # validated FINDINGs + invalidation ledger (RMM: FINDING/EVIDENCE)
    evidence/          # generated EVIDENCE/CERTIFICATION
    plans/             # frozen PLANs
    missions/          # mission records
```

Every directory above maps to an RMM entity used as a §9.7 product extension ("Must reference base Kernel entity; stored in product-controlled space; must not claim to be part of Kernel"). The Runtime **reads** the Kernel and **never writes** to it — satisfying §8's "Extensions must not modify Kernel artifacts" by construction.

## B. The Mandatory Engineering Pipeline (Runtime-enforced)

The Runtime executes the §2 stage table as a single non-skippable `PROCESS`/`WORKFLOW` in front of `AI_EXECUTION_PROTOCOL.md` EX-1..EX-7, halting on any `KERNEL_VALIDATION_PROTOCOL.md` violation (EX-SC stop conditions). Until a *binding* version of this pipeline is ratified (governance-gated; see Part IV), the Runtime enforces it as a Consumer process layered on the already-mandatory EX-1..EX-7 spine.

## C. Knowledge Reconstruction (session start)

On every session start the Runtime rebuilds — from `runtime/`, never from prior conversation — the current mission, state, knowledge graph, `TOPOLOGY`, reasoning graph, impact graph, open `DECISION`s, pending `TASK`s, `CONTRACT`s, and `EVIDENCE`. Reconstruction is a *fixed-order, complete, no-fabrication* read (`KERNEL_DOCUMENT_REGISTRY.md` §7; KI-IX-04; KI-LK-06), so every session/model rebuilds the identical state. Implementation may begin **only after reconstruction succeeds** — the Runtime gate the mission specifies.

## D. Knowledge Graph, Topology, Reasoning, Impact

Integrated by reference: nodes = RMM entities + §9.7 product extensions; edges = typed `TRACEABILITY_LINK` ("may not be semantically empty"); the long `Users → … → Evidence` surface is the typed graph of `ENGINEERING_INTELLIGENCE_DETERMINATION.md` §10; "know the complete affected engineering surface before implementation" is the forward edge-closure of `ENGINEERING_REASONING_DETERMINATION.md` §6; intent ("why does it exist / which decision / which invariant / which regression") is the Tier-10 + `INVARIANT`/`RULE`/`CONTRACT` traversal of the reasoning determination; the reconstructed-system-first model is `TOPOLOGY` (`ENGINEERING_SYSTEM_RECONSTRUCTION_DETERMINATION.md`).

## E. Engineering Truth Model (the new operational module)

The `runtime/truth/` store holds only `FINDING`s in `Validated`/`Published` state, each carrying: **Source** (origin node), **Evidence** (`EVIDENCE` ref), **Verification** (the Review that advanced it past *Documented*), **Dependencies** (`derived-from`/`verified-by` `TRACEABILITY_LINK`s), **Invalidation Rules** (the source-commit condition under which it returns to *Challenged*), **Commit + Timestamp** (`SNAPSHOT`/`RECORD`). On any source-node change, the Runtime walks the reverse edge closure and moves every dependent `FINDING`/`CONCLUSION` to *Challenged* — automatic invalidation, grounded in the `FINDING` lifecycle and "may not contradict its own Evidence." `[EVIDENCE BOUNDARY]`: a scalar Confidence is a consumer annotation; the Kernel guarantees the *state machine and the non-contradiction rule*, not a probability.

## F. Reference Understanding (anti-copy)

Integrated by reference: `KERNEL_SCOPE_DEFINITION.md` §9.3 Technology Bridge Pattern ("the implementation technology SHALL provide X," never "Technology T provides X") + `04-PATTERNS/` (patterns + anti-patterns) + `PRECEDENT`. The Runtime admits a reference (SAS4, ERP, CRM, POS…) only as an abstract pattern node — *read → understand behaviour → extract pattern/constraints → compare → adapt → implement* — never as copied code/schema/API (§9.5). This is the standing reference-isolation discipline (`KERNEL_OPERATIONAL_CAPABILITY_REVIEW.md` Area 9).

## G. Runtime Update Protocol (primary output)

Session close commits the updated `runtime/` (new/advanced `FINDING`s, extended `TOPOLOGY` toward *Evolving*, new typed edges, `EVIDENCE`, frozen `PLAN`, `CHECKPOINT`/`SNAPSHOT`, `AUDIT_TRAIL`). The commit — not the code — is the deliverable; code is the consequence. This is repository-as-memory applied in consumer space.

## H. Determinism Across Sessions, Models, Projects

Identical persisted `runtime/` state + identical RMM grammar + fixed read-order + completeness (KI-IX-04) + no-fabrication (KI-LK-06) ⇒ every AI reconstructs the same engineering state and behaves like the same senior architect, without conversation history. `[EVIDENCE BOUNDARY]`: identity holds over the *committed* Runtime; **completeness and correctness of the product graph are a consumer data-quality property** — the Kernel guarantees the reconstruction discipline and reproducibility, not omniscience over a graph it does not host, and does not *perform* the Runtime's work.

---

# PART IV: WHAT CAN ADVANCE NOW vs. WHAT IS GATED; BOUNDARIES

**Unblocked now (no ratification):** this DERIVED evaluation/blueprint; the entire `runtime/` *as a Consumer artifact in product space* (§8/§9.7) — its `TOPOLOGY`, `ASSEMBLY`, `FINDING`, and `TRACEABILITY_LINK` instances are all **AI Creatable: Yes**; the reconstruction engine and pipeline enforcer as consumer software; `kernel.lock` version pin.

**Gated by `GAP-001`/`GOVERNANCE_WAIT`:** the pipeline as a *binding* Kernel-side `PROCESS`/`WORKFLOW` (AI Creatable: No); binding `PLAN`/`DECISION`/`DECISION_RECORD`/`CONCLUSION` (Approval); `PRECEDENT` (AI Creatable: No); any NORMATIVE Runtime specification promoted into the Kernel; `EVENT`/`TRANSACTION` as Kernel entities. None blocks the Consumer Runtime; each has an unblocked consumer or DERIVED form.

**Boundaries (reaffirmed, not newly created):** rollback strategy is ungrounded (rollback structurally absent, `PHASE_3_EXECUTION_CONTROL_ARCHITECTURE.md` §10 — strongest standing boundary); a scalar Confidence value is a consumer annotation, not an RMM field; the Kernel cannot *perform* reconstruction nor guarantee completeness of a graph it does not host; deployment/migration are out of Kernel scope (§3.3); `EVENT` remains referenced-but-undefined. **And the decisive placement boundary: the Runtime may not live inside `radius1-kernel` (§9.5) — it is constitutionally valid only in product-controlled space.**

---

# PART V: Final Evaluation

**The proposed operational Engineering Runtime can be implemented entirely on top of the existing Kernel without violating any constitutional boundary — and the Consumer/Kernel split the mission proposes is the only constitutionally valid placement, because the Kernel was explicitly built (`KERNEL_SCOPE_DEFINITION.md` §8/§9.5/§9.7) to be consumed exactly this way.** The Runtime is a downstream, version-pinned Consumer artifact in each product's own space; it reads and references the Kernel and never modifies it, so it adds no architectural layer and touches no frozen or constitutional artifact. Its mandatory pipeline is the already-non-skippable `AI_EXECUTION_PROTOCOL.md` EX-1..EX-7 plus `PROCESS`/`WORKFLOW` grammar; its knowledge graph, topology, reasoning, and impact closure are the six prior determinations made operational; and its one genuinely new module — **Engineering Truth** — is grounded directly in the frozen `FINDING` lifecycle (*Observed → Validated → Published → Challenged → Corrected*), which already encodes Observation→Verified-Fact promotion and source-driven invalidation, with `CONCLUSION` as Derived Fact and `EVIDENCE` as the verifiable source. The primary output of a session is the committed Runtime, not code; determinism across sessions, models, and projects follows from identical persisted state under an identical grammar. Within the two honestly-marked bounds — the Kernel cannot perform the Runtime's work, and cannot guarantee the completeness of a graph it does not host — this makes any compliant AI behave like the same experienced software architect, exactly as the mission requires, with **no Constitution change, no RMM amendment, no new layer, and nothing written into the Kernel repository.**

---

# PART VI: REVISION HISTORY

| Version | Date | Author | Change | Reference |
|---------|------|--------|--------|-----------|
| 1.0.0 | 2026-06-28 | Engineering Kernel Architect | Operational Runtime evaluation + blueprint; established that the Runtime is constitutionally valid only as a version-pinned Consumer in product space (§8/§9.5/§9.7) and must not live in the Kernel repo; grounded the new "Engineering Truth" model in the frozen FINDING lifecycle (Observed→Validated→Published→Challenged→Corrected) with CONCLUSION as Derived Fact and EVIDENCE as source; mapped the full mandatory pipeline and per-project runtime/ structure to existing primitives + the six prior determinations; marked rollback, scalar-confidence, graph-completeness, and Kernel-placement as boundaries; no Kernel/Constitution/RMM modification | OPERATIONAL ENGINEERING RUNTIME — EVALUATION & BLUEPRINT |

---

*End of ENGINEERING_RUNTIME_BLUEPRINT.md*
