# Skills, Plugins, Agents, and Hooks

Sources:

- Skills: <https://code.claude.com/docs/en/skills>
- Plugins: <https://code.claude.com/docs/en/plugins>
- Sub-agents: <https://code.claude.com/docs/en/sub-agents>
- Hooks: <https://code.claude.com/docs/en/hooks>

## Skills

Use skills when a workflow needs reusable instructions, scripts, or bundled resources. Project skills live under `.claude/skills/<skill>/SKILL.md`.

## Plugins

Use plugins when you want installable bundles. Plugins can include skills, MCP servers, slash commands, agents, and hooks. Review the source before installation.

## Agents

Use agents for focused roles such as code review, research, testing, migration planning, or release work.

## Hooks

Use hooks sparingly. Hooks execute shell commands and should be reviewed like code.

