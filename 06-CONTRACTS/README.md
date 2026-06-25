# 06-CONTRACTS

## Purpose

This directory contains binding agreements between entities: interfaces, commitments, SLAs, and dependency contracts that formalize mutual obligations within the Radius1 Kernel.

## What Belongs Here

- Interface contracts between modules and components
- Service level agreements and commitments
- Dependency contracts and version guarantees
- Obligation and entitlement definitions
- Contract lifecycle records (negotiation, ratification, expiration)

## What Is Forbidden Here

- Governance instruments or policy documents
- Standards or constraints (belong in `03-STANDARDS/`)
- Evidence or audit artifacts (belong in `05-EVIDENCE/`)
- Implementation code
- Unilateral declarations without mutual agreement

## Relation With the Rest of the Repository

- Binds entities defined in `01-META-MODEL/`
- Enforced by constraints in `03-STANDARDS/`
- Compliance verified through `05-EVIDENCE/`
- May be created or modified through `07-WORKFLOW/` processes
