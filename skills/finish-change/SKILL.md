---
name: finish-change
description: "Finishes a change the user approved: reviews the diff, runs the project's checks, updates its TODO if it keeps one, commits locally and never pushes. Use when an approved change is done."
---

# Finish an approved change

Only for a change the user said yes to; anything beyond it needs its own yes.

## Steps

1. Read the diff of this task's files (`git diff -- <files>`) and
   `git status --short`. Leave alone a stray file or a change this task did
   not make, and say so.
2. No secret in the diff: no key, token or password. A `.env` or key file is
   never staged.
3. Run the checks the project documents (its README, AGENTS.md or
   CONTRIBUTING): tests, linter, type checks. Show the counts. On a failure,
   stop and report it; commit nothing.
4. If the project keeps a TODO, changelog or plan, update it as it does; a
   project with none gets no new file.
5. Commit locally: stage this task's files by path, never `git add -A` or
   `git add .`. The message says what changed and why, with the numbers the
   checks gave. Never `--no-verify`.
6. Push only when the user asks, and never with `--force`.
7. Report the commit hash, the check results, and what was not verified.

## Done when

- The commit holds this task's files and nothing else, and the checks passed.
