# Troubleshooting

## `claude: command not found`

Reopen the terminal, verify the install command from <https://code.claude.com/docs/en/installation>, and check the npm global binary path.

## API Key Not Detected

Verify the variable exists without printing it. Check <https://code.claude.com/docs/en/env-vars> for the current environment variable behavior.

## MCP Auth Failure

Check `/mcp`, confirm the token exists locally, verify scopes, and re-add the server with placeholder-safe commands from <https://code.claude.com/docs/en/mcp>.

## Insufficient VRAM

Use a smaller Gemma 4 model, shorter context, or smaller quantization. Record the exact runtime and artifact used.

## Accidentally Committed Secrets

Revoke the key, rotate it, and follow GitHub's guidance: <https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository>.

