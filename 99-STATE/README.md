# 99-STATE

**Status:** CANONICAL  
**Stability:** Fast  
**Owner:** Session

---

## Purpose

This directory contains runtime state, session management, and operational context for the RADIUS1 Kernel. It captures the dynamic, temporal aspects of the system that change during operation.

## Contents

| Subdirectory | Purpose |
|-------------|---------|
| `Context/` | Situational frames for entity interpretation and access |
| `View/` | Perspective-specific representations of the kernel structure |
| `Sessions/` | Active and historical session records |

## Key Entities

- **Session** (Tier 8) — Bounded period of engagement during which actors perform work
- **Context** (Tier 9) — Situational frame for entity interpretation and execution
- **Environment** (Tier 9) — Complete operational surroundings for process execution
- **Participant** (Tier 8) — Binding of Actor to Session with role assignments
- **View** (Tier 20) — Perspective-specific representation of kernel structure

## State Lifecycle

```
Created → Active → Modified → Saved → Discarded
```

---

*State is fast-moving and session-scoped. State entities may not persist beyond the situation they represent and may not override frozen invariants. This directory is the runtime workspace; persistent truths belong in their canonical source-of-truth locations.*
