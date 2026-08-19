# ADR-001 — Directory Groups as the Authorization Boundary

**Status:** Accepted

## Context

The enterprise IAM system must manage access to an application platform that already has its own RBAC model. Directly exposing application permissions to IAM would tightly couple two lifecycle models.

## Decision

Represent each managed platform entitlement by an enterprise-directory security group. IAM manages user membership in those groups. The platform maps trusted groups to internal RBAC roles, and roles map to application permissions.

```text
IAM Entitlement → Directory Group → Platform Role → Permissions
```

## Consequences

### Positive

- stable integration contract;
- IAM vendor is decoupled from internal permission implementation;
- centralized membership management;
- auditable mapping;
- easier reconciliation of expected vs actual access.

### Negative / trade-offs

- group catalogue must be governed;
- group/role mapping changes affect multiple users;
- directory propagation/session semantics must be understood operationally.

## Guardrails

- one explicit mapping record for every managed role;
- no reuse of a PROD group for TEST;
- group naming is not the security model — the catalogue and ownership are authoritative;
- stale mappings are detected during review.
