---
name: official-docs
description: "Answers a question about a tool, version, setting or API from the vendor's official docs and the installed version's release notes, quoted with links. Use before any advice that depends on them."
---

# Official docs first

Answer from what the vendor says for the version in use, and show it.

## Steps

1. Name what the answer depends on: the tool, the setting, flag, path or limit.
2. Find the version in use: the tool's own `--version`, the project's lockfile
   or the package manager. Say so when you cannot.
3. Read the vendor's own page: the docs site, then the release notes or
   changelog of that version; the docs folder of the vendor's repository if
   the site fails. A blog, a forum or an answer site is never the source.
4. A fix or feature "since version X" holds only if the version in use has it:
   fixes are backported, features renamed.
5. Fetch the section that answers, never whole sites or large source files:
   five pages a question at most.
6. Answer with the evidence first: the line quoted exactly, its URL and the
   date read. Then the conclusion, then what you could not verify.

## Done when

- Every claim about the tool carries a quoted line and its link.
