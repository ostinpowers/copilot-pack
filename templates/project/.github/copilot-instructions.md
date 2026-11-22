# This project

- Manages: <AWS accounts, Azure subscriptions, Linux and Windows servers>, with <Terraform, Bicep, CloudFormation, scripts>.
- Check a change: <`terraform fmt -check` and `terraform validate`>, <`Invoke-Pester`>, <`shellcheck scripts/*.sh`>.

## Working on infrastructure

- Before a cloud or server command, state the account or subscription, the region and the target.
- Read first: describe, list, show. A change runs only after a plan and my yes, with its rollback written down.
- Infrastructure as code: preview before apply (`terraform plan`, `what-if`, a change set), and apply only the reviewed plan.
- Secrets stay in the vault. State files (`*.tfstate`) and `.env` files hold secrets: leave them unread.
- Scripts: PowerShell 7 for Windows servers, bash for Linux; idempotent; `-WhatIf` or `--dry-run` first where supported.
