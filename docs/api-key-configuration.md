# API Key Configuration

Canonical source: <https://code.claude.com/docs/en/env-vars>.

Never commit real API keys. Use placeholders only.

```bash
ANTHROPIC_API_KEY="your_api_key_here"
```

## Temporary

PowerShell:

```powershell
$env:ANTHROPIC_API_KEY="your_api_key_here"
claude
```

macOS/Linux:

```bash
export ANTHROPIC_API_KEY="your_api_key_here"
claude
```

## Persistent

PowerShell:

```powershell
setx ANTHROPIC_API_KEY "your_api_key_here"
```

macOS/Linux:

```bash
echo 'export ANTHROPIC_API_KEY="your_api_key_here"' >> ~/.zshrc
source ~/.zshrc
```

## Verify Without Printing Secrets

PowerShell:

```powershell
if ($env:ANTHROPIC_API_KEY) { "ANTHROPIC_API_KEY is set" } else { "ANTHROPIC_API_KEY is missing" }
```

macOS/Linux:

```bash
if [ -n "$ANTHROPIC_API_KEY" ]; then echo "ANTHROPIC_API_KEY is set"; else echo "ANTHROPIC_API_KEY is missing"; fi
```

## Remove

PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", $null, "User")
Remove-Item Env:\ANTHROPIC_API_KEY
```

macOS/Linux:

```bash
unset ANTHROPIC_API_KEY
```

If a key was committed, revoke it first, then remove it from Git history if necessary.

