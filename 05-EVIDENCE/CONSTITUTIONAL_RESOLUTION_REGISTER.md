<!--
  ============================================
  CONSTITUTIONAL_RESOLUTION_REGISTER.md — Engineering Kernel
  Phase 1.11 — Constitutional Resolution
  Constitutional Authority Board.
  Issues Constitutional Resolutions only. No redesign, no implementation,
  no document rewriting, no RMM freeze/unfreeze, no new entities.
  ============================================
-->

# CONSTITUTIONAL RESOLUTION REGISTER

| Property | Value |
|---|---|
| **Title** | Constitutional Resolution Register |
| **Classification** | DERIVED |
| **Role** | Constitutional Authority Board — Constitutional Resolution |
| **Repository State** | `main` (current HEAD) |
| **Mandate** | Classify the constitutional resolution required for every CONFIRMED finding in `CANONICAL_ARBITRATION_LEDGER.md`. No document modification, no implementation, no RMM freeze/unfreeze. |
| **Date** | 2026-06-26 |

---

## Section 1 — Executive Summary

This register resolves all **13 CONFIRMED findings** of `05-EVIDENCE/CANONICAL_ARBITRATION_LEDGER.md` (ISSUE-001–007, 014, 015, 016, 017, 019, 020) under the authority hierarchy fixed by `AUTHORITY_ARBITRATION_REPORT.md`: **Constitution > RMM v1.1 > Derived Specifications > Registry > Repository**. That hierarchy is accepted as given and is not reconsidered here.

Applying it changes the disposition of 8 findings relative to the Ledger's own self-assigned action type. The Ledger classified ISSUE-001–007 and ISSUE-016 as `REQUIRES_RMM_AMENDMENT` — i.e., it proposed changing the *higher*-authority artifact (RMM) to match the *lower*-authority artifact (repository file locations). Under the accepted hierarchy this is backwards: RMM is authoritative over the repository, so the constitutionally correct resolution is the repository conforms to RMM, not the reverse. This register therefore reclassifies those 8 findings as **Repository Correction**.

Net result: **0 findings require Constitutional Amendment. 0 findings require RMM Amendment** as an actionable present disposition. **8 require Repository Correction. 1 requires Derived Document Correction. 4 are Deferred Future Phase Items.** No finding is constitutionally blocking.

| Disposition | Count | Findings |
|---|---|---|
| No Action | 0 | — |
| Repository Correction | 8 | ISSUE-001, 002, 003, 004, 005, 006, 007, 016 |
| Derived Document Correction | 1 | ISSUE-014 |
| Constitutional Amendment Required | 0 | — |
| RMM Amendment Required | 0 | — |
| Future Phase Item | 4 | ISSUE-015, 017, 019, 020 |

---

## Section 2 — Constitutional Authority

This Board acts as the **Constitutional Authority Board**, not as Reviewer, Auditor, Engineer, Author, or Arbiter. Its sole output is a Constitutional Resolution per finding — a classification of *what kind of authority must act*, never the content of the fix.

The Board's own authority to issue these resolutions derives from the Constitution's own chain: `CONSTITUTION.md` §4.1 (Authority Origin/Terminus) — CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR. This register does not modify the Constitution, the RMM, or any other canonical document; it produces a single new evidentiary artifact, consistent with `KERNEL_AUTHORITY_MODEL.md` line 17 ("CONSTITUTION (self-owning, supreme)") and V-12 ("No entity may contradict the Constitution").

Per `AUTHORITY_ARBITRATION_REPORT.md` §5, no "Arbiter" role is chartered anywhere in the Constitution, RMM, Role Model, or Governance Model. The Ledger's self-declared status as "final arbitration authority... supersedes all previous reviews" (Ledger §1.1, §16.2) is therefore evidentiary only — Tier 4 under the Ledger's own hierarchy, and subordinate to the Constitution under the accepted hierarchy. This register treats the Ledger strictly as a source of *findings* (the factual record of what was found), not as a source of *authority* over how those findings must be resolved.

---

## Section 3 — Accepted Authority Hierarchy

Per instruction, the following hierarchy from `AUTHORITY_ARBITRATION_REPORT.md` §3/§6 is accepted as fixed and is **not reconsidered**:

