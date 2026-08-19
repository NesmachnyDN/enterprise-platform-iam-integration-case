# ADR-004 — Environment-Specific Role Catalogues

**Status:** Accepted

## Context

The platform has separate TEST and PROD environments. Reusing one entitlement across both makes production access difficult to control and review independently.

## Decision

Model TEST and PROD access as separate entitlement catalogue objects with separate directory groups and mappings, even when the human-readable application role name is similar.

## Consequences

### Positive

- production access is independently approved and reviewable;
- lower risk of accidental privilege inheritance;
- clear environment-level audit trail;
- simpler SoD and reconciliation scope.

### Trade-offs

- larger role/group catalogue;
- more mapping records to maintain;
- users requiring both environments need two explicit entitlements.

## Invariant

No TEST entitlement or directory group grants PROD permissions implicitly.
