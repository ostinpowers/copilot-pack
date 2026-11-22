---
name: handoff
description: "Writes a handoff at the end of a task: what was done, what is left, what comes next, what is unverified, how to resume. Use when wrapping up a task, before a new chat, or when asked for a handoff."
---

# Handoff

Leave the task so that a new chat, with none of this one's memory, can carry
on. A long chat buries its early decisions, and a new one is cheaper.

## Steps

1. Collect the facts from the project, not from memory:
   - `git status --short`: what changed and is not committed, and any stray file.
   - `git log --oneline` back to where this task began: its commits.
   - The last test or check run, and its result.
2. Write the handoff in this shape, every line specific:

   ```
   Handoff, <date>: <the task>
   Done: <what, with commit hashes>
   Left: <what is not done of this task>
   Next: <the steps, in dependency order>
   Unverified: <what was not checked, and why>
   Resume: <the first file to read and the first command to run>
   ```

3. Put it where the project keeps its state, in that file's own format: its
   TODO, plan or progress notes. A project with none gets no new file: give
   the handoff in the chat, for the user to paste into the next one.
4. Asked for by the user, a handoff is its own yes to update those files and
   nothing else. Thought of by you, it is a suggestion: offer it, then wait.

## Done when

- A new chat could start from the handoff without reading this one.