```
1. CONSTITUTION                      (supreme in any conflict)
2. RMM v1.1                          (supreme ontological authority; FROZEN)
3. Derived canonical specifications  (KSS, DSS, KAM, KEM, KRM, KGM, KDM, KRLM, AFM, ...)
4. KERNEL_DOCUMENT_REGISTRY          (terminal consumer; authoritative over registration only)
5. Repository files / instances      (must conform to all above)
```

This register additionally carries forward two binding determinations from the Authority Arbitration Report that directly govern how findings are resolved below:

- **§4.1**: "Where a committed file's location or content disagrees with the frozen RMM, the RMM holds authority and the repository is the party out of conformance... the remedy is to conform the file, or amend the RMM."
- **§5**: Directing the unfreeze of RMM in order to amend it **exceeded the issuing Arbiter's authority** — RMM modification is reserved to a GovernanceBody-approved Amendment (RMM AMENDMENT #6) executed through a procedure the Constitution itself marks `[UNSUPPORTED]` (`CONSTITUTION.md` §11.2), and `[UNSUPPORTED]` properties may not be used as the basis for any governance decision (`CONSTITUTION.md` §8.1).

---

## Section 4 — Resolution Rules

The following rules translate the accepted hierarchy into a deterministic resolution procedure. They were applied uniformly to every CONFIRMED finding.

| Rule | Statement | Basis |
|---|---|---|
| **R1** | If a finding is a disagreement between a committed repository file (location or content) and the frozen RMM, the repository is out of conformance and the disposition is **Repository Correction** — not RMM Amendment — because RMM outranks the repository and the repository, not RMM, is the non-conforming party. | AUTHORITY_ARBITRATION_REPORT.md §4.1; KDR §12 Rule 1/Rule 8, RI-04 |
| **R2** | If a finding is a derived canonical specification (Tier 3) misrepresenting or incorrectly restating its source (RMM or another Tier-3 document), the disposition is **Derived Document Correction** — the derived document's own content is wrong, independent of RMM or repository location. | KSS §1 ("derived directly from RMM"); AUTHORITY_ARBITRATION_REPORT.md §4.2 |
| **R3** | A finding may only be dispositioned **RMM Amendment Required** if resolving it requires changing RMM's substantive content (not merely conforming a file to RMM) **and** a constitutionally defined amendment procedure exists to do so. Because `CONSTITUTION.md` §11.2 marks the amendment procedure `[UNSUPPORTED]`, and §8.1 forbids basing a governance decision on an `[UNSUPPORTED]` property, **no finding may presently be given this disposition as an actionable resolution.** Any finding that would otherwise qualify is instead routed to Future Phase Item, pending definition of the amendment procedure. | CONSTITUTION.md §8.1, §11.2; RMM AMENDMENT #6; AUTHORITY_ARBITRATION_REPORT.md §5 |
| **R4** | A finding may only be dispositioned **Constitutional Amendment Required** if resolving it requires changing Constitution content itself. None of the 13 CONFIRMED findings touch Constitution content (confirmed independently below, Section 9). | CONSTITUTION.md §4.4, P-1 |
| **R5** | If the required resolution is the creation of an artifact, tool, or process that does not yet exist (a new document, new validation infrastructure, a multi-document harmonization effort, or a batch resolution of many independent gaps), the disposition is **Future Phase Item** — such work exceeds "correction" of an existing artifact and is properly scheduled, not resolved by classification alone. | Ledger §15.2 (own Phase 2 scheduling of the same items) |
| **R6** | **No Action** applies only to findings already OBSOLETE or BY_DESIGN. None of the 13 CONFIRMED findings qualify (by definition — CONFIRMED findings describe a still-present condition). | Ledger §6, §8, §9 |

---

## Section 5 — Confirmed Findings Resolution Matrix

