<!--
  ============================================
  OPERATIONAL_DOCUMENT_INVENTORY.md — Engineering Kernel
  ============================================
  Classification:   NORMATIVE
  Authority:        Engineering Kernel Architect
  Source of Truth:  05-EVIDENCE/ (per Constitution §10)
  Status:           Active
  Version:          1.0.0
  ============================================
-->

# OPERATIONAL DOCUMENT INVENTORY

## Section A: Document Identification

| Property | Value |
|----------|-------|
| **Title** | Operational Document Inventory |
| **Short** | OPERATIONAL_DOCUMENT_INVENTORY |
| **Classification** | NORMATIVE |
| **Owner** | Engineering Kernel Architect |
| **Source of Truth** | `05-EVIDENCE/` (per Constitution §10) |
| **Status** | Active |
| **Version** | 1.0.0 |
| **Scope** | Acknowledge and inventory 7 operational-layer documents discovered in Phase 1.5 |

---

## Section B: Purpose

This document acknowledges and inventories **7 operational-layer documents** that exist in the repository but are not listed in the `KERNEL_DOCUMENT_REGISTRY.md` (which tracks only 21 canonical documents). These documents were produced during Phase 1.5 (between Phase 1 missions and Phase 2 planning) and are recognized per `REPOSITORY_LAYOUT_SPECIFICATION.md` (SHA `9a051c9e`) §3 LS-CL-03.

These operational documents are **not canonical** in the sense of the 21 registry documents, but they are **authorized** by their MISSION authorities and are **required** for repository operation.

---

## Section C: Operational Document Inventory

### C.1 Governance Documents (2)

| # | Document | SHA | Location | MISSION Authority | Entity | Status |
|---|----------|-----|----------|------------------|--------|--------|
| 1 | `REPOSITORY_INFORMATION_MODEL.md` | `17ff5b1f` | `02-GOVERNANCE/` | MISSION-019 | INFORMATION | Active |
| 2 | `REPOSITORY_LAYOUT_SPECIFICATION.md` | `9a051c9e` | `02-GOVERNANCE/` | MISSION-020 | LAYOUT | Active |

### C.2 Workflow Documents (2)

| # | Document | SHA | Location | MISSION Authority | Entity | Status |
|---|----------|-----|----------|------------------|--------|--------|
| 3 | `KERNEL_BOOT_PROTOCOL.md` | `98a534ff` | `07-WORKFLOW/` | MISSION-022 | BOOT | Active |
| 4 | `AI_EXECUTION_PROTOCOL.md` | `f17a5f31` | `07-WORKFLOW/` | MISSION-021 | EXECUTION | Active |

### C.3 Tool Documents (3)

| # | Document | SHA | Location | MISSION Authority | Entity | Status |
|---|----------|-----|----------|------------------|--------|--------|
| 5 | `KNOWLEDGE_INDEX_SPECIFICATION.md` | `af906dcf` | `09-TOOLS/` | MISSION-024 | KNOWLEDGE | Active |
| 6 | `SKILL_MANIFEST_SPECIFICATION.md` | `c08cb550` | `09-TOOLS/` | MISSION-023 | SKILL | Active |
| 7 | `KERNEL_VALIDATION_PROTOCOL.md` | `4aa531d9` | `09-TOOLS/` | MISSION-025 | VALIDATION | Active |

---

## Section D: Reserved Directory Status

The following directories are defined in Constitution §10 with reserved status:

| Directory | Constitution §10 Assignment | Status | Contents |
|-----------|---------------------------|--------|----------|
| `04-PATTERNS/` | Engineering patterns | Reserved — Empty | None |
| `08-TEMPLATES/` | Document templates | Reserved — Empty | None |
| `09-TOOLS/` | Tool specifications, validation, automation | Reserved — Contains Files | 3 operational documents (see C.3) |

**Note:** The presence of operational documents in `09-TOOLS/` is a known condition. These files were placed by governance decision during Phase 1.5. They are acknowledged here but not modified during Phase 2. The `09-TOOLS/` directory status will be formally resolved during RMM v1.2 (G-05: Storage Abstraction).

---

## Section E: RMM Cross-References

The operational documents reference the following RMM entities but do not define new canonical entities:

| Operational Document | RMM Entities Referenced |
|---------------------|------------------------|
| `REPOSITORY_INFORMATION_MODEL.md` | DOCUMENT, ENTITY, PROPERTY, RELATIONSHIP |
| `REPOSITORY_LAYOUT_SPECIFICATION.md` | DIRECTORY, STRUCTURE, SOT, LIFECYCLE |
| `KERNEL_BOOT_PROTOCOL.md` | SESSION, ACTOR, TASK, BOOT |
| `AI_EXECUTION_PROTOCOL.md` | SESSION, ACTOR, AI, EXECUTION |
| `KNOWLEDGE_INDEX_SPECIFICATION.md` | KNOWLEDGE, INDEX, ARTIFACT |
| `SKILL_MANIFEST_SPECIFICATION.md` | SKILL, MANIFEST, CAPABILITY |
| `KERNEL_VALIDATION_PROTOCOL.md` | VALIDATION, CHECK, EVIDENCE |

None of these documents introduce new entities to the 79-entity RMM catalog.

---

## Section F: Relationship to Canonical Registry

| Aspect | Canonical Registry (21 docs) | Operational Documents (7 docs) |
|--------|------------------------------|-------------------------------|
| **Classification** | CANONICAL | NORMATIVE / PROCEDURAL |
| **Authority** | Constitution | MISSION Authority |
| **Registry Entry** | Listed in KDR | Listed in this inventory only |
| **RMM Modification** | No | No |
| **Entity Introduction** | No | No |
| **Phase 2 Modification** | Registry updated | Acknowledged only |
| **SOT Directory** | Per RMM #15 | Per RLS §3 LS-CL-03 |

---

## Section G: Revision History

| Version | Date | Authority | Change | Mission | Description |
|---------|------|-----------|--------|---------|-------------|
| 1.0.0 | 2026-06-27 | Engineering Kernel Architect | Added | P2-M07 | Initial inventory of 7 operational-layer documents |

---

*END OF OPERATIONAL DOCUMENT INVENTORY*
