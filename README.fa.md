# راهنمای نصب محلی Claude Code و ورک‌استیشن Gemma 4

این ریپازیتوری یک راهنمای آماده انتشار برای نصب محلی Claude Code، پیکربندی امن Skills/Plugins/MCP، تنظیم کلید API محلی، و انتخاب مدل مناسب Gemma 4 برای سخت‌افزار شماست.

![پیش‌نمایش متحرک نصب Claude Code](assets/animations/claude-code-install-flow.gif)

[English](README.md) | [Deutsch](README.de.md) | [فارسی](README.fa.md)

> وضعیت: این یک ریپازیتوری مستندات است، نه وب‌سایت و نه اپلیکیشن Next.js. نسخه انگلیسی README نسخه مرجع با لینک‌های کامل منابع است.

## این راهنما چه چیزهایی را پوشش می‌دهد

- نصب محلی Claude Code روی Windows، macOS، Linux و WSL. منبع: [Claude Code installation](https://code.claude.com/docs/en/installation)
- تنظیم، بررسی، حذف و چرخش کلید API برای استفاده محلی. منبع: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars)
- جایگزین کردن backend برای Claude Code: استفاده مستقیم از LM Studio، استفاده مستقیم از OpenRouter با محدودیت‌ها، و استفاده از GPT/Gemini/RouteLLM/NVIDIA از طریق gateway سازگار با Anthropic. جزئیات: [docs/provider-routing.md](docs/provider-routing.md)
- پیکربندی پروژه با `CLAUDE.md`، مسیر `.claude/skills/<skill>/SKILL.md`، فایل `.mcp.json`، فایل `.claude/settings.local.json` و پلاگین‌ها. منابع: [skills](https://code.claude.com/docs/en/skills)، [MCP](https://code.claude.com/docs/en/mcp)، [plugins](https://code.claude.com/docs/en/plugins)، [settings](https://code.claude.com/docs/en/settings)
- مثال‌های MCP برای GitHub، فایل‌سیستم، مرورگر، Postgres و جستجوی مستندات.
- راهنمای انتخاب Gemma 4 با تفکیک واضح بین اطلاعات منبع‌دار، محاسبه‌شده و تخمینی. منابع: [Google Gemma 4](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) و [Google Developers edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

## نصب محلی Claude Code

### پیش‌نیازها

| پیش‌نیاز | کاربرد | بررسی |
|---|---|---|
| Node.js | نصب npm طبق مستندات رسمی Claude Code پشتیبانی می‌شود. | `node --version` |
| Git | برای کار معمول با ریپازیتوری‌ها لازم است. | `git --version` |
| GitHub CLI، اختیاری | برای Issue، Pull Request و اتوماسیون GitHub مفید است. | `gh --version` |
| حساب Claude یا روش احراز هویت فعلی | قبل از انتشار، روش رسمی احراز هویت را دوباره بررسی کنید. | `claude` |

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

برای پروژه‌های WSL بهتر است Node، Git و Claude Code را داخل WSL نصب کنید و ریپازیتوری‌ها را در فایل‌سیستم WSL نگه دارید. منابع: [Microsoft WSL](https://learn.microsoft.com/windows/wsl/) و [Claude Code installation](https://code.claude.com/docs/en/installation)

## Changing or Configuring the Claude Code API Key for Local Use

Claude Code بسته به تنظیمات شما می‌تواند از احراز هویت حساب یا متغیرهای محیطی استفاده کند. قبل از انتشار، روش رسمی فعلی را بررسی کنید. منبع: [Claude Code environment variables](https://code.claude.com/docs/en/env-vars)

هرگز کلید واقعی را commit نکنید. فقط از placeholder استفاده کنید:

```bash
ANTHROPIC_API_KEY="your_api_key_here"
```

### تنظیم موقت در ترمینال فعلی

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

### تنظیم دائمی

Windows PowerShell:

```powershell
setx ANTHROPIC_API_KEY "your_api_key_here"
```

macOS/Linux با Zsh:

```bash
echo 'export ANTHROPIC_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

اگر shell شما Bash است، به‌جای `~/.zshrc` از `~/.bashrc` استفاده کنید.

### بررسی بدون چاپ کلید

```bash
claude --version
claude
```

PowerShell:

```powershell
if ($env:ANTHROPIC_API_KEY) { "ANTHROPIC_API_KEY is set" } else { "ANTHROPIC_API_KEY is missing" }
```

macOS/Linux:

```bash
if [ -n "$ANTHROPIC_API_KEY" ]; then echo "ANTHROPIC_API_KEY is set"; else echo "ANTHROPIC_API_KEY is missing"; fi
```

### حذف یا چرخش کلید

PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
Remove-Item Env:\ANTHROPIC_API_KEY
```

macOS/Linux:

```bash
unset ANTHROPIC_API_KEY
```

اگر کلید به‌اشتباه commit شد، فوراً آن را revoke/rotate کنید و diff یا تاریخچه Git را پاک‌سازی کنید. منابع: [GitHub secret scanning](https://docs.github.com/code-security/secret-scanning/about-secret-scanning)، [removing sensitive data](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

## جایگزین کردن backend Claude Code با LM Studio، GPT، Gemini، RouteLLM یا NVIDIA

Claude Code می‌تواند به endpoint دیگری route شود، اما آن endpoint باید فرمتی را پشتیبانی کند که Claude Code می‌فهمد. LM Studio برای Claude Code یک endpoint سازگار با Anthropic به شکل `POST /v1/messages` مستند کرده است. GPT/OpenAI، Gemini OpenAI Compatibility، NVIDIA NIM و بسیاری از routerها معمولاً OpenAI-compatible هستند (`/v1/chat/completions`) و برای Claude Code به یک gateway سازگار با Anthropic نیاز دارند.

راهنمای کامل مرحله‌به‌مرحله: [docs/provider-routing.md](docs/provider-routing.md)

LM Studio محلی:

```bash
lms server start --port 1234
export ANTHROPIC_BASE_URL="http://localhost:1234"
export ANTHROPIC_AUTH_TOKEN="lmstudio"
export ANTHROPIC_API_KEY=""
claude --model your_lm_studio_model_id_here
```

الگوی gateway عمومی:

```bash
export ANTHROPIC_BASE_URL="http://localhost:4000"
export ANTHROPIC_AUTH_TOKEN="your_gateway_token_here"
export ANTHROPIC_API_KEY=""
export ANTHROPIC_MODEL="your_gateway_model_id_here"
claude
```

بررسی:

```txt
/status
/model
```

## پیکربندی Claude Code

| فایل یا workflow | کاربرد |
|---|---|
| `CLAUDE.md` | دستورالعمل‌ها و context پروژه. |
| `.claude/skills/<skill>/SKILL.md` | Skillهای قابل استفاده مجدد. |
| `.mcp.json` | پیکربندی MCP قابل اشتراک بدون secret واقعی. |
| `.claude/settings.local.json` | تنظیمات محلی ماشین؛ معمولاً نباید commit شود. |
| Plugin marketplace | نصب bundleهایی شامل Skills، MCPها، Agents، Commands و Hooks. |

منابع: [memory](https://code.claude.com/docs/en/memory)، [skills](https://code.claude.com/docs/en/skills)، [MCP](https://code.claude.com/docs/en/mcp)، [plugins](https://code.claude.com/docs/en/plugins)، [settings](https://code.claude.com/docs/en/settings)

## راه‌اندازی MCP

![انیمیشن معماری MCP](assets/animations/mcp-architecture.gif)

```mermaid
flowchart LR
  A["Terminal"] --> B["Claude Code"]
  B --> C["MCP config"]
  C --> D["GitHub"]
  C --> E["Filesystem"]
  C --> F["Browser"]
  C --> G["Postgres"]
  C --> H["Docs/Search"]
```

نمونه‌ها با placeholder:

```bash
claude mcp add --transport stdio github --env GITHUB_TOKEN=your_github_token_here -- npx -y @modelcontextprotocol/server-github
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem "/absolute/path/to/allowed/workspace"
claude mcp add --transport stdio playwright -- npx -y @playwright/mcp@latest
claude mcp add --transport stdio postgres --env DATABASE_URL=postgresql://user:password@localhost:5432/dbname -- npx -y @modelcontextprotocol/server-postgres
```

## Skills، Plugins، Agents و Hooks

- Skills: دستورالعمل‌ها، اسکریپت‌ها و منابع قابل استفاده مجدد. منبع: [skills](https://code.claude.com/docs/en/skills)
- Plugins: بسته‌های قابل نصب شامل Skills، MCPها، slash commands، agents و hooks. منبع: [plugins](https://code.claude.com/docs/en/plugins)
- Agents: زیرعامل‌های تخصصی برای review، تحقیق، تست یا کار دامنه‌ای. منبع: [sub-agents](https://code.claude.com/docs/en/sub-agents)
- Hooks: commandهای shell روی eventهای Claude Code؛ قبل از استفاده باید review شوند. منبع: [hooks](https://code.claude.com/docs/en/hooks)

## Gemma 4

Google مدل Gemma 4 را به‌عنوان خانواده‌ای از مدل‌های open برای reasoning و agentic workflows معرفی کرده و اندازه‌های E2B، E4B، 26B A4B و 31B را ذکر می‌کند. منابع: [Google Gemma 4](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/)، [edge post](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

![انتخاب مدل Gemma 4](assets/animations/gemma4-model-selector.gif)

نیاز حافظه بسته به طول context، KV cache، ورودی‌های multimodal، batch size، runtime، سربار driver GPU و فرمت quantization تغییر می‌کند.

| مدل | پیشنهاد | VRAM تخمینی Q4 | حافظه وزن BF16/FP16، محاسبه‌شده |
|---|---|---:|---:|
| E2B | edge/mobile/low-end | 2-4 GB | حدود 4 GB قبل از overhead |
| E4B | laptop/dev daily driver | 4-6 GB | حدود 8 GB قبل از overhead |
| 26B A4B | high-end consumer hardware | 16-24 GB | حدود 52 GB قبل از overhead |
| 31B | workstation class | 20-32 GB | حدود 62 GB قبل از overhead |

در این ریپازیتوری Q8 به‌عنوان عدد رسمی منبع‌دار ارائه نشده است. ادعاهای برابری benchmark باید برای هر benchmark جداگانه اعتبارسنجی شوند.

## دیاگرام‌ها

```mermaid
flowchart TD
  A["Install Node.js + Git"] --> B["Install Claude Code"]
  B --> C["Run claude"]
  C --> D["Authenticate"]
  D --> E["Verify claude --version"]
  E --> F["Configure CLAUDE.md, Skills, MCPs, Plugins"]
```

![استک ورک‌استیشن AI محلی](assets/animations/local-ai-workstation-stack.gif)

## مسیرهای پیشنهادی

- مسیر مبتدی: Node و Git را نصب کنید، Claude Code را نصب کنید، `claude --version` را اجرا کنید، سپس یک `CLAUDE.md` ساده اضافه کنید.
- مسیر power-user: `.mcp.json`، Skills و Plugins را بعد از review اضافه کنید و secrets را فقط محلی نگه دارید.
- مسیر local AI: با E2B یا E4B شروع کنید، سپس در صورت کافی بودن VRAM به 26B A4B یا 31B بروید.
- مسیر تیمی: `CLAUDE.md` و configهای non-secret را commit کنید؛ secrets و settings محلی را commit نکنید.

## چک‌لیست بررسی

```bash
node --version
claude --version
claude mcp list
```

داخل Claude Code:

- `/mcp`
- `/plugin`
- اجرای test skill
- smoke test مدل محلی

## عیب‌یابی

| مشکل | راه‌حل |
|---|---|
| `command not found` | ترمینال را دوباره باز کنید، PATH را بررسی کنید، مستندات نصب را بخوانید. |
| مشکل optional dependency در npm | Node/npm را به‌روز کنید یا مسیر native binary رسمی را بررسی کنید. |
| Windows PATH | `where claude`، npm prefix و terminal جدید را بررسی کنید. |
| WSL | ابزارها را داخل WSL نصب کنید و از فایل‌سیستم WSL استفاده کنید. |
| MCP auth failure | token، scope و `/mcp` را بررسی کنید. |
| VRAM ناکافی | مدل کوچک‌تر، quantization پایین‌تر یا context کوتاه‌تر انتخاب کنید. |
| API key not detected | shell درست، terminal جدید و auth docs فعلی را بررسی کنید. |
| secret commit شده | key را revoke/rotate کنید و راهنمای GitHub را دنبال کنید. |

جزئیات کامل: [README.md](README.md)، [docs/](docs/)، [docs/sources.md](docs/sources.md).
