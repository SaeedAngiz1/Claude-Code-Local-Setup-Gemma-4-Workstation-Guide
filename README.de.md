# Claude Code Local Setup + Gemma 4 Workstation Guide

Ein produktionsreifes GitHub-Handbuch fuer die lokale Installation von Claude Code, sichere Skills/Plugins/MCP-Konfiguration, lokale API-Schluessel und die Auswahl eines passenden Gemma-4-Modells fuer deine Hardware.

![Animierte Vorschau der Claude-Code-Installation](assets/animations/claude-code-install-flow.gif)

[English](README.md) | [Deutsch](README.de.md) | [فارسی](README.fa.md)

> Status: Dokumentations-Repository, keine Website und keine Next.js-App. Die englische README ist die kanonische Version mit den vollstaendigen Quellenlinks.

## Inhalt

- Claude Code lokal installieren: Windows, macOS, Linux und WSL. Quelle: [Claude Code Installation](https://code.claude.com/docs/en/installation)
- API-Key lokal setzen, pruefen, entfernen und rotieren. Quelle: [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars)
- Claude-Code-Backend ersetzen: LM Studio direkt, OpenRouter direkt mit Einschraenkungen, und GPT/Gemini/RouteLLM/NVIDIA ueber ein Anthropic-kompatibles Gateway. Details: [docs/provider-routing.md](docs/provider-routing.md)
- Projektkonfiguration mit `CLAUDE.md`, `.claude/skills/<skill>/SKILL.md`, `.mcp.json`, `.claude/settings.local.json` und Plugins. Quellen: [Skills](https://code.claude.com/docs/en/skills), [MCP](https://code.claude.com/docs/en/mcp), [Plugins](https://code.claude.com/docs/en/plugins), [Settings](https://code.claude.com/docs/en/settings)
- MCP-Beispiele fuer GitHub, Dateisystem, Browser, Postgres und Docs/Search.
- Gemma-4-Modellwahl mit klar getrennten Quellenangaben, Berechnungen und Schaetzungen. Quellen: [Google Gemma 4](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) und [Google Developers Edge Post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

## Lokale Claude-Code-Installation

### Voraussetzungen

| Voraussetzung | Zweck | Pruefen |
|---|---|---|
| Node.js | Claude Code kann laut offizieller Dokumentation per npm installiert werden. | `node --version` |
| Git | Notwendig fuer normale Repository-Arbeit. | `git --version` |
| GitHub CLI, optional | Hilfreich fuer Issues, Pull Requests und GitHub-Automatisierung. | `gh --version` |
| Claude-Account oder aktueller Auth-Flow | Die Authentifizierung kann sich aendern; vor Veroeffentlichung offizielle Doku pruefen. | `claude` |

### Windows PowerShell

```powershell
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

### macOS

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

### Linux

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

### WSL

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

Bei WSL-Projekten ist es meist sauberer, Node, Git und Claude Code innerhalb von WSL zu installieren und Repositories im WSL-Dateisystem zu halten. Quellen: [Microsoft WSL](https://learn.microsoft.com/windows/wsl/) und [Claude Code Installation](https://code.claude.com/docs/en/installation)

## Changing or Configuring the Claude Code API Key for Local Use

Claude Code kann je nach Setup Account-Authentifizierung und Umgebungsvariablen verwenden. Pruefe vor Veroeffentlichung immer die aktuelle offizielle Authentifizierungsmethode. Quelle: [Claude Code Environment Variables](https://code.claude.com/docs/en/env-vars)

Niemals echte API-Keys committen. Nur Platzhalter verwenden:

```bash
ANTHROPIC_API_KEY="your_api_key_here"
```

### Temporaer setzen

Windows PowerShell:

```powershell
$env:ANTHROPIC_API_KEY="your_api_key_here"
claude
```

macOS/Linux:

```bash
export ANTHROPIC_API_KEY="your_api_key_here"
claude
```

### Dauerhaft setzen

Windows PowerShell:

```powershell
setx ANTHROPIC_API_KEY "your_api_key_here"
```

macOS/Linux mit Zsh:

```bash
echo 'export ANTHROPIC_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

Bei Bash nutze `~/.bashrc` statt `~/.zshrc`.

### Pruefen

```bash
claude --version
claude
```

PowerShell ohne Key auszugeben:

```powershell
if ($env:ANTHROPIC_API_KEY) { "ANTHROPIC_API_KEY is set" } else { "ANTHROPIC_API_KEY is missing" }
```

macOS/Linux ohne Key auszugeben:

```bash
if [ -n "$ANTHROPIC_API_KEY" ]; then echo "ANTHROPIC_API_KEY is set"; else echo "ANTHROPIC_API_KEY is missing"; fi
```

### Entfernen oder rotieren

PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
Remove-Item Env:\ANTHROPIC_API_KEY
```

macOS/Linux:

```bash
unset ANTHROPIC_API_KEY
```

Wenn ein Key versehentlich committed wurde: Key sofort widerrufen, neuen Key setzen und Git-History/PR-Diff bereinigen. Quellen: [GitHub Secret Scanning](https://docs.github.com/code-security/secret-scanning/about-secret-scanning), [Removing sensitive data](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

## Claude-Code-Backend durch LM Studio, GPT, Gemini, RouteLLM oder NVIDIA ersetzen

Claude Code kann auf einen anderen Endpoint zeigen, aber dieser Endpoint muss ein Format sprechen, das Claude Code versteht. LM Studio dokumentiert dafuer direkt einen Anthropic-kompatiblen `POST /v1/messages` Endpoint. GPT/OpenAI, Gemini OpenAI Compatibility, NVIDIA NIM und viele Router sind meistens OpenAI-kompatibel (`/v1/chat/completions`) und brauchen deshalb ein Anthropic-kompatibles Gateway dazwischen.

Vollstaendige Schritt-fuer-Schritt-Anleitung: [docs/provider-routing.md](docs/provider-routing.md)

LM Studio lokal:

```bash
lms server start --port 1234
export ANTHROPIC_BASE_URL="http://localhost:1234"
export ANTHROPIC_AUTH_TOKEN="lmstudio"
export ANTHROPIC_API_KEY=""
claude --model your_lm_studio_model_id_here
```

Generic Gateway:

```bash
export ANTHROPIC_BASE_URL="http://localhost:4000"
export ANTHROPIC_AUTH_TOKEN="your_gateway_token_here"
export ANTHROPIC_API_KEY=""
export ANTHROPIC_MODEL="your_gateway_model_id_here"
claude
```

Pruefen:

```txt
/status
/model
```

## Claude-Code-Konfiguration

| Datei/Workflow | Zweck |
|---|---|
| `CLAUDE.md` | Projektanweisungen und Repository-Kontext. |
| `.claude/skills/<skill>/SKILL.md` | Wiederverwendbare lokale Skills. |
| `.mcp.json` | Teilbare MCP-Server-Konfiguration ohne echte Secrets. |
| `.claude/settings.local.json` | Lokale Maschinenkonfiguration; normalerweise nicht committen. |
| Plugin Marketplace | Installierbare Bundles aus Skills, MCPs, Agents, Commands und Hooks. |

Quellen: [Memory](https://code.claude.com/docs/en/memory), [Skills](https://code.claude.com/docs/en/skills), [MCP](https://code.claude.com/docs/en/mcp), [Plugins](https://code.claude.com/docs/en/plugins), [Settings](https://code.claude.com/docs/en/settings)

## MCP Setup

![MCP-Architektur-Animation](assets/animations/mcp-architecture.gif)

```mermaid
flowchart LR
  A["Terminal"] --> B["Claude Code"]
  B --> C["MCP-Konfiguration"]
  C --> D["GitHub"]
  C --> E["Filesystem"]
  C --> F["Browser"]
  C --> G["Postgres"]
  C --> H["Docs/Search"]
```

Beispiele mit Platzhaltern:

```bash
claude mcp add --transport stdio github --env GITHUB_TOKEN=your_github_token_here -- npx -y @modelcontextprotocol/server-github
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem "/absolute/path/to/allowed/workspace"
claude mcp add --transport stdio playwright -- npx -y @playwright/mcp@latest
claude mcp add --transport stdio postgres --env DATABASE_URL=postgresql://user:password@localhost:5432/dbname -- npx -y @modelcontextprotocol/server-postgres
```

## Skills, Plugins, Agents und Hooks

- Skills: wiederverwendbare Anweisungen, Skripte und Ressourcen. Quelle: [Skills](https://code.claude.com/docs/en/skills)
- Plugins: installierbare Bundles mit Skills, MCPs, Slash Commands, Agents und Hooks. Quelle: [Plugins](https://code.claude.com/docs/en/plugins)
- Agents: spezialisierte Sub-Agents fuer Review, Recherche, Tests oder Domaenenarbeit. Quelle: [Sub-agents](https://code.claude.com/docs/en/sub-agents)
- Hooks: Shell-Kommandos an Claude-Code-Lifecycle-Events; vor Nutzung sorgfaeltig pruefen. Quelle: [Hooks](https://code.claude.com/docs/en/hooks)

## Gemma 4

Google beschreibt Gemma 4 als offene Modellfamilie fuer Reasoning und agentische Workflows und nennt die Groessen E2B, E4B, 26B A4B und 31B. Quellen: [Google Gemma 4](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/), [Edge Post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

![Gemma-4-Modellauswahl](assets/animations/gemma4-model-selector.gif)

![Lokaler AI-Workstation-Stack](assets/animations/local-ai-workstation-stack.gif)

Speicherbedarf variiert nach Kontextlaenge, KV-Cache, multimodalen Eingaben, Batch-Groesse, Runtime, GPU-Treiber-Overhead und Quantisierungsformat.

| Modell | Empfehlung | Q4 VRAM, geschaetzt | BF16/FP16 Gewichtsspeicher, berechnet |
|---|---|---:|---:|
| E2B | Edge/Mobile/Low-End | 2-4 GB | ca. 4 GB vor Overhead |
| E4B | Laptop/Dev Daily Driver | 4-6 GB | ca. 8 GB vor Overhead |
| 26B A4B | High-End Consumer Hardware | 16-24 GB | ca. 52 GB vor Overhead |
| 31B | Workstation-Klasse | 20-32 GB | ca. 62 GB vor Overhead |

Q8-Werte sind in diesem Repository nicht als offiziell belegt markiert. Benchmark-Paritaetsbehauptungen muessen pro Benchmark validiert werden.

## Verifikation

```bash
node --version
claude --version
claude mcp list
```

Dann in Claude Code pruefen:

- `/mcp`
- `/plugin`
- Test-Skill ausfuehren
- Lokalen Gemma-4-Smoke-Test ausfuehren

## Fehlerbehebung

| Problem | Loesung |
|---|---|
| `command not found` | Terminal neu oeffnen, PATH pruefen, offizielle Installationsdoku lesen. |
| npm optionale Dependency | Node/npm aktualisieren, Cache pruefen, offiziellen Native-Binary-Weg pruefen. |
| Windows PATH | `where claude`, npm Prefix und neues Terminal pruefen. |
| WSL | Tools innerhalb von WSL installieren und WSL-Dateisystem nutzen. |
| MCP Auth | Tokens/Scopes pruefen, `/mcp` nutzen, Secrets nur als Platzhalter dokumentieren. |
| Zu wenig VRAM | Kleineres Modell, geringere Quantisierung oder kuerzeren Kontext verwenden. |
| API-Key nicht erkannt | Richtige Shell, neuer Terminalprozess und aktuelle Auth-Doku pruefen. |
| Secrets committed | Key widerrufen/rotieren und GitHub Secret-Scanning-Hinweise befolgen. |

Weitere Details: [README.md](README.md), [docs/](docs/), [docs/sources.md](docs/sources.md).
