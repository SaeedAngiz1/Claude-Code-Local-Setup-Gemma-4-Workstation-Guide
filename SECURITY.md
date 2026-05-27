# Security Policy

## Reporting a Vulnerability

Open a private security advisory if the repository is hosted on GitHub, or contact the maintainers through the repository owner's preferred private channel.

Do not open a public issue containing:

- API keys
- access tokens
- passwords
- private MCP server URLs
- private repository names
- logs with secrets

## Secret Handling

This repository must use placeholders only:

```bash
ANTHROPIC_API_KEY="your_api_key_here"
GITHUB_TOKEN="your_github_token_here"
DATABASE_URL="postgresql://user:password@localhost:5432/dbname"
```

If a real secret is committed:

1. Revoke or rotate the secret immediately.
2. Remove it from the repository and pull requests.
3. Follow GitHub's sensitive-data removal guidance.
4. Add a regression check to prevent recurrence.

