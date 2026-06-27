<!--
  ============================================
  AUTHORITY_ARBITRATION_REPORT.md — Engineering Kernel
  Phase 1.10 — Authority Arbitration
  Independent Principal Architecture Board.
  Determines canonical authority order ONLY. No redesign, no repair,
  no engineering work, no RMM/Constitution modification.
  ============================================
-->

# AUTHORITY ARBITRATION REPORT

| Property | Value |
|---|---|
| **Title** | Authority Arbitration Report |
| **Classification** | DERIVED |
| **Role** | Independent Principal Architecture Board — Authority Arbitration |
| **Repository State** | `main` (current HEAD) |
| **Mandate** | Determine canonical authority order only. No modification of any existing document. |
| **Date** | 2026-06-26 |

---

## Section 1 — Scope and Constraint

This is an **authority determination**, not a review, verification, or validation. It answers exactly one class of question: *when two canonical artifacts disagree, which one holds architectural authority?* It proposes no engineering work, edits no document, and assigns no fix. Every determination below cites the repository directly.

The available decisions are fixed by the mandate: **Repository authoritative / RMM authoritative / Constitution authoritative / Structure Specification authoritative / Registry authoritative / Conflict cannot be resolved without Constitutional Amendment.** No other decision is used.

---

## Section 2 — The Two Planes of Authority

The repository establishes two distinct kinds of supremacy, and they must not be conflated:

- **Governance supremacy — the Constitution.** `00-CONSTITUTION/CONSTITUTION.md` §1 (line 198): *"This Constitution is the supreme authority. All other governance instruments derive their legitimacy from it. No entity within the Kernel may claim authority independent of this Constitution."* §4.4 (line 294): *"The Constitution may not be overridden by any entity except by its own amendment procedure."* This supremacy is granted by the RMM's own definition of the CONSTITUTION entity — RMM CONSTITUTION #3 (CONSTITUTION.md line 162): *"overriding all other instruments in case of conflict"*; RMM CONSTITUTION #6 (line 213): *"Supersedes AllGovernanceEntities."*

- **Ontological supremacy — the RMM.** `01-META-MODEL/RMM_v1.1.md` is the root of the dependency DAG (`KERNEL_DOCUMENT_REGISTRY.md` §6.1, line 308: "RMM_v1.1.md (root)") and the sole definition of all 79 entities and their 15 properties. Every other canonical document declares the RMM as its source — e.g. `KERNEL_STRUCTURE_SPEC.md` §1: *"This document is derived directly from RMM property #15."*

