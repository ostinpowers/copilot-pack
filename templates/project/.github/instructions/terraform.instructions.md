---
applyTo: "**/*.tf,**/*.tfvars"
---

# Terraform

- Run `terraform fmt` and `terraform validate` after a change.
- Pin provider and module versions.
- No secret in `.tf` or `.tfvars`: a variable marked `sensitive`, its value from the vault.
- Every variable and output has a `description`.
- State changes only through Terraform: `*.tfstate` stays unopened and unedited.
