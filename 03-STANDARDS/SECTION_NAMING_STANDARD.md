<!--
  ============================================
  SECTION_NAMING_STANDARD.md — Engineering Kernel
  ============================================
  Classification:   NORMATIVE
  Authority:        GovernanceBody
  Source of Truth:  03-STANDARDS/ (per Constitution §10)
  Status:           Active
  Version:          1.0.0
  ============================================
-->

# SECTION NAMING STANDARD

## Section A: Document Identification

| Property | Value |
|----------|-------|
| **Title** | Section Naming Standard |
| **Short** | SECTION_NAMING_STANDARD |
| **Classification** | NORMATIVE |
| **Owner** | GovernanceBody |
| **Source of Truth** | `03-STANDARDS/` (per Constitution §10) |
| **Status** | Active |
| **Version** | 1.0.0 |

---

## Section B: Problem Statement

ISSUE-015 (CONFIRMED) identifies that documents in the Engineering Kernel use **inconsistent section naming schemes**:

- Some documents use **lettered sections** (A, B, C, D, E, F, G, H, I, J)
- Some documents use **numbered sections** (1, 2, 3, ... with decimal subsections)
- Some documents use **mixed schemes** (lettered Part I + numbered Part II)
- `DOCUMENT_STANDARD_SPEC.md` defines a **10-section numbered format** (3.1–3.10) that no document currently follows exactly

This inconsistency creates navigation friction, complicates automated parsing, and weakens the impression of a unified engineering system.

---

## Section C: Current State Inventory

### C.1 Naming Scheme Classification

| Scheme | Description | Documents Using | Count |
|--------|-------------|----------------|-------|
| **Lettered A–J** | Sections labeled A through J; may have numbered subsections | KGM, KRM, KDM, KAM, KEM, REVIEW, LIFECYCLE, DECISION, CHARTER | 9 |
| **Numbered** | Top-level sections numbered 1, 2, 3... with decimal subsections | CONSTITUTION, AFM, KSD, RMMFP, CER, P2MP, KSC | 7 |
| **Mixed** | Lettered top-level + numbered checks/sections | CDV, UMT | 2 |
| **Lettered + Part Division** | Lettered Part I (meta) + numbered Part II (provisions) | KPM | 1 |

### C.2 Detailed Inventory

#### Lettered A–J Documents (9 documents)

| # | Document | Location | Current Scheme | Sections |
|---|----------|----------|---------------|----------|
| 1 | `KERNEL_GOVERNANCE_MODEL.md` | `02-GOVERNANCE/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 2 | `KERNEL_ROLE_MODEL.md` | `00-CONSTITUTION/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 3 | `KERNEL_DECISION_MODEL.md` | `05-EVIDENCE/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 4 | `KERNEL_REVIEW_MODEL.md` | `05-EVIDENCE/Reviews/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 5 | `KERNEL_AMENDMENT_MODEL.md` | `02-GOVERNANCE/Amendments/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 6 | `KERNEL_EVIDENCE_MODEL.md` | `05-EVIDENCE/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 7 | `REPOSITORY_LIFECYCLE_MODEL.md` | `01-META-MODEL/Lifecycles/` | A–J + numbered sub | A, B, C, D, E, F, G, H, I, J |
| 8 | `KERNEL_CHARTER.md` | `00-CONSTITUTION/Charters/` | A–J + numbered sub + Roman | A–J, with Roman numeral sub-parts |
| 9 | `KERNEL_PROCESS_MODEL.md` | `07-WORKFLOW/` | A–J Part I + numbered Part II | A–J (Part I), 1–14 (Part II) |

#### Numbered Documents (7 documents)

| # | Document | Location | Current Scheme | Sections |
|---|----------|----------|---------------|----------|
| 10 | `CONSTITUTION.md` | `00-CONSTITUTION/` | Numbered 1–16 | 1–16 with decimal subsections |
| 11 | `ARTIFACT_FAMILY_MODEL.md` | `01-META-MODEL/` | Numbered 1–13 | 1–13 with decimal subsections |
| 12 | `KERNEL_SCOPE_DEFINITION.md` | `01-META-MODEL/` | Numbered 1–16 | 1–16 with decimal subsections |
| 13 | `RMM_FUTURE_PROPOSALS.md` | `01-META-MODEL/` | Numbered categories + lettered items | Categories A–G with numbered/lettered proposals |
| 14 | `CONSTITUTIONAL_EXECUTION_REPORT.md` | `05-EVIDENCE/` | Numbered 1–9 | 1–9 with decimal subsections |
| 15 | `PHASE_2_MASTER_PLAN.md` | `03-PLANNING/` | Numbered 1–10 + lettered appendices | 1–10, Appendices A–E |
| 16 | `DOCUMENT_STANDARD_SPEC.md` | `01-META-MODEL/` | Numbered 3.1–3.10 | 3.1–3.10 (DSS format) |

#### Mixed Documents (2 documents)

