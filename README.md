# AI-Ready Monorepo Template

> A repo structure that makes AI coding agents productive from the first prompt — Claude Code, Cursor, Codex, Copilot, Gemini CLI, Windsurf, Cline, Aider, and whatever ships next month.

AI agents fail for predictable reasons: they don't know the **rules**, the **map**, or the **domain**. This template gives each its own home, with a single source of truth (`AGENTS.md`) that every tool reads — so you never maintain eight diverging instruction files.

## How it works

**One brain, many adapters.** All agent instructions live in [AGENTS.md](./AGENTS.md). Every tool either reads it natively or gets a thin pointer file that redirects to it. Tool-specific quirks (and nothing else) go in the pointer files.

| Tool | Entry point | How it's wired |
|------|------------|----------------|
| OpenAI Codex | `AGENTS.md` | Native — reads it out of the box |
| Amp, OpenCode, Jules | `AGENTS.md` | Native — reads it out of the box |
| Claude Code | [`CLAUDE.md`](./CLAUDE.md) | Pointer → AGENTS.md |
| Cursor | [`.cursor/rules/agents.mdc`](./.cursor/rules/agents.mdc) | Always-on rule → AGENTS.md |
| GitHub Copilot | [`.github/copilot-instructions.md`](./.github/copilot-instructions.md) | Pointer → AGENTS.md |
| Gemini CLI / Code Assist | [`GEMINI.md`](./GEMINI.md) | Pointer → AGENTS.md |
| Windsurf | [`.windsurf/rules/agents.md`](./.windsurf/rules/agents.md) | Always-on rule → AGENTS.md |
| Cline / Roo Code | [`.clinerules`](./.clinerules) | Pointer → AGENTS.md |
| Aider | [`.aider.conf.yml`](./.aider.conf.yml) | Loads AGENTS.md into every session |

A tool not listed? Almost every agent supports custom instruction files — add one more pointer and you're done.

## What's inside

```
repo/
├── AGENTS.md                     ← the single source of truth for AI agents
├── CLAUDE.md, GEMINI.md, .cursor/, .github/copilot-instructions.md, ...
│                                 ← thin per-tool pointers to AGENTS.md
├── README.project.md             ← README template for YOUR project (becomes README.md)
├── CONTRIBUTING.md               ← git/PR workflow, Conventional Commits
├── TEMPLATE-GUIDE.md             ← setup instructions (delete after setup)
├── docs/
│   ├── GLOSSARY.md               ← domain terms, invariants, naming traps
│   ├── architecture/             ← system overview with diagrams
│   ├── decisions/                ← ADRs: why it's built this way
│   └── guides/                   ← recipes for common tasks
├── apps/example-app/AGENTS.md    ← nested agent rules (copy per app)
└── packages/example-package/     ← package README template (copy per package)
```

The structure maps each failure mode to a fix:

| Agents fail because they don't know… | Solved by |
|--------------------------------------|-----------|
| the rules (commands, conventions, hard limits) | `AGENTS.md` (root + nested) |
| the map (what lives where, how parts connect) | `README`, `docs/architecture/`, package READMEs |
| the domain (what a "Tenant" means, invariants) | `docs/GLOSSARY.md` |
| the history (why it's built this way) | `docs/decisions/` (ADRs) |
| the recipes (how we do common tasks) | `docs/guides/` |

## Getting started

1. Click **Use this template** on GitHub (or clone this repo).
2. Follow the checklist in [TEMPLATE-GUIDE.md](./TEMPLATE-GUIDE.md): fill in placeholders, replace this README with `README.project.md`, write your glossary and first ADRs.
3. Delete `TEMPLATE-GUIDE.md` and the example app/package.
4. Point your favorite agent at the repo and start building.

## Principles

- **Docs change with code.** A PR that changes commands or structure updates the docs in the same PR.
- **AGENTS.md stays short.** Target < 150 lines at the root; details live in `docs/` and get linked.
- **Every repeated explanation becomes a guide.** Explained it twice? It's now `docs/guides/<task>.md`.
- **Agent mistakes are doc bugs.** If the AI keeps doing the wrong thing, fix AGENTS.md — not your prompt.

## Contributing

Issues and PRs welcome — especially pointer files for tools not yet covered and improvements to the doc templates. See [CONTRIBUTING.md](./CONTRIBUTING.md).

## License

[MIT](./LICENSE)
