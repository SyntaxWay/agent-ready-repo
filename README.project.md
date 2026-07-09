# [PROJECT_NAME]

> One-line description of what this product does.

**AI agents:** read [AGENTS.md](./AGENTS.md) first. **Humans:** keep reading.

## Quick Start

```bash
git clone <repo-url> && cd <repo>
pnpm install
cp apps/api/.env.example apps/api/.env   # fill in values — see docs/guides/environment.md
pnpm dev
```

Open http://localhost:3000

## What's in this repo

| Path | Description |
|------|-------------|
| `apps/` | Deployable applications |
| `packages/` | Shared libraries (never deployed alone) |
| `docs/` | Architecture, decisions, guides, glossary |
| `infra/` | Infrastructure as code |

Full map with tech and owners: [AGENTS.md §2](./AGENTS.md#2-monorepo-map)

## Documentation Index

- 🧠 [AGENTS.md](./AGENTS.md) — rules for AI agents (and a great human onboarding doc)
- 🏗️ [Architecture](./docs/architecture/system-overview.md) — how the system fits together
- 📖 [Glossary](./docs/GLOSSARY.md) — domain terms and business rules
- 📜 [Decisions (ADRs)](./docs/decisions/) — why we built it this way
- 🛠️ [Guides](./docs/guides/) — how to do common tasks
- 🤝 [Contributing](./CONTRIBUTING.md) — branch, commit, and PR conventions

## Common Commands

See [AGENTS.md §3 Golden Commands](./AGENTS.md#3-golden-commands-always-use-these--never-invent-your-own).

## Support

- Bugs: open a GitHub issue with the `bug` template
- Questions: #[project-channel] on Slack