| Finding | Title | Ledger's Own Action Type | **Constitutional Resolution** | Rule Applied |
|---|---|---|---|---|
| ISSUE-001 | CHARTER SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-002 | ROLE SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-003 | DECISION SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-004 | REVIEW SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-005 | AMENDMENT SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-006 | LIFECYCLE SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-007 | STATE SOT path mismatch | REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-014 | AFM evidence coverage gap (KEM §J misstates AFM family) | REQUIRES_REPOSITORY_CORRECTION | **Derived Document Correction** | R2 |
| ISSUE-015 | Section naming inconsistency | REQUIRES_REPOSITORY_CORRECTION | **Future Phase Item** | R5 |
| ISSUE-016 | Reserved directory gaps (consolidates 001–007) | REQUIRES_REPOSITORY_CORRECTION / REQUIRES_RMM_AMENDMENT | **Repository Correction** | R1 |
| ISSUE-017 | Process entity unmodeled (no KERNEL_PROCESS_MODEL.md) | REQUIRES_REPOSITORY_CORRECTION | **Future Phase Item** | R5 |
| ISSUE-019 | Cross-document validation gap (no tooling exists) | REQUIRES_REPOSITORY_CORRECTION | **Future Phase Item** | R5 |
| ISSUE-020 | [UNSUPPORTED] markers present (37, across 11 docs) | REQUIRES_RMM_AMENDMENT | **Future Phase Item** | R3, R5 |

**Note on ISSUE-014 disposition.** The Ledger labeled this `REQUIRES_REPOSITORY_CORRECTION`, but the artifact requiring correction — `KERNEL_EVIDENCE_MODEL.md` §J — is a Tier-3 derived canonical specification (derived from RMM TIER 10 and AFM), not a raw repository instance. R2 applies more precisely than R1: the defect is KEM's own misstatement of AFM family assignments, not a location/content disagreement between repository and frozen RMM. This is a terminological correction to the Ledger's classification, not a disagreement with its underlying finding.

**Note on ISSUE-016.** This finding is the Ledger's own consolidation of the identical SOT mismatches already itemized in ISSUE-001–007 (Ledger §"Section 16: Reserved Directory Gaps" table reproduces the same 7 entities). It receives the same disposition for the same reason and is not double-counted as a distinct repository action.

---

## Section 6 — Repository Corrections

The following 8 findings resolve to **Repository Correction**: the committed repository file (location) must be brought into conformance with the frozen, authoritative RMM #15 Source-of-Truth value. Per R1, RMM is not amended; the repository is corrected.

| Finding | Entity | RMM #15 (authoritative) | Current Repository Location (non-conforming) |
|---|---|---|---|
| ISSUE-001 | CHARTER | `00-CONSTITUTION/Charters/` | `00-CONSTITUTION/KERNEL_CHARTER.md` |
| ISSUE-002 | ROLE | `00-CONSTITUTION/` | `02-GOVERNANCE/KERNEL_ROLE_MODEL.md` |
| ISSUE-003 | DECISION | `05-EVIDENCE/` | `02-GOVERNANCE/KERNEL_DECISION_MODEL.md` |
| ISSUE-004 | REVIEW | `05-EVIDENCE/Reviews/` | `02-GOVERNANCE/KERNEL_REVIEW_MODEL.md` |
| ISSUE-005 | AMENDMENT | `02-GOVERNANCE/Amendments/` | `02-GOVERNANCE/KERNEL_AMENDMENT_MODEL.md` |
| ISSUE-006 | LIFECYCLE | `01-META-MODEL/Lifecycles/` | `99-STATE/REPOSITORY_LIFECYCLE_MODEL.md` |
| ISSUE-007 | STATE | `01-META-MODEL/` | `99-STATE/REPOSITORY_LIFECYCLE_MODEL.md` |
| ISSUE-016 | (consolidates all of the above) | — | — |

This register does not prescribe *how* the correction is executed (move file, create directory, symlink, or other mechanism) — that is engineering work outside this Board's mandate. It establishes only that the constitutionally consistent direction of correction runs **from repository toward RMM**, never the reverse, for as long as RMM remains FROZEN and Tier 2.

---

## Section 7 — Derived Document Corrections

| Finding | Document | Defect | Required Correction Type |
|---|---|---|---|
| ISSUE-014 | `05-EVIDENCE/KERNEL_EVIDENCE_MODEL.md` §J | Claims AFM §3 (Evidence Family) covers all 7 RMM TIER 10 entities; AFM §3 in fact defines only 3 (EVIDENCE, FINDING, CONCLUSION) — the other 4 (DECISION_RECORD, AUDIT, REVIEW, TRANSPARENCY_REPORT) are defined in AFM §4/§9/§12 | KEM §J must be corrected to cite each entity's actual AFM family location. This is a correction internal to a Tier-3 derived document's own restatement of another Tier-3 document (AFM); it does not touch RMM, Constitution, or repository structure. |

