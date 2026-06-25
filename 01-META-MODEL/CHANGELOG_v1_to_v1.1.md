# CHANGELOG: RMM v1 → v1.1

**Release Date:** 2026-06-26
**Release Type:** Bug Fix (Engineering Corrections Only)
**Release Engineer:** Repository Architecture Review Board
**Authority:** Engineering corrections per approved ChangeSet

---

## Summary

| Metric | Value |
|--------|-------|
| Total Engineering Fixes | 21 |
| Owner Normalizations | 19 |
| Dangling Reference Removals | 12 |
| Internal Consistency Fixes | 3 |
| Self-Contradiction Fixes | 2 |
| Metadata Corrections | 3 |
| Affected Entities | 28 of 79 |
| Architecture Changes | 0 (intentional) |

**Classification:** Every fix is an objective engineering correction (contradiction, inconsistency, broken reference, or invalid value). No architectural changes were made.

---

## Critical Fixes: Owner Normalization (19)

Non-canonical owner strings that referenced entities outside the 79-entity catalog were normalized to canonical entities.

| # | Entity | Property | From | To | Trigger |
|---|--------|----------|------|-----|---------|
| 1 | Credential | #4 Owner | Stakeholder | Actor | Stakeholder subsumed into Actor (dedup log) |
| 2 | Signature | #4 Owner | Stakeholder | Actor | Same |
| 3 | Artifact | #4 Owner | Constitution | Process | Constitution is governance, not production entity |
| 4 | Log | #4 Owner | System | Kernel | "System" not in 79-entity catalog |
| 5 | Snapshot | #4 Owner | System | Kernel | Same |
| 6 | AuditTrail | #4 Owner | System | Kernel | Same |
| 7 | Audit | #4 Owner | Independent Auditor | GovernanceBody | Not a canonical entity |
| 8 | Review | #4 Owner | Reviewer (appointed Role) | GovernanceBody | Role instance, not entity type |
| 9 | Standard | #4 Owner | Standards Authority | GovernanceBody | Not a canonical entity |
| 10 | Guideline | #4 Owner | Working Group or Subject Matter Authority | GovernanceBody | Not a canonical entity |
| 11 | Sanction | #4 Owner | Sanctioning authority | GovernanceBody | Not a canonical entity |
| 12 | Approval | #4 Owner | Approver (authorized Role) | Role | Role instance, not entity type |
| 13 | Authorization | #4 Owner | Authorizing authority | GovernanceBody | Not a canonical entity |
| 14 | Certification | #4 Owner | Certifying Authority | GovernanceBody | Not a canonical entity |
| 15 | Amendment | #4 Owner | Proposer | Actor | Not a canonical entity type |
| 16 | Appeal | #4 Owner | Appellant | Actor | Not a canonical entity type |
| 17 | Recusal | #4 Owner | Recusing party or requiring authority | Actor | Not a canonical entity type |
| 18 | Dispute | #4 Owner | Disputing parties or mediating authority | Actor | Not a canonical entity type |
| 19 | Veto | #4 Owner | Veto-holder (Role designated by Constitution or Charter) | Role | Role instance descriptor |

Additional owner normalizations applied:
- **Constitution**: Owner changed from "Founders Circle" to "Constitution" (self-owned, supreme instrument)
- **Interface**: Owner changed from "Owner of the exposing entity" (indirect reference) to "Module" (primary exposer)
- **Escalation**: Owner changed from "Escalating Actor" to "Actor"
- **Precedent**: Owner changed from "GovernanceBody that established it" to "GovernanceBody"
- **Exception**: Owner changed from "Excepted entity's owner or GovernanceBody" to "GovernanceBody"
- **View**: Owner changed from "Governance Board (for canonical views)" to "GovernanceBody (for canonical views)"
- **Concern**: Owner changed from "Governance Board" to "GovernanceBody"
- **Role**: Owner changed from "Governance Board" to "GovernanceBody"
- **Subsystem**: Owner qualifier changed from "assigned by Governance Board" to "assigned by GovernanceBody"
- **Baseline, DecisionRecord, Conclusion, Waiver, Metric, Lifecycle, State**: Owner changed from "Governance" (incomplete) to "GovernanceBody"

---

## Critical Fixes: Dangling Reference Removal (12)

Removed references to non-canonical entities from `Allowed Relationships` fields.

