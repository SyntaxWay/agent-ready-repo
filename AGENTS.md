# AGENTS.md — AI Agent Instructions (Root)

> This file is the single entry point for AI coding agents (Claude Code, Cursor, Copilot, Codex,
> Gemini, Windsurf, Cline, Aider, etc.). Read this FIRST before making any changes. Each app/package
> may have its own nested AGENTS.md with more specific rules — the nearest AGENTS.md to the file
> you're editing wins. Tool-specific pointer files (CLAUDE.md, GEMINI.md, .clinerules,
> .cursor/rules/, .windsurf/rules/, .github/copilot-instructions.md, .aider.conf.yml) all redirect
> here — shared rules belong in this file, never in the pointers.

## 1. Project Overview (one paragraph, keep it current)

<!-- TEMPLATE: Replace with 3-5 sentences. What does this product do? Who uses it? What is the core domain? -->
[PROJECT_NAME] is a [type of product] that [core value proposition] for [target users].
The monorepo contains [N] deployable apps and [N] shared packages.

## 2. Monorepo Map

| Path | What it is | Tech | Owner |
|------|-----------|------|-------|
| `apps/web` | Customer-facing web app | Next.js 15, TypeScript | @team-frontend |
| `apps/api` | REST/GraphQL backend | Node.js, Fastify | @team-backend |
| `packages/ui` | Shared component library | React, Tailwind | @team-frontend |
| `packages/core` | Domain logic, shared types | TypeScript (no framework deps) | @team-backend |
| `packages/config` | Shared ESLint/TS/Tailwind configs | — | @team-platform |
| `infra/` | IaC, Docker, K8s manifests | Terraform, Helm | @team-devops |

**Dependency rule:** `apps/*` may depend on `packages/*`. Packages may NOT depend on apps. `packages/core` must stay framework-free.

## 3. Golden Commands (always use these — never invent your own)

```bash
pnpm install              # install all workspace deps
pnpm dev                  # run all apps in dev mode
pnpm dev --filter web     # run one app
pnpm build                # build everything
pnpm test                 # run all tests
pnpm test --filter core   # test one package
pnpm lint                 # lint + typecheck
pnpm format               # auto-format (Prettier)
```

> If a command fails, do NOT work around it with ad-hoc scripts. Fix the root cause or ask.

## 4. Tech Stack & Versions

- **Language:** TypeScript 5.x, strict mode ON everywhere
- **Package manager:** pnpm workspaces (never use npm/yarn; do not commit package-lock.json)
- **Monorepo tooling:** Turborepo
- **Runtime:** Node 22 LTS
- **Database:** PostgreSQL 16 via Prisma (schema in `apps/api/prisma/schema.prisma`)
- **Testing:** Vitest (unit), Playwright (e2e)
- **CI:** GitHub Actions (`.github/workflows/`)

## 5. Hard Rules (violating these fails code review)

1. **Never** commit secrets, API keys, or `.env` files. Use `.env.example` to document required vars.
2. **Never** edit generated files (`*.gen.ts`, `dist/`, Prisma client). Regenerate instead.
3. **All** new code requires tests. Bug fixes require a regression test.
4. **All** cross-package imports go through the package's public entry (`packages/x/src/index.ts`) — no deep imports.
5. **Database changes** only via migrations (`pnpm db:migrate:dev`), never manual SQL against shared envs.
6. **Public API changes** (REST routes, GraphQL schema, package exports) require an ADR in `docs/decisions/`.
7. Do not add new dependencies without checking `docs/guides/dependencies.md` for approved alternatives.

## 6. Code Conventions (summary — full doc: docs/guides/coding-standards.md)

- Naming: `kebab-case` files, `PascalCase` components/types, `camelCase` functions/vars, `SCREAMING_SNAKE` env vars
- Prefer pure functions in `packages/core`; side effects live at app edges
- Errors: throw typed errors from `packages/core/errors`; never throw raw strings
- No `any`. Use `unknown` + narrowing. `// @ts-expect-error` requires a comment explaining why
- Comments explain WHY, not WHAT. Keep them rare and high-value

## 7. Where Things Live (fast lookup)

- Domain terms & business rules → `docs/GLOSSARY.md`
- System architecture & diagrams → `docs/architecture/`
- Why we chose X over Y → `docs/decisions/` (ADRs)
- How to do common tasks → `docs/guides/` (add a route, add a package, run migrations…)
- Environment variables → each app's `.env.example`
- API contracts → `apps/api/openapi.yaml` (source of truth)

## 8. Definition of Done (for any AI-generated change)

- [ ] `pnpm lint` and `pnpm test` pass locally
- [ ] New/changed behavior has tests
- [ ] No secrets, no generated-file edits, no deep imports
- [ ] Docs updated if behavior, commands, or architecture changed (including this file)
- [ ] Commit message follows Conventional Commits (`feat:`, `fix:`, `chore:`, `docs:`…)

## 9. What NOT to Touch

- `infra/production/` — human approval required
- `packages/legacy-billing/` — frozen; scheduled for removal, bug fixes only
- Anything under `third_party/`

## 10. When Unsure

Prefer asking over guessing when: changing auth, payments, data deletion, migrations, or anything under `infra/`. For everything else, follow existing patterns in the nearest similar file.
