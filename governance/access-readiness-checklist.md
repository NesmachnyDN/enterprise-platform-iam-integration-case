# Access architecture readiness checklist

Use this checklist before enabling centralized provisioning for a platform role.

## Catalogue

- [ ] Role has a stable identifier.
- [ ] Role purpose is documented.
- [ ] Target environment is explicit.
- [ ] Role owner is assigned.
- [ ] Privilege class is defined.
- [ ] Approval policy is defined.
- [ ] Review period is defined.

## Directory mapping

- [ ] Directory group exists.
- [ ] Group naming matches environment convention.
- [ ] Group maps to exactly the intended platform role.
- [ ] No orphan/duplicate mapping exists.

## Provisioning

- [ ] IAM entitlement maps to the correct group.
- [ ] Add-membership operation is tested.
- [ ] Remove-membership operation is tested.
- [ ] Provisioning result is auditable.
- [ ] Failure/retry behavior is defined.

## Authorization

- [ ] Platform resolves the group into the intended role.
- [ ] Role grants only expected permissions.
- [ ] TEST and PROD mappings are isolated.
- [ ] Authentication does not require a runtime IAM call.

## Governance

- [ ] SoD conflicts are defined.
- [ ] Privileged-role approval is appropriate.
- [ ] Reconciliation can identify the entitlement, group and role.
- [ ] Access review process includes this role.
- [ ] Role retirement procedure is defined.

## Failure mode

- [ ] IAM outage behavior is documented.
- [ ] Existing-user access behavior is validated.
- [ ] Emergency access/revocation policy is defined where required.
- [ ] Manual exceptions are logged and reconciled after recovery.