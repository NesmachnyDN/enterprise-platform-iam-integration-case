# Architecture diagram sources

This directory contains Mermaid sources for the architecture views used by the case. Rendered portfolio-grade SVG views are stored in [`../assets/`](../assets/).

| File | View |
|---|---|
| `control-runtime-plane.mmd` | Separation of IAM control plane and platform runtime plane |
| `access-provisioning-sequence.mmd` | Access request and provisioning sequence |
| `approval-workflow.mmd` | Governed approval flow before provisioning |
| `role-mapping.mmd` | Directory-group to platform-role mapping |
| `access-lifecycle.mmd` | Governed access lifecycle |
| `sod-model.mmd` | Example Segregation of Duties conflicts |
| `iam-failure-model.mmd` | Degraded mode when IAM is unavailable |

Main rendered views:

- [`control-runtime-architecture.svg`](../assets/control-runtime-architecture.svg)
- [`role-governance.svg`](../assets/role-governance.svg)
- [`access-lifecycle.svg`](../assets/access-lifecycle.svg)
- [`iam-failure-model.svg`](../assets/iam-failure-model.svg)
- [`enterprise-platform-iam-social-preview.svg`](../assets/enterprise-platform-iam-social-preview.svg)

All diagrams are synthetic. They do not reproduce any corporate diagram, source file, system identifier or original document layout.