| # | Document | Location | Current Scheme | Sections |
|---|----------|----------|---------------|----------|
| 17 | `CROSS_DOCUMENT_VALIDATOR.md` | `03-STANDARDS/` | Lettered A–H + numbered CHECK-1–8 | A–H top-level, CHECK-1–8 within |
| 18 | `UNSUPPORTED_MARKER_TRACKER.md` | `03-STANDARDS/` | Lettered A–H + numbered D.1–D.12 | A–H top-level, D.1–D.12 within |

### C.3 Summary Statistics

| Scheme | Count | Percentage |
|--------|------:|-----------:|
| Lettered A–J | 9 | 50% |
| Numbered | 7 | 39% |
| Mixed | 2 | 11% |
| **Total** | **18** | **100%** |

(Note: 10 of 28 documents are not entity-model documents and are not included in this inventory; operational-layer documents use their own conventions.)

---

## Section D: Authoritative Standard

### D.1 Dual Convention Standard

The Engineering Kernel adopts a **dual convention** approach: the naming scheme is determined by **document type**, not universal mandate. This respects the different structural needs of different document categories while ensuring consistency within each category.

### D.2 Convention Rules

| Document Type | Naming Scheme | Rationale | Examples |
|--------------|---------------|-----------|----------|
| **Entity-Defining Documents** | Lettered A–J (10 sections) | Entity models follow a standard 10-section meta-structure; letters are semantically neutral and accommodate the fixed 10-section format | KGM, KRM, KDM, KAM, KEM, REVIEW, LIFECYCLE, DECISION, CHARTER |
| **Constitutional Documents** | Numbered | Constitutional documents are read sequentially; numbering reflects logical dependency order | CONSTITUTION |
| **Standards/Specifications** | Numbered with decimals | Standards have hierarchical structure; decimal numbering supports deep nesting | AFM, KSD, KSC, DSS |
| **Plans and Reports** | Numbered + Lettered Appendices | Main body is sequential; appendices are reference material | P2MP, CER |
| **Procedural Checklists** | Lettered framework + Numbered checks | Framework provides structure; checks are executable items | CDV |
| **Trackers/Registries** | Lettered framework + Numbered items | Framework provides structure; items are catalog entries | UMT, KDR |
| **Proposals/Backlogs** | Lettered categories + Numbered items | Categories are thematic; items are sequential within category | RMMFP |

### D.3 Entity-Defining Document 10-Section Standard

All entity-defining documents SHALL use the following A–J section mapping:

| Section | Title | Required Content |
|---------|-------|-----------------|
| **A** | Document Identification | Title, Short Name, Entity, Classification, Owner, SOT, Status, Version |
| **B** | Entity Properties | RMM #1–#15 summary table, Stability, Versionable, Freezable, AI/Human permissions |
| **C** | Classification and Scope | Classification basis, scope statement, jurisdiction |
| **D** | Status and Lifecycle | Document status, entity lifecycle diagram, lifecycle states table |
| **E** | Version | Version number, scheme, baseline description |
| **F** | Ownership and Authority | Owner, authority derivation, authority scope table, cardinality |
| **G** | Dependencies | Normative references table, forbidden dependencies |
| **H** | Change Log | Version history table |
| **I** | Approval | Approval status, approver, date, method, conditions |
| **J** | RMM Property Manifest | All 15 RMM properties with document reference mapping |

**After Section J:** Part II with numbered provisions (1, 2, 3...) containing the entity's normative content.

### D.4 Constitutional Document Section Standard

Constitutional documents SHALL use numbered sections with the following structure:

| Section | Title | Required Content |
|---------|-------|-----------------|
| **1** | Preamble/Header | Document metadata, supremacy statement |
| **2** | Principles | Immutable principles (P-1 through P-N) |
| **3** | Scope | In-scope and out-of-scope domains |
| **4** | Authority | Authority chain, delegation rules |
| **5** | Governance | Governance body definitions and procedures |
| **6** | Lifecycle | Freeze/unfreeze mechanisms |
| **7** | Amendments | Amendment procedure (or [UNSUPPORTED] if undefined) |
| **8** | Transition | Phase transition rules |
| **9+** | Specific Content | Document-specific provisions |

### D.5 Standard/Specification Document Section Standard

Standards and specifications SHALL use numbered sections with decimal subsections:

| Section | Title |
|---------|-------|
| **1** | Purpose |
| **2** | Scope |
| **3** | Normative References |
| **4** | Terms and Definitions |
| **5** | Requirements/Specifications |
| **6** | Validation/Verification |
| **7** | Constraints |
| **8** | Examples (optional) |
| **9** | Appendices (optional) |

---

## Section E: Harmonization Plan

### E.1 Documents Requiring Harmonization

