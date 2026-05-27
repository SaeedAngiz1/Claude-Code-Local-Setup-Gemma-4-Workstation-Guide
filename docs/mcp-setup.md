# MCP Setup

Canonical source: <https://code.claude.com/docs/en/mcp>.

MCP servers connect Claude Code to tools and services. Use local scope for machine-specific config, project scope for shareable repository config, and user scope for cross-project config.

## Examples

```bash
claude mcp add --transport stdio github --env GITHUB_TOKEN=your_github_token_here -- npx -y @modelcontextprotocol/server-github
claude mcp add --transport stdio filesystem -- npx -y @modelcontextprotocol/server-filesystem "/absolute/path/to/allowed/workspace"
claude mcp add --transport stdio playwright -- npx -y @playwright/mcp@latest
claude mcp add --transport stdio postgres --env DATABASE_URL=postgresql://user:password@localhost:5432/dbname -- npx -y @modelcontextprotocol/server-postgres
claude mcp add --transport stdio docs-search --env SEARCH_API_KEY=your_search_key_here -- npx -y your-docs-search-mcp
```

## Verification

```bash
claude mcp list
```

Inside Claude Code, run:

```txt
/mcp
```

