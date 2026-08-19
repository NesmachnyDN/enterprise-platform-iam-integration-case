# ADR-003 — Workflow-Governed Access Provisioning

**Status:** Accepted

## Context

Privileged and business access must be attributable to an approved request rather than unmanaged administrator actions.

## Decision

Normal grants, changes and revocations originate from an access-request workflow. Approval uses responsibility blocks such as requester management, security and resource owner where applicable. IAM executes the approved entitlement transition.

## Consequences

### Positive

- traceable decision chain;
- consistent access process;
- separation between approval and technical execution;
- supports audit and periodic review.

### Trade-offs

- access changes depend on workflow and IAM control-plane availability;
- approval design requires maintained organizational ownership;
- excessive approval depth can increase lead time.

## Design rule

Approval schemes should reference organizational roles/functions where practical rather than individual employee names, reducing maintenance caused by personnel changes.
