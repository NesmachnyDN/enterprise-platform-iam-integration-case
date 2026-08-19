# Access Review Checklist

Use this checklist for a periodic review of managed platform access.

## Catalogue

- [ ] Every active entitlement has an owner.
- [ ] Every entitlement maps to exactly one intended directory group for its environment.
- [ ] Every directory group maps to a valid platform role.
- [ ] TEST and PROD mappings are distinct.
- [ ] Obsolete roles/groups are marked for retirement.

## User access

- [ ] Each privileged membership has a valid approved entitlement reference.
- [ ] Temporary access has a valid expiry date.
- [ ] Users who changed role/team have been reviewed.
- [ ] Leavers and inactive identities are not present in managed groups.
- [ ] No unexplained direct/manual membership exists.

## Segregation of Duties

- [ ] Current assignments are evaluated against the SoD matrix.
- [ ] DENY conflicts have no active unapproved exceptions.
- [ ] WARN exceptions are time-bounded and explicitly approved.
- [ ] Access Controllers remain independent from the privileges they review.

## Reconciliation

- [ ] Approved entitlements and actual group membership were compared.
- [ ] `DRIFT`, `ORPHAN`, and `MISSING` findings have owners.
- [ ] Failed revocations are prioritized.
- [ ] Manual emergency changes have post-event reconciliation evidence.

## Evidence

- [ ] Request and approval records are traceable.
- [ ] Provisioning/deprovisioning results are recorded.
- [ ] Review decision and reviewer are recorded.
- [ ] Remediation actions are linked to findings.
