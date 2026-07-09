# Glossary — Domain Terms & Business Rules

> This is the most underrated file for AI comprehension. Code uses domain words;
> if the AI doesn't know what a "Tenant" or "Policy" means IN YOUR PRODUCT, it will guess wrong.
> Keep entries short. Link to code where the concept lives.

## Terms

| Term | Meaning in this product | Code location |
|------|------------------------|---------------|
| **Tenant** | A paying customer organization. All data is scoped by `tenant_id`. | `packages/core/tenant/` |
| **Workspace** | A sub-division inside a Tenant (e.g., a team). Users belong to workspaces, not tenants directly. | `packages/core/workspace/` |
| **Policy** | A rule set applied to requests, evaluated in order of `priority` (lower = first). | `packages/core/policy/` |
| **Plan** | Billing tier: `free`, `pro`, `enterprise`. Feature gates read from `packages/core/plans.ts`. | `packages/core/plans.ts` |

<!-- TEMPLATE: add every noun that appears in your database schema or API. -->

## Invariants & Business Rules (things that must ALWAYS be true)

1. A User always belongs to ≥1 Workspace. Deleting the last workspace membership deletes the user's tenant access.
2. `tenant_id` is required on every query touching tenant data — enforced by the Prisma middleware in `apps/api/src/db/tenancy.ts`. Never bypass it.
3. Soft-delete only: rows get `deleted_at`, they are never hard-deleted (compliance requirement).
4. All monetary values are stored as integer minor units (fils/cents), never floats.

## Naming Traps (same word, different meanings)

- **"Project"** in the UI = **"Workspace"** in the code/DB. (Renamed in marketing, not in schema — see ADR-0007.)
- **"Admin"** means tenant admin, NOT platform superuser. Superusers are called **"Operators"**.
