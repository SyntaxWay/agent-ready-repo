# Guides — Task Recipes

> Step-by-step recipes for common tasks. These are gold for AI agents:
> instead of reverse-engineering the pattern from code, the agent follows the recipe.
> Add a new guide whenever you explain the same thing twice.

## Index

- [coding-standards.md](./coding-standards.md) — style, structure, testing, git
- [environment.md](./environment.md) — env vars per app, how to get secrets
- [dependencies.md](./dependencies.md) — approved libraries, how to add a new one
- [add-api-endpoint.md](./add-api-endpoint.md) — recipe below is the pattern to copy

---

## Example Recipe Format (copy this structure for every guide)

### Add a new API endpoint

**When:** you need a new REST route in `apps/api`.

1. Define the route schema in `apps/api/src/routes/<domain>/schemas.ts` (zod).
2. Add the handler in `apps/api/src/routes/<domain>/handlers.ts` — handlers only parse/respond; logic goes in `packages/core`.
3. Register it in `apps/api/src/routes/<domain>/index.ts`.
4. Update `apps/api/openapi.yaml` (it is the contract source of truth).
5. Add tests: unit for the core logic, one integration test in `apps/api/test/routes/`.
6. Run `pnpm test --filter api && pnpm lint`.

**Reference example:** `apps/api/src/routes/policies/` is the canonical implementation to imitate.
