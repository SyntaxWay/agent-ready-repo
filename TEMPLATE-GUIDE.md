# How to Use This Template (delete this file after setup)

## The philosophy

AI agents fail for one of three reasons: they don't know the **rules**, they don't know the
**map**, or they don't know the **domain**. This template gives each its own home:

| Problem | Solved by |
|---------|-----------|
| Doesn't know the rules (commands, conventions, hard limits) | `AGENTS.md` (root + nested) |
| Doesn't know the map (what lives where, how parts connect) | `README.md`, `docs/architecture/`, package READMEs |
| Doesn't know the domain (what a "Tenant" means, invariants) | `docs/GLOSSARY.md` |
| Doesn't know the history (why it's built this way) | `docs/decisions/` (ADRs) |
| Doesn't know the recipes (how we do common tasks) | `docs/guides/` |

## File tree

```
repo/
├── AGENTS.md                     ← AI entry point (the most important file)
├── CLAUDE.md                     ← thin pointer to AGENTS.md + Claude Code-only notes
├── GEMINI.md                     ← thin pointer to AGENTS.md + Gemini-only notes
├── .clinerules                   ← thin pointer to AGENTS.md (Cline / Roo Code)
├── .aider.conf.yml               ← loads AGENTS.md into Aider sessions
├── .cursor/
│   └── rules/agents.mdc          ← always-on Cursor rule → AGENTS.md
├── .windsurf/
│   └── rules/agents.md           ← always-on Windsurf rule → AGENTS.md
├── README.md                     ← about this template (replaced during setup)
├── README.project.md             ← README template for your project
├── CONTRIBUTING.md               ← git/PR workflow
├── LICENSE                       ← MIT (replace with your project's license)
├── TEMPLATE-GUIDE.md             ← this file (delete after setup)
├── .github/
│   ├── copilot-instructions.md   ← thin pointer to AGENTS.md (GitHub Copilot)
│   └── PULL_REQUEST_TEMPLATE.md
├── docs/
│   ├── GLOSSARY.md               ← domain terms, invariants, naming traps
│   ├── architecture/
│   │   └── system-overview.md    ← C4-ish overview, Mermaid diagrams
│   ├── decisions/
│   │   ├── 0000-adr-template.md
│   │   └── 0001-use-pnpm-and-turborepo.md  ← example
│   └── guides/
│       ├── README.md             ← recipe index + recipe format
│       └── coding-standards.md
├── apps/
│   └── example-app/
│       └── AGENTS.md             ← nested agent rules (copy per app)
└── packages/
    └── example-package/
        └── README.md             ← package README template (copy per package)
```

## Setup checklist

1. Replace the root `README.md` (which describes this template) with `README.project.md`:
   `mv README.project.md README.md`
2. Replace all `[PROJECT_NAME]` / `[...]` placeholders and the example table rows.
3. Copy `apps/example-app/AGENTS.md` into each real app; copy the package README into each real package.
4. Fill `docs/GLOSSARY.md` from your database schema — every table/entity gets a row.
5. Write ADR-0001..000N for the big decisions you've already made (stack, DB, auth approach).
6. Update `LICENSE` to whatever fits your project (delete it if the code is private).
7. Delete `example-app`, `example-package`, and this file.

## Which AI tools are covered

`AGENTS.md` is the single source of truth. OpenAI Codex, Amp, OpenCode, and Jules read it
natively. Claude Code (`CLAUDE.md`), Gemini (`GEMINI.md`), Cursor (`.cursor/rules/`),
Windsurf (`.windsurf/rules/`), Cline / Roo Code (`.clinerules`), GitHub Copilot
(`.github/copilot-instructions.md`), and Aider (`.aider.conf.yml`) are wired to it via thin
pointer files. Delete the pointer files for tools your team doesn't use, and put
tool-specific quirks ONLY in the pointer files — everything shared belongs in AGENTS.md.

## Maintenance rules (put these in your team norms)

- **Docs change with code.** A PR that changes commands, structure, or behavior updates the docs in the same PR — the checklist enforces it.
- **AGENTS.md stays short.** Target < 150 lines at the root. Details go to `docs/`, linked from AGENTS.md.
- **Every repeated explanation becomes a guide.** Explained it twice in Slack? It's now `docs/guides/<task>.md`.
- **Agent mistakes are doc bugs.** If the AI keeps doing the wrong thing, the fix is usually a line in AGENTS.md or a Known Gotcha, not a longer prompt.
