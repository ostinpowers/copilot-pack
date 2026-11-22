# Copilot in VS Code, fast and frugal

What makes GitHub Copilot in VS Code answer well while spending few tokens,
for every kind of customisation, on Windows and macOS. Tuned for Claude Opus
5.5; most of it holds for any model. Each rule names its source in
[SOURCES.md](SOURCES.md). Where a plan or a policy blocks a feature, skip it:
the rest still holds.

## Where the tokens go

Every request carries the system prompt, every always-on instruction file,
the definitions of every enabled tool, the chat so far, the files you
attached, and each tool result [S13]. Business and Enterprise plans pay per
token in AI credits: Enterprise includes 3,900 credits a user a month, one
credit is $0.01 [S19]. Claude Opus 5.5 costs $4 per million input tokens,
$0.20 for cached input, and $20 per million output tokens [S18]. So the
levers, biggest first:

1. Less text that loads with every request: instructions and tools.
2. Shorter chats: one task per session.
3. The right model and effort for the task.
4. Short answers: output costs five times input.
5. A stable prompt prefix, which the cache serves at a twentieth of the
   price.

## Models, effort and credits

- Opus 5.5 for hard reasoning: architecture, multi-step debugging. Sonnet
  5.5 costs half as much for output and suits most coding; Haiku suits
  simple and delegated tasks [S18, S26].
- Auto model selection takes 10% off and picks a model per task on paid plans
  [S20].
- Effort: the default works well. Raise it only for a measured gain; lower
  it for simple tasks and subagents, which also gives fewer and terser tool
  calls [S12, S23]. Set it in the model picker's `>` submenu; it holds for the
  session [S14].
- Pick model and effort before the first prompt: changing effort mid-chat
  throws away the prompt cache [S23].
- Keep the regular context window; the 1M option is for when you need it
  [S17].
- Watch the cost: hover a reply for its credits, the context control in the
  chat input for the session's tokens and cost, the Copilot status bar item
  for the month [S12].

## Sessions and context

- One task per session: start a new one when the topic changes; `/fork` a
  side question instead of re-asking [S12].
- `/compact <focus>` shrinks a long chat on purpose; VS Code also compacts by
  itself near the limit, and may drop details when it does [S13].
- Attach the files a task needs, not folders; let search find the rest
  [S12].
- Search snippets count toward the context: keep build output, dependencies
  and state files out of search with `search.exclude` and `files.exclude`
  [S12].
- Paste less: a long log or listing filtered first (`Select-String`,
  `Select-Object -First 50`, `head`) costs a fraction of the raw one.

## Instructions

Always on, so every line costs on every request [S3].

- Copilot harness, user level: `%USERPROFILE%\.copilot\instructions\*.instructions.md`
  and `%USERPROFILE%\.copilot\copilot-instructions.md` (`~/.copilot/` on
  macOS); not synced by Settings Sync [S2, S6].
- Project level: `.github/copilot-instructions.md` or `AGENTS.md`; Copilot
  combines every `AGENTS.md` from the root to the folders it works in [S2].
- Rules for one kind of file go in `.github/instructions/<name>.instructions.md`
  with `applyTo` globs: they load only when the agent works with matching
  files [S2].
