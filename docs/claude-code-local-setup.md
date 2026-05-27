# Claude Code Local Setup

This page expands the setup flow from the main README. Always confirm the current install command against the official docs before publishing automation: <https://code.claude.com/docs/en/installation>.

## Windows

```powershell
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

If `claude` is not found, open a new terminal and verify the npm global binary path is on `PATH`.

## macOS

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

## Linux

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

## WSL

```bash
node --version
git --version
npm install -g @anthropic-ai/claude-code
claude
claude --version
```

For WSL, keep project files and tooling inside the WSL environment unless you have a specific reason to bridge Windows and Linux paths.

