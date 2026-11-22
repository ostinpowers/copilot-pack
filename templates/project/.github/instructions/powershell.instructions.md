---
applyTo: "**/*.ps1,**/*.psm1,**/*.psd1"
---

# PowerShell

- PowerShell 7 syntax, unless the script must run on Windows PowerShell 5.1: say which.
- `Set-StrictMode -Version Latest` and `$ErrorActionPreference = 'Stop'` at the top of a script.
- A function that changes state supports `-WhatIf`: `[CmdletBinding(SupportsShouldProcess)]`.
- Approved verbs; `Invoke-ScriptAnalyzer` on changed files when it is installed.
