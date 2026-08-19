# Lessons learned

## 1. IAM integration is primarily a boundary-design problem

The key decision is not a connector or API. It is deciding which system owns identity, entitlement lifecycle, group membership, roles and permissions.

## 2. Provisioning and runtime authorization should not be conflated

A system can govern how access is created without participating in every runtime authorization decision. Keeping IAM in the control plane reduces coupling and avoids expanding the runtime failure domain.

## 3. Directory groups make a useful stable contract

A directory group can bridge enterprise access management and application RBAC without forcing IAM to understand every application permission.

The contract is still governed: groups must have owners, catalogue entries and lifecycle rules.

## 4. Application roles remain an application architecture concern

Centralized IAM does not eliminate the need for a good application role model. Poorly designed roles simply become centrally provisioned poor roles.

## 5. Environment separation must exist in entitlements, not only infrastructure

Separate TEST and PROD infrastructure is insufficient if the same entitlement or group silently grants access to both environments.

## 6. Segregation of Duties is cross-system

SoD rules must be traceable from entitlement request through directory membership to effective application permission. A workflow-only check can be bypassed if manual changes are possible elsewhere.

## 7. Reconciliation closes the control loop

Approval and provisioning establish intended state. Reconciliation proves whether actual state still matches that intent.

Without reconciliation, manual changes, partial revocations and stale groups can remain invisible.

## 8. Failure behavior is part of security architecture

Security controls should define their degraded mode. Treating IAM outage as an unspecified exceptional situation can either block the business unnecessarily or create uncontrolled manual workarounds.

## 9. Exceptional access must reconcile back to normal governance

Emergency procedures are sometimes necessary. Their defining property should be that they are time-bounded, attributable and eventually brought back into the governed access model.

## 10. The most useful architecture artifact is a chain of ownership

A reviewer should be able to trace:

```text
Approved business need
        ↓
Enterprise entitlement
        ↓
Directory group
        ↓
Platform role
        ↓
Effective permissions
```

That traceability makes the design understandable to security, operations, IAM and application teams at the same time.