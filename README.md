# Copilot pack

Instructions, skills, agents, hooks and settings that keep GitHub Copilot in
VS Code fast and frugal, tuned for Claude Opus 5.5, on Windows and macOS. A
plan or an organisation's policy may block some of them: apply what yours
allows, the rest still holds.

- [GUIDE.md](GUIDE.md): every kind of customisation, what it costs, and how
  to make it cheaper; each rule with its source.
- [APPLY.md](APPLY.md): the steps an agent follows to apply this pack to a
  computer and a project.
- [PROMPT.md](PROMPT.md): the prompts to paste into Copilot Chat.
- [SOURCES.md](SOURCES.md): the official pages behind every rule, read
  2026-11-22, and what they leave unverified.

## What is in it

```
plugin.json                    the plugin's manifest: VS Code installs the skills and agents from it
skills/                        token-audit, cloud-read-first, server-change, iac-review,
                               handoff, official-docs, finish-change
com.github.copilot/agents/     researcher and implementer: narrow tools, low effort
templates/user/                your own setup: instructions, settings.json, mcp-config.json, hooks/
templates/project/             starters for an AWS, Azure, Linux and Windows servers project:
                               .github/copilot-instructions.md, .github/instructions/, .vscode/settings.json
```

## Publish it

From a folder holding only this pack, with the GitHub CLI signed in:

```
git init -b main
git add .
git commit -m "Copilot pack"
gh repo create <repo> --public --source . --push
```

Or create an empty public repository on github.com, then
`git remote add origin https://github.com/<you>/<repo>.git` and
`git push -u origin main`. Then replace `<you>/<repo>` in
[PROMPT.md](PROMPT.md) with its name.

## Use it on a Windows laptop

Pick the first way your policy allows.

1. **As a plugin**: no tokens spent. In VS Code settings turn on
   `chat.plugins.enabled`, then run **Chat: Install Plugin from Source**
   from the Command Palette and enter `https://github.com/<you>/<repo>`. The
   skills run as `/copilot-pack:<skill>`; the agents join the agents list.
   Then run `/copilot-pack:token-audit` for the rest: instructions, settings,
   hooks.
2. **With a prompt**: paste the first prompt of [PROMPT.md](PROMPT.md) into a
   new chat with the project open. The agent clones or reads this
   repository, measures your setup, shows its plan, and changes nothing
   until you say yes.
3. **By hand**: copy into `%USERPROFILE%\.copilot\`:
   `templates\user\instructions\*` into `instructions\`, `skills\*` into
   `skills\`, `com.github.copilot\agents\*` into `agents\`,
   `templates\user\hooks\guard.json` into `hooks\`; merge
   `templates\user\settings.json` into `%APPDATA%\Code\User\settings.json`.

On macOS the same, with `~/.copilot/` and
`~/Library/Application Support/Code/User/settings.json`.

## Check that it works

- **Chat: Open Customizations** lists the instructions, skills and agents.
- In a new chat, `/` shows the skills; ask for a task in a skill's words and
  it runs.
- **Developer: Policy Diagnostics** shows what your organisation turned off.
- Hover a reply for its credits, before and after: that is the saving.

## Keep it current

Copilot changes month by month. Before relying on a rule, read its source in
[SOURCES.md](SOURCES.md) again; the `official-docs` skill does that for you.
