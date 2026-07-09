# AGENTS.md — apps/example-app

> Nested agent instructions. Rules here OVERRIDE the root AGENTS.md for files in this app.
> Keep this file short — only what's different or specific to this app.

## What this app is

<!-- 1-2 sentences -->
The customer-facing web app. Server components by default; client components only when interactive.

## Commands (from repo root)

```bash
pnpm dev --filter example-app
pnpm test --filter example-app
pnpm build --filter example-app
```

## Local rules

- Routing: Next.js App Router. New pages go in `src/app/<route>/page.tsx`.
- Data fetching: server components call `packages/core` directly; client components use the typed API client in `src/lib/api.ts`. Never `fetch()` raw URLs.
- Styling: Tailwind only. No CSS modules, no styled-components. Design tokens in `packages/ui/tokens.ts`.
- State: URL state > server state (React Query) > local state. No global stores without an ADR.

## This app's structure

```
src/
├── app/          # routes (App Router)
├── components/   # app-specific components (shared ones → packages/ui)
├── lib/          # api client, auth helpers, utilities
└── styles/
```

## Known gotchas

<!-- The highest-value section. List traps that waste time. -->
- `middleware.ts` runs on the Edge runtime — no Node APIs there.
- Auth cookies are httpOnly; client components must use `useSession()`, never read cookies directly.