The Constitution is the higher authority, because the RMM itself confers that supremacy on the Constitution entity (RMM CONSTITUTION #3, #6) and the Constitution exercises it (P-1, §4.4). The RMM is supreme over **everything except the Constitution**. Crucially, supremacy is not the power to silently overwrite: the Constitution cannot edit RMM content directly either — P-10 (CONSTITUTION.md line 327) reserves RMM modification to "an Amendment ratified through the constitutional amendment procedure." Authority therefore resolves *which artifact governs*; it does not by itself authorize a change to the other.

---

## Section 3 — Canonical Authority Hierarchy

Derived strictly from repository evidence:

| Tier | Authority | Basis (direct evidence) |
|---|---|---|
| **1** | **CONSTITUTION** | CONSTITUTION.md §1, §4.4, P-1; RMM CONSTITUTION #3 ("overriding all other instruments in case of conflict"), #6 ("Supersedes AllGovernanceEntities"); KAM line 17 ("CONSTITUTION (self-owning, supreme)"), V-12 ("No entity may contradict the Constitution... implied for all"). |
| **2** | **RMM v1.1** | Root of the dependency DAG (KDR §6.1); defines all 79 entities and property #15; FROZEN baseline (KDR §10; KAM line 118/511 "Status: FROZEN"). Supreme ontological authority — subordinate only to the Constitution, and only in direct governance conflict. |
| **3** | **Derived canonical specifications** (KERNEL_STRUCTURE_SPEC, DOCUMENT_STANDARD_SPEC, KERNEL_SCOPE_DEFINITION, KERNEL_AUTHORITY_MODEL, etc.) | Each self-declares derivation from RMM and sits below RMM in the read/dependency order (KDR §6, §7). Cannot override their source. |
| **4** | **KERNEL_DOCUMENT_REGISTRY** | Terminal consumer of all normative references (KDR §6.3: "depends on all"); restates §3 of its sources. Authoritative only over its own domain — the canonical document inventory and registration. |
| **5** | **Repository files / entity instances** | The actual committed files. The Ledger's own Evidence Hierarchy places "Committed repository files" at Tier 3, below RMM (CANONICAL_ARBITRATION_LEDGER.md §2.1). Instances must conform to the model; the model does not conform to the instances. |

**Note on the Arbitration Ledger's own hierarchy.** `CANONICAL_ARBITRATION_LEDGER.md` §2.1 lists RMM at Tier 1 *above* CONSTITUTION at Tier 2. This inverts the Constitution's supremacy and is itself contradicted by RMM CONSTITUTION #3/#6, which the RMM defines and which place the Constitution above all governance instruments. The Ledger's local ordering has no authority to subordinate the Constitution; on this point the Ledger is overruled by both the Constitution and the RMM's own CONSTITUTION entity definition.

---

## Section 4 — Required Conflict Decisions

### 4.1 If RMM and Repository disagree — **RMM is authoritative.**

**Evidence:** `KERNEL_DOCUMENT_REGISTRY.md` §12 Rule 1 (line 449): *"Every artifact SHALL be stored in the directory matching its RMM Source of Truth"*; Rule 8 (line 456): *"RMM #15 Source of Truth is the canonical location for each entity type."* RI-04 (line 471): FROZEN RMM may not be modified without Amendment. The Ledger §2.1 ranks RMM (Tier 1) above repository files (Tier 3). The model is the standard; a non-conforming file is non-conforming, it is not a counter-authority. Therefore where a committed file's location or content disagrees with the frozen RMM, **the RMM holds authority** and the repository is the party out of conformance. (The remedy — conform the file, or amend the RMM — is an engineering/governance act outside this arbitration; authority itself rests with the RMM.)

### 4.2 If KERNEL_STRUCTURE_SPEC and RMM disagree — **RMM is authoritative.**

**Evidence:** `KERNEL_STRUCTURE_SPEC.md` §1 self-declares it is *"derived directly from RMM property #15."* A derived document cannot overrule its source. In the dependency DAG (KDR §6.1) RMM is the root and KSS is a dependent; in the Read Order (KDR §7) RMM is position 1 and KSS positions 2–3. RMM is FROZEN; KSS is `Status: Active`. Therefore on any entity Source-of-Truth, naming, version, or freeze fact, **RMM property values govern over KSS's restatement of them.** Where KSS §2/§5/§6 diverge from RMM (e.g., directory assignments, versionable/freezable counts), the RMM is authoritative and KSS is in error.

### 4.3 If Registry contradicts Structure — **Structure Specification is authoritative.**

**Evidence:** `KERNEL_DOCUMENT_REGISTRY.md` §12 (line 446) introduces its navigation rules with *"From KERNEL_STRUCTURE_SPEC:"* and every row carries an explicit `Source: KSS x.y` citation. The Registry is, by its own declaration, restating KSS. KSS is more foundational in the dependency order (KDR §7: KSS position 2–3; KDR position 9) and the Registry is the terminal consumer (KDR §6.3: "depends on all... terminal"). Where the Registry's restatement of a structural/navigation rule diverges from KSS, **the original (KSS) governs.** The Registry retains authority only over its own proper domain — the canonical document inventory and what is/is not registered (§2, §3, RI-01…RI-08). (This decision concerns structural conflicts; both KSS and the Registry remain jointly subordinate to RMM and the Constitution.)

### 4.4 If Constitution contradicts RMM — **Constitution is authoritative.**

**Evidence:** RMM CONSTITUTION #3 (CONSTITUTION.md line 162): *"overriding all other instruments in case of conflict."* RMM CONSTITUTION #6 (line 213): *"Supersedes AllGovernanceEntities."* CONSTITUTION.md §1 (line 198) and §4.4 (line 294); P-1 (line 318). KAM line 17: "CONSTITUTION (self-owning, supreme)"; KAM V-12: "No entity may contradict the Constitution." The supremacy is not self-asserted in a vacuum — it is written into the RMM's *own* definition of the CONSTITUTION entity. Therefore in a direct governance conflict, **the Constitution prevails over the RMM.** (The apparent circularity — RMM defines the Constitution, yet the Constitution outranks the RMM — resolves cleanly: the RMM is the ontological author of the Constitution entity but assigns that entity supremacy over all governance conflict, including conflicts with the RMM's other entities.)

### 4.5 If two frozen artifacts disagree — **Conflict cannot be resolved without Constitutional Amendment.**

**Evidence:** A frozen artifact is, by definition, immutable except through amendment: `KERNEL_DOCUMENT_REGISTRY.md` RI-04 (line 471): *"FROZEN documents may not be modified without Amendment"*; CONSTITUTION.md P-10 (line 327): the RMM *"may not be modified without an Amendment ratified through the constitutional amendment procedure"*; RMM CONSTITUTION #7 / P-1: the Constitution may be overridden only by its own amendment procedure. If two frozen artifacts genuinely disagree, neither may be changed to match the other by any ordinary authority, and no third canonical document may rewrite either of them. The only mechanism that can lawfully alter a frozen artifact is the constitutional amendment procedure. **Therefore a genuine frozen-vs-frozen conflict is escalated; it cannot be resolved without Constitutional Amendment.** (Exception: if one of the two frozen artifacts is the Constitution itself, §4.4 applies and the Constitution prevails; if one is the RMM and the other a frozen derived spec, §4.2 applies and the RMM prevails. The "cannot be resolved" outcome is reserved for two frozen artifacts of equal standing with no derivation relationship between them.)

---

## Section 5 — Was the Ledger's "Unfreeze RMM" Recommendation Within the Arbiter's Authority?

**Determination: It EXCEEDED the Arbiter's authority.**

The `CANONICAL_ARBITRATION_LEDGER.md` §14.4 (lines 978–986) and §11.4 recommend: *"Unfreeze RMM v1.1 — Change status from FROZEN to ACTIVE,"* apply seven SOT amendments, and refreeze. The repository evidence places this outside the authority of an "Independent Engineering Arbiter":

1. **RMM modification is constitutionally reserved.** CONSTITUTION.md P-10 (line 327): the RMM *"may not be modified without an Amendment ratified through the constitutional amendment procedure."* Unfreezing-in-order-to-modify is RMM modification. RI-04 confirms: FROZEN documents may not be modified without Amendment.

2. **The approval authority is the GovernanceBody, not an arbiter.** RMM AMENDMENT #6 (CANONICAL_ARBITRATION_LEDGER.md line 773; CONSTITUTION.md §9): an Amendment is *"ApprovedBy GovernanceBody."* The authority chain is fixed — CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR (CONSTITUTION.md §4.1 line 275; KAM line 17). An "Independent Engineering Arbiter" appears nowhere in this chain.

3. **No "Arbiter" authority is chartered anywhere.** A repository-wide search of `00-CONSTITUTION/`, `RMM_v1.1.md`, `KERNEL_ROLE_MODEL.md`, and `KERNEL_GOVERNANCE_MODEL.md` returns **zero** definitions of an "Arbiter" or "Arbitration" role or entity. Under CONSTITUTION.md §1 (line 198), *"No entity within the Kernel may claim authority independent of this Constitution"* — an un-chartered Arbiter cannot hold decision authority over the frozen ontological root.

4. **The proposed resolution rests on an [UNSUPPORTED] procedure.** CONSTITUTION.md §11.2 (line 445): *"[UNSUPPORTED — RMM does not define the specific amendment procedure steps]."* CONSTITUTION.md §8.1 (line 383): *"An [UNSUPPORTED] property may not be used as the basis for any governance decision."* A directive to execute an amendment procedure that the Constitution marks [UNSUPPORTED] cannot be grounded in current authority.

5. **The Ledger inverts the authority order it is bound by.** It declares the FROZEN RMM "wrong" and the repository "correct" (e.g. §14.4 line 986: "fixes the frozen meta-model which contains errors"), then directs that RMM be changed to match the repository. Per §4.1 above and the Ledger's own §2.1 hierarchy, the repository is the *lower* authority; an arbiter cannot promote the lower artifact to overrule the higher one and order the higher one rewritten.

**Boundary of what WAS within authority.** Identifying the SOT path mismatches as factual findings (ISSUE-001…007) is a legitimate evidentiary/review act — an arbiter or reviewer may surface a conflict. What exceeds authority is **deciding the resolution** of that conflict by directing the unfreezing of the frozen ontological root. That decision belongs solely to the GovernanceBody acting through the constitutional amendment procedure. The correct ceiling of the Arbiter's output was: *record the conflict and escalate it to Constitutional authority* — precisely the "Conflict cannot be resolved without Constitutional Amendment" outcome of §4.5. By prescribing the unfreeze instead of escalating, the recommendation exceeded the Arbiter's authority.

---

## Section 6 — Final Questions

**1. What is the canonical authority hierarchy?**

```
1. CONSTITUTION                      (supreme in any conflict)
2. RMM v1.1                          (supreme ontological authority; FROZEN)
3. Derived canonical specifications  (KSS, DSS, KSD, KAM, ... — derive from RMM)
4. KERNEL_DOCUMENT_REGISTRY          (terminal consumer; authoritative over registration only)
5. Repository files / instances      (must conform to all above)
```
Evidence: CONSTITUTION.md §1/§4.1/§4.4/P-1; RMM CONSTITUTION #3/#6; KDR §6.1 (RMM = DAG root), §6.3 (KDR terminal), §7 (read order), §12 (Registry restates KSS); KAM line 17, V-12; CANONICAL_ARBITRATION_LEDGER.md §2.1 (repository files lowest).

**2. Can an engineer decide which artifact is correct, or must every unresolved conflict be escalated to Constitutional authority?**

An engineer may decide **only the cases the hierarchy already settles deterministically** — i.e., where one artifact derives from another (repository vs RMM → RMM; KSS vs RMM → RMM; Registry vs KSS → KSS; Constitution vs RMM → Constitution). In those cases the higher artifact wins by the rules in Section 4, and no escalation is needed to *determine authority*.

However, an engineer **may not act on that determination by modifying a frozen artifact.** Any resolution that requires changing the RMM or the Constitution must be escalated: CONSTITUTION.md P-10 and RI-04 reserve such modification to the constitutional amendment procedure approved by the GovernanceBody. And any **genuine conflict between two frozen artifacts of equal standing** has no engineer-level resolution at all — per §4.5 it must be escalated to Constitutional authority. In short: **an engineer can read off which artifact is authoritative, but cannot unilaterally reconcile the documents when reconciliation touches a frozen artifact — that requires Constitutional Amendment.**

**3. Was the recommendation inside CANONICAL_ARBITRATION_LEDGER to unfreeze RMM within the Arbiter's authority, or did it exceed it?**

**It exceeded the Arbiter's authority.** Unfreezing the RMM is RMM modification (CONSTITUTION.md P-10; KDR RI-04), reserved to a GovernanceBody-approved Amendment (RMM AMENDMENT #6) executed through a procedure the Constitution itself marks [UNSUPPORTED] (CONSTITUTION.md §11.2, §8.1). No "Arbiter" role is chartered in the Constitution, RMM, Role Model, or Governance Model, and CONSTITUTION.md §1 forbids any entity claiming authority independent of the Constitution. The Arbiter was within authority to *identify* the SOT mismatches and to *escalate* them; it exceeded authority by *deciding* the resolution and directing the unfreeze of the frozen ontological root. The correct disposition of those findings is escalation to Constitutional authority — not an arbiter-issued unfreeze directive.

---

*END OF REPORT*
