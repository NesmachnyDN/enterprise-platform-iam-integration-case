# Access reconciliation model

## Objective

Verify that effective platform access remains traceable to approved entitlements.

## Comparison chain

```text
Approved entitlement
      ↓
Expected directory group membership
      ↓ compare
Actual directory group membership
      ↓
Resolved platform role
```

## Result states

| State | Meaning | Action |
|---|---|---|
| MATCH | Approved and actual states agree | retain evidence |
| MISSING | Approved entitlement exists but expected membership is absent | investigate provisioning failure |
| DRIFT | Actual membership exists but differs from governed expectation | investigate manual/incorrect change |
| ORPHAN | Group/role has no valid catalogue relationship | remove or formalize mapping |
| CONFLICT | Effective roles violate SoD rule | revoke/adjust or approve documented exception |

## Minimum reconciliation dataset

- user identifier;
- entitlement identifier;
- role identifier;
- environment;
- expected group;
- actual group membership;
- effective platform role;
- approval/reference identifier;
- validity/review date;
- SoD result.

## Frequency

The synthetic case does not prescribe one universal frequency. Privileged production access should normally be reviewed more frequently than standard access. The role catalogue carries the review policy.

## Exception reconciliation

Any manual access change made during a control-plane incident must appear as drift until it is either:

1. converted into a governed entitlement; or
2. removed.

An exception is not considered closed merely because the incident has ended.