No other CONFIRMED finding falls in this category. ISSUE-008–013 (OBSOLETE) were historically Derived Document Corrections of this same kind, already executed prior to this register (Ledger §7) — cited here only for pattern confirmation, not as open items.

---

## Section 8 — RMM Amendment Candidates

The Ledger proposed nine RMM amendments (RMM-AMEND-001 through 009, Ledger §11) as the resolution to ISSUE-001–007, 017, and 020. Under R1/R3, **none of these nine candidates is presently dispositioned as RMM Amendment Required**:

| Candidate | Origin | Why Not Actionable Now |
|---|---|---|
| RMM-AMEND-001–007 (SOT path corrections) | ISSUE-001–007 | R1: the repository, not RMM, is the non-conforming party. Amending RMM to match repository file locations would invert the accepted hierarchy — exactly the defect identified in AUTHORITY_ARBITRATION_REPORT.md §5 regarding the Ledger's unfreeze recommendation. |
| RMM-AMEND-008 (add PROCESS as formal Kernel-modeled entity) | ISSUE-017 | PROCESS is already a fully-defined RMM entity (TIER 5, #1–15); no RMM content change is needed to create a derived `KERNEL_PROCESS_MODEL.md` — see Section 10. |
| RMM-AMEND-009 (batch-resolve 37 [UNSUPPORTED] markers) | ISSUE-020 | R3: resolving `[UNSUPPORTED]` properties is itself an amendment to RMM content, gated by an amendment procedure that `CONSTITUTION.md` §11.2 marks `[UNSUPPORTED]`. Per §8.1, an `[UNSUPPORTED]` property cannot be the basis of a governance decision — so this candidate cannot be actioned as "RMM Amendment Required" until the amendment procedure itself is constitutionally defined. It is carried to Section 10 as a Future Phase Item instead. |

These candidates remain visible here as a historical record of what the Ledger proposed; this register does not adopt them as required dispositions.

---

## Section 9 — Constitutional Amendment Candidates

**None.** Independently confirmed, consistent with the Ledger's own finding (Ledger §12.2: "No constitutional violations detected. All findings are at RMM or document level."):

- No CONFIRMED finding alleges or evidences a defect in `CONSTITUTION.md` content, a Principle (P-1–P-10), or the Authority Chain (`CONSTITUTION → CHARTER → GOVERNANCE_BODY → ROLE → ACTOR`, §4.1).
- ISSUE-017's only discussed indirect Constitutional consideration (Ledger §12.1 — *if* PROCESS were elevated to constitutional significance) is explicitly speculative and at GovernanceBody discretion; it is not a present finding requiring amendment and is not adopted as a disposition here.

---

## Section 10 — Deferred Future Work

The following 4 findings are dispositioned **Future Phase Item** — confirmed, valid, not constitutionally blocking, but requiring creation of new artifacts/infrastructure or multi-document harmonization that exceeds "correction of an existing artifact":

| Finding | Title | Why Deferred | Note |
|---|---|---|---|
| ISSUE-015 | Section naming inconsistency (numbered vs. lettered vs. DSS §3 hierarchical numbering, none fully followed) | Cosmetic; touches 10+ documents; no single document is "wrong" in isolation — it is a cross-document harmonization effort | LOW severity (Ledger) |
| ISSUE-017 | Process entity unmodeled (no `KERNEL_PROCESS_MODEL.md`, though RMM PROCESS #1–15 is fully defined) | Requires creating a new derived document; PROCESS already exists in RMM so no RMM Amendment is needed, but document creation is new work, not a correction of an existing artifact | This register does not authorize or perform the creation; it records that the work is in-scope for Phase 2 and requires no RMM/Constitution change |
| ISSUE-019 | Cross-document validation gap (no automated/procedural validation exists) | Requires new infrastructure (tooling or checklist) that does not yet exist anywhere in the repository | HIGH priority per Ledger §10.5 |
| ISSUE-020 | [UNSUPPORTED] markers present (37 across 11 documents, all legitimate) | Per R3, cannot presently be dispositioned RMM Amendment Required; resolving the markers is amendment-shaped work blocked on an undefined amendment procedure | The markers themselves are not errors (Ledger §"Analysis": "honest and acceptable") — only their long-term resolution is deferred |

---

## Section 11 — Phase 2 Entry Conditions

Phase 2 entry is evaluated strictly against the dispositions above, not against the Ledger's own (partially superseded) Phase 2 sequencing (Ledger §15.3).

| Condition | Status | Basis |
|---|---|---|
| All 13 CONFIRMED findings have received a Constitutional Resolution | YES | Section 5, this register |
| No finding requires Constitutional Amendment | YES (0 findings) | Section 9 |
| No finding requires RMM Amendment as an actionable present disposition | YES (0 findings) | Section 8, Rule R3 |
| No finding requires unfreezing RMM | YES — none of the 13 dispositions touches RMM content; RMM remains FROZEN and untouched by this register | Section 6, Section 8 |
| Repository Corrections are independently executable without Constitutional or RMM action | YES — all 8 are Tier-5 (repository) actions per R1 | Section 6 |
| Derived Document Correction is independently executable without Constitutional or RMM action | YES — ISSUE-014 is a Tier-3 self-correction | Section 7 |
| Deferred items are tracked, not silently dropped | YES — 4 items in Section 10 | Section 10 |

**Phase 2 is not constitutionally conditioned on completing the Repository Corrections or Derived Document Correction first** — none of them touches a frozen artifact, so none can produce a Constitutional or RMM-level blocker. They are operationally recommended before Phase 2 work that depends on SOT navigation, but their absence is not a constitutional bar.

---

## Section 12 — Final Constitutional Verdict

Phase 1's 13 CONFIRMED findings resolve cleanly under the accepted hierarchy without touching the Constitution or the frozen RMM. Every finding that the Ledger proposed resolving by amending RMM (ISSUE-001–007, 016, 020) is, under Constitution > RMM > Derived Specifications > Registry > Repository, properly a repository-side correction or a deferred item — never an RMM change. Zero findings rise to a Constitutional Amendment. This is consistent with, and reinforces, `AUTHORITY_ARBITRATION_REPORT.md` §5's determination that the Ledger's unfreeze recommendation exceeded its issuing Arbiter's authority: this register confirms that unfreezing was never the *required* resolution in the first place — a fully constitutional, non-amendment resolution path (Repository Correction) was available for every SOT mismatch finding.

Phase 1 is **constitutionally resolvable without amendment**. What remains is execution of 8 Repository Corrections and 1 Derived Document Correction (engineering work, outside this Board's mandate) plus tracking of 4 deferred items into Phase 2.

---

## Final Questions

**1. Is Phase 1 constitutionally closed?**

Not yet — **classification is complete, execution is not.** Every CONFIRMED finding now has a definitive Constitutional Resolution (Section 5), and none of those resolutions requires touching a frozen artifact. But the 8 Repository Corrections (Section 6) and 1 Derived Document Correction (Section 7) remain unexecuted as of this register. Phase 1 reaches constitutional closure once those 9 items are executed; no Constitutional or RMM Amendment stands between Phase 1 and closure.

**2. Can Phase 2 begin constitutionally?**

**Yes.** None of the 13 CONFIRMED findings produces a Constitutional or RMM-level blocker (Section 11). The Repository Correction and Derived Document Correction items are recommended to precede Phase 2 work that depends on SOT-path navigation, but their absence is an operational risk, not a constitutional bar.

**3. Does any unresolved issue still block Phase 2?**

**No.** Zero findings are dispositioned Constitutional Amendment Required or RMM Amendment Required (Sections 8–9) — the only disposition types capable of constituting a constitutional blocker under the accepted hierarchy. The remaining open items (8 Repository Corrections, 1 Derived Document Correction, 4 Future Phase Items) are all Tier-3/Tier-5 actions that do not require touching the Constitution or the frozen RMM.

**4. Which findings require Constitutional Amendment?**

**None.** Zero of the 13 CONFIRMED findings (Section 9).

**5. Which findings require only Repository Corrections?**

**ISSUE-001, ISSUE-002, ISSUE-003, ISSUE-004, ISSUE-005, ISSUE-006, ISSUE-007, and ISSUE-016** (8 findings — all RMM #15 Source-of-Truth path mismatches, resolved by conforming the repository's file locations to the frozen, authoritative RMM rather than amending RMM) (Section 6).

---

*END OF REGISTER*
