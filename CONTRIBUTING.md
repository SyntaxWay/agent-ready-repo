# Contributing

## Workflow

1. Branch from `main`: `feat/<ticket>-short-desc` or `fix/<ticket>-short-desc`
2. Make changes; keep PRs to one logical change
3. Ensure `pnpm lint && pnpm test` pass
4. Open a PR using the template; link the ticket
5. 1 approval required; squash-merge with a Conventional Commit title

## Commit Messages (Conventional Commits)

```
feat(api): add policy priority ordering
fix(web): prevent double submit on signup
docs: update glossary with Workspace definition
chore(deps): bump prisma to 6.2
```

Scopes = app/package names. Breaking changes: add `!` and a `BREAKING CHANGE:` footer.

## PR Checklist (also enforced by the PR template)

- [ ] Tests added/updated
- [ ] Docs updated (`AGENTS.md`, `docs/`, `.env.example`) if behavior/commands changed
- [ ] No secrets, no generated-file edits
- [ ] ADR added if the change alters architecture or public contracts

## Using AI Agents

AI-generated code is welcome and held to the same standard. You (the human) own what you merge:
review it, understand it, and make sure the agent followed `AGENTS.md`. If an agent repeatedly
makes the same mistake, that's a documentation bug — fix `AGENTS.md` or the relevant guide.
