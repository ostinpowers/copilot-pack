# Apply this pack

For the agent asked to apply this repository to a computer and a project.
Work through the steps in order. Steps 1 to 4 only read; nothing changes
before the user's yes. Paths are given for Windows, then macOS.

## 1. Read what is there

- The harness of this session: Copilot (the default) or Local, which is
  deprecated and reads other folders [GUIDE.md, Instructions].
- The user's Copilot folder: `$env:COPILOT_HOME`, else `$env:USERPROFILE\.copilot`
  (`~/.copilot`): `instructions\`, `copilot-instructions.md`, `skills\`,
  `agents\`, `hooks\`, `mcp-config.json`. List each file with its size.
- Files only the Local harness reads: `$env:APPDATA\Code\User\prompts\`
  (`~/Library/Application Support/Code/User/prompts/`).
- VS Code's user settings: `$env:APPDATA\Code\User\settings.json`
  (`~/Library/Application Support/Code/User/settings.json`): the keys that
  [templates/user/settings.json](templates/user/settings.json) sets.
- The open project: every `AGENTS.md`, `.github/copilot-instructions.md`,
  `.github/instructions/`, `.github/skills/`, `.github/agents/`,
  `.github/hooks/`, `.mcp.json`, `.vscode/settings.json`, with sizes.
- The enabled MCP servers and how many tools each exposes (Chat: Open
  Customizations → Tools).

## 2. Measure

- The text that loads with every request: user instructions plus project
  instructions, in bytes; a token is about four bytes.
- The same rule in more than one file.
- MCP servers with `"*"` tools, or that this project does not use.

## 3. Compare with GUIDE.md

For each section of [GUIDE.md](GUIDE.md), what applies here and is not done
yet. Take the templates from [templates/](templates/) and the skills from
[skills/](skills/).

## 4. Show the plan, then wait

- One line per change: the file, what changes, the bytes or tools saved.
- The user's own setup first, then the project's. Mark what a project's
  other contributors would see: a shared repository gets its files only on
  the user's explicit yes.
- Adapt each template to what step 1 found: the project's own commands,
  paths and tools, never a placeholder left in.
- End with one question: should I apply it?

## 5. Apply what was approved

- Back up each file before replacing it: `<file>.bak-<yyyy-MM-dd>` beside it.
- Merge settings into the user's `settings.json`; never overwrite the file.
- Skip what a policy blocks, and say which policy, if Developer: Policy
  Diagnostics shows it.

## 6. Check it works

- A new chat: Chat: Open Customizations lists the instructions, skills and
  agents.
- `/` shows the skills; a test prompt that should use one does.
- A hook installed: its test in [GUIDE.md](GUIDE.md), Hooks, prints its
  decision.
- A reply's credits, hovered, against one from before the change.

## 7. Report

What changed, the always-on bytes before and after, what was skipped and
why, and where the backups are.
