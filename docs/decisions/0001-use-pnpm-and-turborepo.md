# ADR-0001: Use pnpm workspaces + Turborepo for the monorepo

- **Status:** Accepted
- **Date:** 2026-01-15
- **Deciders:** Platform team

## Context

We have multiple apps sharing UI components and domain logic. We need fast installs, strict
dependency boundaries, and cached builds in CI.

## Options Considered

1. **npm workspaces** — zero extra tooling, but slow installs and phantom dependency issues.
2. **Nx** — powerful, but heavier config surface than we need today.
3. **pnpm + Turborepo (chosen)** — strict node_modules (catches phantom deps), remote build cache, minimal config.

## Decision

pnpm for package management, Turborepo for task orchestration and caching.

## Consequences

- **Positive:** installs are ~3x faster; deep-import bugs surface at install time; CI caching works.
- **Negative:** contributors must install pnpm; some tools assume npm and need config tweaks.
- **For future code:** never commit `package-lock.json` or `yarn.lock`; all task scripts are defined in `turbo.json`.

## Follow-ups

- [x] Add pnpm version pin via `packageManager` field in root package.json
