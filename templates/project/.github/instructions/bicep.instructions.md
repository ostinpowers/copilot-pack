---
applyTo: "**/*.bicep,**/*.bicepparam"
---

# Bicep

- Build and lint after a change: `az bicep build --file <file>`, `az bicep lint --file <file>`.
- Mark secret parameters `@secure()`; no secret in a `.bicepparam` file.
- Preview with `az deployment group what-if` before any deploy.
