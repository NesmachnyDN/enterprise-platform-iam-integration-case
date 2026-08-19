# ADR-005 — Segregation of Duties and Reconciliation

**Status:** Accepted

## Context

Centralized provisioning alone does not guarantee correct access. Privileged roles can conflict, and actual directory membership can diverge from approved state because of manual changes or failed operations.

## Decision

Maintain explicit Segregation of Duties rules for sensitive role combinations and perform periodic reconciliation between approved entitlements and actual directory membership.

## Consequences

### Positive

- conflicts can be prevented before provisioning;
- out-of-band changes become detectable;
- failed grants/revocations are visible;
- access review is based on evidence rather than assumed workflow correctness.

### Trade-offs

- SoD rules require ownership and maintenance;
- reconciliation findings create an operational remediation queue;
- exceptions need explicit governance.

## Reconciliation outcomes

- `MATCH` — state is consistent;
- `DRIFT` — approved and actual state differ;
- `ORPHAN` — membership lacks a valid entitlement reference;
- `MISSING` — approved entitlement is absent from actual state.
