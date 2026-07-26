# MCP Configuration

Add to `.claude/settings.json` in the project root.

## GitHub MCP

Required for Mode 1 (External PR) in `existing-project/code-review.md`.

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

Token scopes: `repo`, `read:org`
Generate: GitHub → Settings → Developer settings → Personal access tokens

Verify: run `/mcp` — should list `github` as active.

If MCP is unavailable, run the diff manually in terminal and paste output:
```bash
gh pr diff <n> --repo <owner>/<repo>
```

## What It Enables

| Command | Use |
|---------|-----|
| `gh pr diff <n>` | Full PR diff |
| `gh pr view <n>` | PR description + status |
| `gh pr list` | Open PRs |
| `gh pr checks <n>` | CI status |
