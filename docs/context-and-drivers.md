# Context and architecture drivers

## Context

A large enterprise platform exposes operational, integration and security functions to several categories of users. The platform has its own RBAC model, but corporate policy requires user access to be issued and revoked through a centralized identity-and-access-management process.

The public scenario assumes the following synthetic enterprise capabilities:

- an **Access Request Portal** for submitting access requests;
- an **Approval Workflow** for business and security approval;
- an **Enterprise IAM / IdM** system for provisioning and deprovisioning;
- an **Enterprise Directory** used for authentication and security-group membership;
- an **Enterprise Platform** with internal RBAC.

The design intentionally avoids a direct runtime dependency between the platform and IAM.

## Problem statement

A naive design can make IAM part of every login or authorization decision. That creates unnecessary coupling and expands the failure domain: if IAM is unavailable, the business platform may become unavailable even though the user identity, directory and application are healthy.

The target architecture must centralize access lifecycle without making the lifecycle-management tool part of the application runtime path.

## Architecture drivers

| Driver | Architecture consequence |
|---|---|
| Centralized access lifecycle | Provisioning and revocation are executed through IAM |
| Enterprise authentication | The platform trusts the enterprise directory for user identity |
| Application-specific authorization | Platform permissions remain expressed as platform roles |
| Low runtime coupling | IAM is excluded from the login and normal authorization path |
| Auditable access requests | Entitlements originate from approved requests |
| Stable integration contract | Directory groups bridge IAM entitlements and platform RBAC |
| Environment isolation | TEST and PROD use separate group/role catalogues |
| Least privilege | Roles are purpose-specific and contain bounded permissions |
| Segregation of Duties | Selected role combinations are prohibited or require exception approval |
| Drift detection | Expected access is periodically compared with actual directory membership and resolved roles |
| IAM outage containment | Existing runtime access continues when directory and platform remain available |
| Controlled exceptions | Emergency manual changes are exceptional, logged and reconciled later |

## Quality attributes

### Availability

IAM failure should affect **access administration**, not automatically the **runtime availability of the enterprise platform**.

### Security

All access must be traceable from approved entitlement to directory group and platform role. Administrative conflicts must be explicitly modeled.

### Auditability

For each effective role, the organization should be able to determine:

1. which directory group grants it;
2. which approved entitlement caused group membership;
3. who approved the request;
4. when the entitlement should expire or be reviewed;
5. whether the actual state matches the expected state.

### Maintainability

The IAM integration should not need to know platform-internal permission details. IAM manages named entitlements/groups; the platform owns the mapping from role to permissions.

## Scope

Included:

- access request and approval lifecycle;
- provisioning/deprovisioning boundary;
- enterprise-directory integration;
- platform RBAC mapping;
- environment separation;
- SoD;
- reconciliation;
- IAM outage behavior.

Out of scope:

- specific IAM vendor products;
- directory topology;
- password policy and MFA implementation;
- privileged-access-management product design;
- network topology;
- real organizational approval chains;
- real service accounts, domains and group names.