- Keep each rule once. The old Local harness read instructions from the VS
  Code profile (`%APPDATA%\Code\User\prompts\`); copies there and in
  `~/.copilot` cost twice in Local sessions [S6].
- Write only what the agent cannot find by itself: the commands, paths and
  conventions; leave out what the code shows and what a linter enforces
  [S2, S24].
- A Markdown link does not pull the linked file in: what must hold goes in
  the file itself [S2].
- For Opus: say what to do rather than what not to do, give the reason, and
  write calmly: `CRITICAL: you MUST` makes recent models over-apply a rule.
  Ask for concise answers explicitly. Drop "think carefully" lines and old
  self-check instructions [S23].
- Start small, and add a rule only for a failure you have seen [S24].

## Skills

Loaded in steps: only the name and description until a request matches, so
many skills cost almost nothing [S4, S25].

- Where: `%USERPROFILE%\.copilot\skills\<name>\SKILL.md` (or
  `%USERPROFILE%\.agents\skills\`); in a project `.github/skills/` [S4, S21].
- `name`: lowercase letters, digits and hyphens, the folder's own name, at
  most 64; any other name is skipped without a word [S4].
- `description`: at most 1,024 characters, with the words a request would
  use [S4].
- Body under 500 lines; long material in `references/`, linked, one level
  deep [S25].
- `disable-model-invocation: true` keeps a skill you call by hand (`/name`)
  out of automatic matching [S4].
- `context: fork` (experimental) runs a skill in a subagent, so only its
  result returns to the chat [S4].
- Procedures belong in skills; rules in instructions [S3].

## Custom agents and subagents

- Where: `%USERPROFILE%\.copilot\agents\*.agent.md`, or `.github/agents/` [S5].
- A narrow `tools` list (`read`, `search`, `edit`, `execute`, `web`, `agent`,
  `todo`) means fewer tool definitions per request [S5, S12].
- `model` (an ordered list; the first available wins) and `reasoning-effort`
  let a research or bounded-change agent run cheaper than the main chat
  [S5].
- Plan with a strong model, delegate bounded tasks to cheaper agents; keep
  small tasks in the main chat, as delegating costs tokens too [S12].
- Copilot delegates with its own `task` tool: write "delegate to the
  researcher agent" rather than a tool name [S6].
- Copilot harness sessions may need `github.copilot.chat.cli.customAgents.enabled`
  [S11].

## Tools and MCP servers

- Every enabled tool's definition goes with every request; a request is
  capped at 128 tools [S11, S12].
- Turn off the servers and tools a project does not use: Chat: Open
  Customizations → Tools; it persists per harness [S8].
- In `%USERPROFILE%\.copilot\mcp-config.json`, list the tools you use instead
  of `"*"` [S7].
- The GitHub MCP server's read-only, one-toolset URL
  (`https://api.githubcopilot.com/mcp/x/repos/readonly`) exposes a few
  repository tools instead of the default five toolsets [S22].
- A command-line tool (`az`, `aws`, `gh`) through the terminal can replace an
  MCP server with dozens of tools; narrow its output with `--query` and
  `-o table` [S12].

## Hooks

Rules that must hold every time, checked by a script rather than repeated
to the model [S16].

- Where: `%USERPROFILE%\.copilot\hooks\*.json`, or `.github/hooks/*.json` in a
  project [S16].
- Format: `{"version": 1, "hooks": {"preToolUse": [...]}}`; each entry has a
  `powershell` and a `bash` command, an optional `matcher` regex on the tool
  name, and `timeoutSec` [S16].
- A `preToolUse` hook answers `permissionDecision`: `allow`, `ask` or `deny`,
  with a reason [S16].
- A crashed `preToolUse` hook denies the tool; a timed-out one lets it run:
  write hooks that exit cleanly on anything they do not understand [S16].
- `postToolUse` can replace a tool's result, for example to cut a huge
  output before the model reads it [S16].
- [templates/user/hooks/](templates/user/hooks/) asks before any `git push`,
  refuses a force push, and keeps secret files unread. Its commands are
  inline, so no script file meets PowerShell's execution policy.
- Each matched tool call starts a shell for the hook: keep hooks few, and
  the `matcher` narrow.
- Test a hook before relying on it, with a sample event on its input:

  ```powershell
  $cmd = (Get-Content "$env:USERPROFILE\.copilot\hooks\guard.json" -Raw | ConvertFrom-Json).hooks.preToolUse[0].powershell
  '{"toolName":"bash","toolArgs":{"command":"git push"}}' | powershell -NoProfile -Command $cmd
  ```

  It should print the `ask` decision.

## Plugins

- A plugin bundles skills, agents, hooks and MCP servers, and installs from
  a Git URL: Chat: Install Plugin from Source, or Customizations → Plugins →
  `+`. It needs `chat.plugins.enabled` [S10].
- Its skills run as `/<plugin>:<skill>` [S10]. This repository is one.

## Settings

[templates/user/settings.json](templates/user/settings.json), each with its
reason [S9, S11]:

- `chat.tools.compressOutput.enabled`: shorter terminal output (preview).
- `github.copilot.chat.summarizeAgentConversationHistory.enabled`: a long
  chat summarised instead of failing (on by default).
- `chat.tools.terminal.autoApprove`: read-only commands run without asking.
  Copilot reads it from User settings only.
- `chat.agentHost.agentDebugLog.enabled`: tokens, tool calls and cache hits
  per session, in Agent Debug Logs.
- `chat.agent.maxRequests` (25 by default) caps a runaway turn.

## The terminal on Windows

- Copilot runs commands with its own shell tool; the integrated terminal's
  settings apply to the Local harness only [S8].
- `chat.agentHost.shellTool.initScript.enabled` loads your PowerShell
  profiles before each command (off by default, and faster off) [S11].
- Hooks take a `powershell` command [S16].

## Enterprise policies

An organisation can turn features off: Developer: Policy Diagnostics shows
what applies [S15]. The ones this pack meets:

- `ChatPluginsEnabled`: plugins.
- The GitHub policy "MCP servers in Copilot", `ChatMCP`, `allowedMcpServers`:
  MCP servers [S15, S22].
- "Editor preview features" off: the marketplace and connectors [S15].
- `ChatAllowManagedHooksOnly`: your own hooks [S15].
- `ChatStrictPluginOnlyCustomization`: standalone skills, agents and
  instructions, plugins only [S15].
- `ChatAgentNetworkFilter` with allowed domains: what the fetch tool may
  reach [S15].
- Model availability, set by the organisation [S15, S17].

## Measure, then cut

- Agent Debug Logs: tokens, tool calls and time per session; the Cache
  Explorer shows prompt-cache hits [S12].
- The Chat Customizations Evaluations extension flags vague, contradictory or
  overly complex rules [S27].
- After each change, run one real task in a new chat and compare its credits
  [S12].
