<!--
  ============================================
  AI_EXECUTION_PROTOCOL.md — Engineering Kernel (Operational Layer)
  Phase 1.5 — MISSION-024
  Governed by DOCUMENT_STANDARD_SPEC.md. Operationalizes execution under the
  frozen Kernel. Permissions derive from RMM Matrix 7 and KERNEL_AUTHORITY_MODEL;
  forbidden outcomes from KERNEL_SCOPE_DEFINITION §13. Execution only — no other
  workflows, no implementation, no code.
  ============================================
-->

# AI EXECUTION PROTOCOL

## A. Header

| Property | Value |
|---|---|
| **Title** | AI Execution Protocol |
| **Short Title** | AI_EXECUTION_PROTOCOL |
| **Entity Type** | PROCESS |
| **Classification** | PROCEDURAL |
| **Owner** | GovernanceBody (per RMM PROCESS #4 = Governance) |
| **Source of Truth** | `07-WORKFLOW/AI_EXECUTION_PROTOCOL.md` |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Date** | 2026-06-26 |
| **Authority** | MISSION-024 |

## B. Metadata
```metadata
Entity Type: PROCESS
Entity Purpose: To define the execution lifecycle, allowed and forbidden
                operations, validation points, and stop conditions for an AI
                operating under the Kernel.
Entity Owner: GovernanceBody
Lifecycle: Defined → Documented → Approved → Operational → Under-Review → Updated → Retired
Cardinality: N
Stability: Slow
Versionable: Yes
Freezable: Yes
AI Creatable: No
AI Modifiable: With Approval
Human Modifiable: Yes
Source of Truth: 07-WORKFLOW/
```

## C. Classification
PROCEDURAL (DOCUMENT_STANDARD_SPEC §3.3).

## D. Status
Active. Lifecycle state: Operational (RMM PROCESS #5).

## E. Version
1.0.0.

## F. Authority
MISSION-024 → GovernanceBody → Charter → Constitution. All permissions herein are extracted from RMM Matrix 7 and KERNEL_AUTHORITY_MODEL; none are invented. SHALL NOT contradict the Constitution.

## G. Dependencies
### G.1 Allowed Dependencies (Normative)
| Reference | Type | Required |
|---|---|---|
| `01-META-MODEL/RMM_v1.1.md` (Matrix 7 Permissions; Matrix 5 Freeze) | Normative | Yes |
| `01-META-MODEL/KERNEL_AUTHORITY_MODEL.md` (§13 V-rules) | Normative | Yes |
| `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` (§3, §10, §13, §14) | Normative | Yes |
| `01-META-MODEL/Repository_State_Model.md` (states, transitions) | Normative | Yes |
| `07-WORKFLOW/KERNEL_BOOT_PROTOCOL.md` | Normative | Yes |
| `09-TOOLS/KERNEL_VALIDATION_PROTOCOL.md` | Normative | Yes |

### G.2 Forbidden Dependencies
| Reference | Rationale |
|---|---|
| Product/technology artifacts | KERNEL_SCOPE_DEFINITION §3.1, §3.2 |
| Workflows outside execution | Phase 1.5: "No workflows outside execution" |
| Executable code / runtime | Phase 1.5: no implementation |

## H. Revision History
| Version | Date | Author | Change Type | Authority | Description |
|---|---|---|---|---|---|
| 1.0.0 | 2026-06-26 | GovernanceBody | Added | MISSION-024 | Initial AI Execution Protocol |

## I. Acceptance
| Status | Approver | Date | Method | Conditions |
|---|---|---|---|---|
| Granted | MISSION-024 (GovernanceBody) | 2026-06-26 | Record | Phase 1.5 quality gates PASS |

## J. Canonical References
| Reference | Location |
|---|---|
| Repository Meta Model v1.1 (Matrix 7) | `01-META-MODEL/RMM_v1.1.md` |
| Kernel Authority Model | `01-META-MODEL/KERNEL_AUTHORITY_MODEL.md` |
| Kernel Scope Definition | `01-META-MODEL/KERNEL_SCOPE_DEFINITION.md` |
| Repository State Model | `01-META-MODEL/Repository_State_Model.md` |
| Kernel Validation Protocol | `09-TOOLS/KERNEL_VALIDATION_PROTOCOL.md` |

---

# PART II — EXECUTION PROTOCOL

## 1. Execution Lifecycle

The execution lifecycle is the ordered set of phases for any single operation. It maps to RMM `SESSION` → `TASK` and `PROCESS` lifecycles (RMM Matrix 2); state transitions are governed by `Repository_State_Model.md`.

| Phase | Definition | Governing source |
|---|---|---|
| EX-1 BOOT | Load the boot set; establish governance context. | KERNEL_BOOT_PROTOCOL §1, §3 |
| EX-2 AUTHORIZE | Bind a valid Authority (MISSION/EWO/ECO/TASK) and an Actor holding a Role. | DOCUMENT_STANDARD_SPEC §3.6; RMM ACTOR #7 |
| EX-3 PRE-VALIDATE | Run the precondition validation point (§4). | KERNEL_VALIDATION_PROTOCOL |
| EX-4 OPERATE | Perform only allowed operations (§2) on the target. | RMM Matrix 7 |
| EX-5 POST-VALIDATE | Run the postcondition validation point (§4). | KERNEL_VALIDATION_PROTOCOL |
| EX-6 RECORD | Emit Evidence and an Audit Trail entry for the state change. | KERNEL_SCOPE_DEFINITION §10.5; RMM AUDIT_TRAIL |
| EX-7 COMPLETE | Transition the Task/Session to its terminal state. | Repository_State_Model; RMM Matrix 2 |

A phase SHALL NOT be skipped. A failed validation point (EX-3 or EX-5) triggers a stop condition (§5).

## 2. Allowed Operations

EX-AO-01. **Read** any canonical artifact (read-only loading is always permitted; KERNEL_SCOPE_DEFINITION §10.5).

EX-AO-02. **Create** an instance of an entity only where RMM Matrix 7 `AI Creatable` = `Yes` or `With Approval` (with the required Approval entity in the latter case).

EX-AO-03. **Modify** an entity only where RMM Matrix 7 `AI Modifiable` = `Yes` or `With Approval` (with Approval in the latter case).

EX-AO-04. **Produce** DERIVED artifacts (Report, Assessment, Evidence, Record, Audit Trail) per DOCUMENT_STANDARD_SPEC, placed at the RMM Source of Truth.

EX-AO-05. All operations SHALL remain within scope (KERNEL_SCOPE_DEFINITION §2) and SHALL preserve technology independence and product agnosticism (KERNEL_SCOPE_DEFINITION §10.1, §10.2).

## 3. Forbidden Operations

EX-FO-01. **Modify** any entity where RMM Matrix 7 `AI Modifiable` = `No` — including `CONSTITUTION`, `INVARIANT`, `PRIMITIVE`, `SIGNATURE`, and the RMM itself (`AI Modifiable = No`; KERNEL_AUTHORITY_MODEL §3, V-11; KERNEL_STRUCTURE_SPEC §2.2).

EX-FO-02. **Create** any entity where RMM Matrix 7 `AI Creatable` = `No`.

EX-FO-03. **Modify a Frozen artifact** (RMM Matrix 5 `Freezable` = Yes and in frozen state) without the unfreeze → modify → refreeze cycle authorized by an Approval (KERNEL_STRUCTURE_SPEC §6.1).

EX-FO-04. **Architectural operations** are forbidden to execution: redesign, rename a concept, add/merge/split an entity, modify the RMM, modify the Constitution, change governance, or create alternative architecture (Phase 1.5 authority limits; KERNEL_SCOPE_DEFINITION §13.3, §13.8).

EX-FO-05. **Out-of-scope operations** (KERNEL_SCOPE_DEFINITION §3): product implementation, technology selection, infrastructure operations, and the other §3 domains.

EX-FO-06. Any operation that would realize a **failure criterion** (KERNEL_SCOPE_DEFINITION §13): emitting a technology name in a normative document, embedding product logic, creating an entity not in the RMM, breaking an authority chain, omitting an audit trail, or producing two contradicting artifacts.

## 4. Validation Points

EX-VP-01. **Precondition (EX-3):** boot complete (KERNEL_BOOT_PROTOCOL §3); Authority valid and Actor holds a Role; the target operation is permitted by RMM Matrix 7; the target, if frozen, is not being modified outside the unfreeze cycle.

EX-VP-02. **Postcondition (EX-5):** the produced artifact conforms to DOCUMENT_STANDARD_SPEC §4; no failure criterion is present (KERNEL_SCOPE_DEFINITION §13); all references resolve (KERNEL_STRUCTURE_SPEC §8.4); the dependency graph remains acyclic (KERNEL_DOCUMENT_REGISTRY RI-03).

EX-VP-03. **Freeze point:** before any freeze, the freeze checks of `09-TOOLS/KERNEL_VALIDATION_PROTOCOL.md` SHALL pass.

EX-VP-04. The detailed check sequence for all validation points is defined by `09-TOOLS/KERNEL_VALIDATION_PROTOCOL.md` (this protocol invokes it; it does not duplicate it).

## 5. Stop Conditions

Execution SHALL halt immediately when any of the following holds. On halt, no further phase proceeds and the condition is recorded (EX-6 best-effort).

| ID | Stop Condition | Source |
|---|---|---|
| EX-SC-01 | Boot incomplete (a boot-set document absent/unresolved). | KERNEL_BOOT_PROTOCOL §3 |
| EX-SC-02 | A required input or dependency is `[UNSUPPORTED]` / undefined in the Kernel. | Phase 1.5 protocol |
| EX-SC-03 | The operation is not permitted by RMM Matrix 7 (AI Creatable/Modifiable = No). | RMM Matrix 7 |
| EX-SC-04 | The target is frozen and no unfreeze/refreeze Approval exists. | KERNEL_STRUCTURE_SPEC §6.1 |
| EX-SC-05 | The authority chain is broken or untraceable to the Constitution. | KERNEL_SCOPE_DEFINITION §13.6 |
| EX-SC-06 | A true architectural contradiction is encountered (would require a forbidden operation, EX-FO-04). | KERNEL_SCOPE_DEFINITION §13.8 |
| EX-SC-07 | A precondition or postcondition validation point fails (§4). | KERNEL_VALIDATION_PROTOCOL |
| EX-SC-08 | A required artifact (boot set or canonical inventory) is missing. | SKILL_MANIFEST_SPECIFICATION §4 |

This protocol defines execution phases, permissions, validation points, and stop conditions only. It defines no scheduler, engine, or code — **[implementation: out of scope, Phase 1.5]** — and no workflow other than execution.

---

## QUALITY GATE (PCS) — PASS

| Gate | Result | Note |
|---|---|---|
| Engineering Self Review | PASS | Every allowed/forbidden operation and stop condition cites RMM Matrix 7, KAM, or KSD §13/§3; nothing invented. |
| PCS Compliance Review | PASS | Execution only; no extra workflows, no code, no technology, no governance redesign. Forbidden operations explicitly include the Phase 1.5 SHALL-NOT list. |
| Correction Cycle | PASS | Detailed checks delegated to the Validation Protocol; undefined dependencies routed to stop condition EX-SC-02. |
| Final Verification | PASS | Conforms to DOCUMENT_STANDARD_SPEC; placed at canonical Process home `07-WORKFLOW/`. |

*END OF DOCUMENT*
