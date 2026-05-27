# Claude Code Local Setup + Gemma 4 Workstation Guide

A publish-ready workstation guide for installing Claude Code locally, wiring skills/plugins/MCPs safely, configuring local API keys, and choosing a Gemma 4 model for your hardware.

![Claude Code Local Setup animated preview](assets/animations/claude-code-install-flow.gif)

[English](README.md) | [Deutsch](README.de.md) | [فارسی](README.fa.md)

> Status: documentation repository, not a web app. This guide uses official Claude Code documentation first, Google Gemma 4 sources second, and community repositories only where they are clearly labeled.

## What This Guide Covers

- Local Claude Code installation for Windows, macOS, Linux, and WSL using the official installation guidance from Anthropic. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)
- Claude Code API-key configuration with placeholder-only examples and local secret hygiene. Source: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars)
- Claude Code project configuration through `CLAUDE.md`, `.claude/skills/<skill>/SKILL.md`, `.mcp.json`, settings files, and plugin marketplace flows. Sources: [skills](https://code.claude.com/docs/en/skills), [MCP](https://code.claude.com/docs/en/mcp), [plugins](https://code.claude.com/docs/en/plugins), [settings](https://code.claude.com/docs/en/settings)
- MCP examples for GitHub, filesystem, browser automation, Postgres, and documentation/search. Source: [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)
- A curated repository catalog for skills, plugins, agents, hooks, and marketplaces, separated by official, curated, and community trust levels.
- Gemma 4 model selection for local hardware, with sourced statements separated from calculated or estimated VRAM guidance. Sources: [Google Gemma 4 announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) and [Google Developers Gemma 4 edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

## Claude Code Local Setup

Claude Code is installed and run locally from a terminal. Anthropic documents installation, native binary installation, Node/npm installation, authentication, and troubleshooting in the official installation page. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

### Requirements

| Requirement | Why it matters | Verify |
|---|---|---|
| Node.js | Claude Code supports npm-based installation in the official install docs. Source: [installation](https://code.claude.com/docs/en/installation) | `node --version` |
| Git | Git is needed for normal repository work, team workflows, and GitHub MCP usage. Source: [Git docs](https://git-scm.com/doc) | `git --version` |
| GitHub CLI, optional | Useful for repository auth, issue/PR workflows, and GitHub automation. Source: [GitHub CLI manual](https://cli.github.com/manual/) | `gh --version` |
| Claude account or supported auth method | Claude Code authentication is covered by Anthropic and can change over time. Source: [installation](https://code.claude.com/docs/en/installation) | `claude` |

### Windows

Use Windows Terminal or PowerShell. If the native Windows path gives you trouble, WSL is often the cleaner developer environment. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

```powershell
# 1. Verify prerequisites
node --version
git --version

# 2. Install Claude Code using the current official method.
# Check the official docs before publishing or automating this command.
npm install -g @anthropic-ai/claude-code

# 3. Start Claude Code and complete authentication.
claude

# 4. Verify the CLI is available.
claude --version
```

Expected result: `node --version` prints a Node version, `git --version` prints a Git version, and `claude --version` prints the installed Claude Code CLI version. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

### macOS

Use Terminal, iTerm2, or another shell. The official docs include npm and native binary installation paths; verify the current recommended path before publishing. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

### Linux

Use your distribution shell. Install Node.js and Git through your normal package manager or version manager, then install Claude Code with the current official method. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

### WSL

WSL gives Windows users a Linux developer environment. Anthropic includes WSL-related troubleshooting in the installation documentation. Source: [Claude Code installation docs](https://code.claude.com/docs/en/installation)

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

Store active repositories inside the WSL filesystem when possible for better developer-tool behavior, and avoid mixing Windows and Linux shell profiles unless you know exactly which terminal will launch Claude Code. Sources: [Microsoft WSL docs](https://learn.microsoft.com/windows/wsl/) and [Claude Code installation docs](https://code.claude.com/docs/en/installation)

## Changing or Configuring the Claude Code API Key for Local Use

Claude Code authentication can use account-based flows and environment variables depending on your setup. Anthropic documents `ANTHROPIC_API_KEY` and other environment variables, and the official authentication method should be verified before publishing this repository. Sources: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars) and [Claude Code installation docs](https://code.claude.com/docs/en/installation)

Never include a real API key in this repository. Use placeholders only:

```bash
ANTHROPIC_API_KEY="your_api_key_here"
```

### Where API Keys Usually Come From

API keys usually come from the provider account or organization that owns Claude API access. For Claude API usage, verify the current official key-management flow in Anthropic's current documentation before publishing. Sources: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars) and [Anthropic console](https://console.anthropic.com/)

### Avoid Committing Secrets

- Put local secrets in shell environment variables, OS credential stores, or ignored local files. Source: [GitHub secret scanning docs](https://docs.github.com/code-security/secret-scanning/about-secret-scanning)
- Do not commit `.env`, `.claude/settings.local.json`, terminal history, screenshots, or copied logs containing keys. Sources: [Claude Code settings](https://code.claude.com/docs/en/settings) and [GitHub secret scanning docs](https://docs.github.com/code-security/secret-scanning/about-secret-scanning)
- Use `.gitignore` and rotate the key immediately if it was committed. Source: [GitHub removing sensitive data](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

### Set an API Key Temporarily in the Current Terminal

Windows PowerShell temporary:

```powershell
$env:ANTHROPIC_API_KEY="your_api_key_here"
claude
```

macOS/Linux temporary:

```bash
export ANTHROPIC_API_KEY="your_api_key_here"
claude
```

Temporary variables apply to the current shell session and child processes launched from that shell. Sources: [PowerShell environment variables](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_environment_variables) and [GNU Bash manual](https://www.gnu.org/software/bash/manual/bash.html)

### Set an API Key Persistently on Windows PowerShell

```powershell
setx ANTHROPIC_API_KEY "your_api_key_here"
```

Open a new terminal after `setx` so the new user environment is loaded. Source: [Microsoft setx command](https://learn.microsoft.com/windows-server/administration/windows-commands/setx)

### Set an API Key Persistently on macOS/Linux Shell

```bash
echo 'export ANTHROPIC_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

Use `~/.bashrc` instead of `~/.zshrc` if your login shell is Bash. Source: [GNU Bash startup files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)

### Verify Claude Code Sees the Configured Key

Use a placeholder-safe check that does not print the key:

![Terminal API key configuration mockup](assets/diagrams/terminal-api-key-flow.svg)

```bash
claude --version
claude
```

If Claude Code still asks for authentication, check the official auth docs and inspect only whether the variable exists, not its value. Source: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars)

PowerShell:

```powershell
if ($env:ANTHROPIC_API_KEY) { "ANTHROPIC_API_KEY is set" } else { "ANTHROPIC_API_KEY is missing" }
```

macOS/Linux:

```bash
if [ -n "$ANTHROPIC_API_KEY" ]; then echo "ANTHROPIC_API_KEY is set"; else echo "ANTHROPIC_API_KEY is missing"; fi
```

### Remove or Rotate the Key

PowerShell user-level removal:

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
```

Current PowerShell session removal:

```powershell
Remove-Item Env:\ANTHROPIC_API_KEY
```

macOS/Linux current shell removal:

```bash
unset ANTHROPIC_API_KEY
```

For rotation, create a new key in the provider console, update your local environment, restart the terminal, verify the variable exists without printing it, and revoke the old key. Sources: [Anthropic console](https://console.anthropic.com/), [Claude Code environment variables](https://code.claude.com/docs/en/env-vars), and [GitHub secret scanning docs](https://docs.github.com/code-security/secret-scanning/about-secret-scanning)

## Claude Code Configuration

| File or workflow | Purpose | Scope | Source |
|---|---|---|---|
| `CLAUDE.md` | Repository instructions and project memory for Claude Code. | Project | [Claude Code memory docs](https://code.claude.com/docs/en/memory) |
| `.claude/skills/<skill>/SKILL.md` | Local skills that package instructions, scripts, and resources. | Project or user | [Claude Code skills docs](https://code.claude.com/docs/en/skills) |
| `.mcp.json` | Project MCP server definitions that can be shared with a repository. | Project | [Claude Code MCP docs](https://code.claude.com/docs/en/mcp) |
| `.claude/settings.local.json` | Local settings intended for one machine and usually not committed. | Local | [Claude Code settings docs](https://code.claude.com/docs/en/settings) |
| Plugin marketplace workflow | Discover and install plugin bundles of skills, MCPs, agents, commands, and hooks. | User/project depending on plugin | [Claude Code plugins docs](https://code.claude.com/docs/en/plugins) |

Plugin marketplace commands and trust prompts can change, so use `/plugin` inside Claude Code and verify the current CLI workflow in the official plugins docs before publishing automation. Source: [Claude Code plugins docs](https://code.claude.com/docs/en/plugins)

## MCP Setup

Claude Code supports MCP server configuration through CLI commands and JSON configuration, with documented local, project, and user scopes. Source: [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)

![MCP architecture animation](assets/animations/mcp-architecture.gif)

```mermaid
flowchart LR
  A["Developer terminal"] --> B["Claude Code"]
  B --> C["MCP registry/config"]
  C --> D["GitHub MCP"]
  C --> E["Filesystem MCP"]
  C --> F["Browser MCP"]
  C --> G["Postgres MCP"]
  C --> H["Docs/Search MCP"]
```

### Scope Model

| Scope | Use when | Source |
|---|---|---|
| Local | The server is only for your current machine or contains machine-specific paths. | [MCP docs](https://code.claude.com/docs/en/mcp) |
| Project | The server config should travel with the repository through `.mcp.json`. | [MCP docs](https://code.claude.com/docs/en/mcp) |
| User | You want the same server available across projects. | [MCP docs](https://code.claude.com/docs/en/mcp) |

### Example MCP Entries

All tokens, keys, and paths are placeholders. Replace them locally and never commit real secrets.

GitHub MCP example:

```bash
claude mcp add --transport stdio github --env GITHUB_TOKEN=your_github_token_here -- npx -y @modelcontextprotocol/server-github
```

Filesystem MCP example:

```bash
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem "/absolute/path/to/allowed/workspace"
```

Browser MCP example:

```bash
claude mcp add --transport stdio playwright -- npx -y @playwright/mcp@latest
```

Postgres MCP example:

```bash
claude mcp add --transport stdio postgres --env DATABASE_URL=postgresql://user:password@localhost:5432/dbname -- npx -y @modelcontextprotocol/server-postgres
```

Docs/search MCP example:

```bash
claude mcp add --transport stdio docs-search --env SEARCH_API_KEY=your_search_key_here -- npx -y your-docs-search-mcp
```

Command shape is based on the official Claude Code MCP CLI patterns; individual server package names must be verified against the server maintainers before use. Source: [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)

## Skills, Plugins, Agents, and Hooks

| Capability | What it does | Use when | Source |
|---|---|---|---|
| Skills | Package repeatable instructions, scripts, and resources behind `SKILL.md`. | You want reusable workflows such as deployment, refactoring, PDF processing, or design review. | [skills docs](https://code.claude.com/docs/en/skills) |
| Plugins | Distribute bundles that can include skills, MCP servers, slash commands, agents, and hooks. | You want installable capability packs or marketplace-based workflows. | [plugins docs](https://code.claude.com/docs/en/plugins) |
| Agents | Delegate specialized work to sub-agents with focused instructions. | You need a reviewer, researcher, tester, or domain specialist pattern. | [sub-agents docs](https://code.claude.com/docs/en/sub-agents) |
| Hooks | Run configured shell commands at Claude Code lifecycle events. | You need policy checks, formatters, logs, or guardrails around tool use. | [hooks docs](https://code.claude.com/docs/en/hooks) |

## Curated Repository Catalog

Trust levels in this table mean: `Official` is controlled by Anthropic or the primary vendor, `Curated` is a maintained community index or toolkit, and `Community` is useful but should be reviewed before installation. Repository metadata was checked through GitHub's API on 2026-05-27.

![Claude Code repository catalog card](assets/diagrams/repository-catalog-card.svg)

| Repository | Category | Install method | Trust level | Why it matters | Source link |
|---|---|---|---|---|---|
| `anthropics/claude-plugins-official` | Official plugin marketplace | Claude Code plugin marketplace workflow | Official | Anthropic-managed directory of Claude Code plugins. | [GitHub](https://github.com/anthropics/claude-plugins-official) |
| `subinium/awesome-claude-code` | Awesome list | Manual review, then install linked resources | Curated | Compact index of Claude Code tools, skills, plugins, and MCP servers. | [GitHub](https://github.com/subinium/awesome-claude-code) |
| `rohitg00/awesome-claude-code-toolkit` | Toolkit index | Manual review, copy/install selected assets | Curated | Large toolkit catalog across agents, skills, commands, plugins, hooks, MCP configs, and ecosystem entries. | [GitHub](https://github.com/rohitg00/awesome-claude-code-toolkit) |
| `applied-artificial-intelligence/claude-code-toolkit` | Workflow toolkit | Manual copy/adapt | Curated | Production-tested workflow patterns, skills, commands, and MCP integrations. | [GitHub](https://github.com/applied-artificial-intelligence/claude-code-toolkit) |
| `jeremylongshore/claude-code-plugins-plus-skills` | Marketplace/skill catalog | `ccpi` workflow or manual review | Community | Large open-source marketplace for plugins, skills, and agents. | [GitHub](https://github.com/jeremylongshore/claude-code-plugins-plus-skills) |
| `levnikolaevich/claude-code-skills` | Plugin suite | Plugin or manual install after review | Community | Delivery-lifecycle skills and bundled MCP servers. | [GitHub](https://github.com/levnikolaevich/claude-code-skills) |
| `serpro69/claude-toolbox` | Config/plugin toolbox | Manual review and copy | Community | Minimal multi-language configs, plugins, MCPs, skills, and agents. | [GitHub](https://github.com/serpro69/claude-toolbox) |
| `rdmgator12/awesome-claude-plugins` | Plugin directory | Manual review | Community | Community-maintained directory of plugin bundles in Anthropic's plugin ecosystem. | [GitHub](https://github.com/rdmgator12/awesome-claude-plugins) |
| `shadowrootdev/awesome-agent-skills-mcp` | MCP skill server | MCP server install after review | Community | MCP server exposing agent skills for multiple MCP clients. | [GitHub](https://github.com/shadowrootdev/awesome-agent-skills-mcp) |
| `nextlevelbuilder/ui-ux-pro-max-skill` | UI/UX skill | Skill install after review | Community | Design-intelligence skill for UI/UX work. | [GitHub](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) |

## Gemma 4 Model and Hardware Guide

Google describes Gemma 4 as its most capable open model family to date, purpose-built for advanced reasoning and agentic workflows. Google lists four sizes: E2B, E4B, 26B A4B, and 31B. Sources: [Google Gemma 4 announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) and [Google Developers edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

Gemma 4 is positioned as a high-performing open model family; benchmark parity claims must be validated per benchmark.

Memory requirements vary by context length, KV cache, multimodal inputs, batch size, runtime, GPU driver overhead, and quantization format.

![Gemma 4 model selector animation](assets/animations/gemma4-model-selector.gif)

![Gemma 4 hardware selection diagram](assets/diagrams/gemma4-hardware-selection.svg)

### Model Selection Table

| Model | Best fit | Intended use case | Source status |
|---|---|---|---|
| E2B | Edge, mobile, low-end machines | On-device assistant, small local tools, low-memory experimentation | Model size and edge positioning sourced from Google; hardware label is a workstation recommendation. Sources: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/), [edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/) |
| E4B | Laptop/dev daily driver | Local coding helper, retrieval workflows, low-latency desktop assistant | Model size sourced from Google; laptop label is a workstation recommendation. Source: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) |
| 26B A4B | High-end consumer hardware | Stronger reasoning/coding where quality matters more than minimum memory | Model size sourced from Google; consumer GPU label is estimated. Source: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) |
| 31B | Workstation class | Best quality local model in this guide; use when VRAM and latency budget allow | Model size sourced from Google; workstation label is estimated. Source: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) |

### VRAM Recommendations

The Q4 estimates below use a simple planning rule: roughly 0.5 bytes per parameter for 4-bit weights plus practical overhead for runtime, KV cache, drivers, and context. These are estimates, not vendor guarantees. BF16/FP16 weight memory is calculated from parameter count at about 2 bytes per parameter before runtime overhead. Q8 values are not listed as sourced unless a model card or runtime publishes them.

| Model | Q4 estimated VRAM | Q8 estimate status | BF16/FP16 calculated weight memory | Label |
|---|---:|---|---:|---|
| E2B | 2-4 GB | Not sourced in this repo | About 4 GB before overhead | Estimated/calculated |
| E4B | 4-6 GB | Not sourced in this repo | About 8 GB before overhead | Estimated/calculated |
| 26B A4B | 16-24 GB | Not sourced in this repo | About 52 GB before overhead | Estimated/calculated |
| 31B | 20-32 GB | Not sourced in this repo | About 62 GB before overhead | Estimated/calculated |

If you need publish-grade VRAM numbers for a specific runtime, benchmark the exact artifact, quantization, context length, and batch size you plan to ship. Sources for model sizes: [Google Gemma 4 announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) and [Google Developers edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

## Diagrams

### Claude Code Local Install Flow

```mermaid
flowchart TD
  A["Install Node.js + Git"] --> B["Install Claude Code"]
  B --> C["Run claude"]
  C --> D["Authenticate"]
  D --> E["Verify claude --version"]
  E --> F["Open project repository"]
  F --> G["Add CLAUDE.md, skills, MCPs, plugins"]
```

### MCP, Plugin, Skill Architecture

```mermaid
flowchart LR
  R["Repository"] --> C["CLAUDE.md"]
  R --> S[".claude/skills/*/SKILL.md"]
  R --> M[".mcp.json"]
  U["User config"] --> P["Plugins"]
  P --> S
  P --> A["Agents"]
  P --> H["Hooks"]
  M --> X["External tools and services"]
```

### Gemma 4 Model Selection by Hardware

```mermaid
flowchart TD
  H["What hardware do you have?"] --> L["Mobile/edge or low RAM"]
  H --> D["Developer laptop"]
  H --> G["High-end consumer GPU"]
  H --> W["Workstation GPU/server"]
  L --> E2["Choose E2B"]
  D --> E4["Choose E4B"]
  G --> A26["Try 26B A4B quantized"]
  W --> B31["Try 31B quantized or BF16/FP16 if memory allows"]
```

### Local AI Workstation Stack

```mermaid
flowchart BT
  OS["OS: Windows, macOS, Linux, or WSL"] --> Node["Node.js + Git"]
  Node --> Claude["Claude Code"]
  Claude --> MCP["MCP servers"]
  Claude --> Skills["Skills / plugins / agents / hooks"]
  MCP --> Runtime["Local model runtime"]
  Runtime --> Gemma["Gemma 4 model"]
```

![Local AI workstation stack animation](assets/animations/local-ai-workstation-stack.gif)

## Step-by-Step Paths

### Beginner Path

1. Install Node.js and Git. Sources: [Node.js](https://nodejs.org/en/download), [Git](https://git-scm.com/downloads)
2. Install Claude Code using the current official instructions. Source: [installation](https://code.claude.com/docs/en/installation)
3. Run `claude`, complete auth, and verify `claude --version`. Source: [installation](https://code.claude.com/docs/en/installation)
4. Add a small `CLAUDE.md` to your repository. Source: [memory docs](https://code.claude.com/docs/en/memory)
5. Add one trusted MCP server and verify it with `/mcp`. Source: [MCP docs](https://code.claude.com/docs/en/mcp)

### Power-User Path

1. Create project-level `.mcp.json` only for shareable non-secret server config. Source: [MCP docs](https://code.claude.com/docs/en/mcp)
2. Add local secrets through environment variables or local settings, not committed files. Sources: [environment variables](https://code.claude.com/docs/en/env-vars), [settings](https://code.claude.com/docs/en/settings)
3. Install reviewed plugins through `/plugin` or the official marketplace workflow. Source: [plugins docs](https://code.claude.com/docs/en/plugins)
4. Add repository-specific skills under `.claude/skills/`. Source: [skills docs](https://code.claude.com/docs/en/skills)
5. Use hooks only after review because hooks execute shell commands. Source: [hooks docs](https://code.claude.com/docs/en/hooks)

### Local AI Path

1. Pick Gemma 4 E2B or E4B first if you are validating on a laptop or edge machine. Sources: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/), [edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)
2. Move to 26B A4B or 31B only if your VRAM budget and latency target allow it. Source: [announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/)
3. Keep runtime selection separate from model selection, because memory use depends on quantization, context, runtime, and batch behavior.
4. Run a smoke test with the exact quantized artifact you plan to use.

### Team/Repository Path

1. Commit `CLAUDE.md`, reviewed skills, and non-secret `.mcp.json` entries. Sources: [memory](https://code.claude.com/docs/en/memory), [skills](https://code.claude.com/docs/en/skills), [MCP](https://code.claude.com/docs/en/mcp)
2. Keep `.claude/settings.local.json` and real secrets out of Git. Sources: [settings](https://code.claude.com/docs/en/settings), [GitHub secret scanning](https://docs.github.com/code-security/secret-scanning/about-secret-scanning)
3. Add a resource review checklist for new plugins, agents, MCPs, and hooks.
4. Require pull requests for changes to skills, MCP config, and hooks.

## Verification Checklist

Run these from a fresh terminal:

```bash
node --version
claude --version
claude mcp list
```

Then verify inside Claude Code:

- Run `/mcp` and confirm expected servers are connected. Source: [MCP docs](https://code.claude.com/docs/en/mcp)
- Run `/plugin` and review installed or available plugins. Source: [plugins docs](https://code.claude.com/docs/en/plugins)
- Invoke a test skill from `.claude/skills/<skill>/SKILL.md`. Source: [skills docs](https://code.claude.com/docs/en/skills)
- Run a local model smoke test for the selected Gemma 4 artifact and record runtime, quantization, context length, memory use, and latency.

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| `claude: command not found` | CLI install path is not on `PATH` or terminal was not restarted. | Reopen the terminal, inspect npm global bin, and re-check the official installation docs. Source: [installation](https://code.claude.com/docs/en/installation) |
| npm optional dependency issue | Platform-specific package resolution or cache issue. | Clear npm cache, update Node/npm, or try the official native binary path if available. Source: [installation troubleshooting](https://code.claude.com/docs/en/installation) |
| Windows PATH issues | `setx`, npm global bin, or terminal profile changed after the shell opened. | Open a new terminal and verify `where claude`, `npm config get prefix`, and user PATH. Sources: [Microsoft setx](https://learn.microsoft.com/windows-server/administration/windows-commands/setx), [installation](https://code.claude.com/docs/en/installation) |
| WSL issues | Mixing Windows paths, Linux paths, and separate shell profiles. | Install and run Claude Code inside WSL for WSL projects, then keep repos under the WSL filesystem. Sources: [Microsoft WSL docs](https://learn.microsoft.com/windows/wsl/), [installation](https://code.claude.com/docs/en/installation) |
| MCP auth failures | Missing token, wrong environment variable, expired OAuth, or wrong scope. | Re-add the MCP with placeholder-safe env vars, then inspect `/mcp`. Source: [MCP docs](https://code.claude.com/docs/en/mcp) |
| Insufficient VRAM | Model, quantization, context, runtime, or batch size exceeds memory. | Choose a smaller Gemma 4 model or lower quantization/context. Sources: [Gemma 4 announcement](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/), [edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/) |
| Plugin trust/security review | Plugin can include executable behavior such as MCPs or hooks. | Review source, maintainer, install commands, hooks, and permissions before installing. Source: [plugins docs](https://code.claude.com/docs/en/plugins) |
| API key not detected | Variable set in the wrong shell, stale terminal, typo, or provider auth mismatch. | Check only whether `ANTHROPIC_API_KEY` exists, restart the terminal, and verify current official auth docs. Source: [environment variables](https://code.claude.com/docs/en/env-vars) |
| Stale or wrong environment variable | Old key remains in user profile, shell RC file, or OS environment. | Remove old entries, reopen terminal, then set only the current key. Sources: [PowerShell env vars](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_environment_variables), [Bash startup files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html) |
| Accidentally committed secrets | Key appears in Git history or open PR diff. | Revoke/rotate the key, remove it from history if needed, and enable secret scanning. Sources: [GitHub removing sensitive data](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository), [secret scanning](https://docs.github.com/code-security/secret-scanning/about-secret-scanning) |

## Sources

Canonical source list is maintained in [docs/sources.md](docs/sources.md) and machine-readable form in [data/sources.json](data/sources.json).
