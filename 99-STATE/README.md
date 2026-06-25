# 99-STATE

## Purpose

This directory contains runtime state, ephemeral data, session records, and operational snapshots that capture the current or historical operational condition of the Radius1 Kernel.

## What Belongs Here

- Session records and state captures
- Runtime configuration snapshots
- Operational metrics and measurements
- Temporary state data and checkpoint records
- Historical state archives

## What Is Forbidden Here

- Permanent specifications or standards
- Governance instruments or policy documents
- Evidence or audit artifacts (belong in `05-EVIDENCE/`)
- Implementation code or tool configurations (belong in `09-TOOLS/`)
- Anything intended to be immutable or canonical

## Relation With the Rest of the Repository

- Captures runtime instances of entities defined in `01-META-MODEL/`
- Reflects the current operational state governed by `02-GOVERNANCE/`
- May be analyzed using tools in `09-TOOLS/`
- Snapshots may become evidence in `05-EVIDENCE/`
- All content in this directory is ephemeral and subject to expiration