| # | Entity | Removed | Replacement |
|---|--------|---------|-------------|
| 1 | Kernel | Registry | (removed) |
| 2 | Domain | referenced by Namespace; without Bridge | without explicit crossing mechanism |
| 3 | Interface | referenced by Port | (removed) |
| 4 | Boundary | crossed by Bridge, Adapter; exposes Port | crossed by explicit crossing mechanism |
| 5 | Channel | connects Port; belongs to Bus | (removed) |
| 6 | Document | Contains Annotations; composed into Catalog | (removed) |
| 7 | Lifecycle | Has LifecycleStage, LifecycleGate; AppliesTo EntityType | Has Stage, Gate; AppliesTo Entity |
| 8 | State | has EntryAction, ExitAction | has Entry-Action, Exit-Action (properties) |
| 9 | Constraint | Dependency (as entity target) | (removed) |
| 10 | Topology | references Dependency, Channel, Bus | (removed) |
| 11 | Component | circular Dependency | circular dependency (lowercase = relationship) |
| 12 | Module | declares Dependency; defines Namespace | (removed) |

---

## Major Fixes: Internal Consistency (3)

| # | Entity | Property | From | To | Reason |
|---|--------|----------|------|-----|--------|
| 1 | Constitution | #9 Stability | Static | Slow | Constitution is amendable (Versionable:Yes, lifecycle includes AmendmentInProgress); Static contradicts these properties |
| 2 | State | #15 Source of Truth | 01-META-Model/ | 01-META-MODEL/ | Casing inconsistency; all other entries use uppercase MODEL |
| 3 | Environment | #15 Source of Truth | 03-STANDARDS/ | 99-STATE/ | Environment describes runtime surroundings, not standards |

---

## Major Fixes: Self-Contradiction Resolution (2)

| # | Entity | Issue | Resolution |
|---|--------|-------|------------|
| 1 | Artifact | "composed of other Artifacts" (N:M) contradicted "may not be self-referential" | Clarified: "may not be directly self-referential (recursive composition of distinct artifacts is permitted)" |
| 2 | Lifecycle | Lifecycle → has → Lifecycle self-loop created infinite regress | Self-loop removed; Lifecycle's lifecycle is managed by GovernanceBody |

---

## Minor Fixes: Metadata (3)

| # | Location | From | To | Reason |
|---|----------|------|-----|--------|
| 1 | Summary header | 78 CANONICAL ENTITIES | 79 CANONICAL ENTITIES | Count error |
| 2 | Relationship graph header | 30 semantic types | 201 semantic types | Actual count from graph |
| 3 | Document header | Status: FINAL | Status: RELEASED | Reflects actual release status |

---

## Validation Claims Updated

| Claim | v1 Status | v1.1 Status |
|-------|-----------|-------------|
| Every ownership unique | [x] | [x] Every ownership references a canonical entity (19 normalized) |
| No undefined concepts | [x] | [x] No undefined concepts in entity catalog (dangling refs removed) |
| No circular authority | [x] | [x] No circular authority in governance chain |
| Technology-independent | [x] | [~] Technology-independent at conceptual layer; storage paths are deployment-specific |
| No implementation leakage | [x] | [~] Source-of-Truth paths reflect repository structure (by design, non-normative) |

---

## What Was NOT Changed (Intentionally Preserved)

The following were classified as architectural proposals, not engineering defects. They are deferred to `RMM_FUTURE_PROPOSALS.md`:

1. **Entity count remains 79** — No entities added, removed, merged, or split
2. **15-property schema preserved** — No properties added or removed
3. **20-tier organization preserved** — No tier changes
4. **Governance apparatus preserved intact** — No profile tagging or restructuring
5. **Relationship graph structure preserved** — No semantic changes to relationships
6. **All 10 matrices preserved** — No matrix additions or removals
7. **"Radius1" naming preserved where it appears in document title and Kernel definition** — This is a product naming concern, not an engineering defect
8. **Stakeholder column in Matrix 1 preserved** — Removing a matrix column is a structural change
9. **"Runtime" terminology preserved** — Terminology standardization is an editorial concern

---

## References

- **Source:** `RMM_v1.1.md` (RMM v1)
- **Future Proposals:** `RMM_FUTURE_PROPOSALS.md`
- **Validation Report:** `VALIDATION_REPORT.md`

---

*End of Changelog*
