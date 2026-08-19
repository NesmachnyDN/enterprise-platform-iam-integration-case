# Centralized IAM Integration for an Enterprise Platform

**Architecture case study for integrating Enterprise IAM / IdM, an enterprise directory, and application RBAC**

[Русская версия](README.md)

![Case cover](assets/enterprise-platform-iam-social-preview.svg)

> A synthetic public architecture case based on practical experience designing centralized access management for an enterprise platform. All names, roles, systems, groups, and data in this repository are fictional and created specifically for the portfolio.

## Executive summary

An enterprise platform owns its RBAC model while access lifecycle must be governed centrally through request, approval, provisioning, revocation and periodic reconciliation.

The architectural problem is not simply to “connect the application to IAM.” It is to separate **authentication**, **authorization**, **provisioning/deprovisioning**, and **access governance**.

Core principle:

> **IAM manages access state but does not become a mandatory runtime dependency of the business platform.**

This reduces coupling: an IAM outage can temporarily stop new assignments and revocations but should not automatically block existing users while the enterprise directory and platform remain available.

## My role

**Solution Architect / Author of the Technical Solution**

Responsibilities represented by this case include control/runtime separation, directory-group-to-role mapping, access lifecycle, Segregation of Duties, IAM failure behavior, access reconciliation and architecture acceptance criteria.

The origin and authorship boundary is documented in [ORIGIN.md](ORIGIN.md).

## 1. Control Plane vs Runtime Plane

![Control Plane and Runtime Plane](assets/control-runtime-architecture.svg)

**Control plane:** request → approval → IAM → enterprise-directory group membership.

**Runtime plane:** user → enterprise directory → enterprise platform → RBAC.

The stable architecture boundary is the **directory security group**. IAM manages membership; the platform maps the group to its application role. Direct runtime communication `Platform → IAM` is not required.

See [Architecture](docs/architecture.md).

## 2. Access model

```text
Authentication
User → Enterprise Directory → Enterprise Platform

Authorization
Directory Group → Platform Role → Permissions

Provisioning
Access Request → Approval → IAM → Directory Group Membership

Deprovisioning
IAM → Remove Group Membership → Access Revoked

Governance
Role Catalogue → SoD Rules → Reconciliation → Review
```

## 3. Role Governance and Segregation of Duties

![Role governance](assets/role-governance.svg)

The platform does not receive arbitrary low-level permissions directly from IAM. The stable contract is:

```text
IAM Entitlement → Directory Group → Platform Role → Permissions
```

Synthetic example:

| Directory Group | Platform Role | Environment | Purpose |
|---|---|---|---|
| PLT-PRD-OPS | Platform Operator | PROD | operational administration |
| PLT-PRD-SEC | Security Administrator | PROD | security administration |
| PLT-PRD-AUD | Access Controller | PROD | access review and audit |
| PLT-PRD-INT | Integration Administrator | PROD | integration configuration |
| PLT-TST-OPS | Platform Operator | TEST | test operations |
| PLT-TST-TESTER | Tester | TEST | functional testing |

Synthetic data: [role catalogue](data/role-catalog.csv) · [SoD matrix](data/sod-matrix.csv) · [access requests](data/access-request-examples.csv).

## 4. Governed access lifecycle

![Access lifecycle](assets/access-lifecycle.svg)

**Request → Approval → Provision → Use → Reconciliation → Review → Revoke/Retain**.

Access remains traceable after provisioning and can be reviewed and centrally revoked.

## 5. IAM failure containment

![IAM failure containment](assets/iam-failure-model.svg)

IAM belongs to the **control plane**, so its failure should not unnecessarily propagate to runtime access. Normal assignments, changes and revocations degrade; existing governed access continues while the directory and platform remain healthy; exceptional manual changes must be reconciled after recovery.

See [Resilience & Controls](docs/resilience-and-controls.md).

## 6. Reconciliation

```text
Approved Entitlements
        │
        ▼
Expected Directory Membership
        │
        ▼ compare
Actual Directory Membership
        │
        ▼
Resolved Platform Roles
        │
        ▼
MATCH / MISSING / DRIFT / ORPHAN / CONFLICT
```

Reconciliation detects manual drift, incomplete revocation, provisioning errors and orphaned mappings.

## Architecture decisions

- [ADR-001 — Directory Groups as the Authorization Boundary](decisions/ADR-001-directory-groups-as-authorization-boundary.md)
- [ADR-002 — No Direct Runtime Dependency on IAM](decisions/ADR-002-no-runtime-dependency-on-iam.md)
- [ADR-003 — Workflow-Governed Access Provisioning](decisions/ADR-003-workflow-governed-provisioning.md)
- [ADR-004 — Environment-Specific Role Catalogues](decisions/ADR-004-environment-specific-role-catalogues.md)
- [ADR-005 — Segregation of Duties and Reconciliation](decisions/ADR-005-sod-and-reconciliation.md)

## Repository map

| Area | Content |
|---|---|
| [Context & Drivers](docs/context-and-drivers.md) | problem, constraints and drivers |
| [Architecture](docs/architecture.md) | control plane, runtime plane and integration boundaries |
| [Access Lifecycle](docs/access-lifecycle.md) | request → approval → provision → review → revoke |
| [Role Governance](docs/role-governance.md) | role catalogue, mapping and SoD |
| [Resilience & Controls](docs/resilience-and-controls.md) | IAM outages, exceptions and reconciliation |
| [Lessons Learned](docs/lessons-learned.md) | generalized architecture lessons |
| [Architecture Decisions](decisions/) | five ADRs |
| [Synthetic Data](data/) | fictional role mapping, SoD and access requests |
| [Governance](governance/) | readiness checklist and reconciliation model |
| [Architecture Sources](architecture/) | Mermaid diagram sources |

## Disclaimer

**This repository contains only synthetic, newly created portfolio material.**

It contains no corporate documents, original diagrams, employer or customer names, internal system identifiers, domains, accounts, network parameters, real security groups, or operational instructions. The public architecture is an independent reconstruction of professional experience.