# Reconciliation Rules

## Objective

Detect divergence between approved entitlement state and actual directory membership.

## Comparison keys

Each comparison uses:

- target identity;
- entitlement ID;
- environment;
- expected directory group;
- actual membership;
- entitlement validity period.

## Findings

| Code | Condition | Default action |
|---|---|---|
| MATCH | approved entitlement and actual membership agree | none |
| MISSING | approved entitlement exists but group membership is absent | retry provisioning / investigate |
| DRIFT | actual group differs from entitlement mapping | investigate configuration or manual change |
| ORPHAN | group membership exists with no valid entitlement | revoke unless formalized through approved process |
| EXPIRED | time-bounded entitlement is past expiry | deprovision immediately |
| ROLE_MAP_ERROR | directory group has no valid platform-role mapping | quarantine mapping change and investigate |
| SOD_CONFLICT | actual assignments violate current SoD rule | remediate or approve explicit exception |

## Priority

Recommended remediation priority:

1. failed/expired revocation;
2. unexplained privileged ORPHAN;
3. DENY SoD conflict;
4. role mapping error;
5. missing approved grant;
6. non-privileged drift.

## Governance rule

Reconciliation does not silently rewrite approved state to match actual state. A discrepancy is a finding requiring either remediation of actual access or a governed change to the entitlement record.
