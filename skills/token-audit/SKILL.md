---
name: token-audit
description: "Audits what Copilot loads with every request on this computer and in this project, and proposes cuts with their savings. Use when asked to optimise instructions, skills, agents, tools or settings."
---

# Token audit

Find what costs tokens on every request, and propose the cuts. Change nothing
before the user's yes.

## Steps

1. List, read only, with sizes in bytes (a token is about four bytes):
   - The user's instructions: `$env:COPILOT_HOME`, else `$env:USERPROFILE\.copilot`
     (`~/.copilot` on macOS): `instructions\` and `copilot-instructions.md`.
   - Copies only the old Local harness reads: the VS Code profile's
     `prompts` folder (`$env:APPDATA\Code\User\prompts\`).
   - The project's: every `AGENTS.md`, `.github/copilot-instructions.md`, and
     `.github/instructions/*.instructions.md` with their `applyTo`.
   - Skills and agents: their count and their description lengths.
   - MCP servers in `mcp-config.json` and `.mcp.json`, and how many tools each
     exposes.
2. Flag:
   - The same rule in two files.
   - Always-on text past about 8 KB in all.
   - A description of the project the agent could read itself; a rule a
     linter or formatter enforces.
   - A procedure that belongs in a skill; `applyTo: "**"` on a file meant
     for some files only.
   - An MCP server with `"*"` tools, or one this project does not use.
   - Prompt files, which the Copilot harness never loads.
3. Propose one line per cut: the file, the change, the bytes saved. Then the
   habits that apply: a new session per task, the model and effort for the
   task, `/compact` in a long chat.
4. Ask before applying, and back up a file before replacing it.

## Done when

- The user has the list of what loads every request, with sizes, and the
  cuts ranked by saving.
