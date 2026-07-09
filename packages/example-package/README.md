# @acme/example-package

> Every package gets this README. 5 sections, keep it under a page.

## What

One sentence: what this package provides. Example: "Domain logic and types for the Policy engine."

## Why it exists

One-two sentences: why is this a separate package? What boundary does it protect?

## Public API

```ts
import { evaluatePolicy, type Policy, PolicyError } from "@acme/example-package";
```

Only import from the package root. Everything under `src/internal/` is private and may change without notice.

## Usage Example

```ts
const result = evaluatePolicy(policy, request);
if (!result.allowed) {
  throw new PolicyError(result.reason);
}
```

## Constraints

- No framework dependencies (no React, no Fastify) — this package must run anywhere.
- No I/O — callers pass data in; this package never touches DB/network.
