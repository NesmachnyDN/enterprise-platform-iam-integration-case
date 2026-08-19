# ADR-002 — No Direct Runtime Dependency on IAM

**Status:** Accepted

## Context

IAM is required to grant, change and revoke access, but the enterprise platform already authenticates users against the enterprise directory and can resolve directory groups into RBAC roles.

Making every runtime access decision depend on IAM would increase the platform's critical dependency chain.

## Decision

Do not introduce a direct runtime `Enterprise Platform → IAM` dependency. IAM changes directory-group membership in the control plane. Runtime authentication and role resolution use the enterprise directory.

## Consequences

### Positive

- IAM outage does not automatically make the application unavailable;
- smaller runtime blast radius;
- simpler platform integration boundary;
- reduced vendor coupling.

### Trade-offs

- access changes may be delayed while IAM is unavailable;
- revocation latency depends on directory/session behavior;
- directory availability becomes a critical runtime dependency.

## Failure rule

During an IAM outage, normal provisioning/deprovisioning is considered degraded. Existing access remains valid while the directory and platform are operational. Any emergency access change is handled as an explicit governed exception and reconciled afterward.
