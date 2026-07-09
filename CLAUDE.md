# CLAUDE.md

See [AGENTS.md](./AGENTS.md) — it is the single source of truth for all AI agents working in this repo.

Claude-specific notes (only add things here that apply ONLY to Claude Code):

- Use `pnpm test --filter <pkg>` for fast feedback loops instead of the full test suite.
- When exploring the codebase, start with `docs/architecture/system-overview.md` and the Monorepo Map in AGENTS.md.
- Long-running commands: `pnpm dev` never exits — run it in the background or ask the user to run it.
