# Coding Standards

> Full version of the summary in AGENTS.md §6. When examples conflict with old code,
> follow THIS document — old code may predate the standard.

## TypeScript

- `strict: true` everywhere. No `any`; use `unknown` and narrow.
- Prefer `type` over `interface` except for public package APIs that consumers extend.
- Exhaustive switch on unions — use the `assertNever` helper from `packages/core/utils`.

## File & Folder Naming

```
kebab-case.ts            # all files
use-thing.ts             # hooks prefixed with use-
thing.test.ts            # tests co-located next to source
thing.types.ts           # only if types are large; otherwise keep inline
```

## Module Structure (per package)

```
packages/<name>/
├── src/
│   ├── index.ts         # PUBLIC API — the only import path other packages may use
│   ├── <feature>/       # feature folders, not layer folders
│   └── internal/        # explicitly private helpers
├── package.json
└── README.md            # what/why/how of this package (see template)
```

## Error Handling

- Throw subclasses of `AppError` from `packages/core/errors` (they carry `code`, `httpStatus`, `isOperational`).
- Never swallow errors silently. Log with context or rethrow.
- User-facing messages come from the error `code` → i18n mapping, never from `error.message`.

## Testing

- Unit tests: Vitest, co-located, name = behavior ("rejects expired tokens", not "test1").
- Follow Arrange-Act-Assert; one behavior per test.
- e2e: Playwright in `apps/web/e2e/`; tag slow ones `@slow`.
- Test data via factories in `packages/testing/factories` — never inline giant objects.

## Git

- Conventional Commits: `feat(api): add policy priority ordering`
- Branch names: `feat/<ticket>-short-desc`, `fix/<ticket>-short-desc`
- One logical change per PR. PRs > ~400 lines of non-generated diff should be split.

## Comments & Docs

- Comments explain WHY. If you need a WHAT comment, the code is unclear — refactor.
- Every exported function in `packages/*` gets a one-line JSDoc.
- If your change alters behavior described in `docs/` or `AGENTS.md`, update those docs in the same PR.
