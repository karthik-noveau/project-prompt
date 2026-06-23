# project-prompt

AI prompt library for React codebases.

## new-project/ — Personal / Greenfield
- `codebase-structure.md` — paste at session start
- `task.md` — engine-based generation, one scope at a time
- `code-review.md` — gate after each engine

## existing-project/ — Office / Team Codebase
- `codebase-structure.md` — fill once, paste before every Figma task
- `code-review.md` — PR review: external / local / self

## config/ — One-time setup
- `lint.md` — ESLint + Vite + aliases
- `mcp.md` — GitHub MCP for live PR diff access

## AI Usage
- **Context first** — paste structure before any task
- **Scope every task** — one engine, one approval
- **Review is a gate** — not optional
- **Config over prompting** — lint enforces style automatically
