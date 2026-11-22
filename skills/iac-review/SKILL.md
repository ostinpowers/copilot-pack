---
name: iac-review
description: "Reviews a Terraform plan, Bicep what-if or CloudFormation change set before it is applied: what is created, changed, replaced or destroyed, and what is risky. Use before any apply or deploy."
---

# Review before apply

## Steps

1. Produce the preview, applying nothing:
   - Terraform: `terraform plan -out=tfplan`, then `terraform show -no-color tfplan`.
   - Bicep: `az deployment group what-if --resource-group <group> --template-file <file>`.
   - CloudFormation: `aws cloudformation create-change-set ...`, then
     `aws cloudformation describe-change-set ...`.
2. Read it filtered, not whole: the lines that destroy, replace (`-/+`,
   `forces replacement`) or change access.
3. Report in four groups: destroyed or replaced; security (roles,
   policies, network rules, public access); data (databases, storage,
   keys); everything else, counted.
4. Flag drift and anything outside the change that was asked for.
5. Apply only after the user's yes, and only the reviewed plan
   (`terraform apply tfplan`).

## Done when

- The user has the four groups, and nothing was applied without their yes.
