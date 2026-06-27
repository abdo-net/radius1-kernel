# 00-CONSTITUTION

**Status:** CANONICAL  
**Stability:** Static  
**Owner:** Constitution (self-owned)

---

## Purpose

This directory contains the supreme governance instrument of the Engineering Kernel — the Constitution. The Constitution establishes the fundamental principles, authority structures, and amendment procedures that provide legitimacy for all governance actions across the entire system.

## Contents

| Document | Purpose |
|----------|---------|
| `Constitution.md` | The supreme governance instrument — fundamental principles, authority structures, and amendment procedures |
| `Charters/` | Chartered governance bodies — scope of authority, decision rights, membership, and dissolution conditions |

## Key Principles

1. **Supremacy** — The Constitution overrides all other governance instruments in case of conflict.
2. **Self-Ownership** — The Constitution is owned by itself; it may only be amended by its own amendment procedure.
3. **Non-Overrideable** — No entity may override the Constitution except by its own amendment procedure.
4. **Legitimacy Source** — The Constitution provides the ultimate source of legitimacy for all governance actions.

## Governance Chain

```
Constitution → Charter → GovernanceBody → Role → Actor → Session → Task
```

The governance chain is a verified DAG with no circular authority. All ownership ultimately traces back to the Constitution.

## Entity Definitions

This directory defines the following canonical entities (Tiers 6+):

- **Constitution** (Tier 6) — Supreme governance instrument
- **Charter** (Tier 6) — Authority establishment for governance bodies
- **Role** (Tier 6) — Named responsibilities, permissions, and authority boundaries

---

*The Constitution may not be overridden by any entity except by its own amendment procedure. Changes require human approval with governance body ratification.*