| Priority | Document | Current Scheme | Target Scheme | Action |
|----------|----------|---------------|---------------|--------|
| P1 | `CONSTITUTION.md` | Numbered 1–16 (deviates: has lettered subsections in some areas) | Numbered 1–N (consistent) | Normalize: ensure all subsections use decimal numbering, no lettered subsections |
| P1 | `KERNEL_CHARTER.md` | A–J + Roman numerals | Lettered A–J (standard) | Normalize: convert Roman numeral sub-parts to decimal subsections |
| P2 | `RMM_FUTURE_PROPOSALS.md` | Mixed (lettered categories + varied item numbering) | Lettered categories + consistent numbered items | Normalize: standardize proposal numbering within each category |
| P2 | `PHASE_2_MASTER_PLAN.md` | Numbered 1–10 + lettered appendices | Numbered + lettered appendices (already standard) | No change needed |
| P3 | `ARTIFACT_FAMILY_MODEL.md` | Numbered 1–13 | Numbered 1–N (already standard) | No change needed |
| P3 | `KERNEL_SCOPE_DEFINITION.md` | Numbered 1–16 | Numbered 1–N (already standard) | No change needed |
| P3 | `CONSTITUTIONAL_EXECUTION_REPORT.md` | Numbered 1–9 | Numbered 1–N (already standard) | No change needed |
| P4 | All entity-defining docs | Lettered A–J (already standard) | Lettered A–J | No change needed |

### E.2 Harmonization Sequence

```
Step 1: CONSTITUTION.md subsection normalization
    |
Step 2: KERNEL_CHARTER.md Roman numeral conversion
    |
Step 3: RMM_FUTURE_PROPOSALS.md proposal numbering standardization
    |
Step 4: Verify all documents conform to dual convention
    |
Step 5: Update DOCUMENT_STANDARD_SPEC.md to reference this standard
```

### E.3 No-Change Documents

The following documents already conform to their document-type standard and require no harmonization:

| Document | Current Scheme | Standard | Status |
|----------|---------------|----------|--------|
| `KERNEL_GOVERNANCE_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_ROLE_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_DECISION_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_REVIEW_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_AMENDMENT_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_EVIDENCE_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `REPOSITORY_LIFECYCLE_MODEL.md` | A–J | Entity-Defining: A–J | ✅ Conformant |
| `KERNEL_PROCESS_MODEL.md` | A–J + numbered Part II | Entity-Defining: A–J + Part II | ✅ Conformant |
| `CROSS_DOCUMENT_VALIDATOR.md` | A–H + CHECK-1–8 | Procedural: Lettered + Numbered checks | ✅ Conformant |
| `UNSUPPORTED_MARKER_TRACKER.md` | A–H + D.1–D.12 | Tracker: Lettered + Numbered items | ✅ Conformant |
| `DOCUMENT_STANDARD_SPEC.md` | 3.1–3.10 | Standard: Numbered decimals | ✅ Conformant |

---

## Section F: Validation

### F.1 Acceptance Criteria

| # | Criterion | Method | Pass Condition |
|---|-----------|--------|----------------|
| 1 | All 18 inventoried documents classified by scheme | Inventory check | Each document has assigned target scheme |
| 2 | Dual convention documented | Standard review | Convention rules table exists with rationale |
| 3 | Entity-defining 10-section standard defined | Section mapping check | A–J mapping table exists with required content |
| 4 | Harmonization sequence defined | Sequence review | Ordered steps with dependencies |
| 5 | No document modified without explicit instruction | Safety check | Plan documents only; no file edits |
| 6 | Zero frozen artifacts modified | SHA check | RMM and Constitution unchanged |

### F.2 Conformance Checklist

| Document | Scheme | Conforms | Harmonization Required |
|----------|--------|----------|----------------------|
| Entity-defining docs (9) | A–J | Yes | No |
| CONSTITUTION.md | Numbered | Partial (subsections) | Yes (subsections) |
| CHARTER.md | A–J | Partial (Roman numerals) | Yes (Roman numerals) |
| Standards (3) | Numbered decimals | Yes | No |
| Plans/Reports (2) | Numbered + Appendices | Yes | No |
| RMMFP.md | Mixed | Partial (item numbering) | Yes (item numbering) |
| Procedural (1) | Lettered + Numbered | Yes | No |
| Trackers (1) | Lettered + Numbered | Yes | No |

---

## Section G: Relationship to Other Standards

| Document | Relationship |
|----------|-------------|
| `DOCUMENT_STANDARD_SPEC.md` | This standard complements DSS by defining section naming conventions; DSS defines section content requirements |
| `KERNEL_STRUCTURE_SPEC.md` | Structure Spec defines repository layout; this standard defines document internal structure |
| `CROSS_DOCUMENT_VALIDATOR.md` | CHECK-2 (Section Naming Consistency) validates against this standard |

---

## Section H: Revision History

| Version | Date | Authority | Change | Mission | Description |
|---------|------|-----------|--------|---------|-------------|
| 1.0.0 | 2026-06-27 | GovernanceBody | Added | P2-M05 | Initial section naming standard; dual convention defined; harmonization plan created |

---

*END OF SECTION NAMING STANDARD*
