# Prompts

Paste one into Copilot Chat in VS Code, in a new session, with the project
open. Replace `<you>/<repo>` with this repository. Sonnet or Auto is enough
for these: no need to spend Opus on reading and comparing.

## Apply everything that fits

```
Read the public GitHub repository https://github.com/<you>/<repo>.
If you may run git, clone it once: git clone --depth 1 https://github.com/<you>/<repo> "$env:TEMP\copilot-pack"
and read its files from there. Otherwise fetch
https://raw.githubusercontent.com/<you>/<repo>/main/APPLY.md and then only the files it names.
Follow APPLY.md for my own Copilot setup and for this project: read and measure first, compare with
GUIDE.md, then show me the plan, one line per change with its saving. Change nothing until I say yes.
Back up every file you replace. Skip what my organisation's policy blocks, and tell me which.
```

## Audit only

```
Using APPLY.md and GUIDE.md from https://github.com/<you>/<repo>, audit my Copilot setup and this
project for token cost: what loads with every request, with sizes, the MCP tools enabled, and the
five biggest savings. Read only: change nothing.
```

## Once the repository is installed as a plugin

```
/copilot-pack:token-audit
```

## Afterwards

Delete the clone when done: `Remove-Item -Recurse -Force "$env:TEMP\copilot-pack"`.
