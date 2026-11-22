# Sources

Every rule in this pack names its source by ID, as `[S4]`. All were read on
2026-11-22. Copilot changes month by month: read a page again before relying
on an old rule.

## VS Code

- **S1** Agent harnesses: https://code.visualstudio.com/docs/agents/run/agent-harnesses
- **S2** Custom instructions reference: https://code.visualstudio.com/docs/agents/reference/custom-instructions-reference
- **S3** Customization concepts: https://code.visualstudio.com/docs/agents/concepts/customization
- **S4** Agent skills: https://code.visualstudio.com/docs/agent-customization/agent-skills
- **S5** Custom agent file reference: https://code.visualstudio.com/docs/agents/reference/custom-agent-file-reference
- **S6** Migrate customizations: https://code.visualstudio.com/docs/agent-customization/migrate-customizations
- **S7** MCP configuration reference: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
- **S8** Tools, and the tools reference: https://code.visualstudio.com/docs/agents/run/tools,
  https://code.visualstudio.com/docs/agents/reference/tools-reference
- **S9** Approvals: https://code.visualstudio.com/docs/agents/run/approvals
- **S10** Agent plugins, and the plugin reference: https://code.visualstudio.com/docs/agent-customization/agent-plugins,
  https://code.visualstudio.com/docs/agents/reference/agent-plugin-reference
- **S11** AI settings reference: https://code.visualstudio.com/docs/agents/reference/ai-settings
- **S12** Optimize usage: https://code.visualstudio.com/docs/agents/guides/optimize-usage
- **S13** Context: https://code.visualstudio.com/docs/agents/concepts/context
- **S14** Language models: https://code.visualstudio.com/docs/copilot/customization/language-models
- **S15** Enterprise AI settings: https://code.visualstudio.com/docs/enterprise/manage-ai-settings
- **S27** Customization overview: https://code.visualstudio.com/docs/agent-customization/overview

## GitHub

- **S16** Hooks reference: https://docs.github.com/en/copilot/reference/hooks-reference
- **S17** Supported models: https://docs.github.com/en/copilot/reference/ai-models/supported-models
- **S18** Models and pricing: https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing
- **S19** Billing for organizations and enterprises: https://docs.github.com/en/copilot/concepts/billing-and-usage/organizations-and-enterprises/billing
- **S20** Auto model selection: https://docs.github.com/en/copilot/concepts/auto-model-selection
- **S21** About agent skills: https://docs.github.com/en/copilot/concepts/agents/about-agent-skills
- **S22** GitHub MCP server: https://github.com/github/github-mcp-server (README,
  docs/remote-server.md, docs/policies-and-governance.md)

## Anthropic and the skills standard

- **S23** Prompting Claude: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices,
  https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5-5,
  https://platform.claude.com/docs/en/build-with-claude/effort
- **S24** Effective context engineering: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- **S25** Agent Skills specification: https://agentskills.io/specification
- **S26** Claude Code costs: https://code.claude.com/docs/en/costs

## Not verified

- No page states the Windows path of `~/.copilot` for instructions, skills
  and agents. The docs say `~` is the home folder, and give
  `%USERPROFILE%\.copilot\hooks\` for hooks; this pack uses
  `%USERPROFILE%\.copilot\` for all of them [S2, S16].
- Which shell the Copilot harness uses on Windows (PowerShell 7 or Windows
  PowerShell 5.1) is not stated.
- The VS Code profile's prompts folder on Windows, `%APPDATA%\Code\User\prompts\`,
  is taken from where VS Code keeps its user settings; no page names it.
- Exactly what `github.copilot.chat.cli.customAgents.enabled` turns on is not
  stated beyond "custom agents in Copilot harness sessions" [S11].
- Model IDs for a custom agent's `model` field come from the editor's
  completions; the docs give no list [S5].
