You are converting THIS repository to the AI-ready monorepo template structure.
Source template: https://github.com/SyntaxWay/agent-ready-repo

Work through the phases below in order. After Phase 2, pause and show me a summary before continuing.

─────────────────────────────────────────────
PHASE 1 — DISCOVERY
─────────────────────────────────────────────

Read every file listed below that exists in this repo:

Project identity:
  README.md, README.rst, README.txt
  package.json, pyproject.toml, Cargo.toml, go.mod, build.gradle, pom.xml

AI tool files already present:
  CLAUDE.md, GEMINI.md, AGENTS.md, CODEX.md
  .cursorrules, .cursor/rules/
  .github/copilot-instructions.md
  .windsurf/rules/, .windsurfrules
  .clinerules, .roo/
  .aider.conf.yml, .aider.env
  .claude/, .gemini/, .continue/

Docs:
  docs/ (all files, up to 3 levels deep)
  CONTRIBUTING.md, CHANGELOG.md

CI / commands:
  .github/workflows/ (all files)
  Makefile, justfile, taskfile.yml

Summarise what you found:
  A) One paragraph: what does this project do, who uses it?
  B) Tech stack table: Language | Framework | Package manager | Runtime | Database | Test runner | CI
  C) Key commands: install, dev, build, test, lint (exact commands, not guesses)
  D) Monorepo map: every app/package path with a one-line description
  E) AI tool files found: list each file and its current content summary

─────────────────────────────────────────────
PHASE 2 — AI TOOL DETECTION & CONFIRMATION
─────────────────────────────────────────────

Based on Phase 1, identify which AI tools are in use by checking these indicators:

  Tool               | Indicator files / dirs
  ─────────────────────────────────────────────────────────────────────
  Claude Code        | CLAUDE.md  ·  .claude/
  Cursor             | .cursorrules  ·  .cursor/rules/
  GitHub Copilot     | .github/copilot-instructions.md
  Gemini CLI         | GEMINI.md  ·  .gemini/
  Windsurf           | .windsurfrules  ·  .windsurf/rules/
  Cline / Roo Code   | .clinerules  ·  .roo/
  Aider              | .aider.conf.yml  ·  .aider.env
  Codex / Amp /      |
    OpenCode / Jules  | AGENTS.md (these read it natively — no pointer file needed)

Then ask the user:

  "I detected these tools: [LIST].
   - Any tools to ADD that aren't listed?
   - Any tools to REMOVE (their files will be deleted)?
   - Reply with the final list or say 'keep as-is'."

Wait for the user's reply before doing anything else.

─────────────────────────────────────────────
PHASE 3 — CREATE / REWRITE AGENTS.md
─────────────────────────────────────────────

IMPORTANT: Re-read this file (.claude/commands/migrate.md) now to ensure you have
the full template below — long Phase 1/2 conversations can compress it out of context.

Using the facts from Phase 1, write AGENTS.md at the repo root.
If one already exists, rewrite it — don't merge stale content.
Use this exact structure (keep all 10 sections, fill every placeholder):

────────────────────────────────────────────────────────────────────────
# AGENTS.md — AI Agent Instructions (Root)

> This file is the single entry point for AI coding agents (list confirmed
> tools from Phase 2). Read this FIRST before making any changes.
> Each app/package may have its own nested AGENTS.md — nearest one wins.
> Tool-specific pointer files all redirect here; shared rules belong here.

## 1. Project Overview
[3-5 sentences from Phase 1-A. What does it do? Who uses it? Core domain?]

## 2. Monorepo Map

| Path | What it is | Tech | Owner |
|------|-----------|------|-------|
[one row per app/package from Phase 1-D. Use "?" for unknown owners.]

**Dependency rule:** [derive from the project, or default: apps/* may depend on
packages/*. Packages may NOT depend on apps. Keep shared logic framework-free.]

## 3. Golden Commands (always use these — never invent your own)

```bash
[exact commands from Phase 1-C — install, dev, build, test, lint, format]
```

> If a command fails, do NOT work around it. Fix the root cause or ask.

## 4. Tech Stack & Versions

[bulleted list from Phase 1-B — include major version numbers where known]

## 5. Hard Rules (violating these fails code review)

1. Never commit secrets, API keys, or .env files.
2. Never edit generated files. Regenerate instead.
3. All new code requires tests. Bug fixes require a regression test.
4. [Add 2-3 more rules specific to THIS project — infer from CI, linting config, existing docs]

## 6. Code Conventions (summary — full doc: docs/guides/coding-standards.md)

[Infer from existing code style, .eslintrc, .prettierrc, pyproject.toml [tool.ruff], etc.
Cover: naming, error handling, comments policy, typing discipline.]

## 7. Where Things Live (fast lookup)

- Domain terms & business rules → docs/GLOSSARY.md
- System architecture & diagrams → docs/architecture/
- Why we chose X over Y → docs/decisions/ (ADRs)
- How to do common tasks → docs/guides/
- Environment variables → each app's .env.example
[Add any project-specific pointers]

## 8. Definition of Done (for any AI-generated change)

- [ ] `[lint command]` and `[test command]` pass locally
- [ ] New/changed behaviour has tests
- [ ] No secrets, no generated-file edits
- [ ] Docs updated if behaviour, commands, or architecture changed
- [ ] Commit message follows [Conventional Commits / whatever style is used]

## 9. What NOT to Touch

[List frozen paths, production infra dirs, legacy code — infer from
.github/CODEOWNERS, comments in code, or leave a TODO if none found.]

## 10. When Unsure

Prefer asking over guessing for: auth, payments, data deletion, migrations, production infra.
For everything else, follow the nearest similar file in the codebase.
────────────────────────────────────────────────────────────────────────

─────────────────────────────────────────────
PHASE 4 — CREATE TOOL POINTER FILES
─────────────────────────────────────────────

For each tool confirmed in Phase 2, create or update the pointer file shown below.
DELETE the pointer file for any tool NOT in the confirmed list (see Phase 6).

CLAUDE CODE — write CLAUDE.md:
  # CLAUDE.md
  See [AGENTS.md](./AGENTS.md) — single source of truth for all AI agents.
  Claude-specific notes (only add things that apply ONLY to Claude Code):
  - [any Claude-specific tips found in existing CLAUDE.md, or leave empty]

CURSOR — write .cursor/rules/agents.mdc:
  ---
  description: Root agent rules — always read AGENTS.md first
  alwaysApply: true
  ---
  See [AGENTS.md](../../AGENTS.md) — single source of truth for all AI agents.
  Cursor-specific notes:
  - [any tips found in existing .cursorrules, or leave empty]

GITHUB COPILOT — write .github/copilot-instructions.md:
  # GitHub Copilot Instructions
  See [AGENTS.md](../AGENTS.md) — single source of truth for all AI agents.
  Copilot-specific notes:
  - [any tips from existing file, or leave empty]

GEMINI CLI — write GEMINI.md:
  # GEMINI.md
  See [AGENTS.md](./AGENTS.md) — single source of truth for all AI agents.
  Gemini-specific notes:
  - [any Gemini-specific tips, or leave empty]

WINDSURF — write .windsurf/rules/agents.md:
  ---
  trigger: always_on
  description: Root agent rules — always read AGENTS.md first
  ---
  See AGENTS.md at the repo root — single source of truth for all AI agents.
  Windsurf-specific notes:
  - [any tips, or leave empty]

CLINE / ROO CODE — write .clinerules:
  # Cline Rules
  See AGENTS.md at the repo root — single source of truth for all AI agents.
  Cline-specific notes:
  - [any tips from existing .clinerules, or leave empty]

AIDER — write .aider.conf.yml:
  # Aider configuration — https://aider.chat/docs/config/aider_conf.html
  read:
    - AGENTS.md

Codex / Amp / OpenCode / Jules — NO pointer file needed. They read AGENTS.md natively.

─────────────────────────────────────────────
PHASE 5 — CREATE DOCS STRUCTURE
─────────────────────────────────────────────

IMPORTANT: Re-read this file (.claude/commands/migrate.md) now to ensure you have
the full file list below — long Phase 1-4 runs can compress it out of context.
You MUST create every missing file in this phase. Do NOT list them as "next steps."

Check which of these exist. Create any that are MISSING.
If a file exists with real content, leave it alone.
If a file exists as an empty placeholder, update it from Phase 1 facts.

docs/GLOSSARY.md
  - Table of domain terms (every noun from DB schema / API), invariants, naming traps

docs/architecture/system-overview.md
  - C4-style overview: components, data flow, deployment
  - Include a Mermaid diagram if topology can be inferred from the code

docs/decisions/0000-adr-template.md
  - Standard ADR template (Status / Context / Decision / Consequences)

docs/guides/README.md
  - Index of guides with one-line descriptions

docs/guides/coding-standards.md
  - Full coding conventions (expand AGENTS.md §6)

CONTRIBUTING.md
  - Branch naming, commit style, PR process, AI agent policy
  - Only create if missing; never overwrite an existing one

.github/PULL_REQUEST_TEMPLATE.md
  - Checklist that mirrors AGENTS.md §8 Definition of Done

─────────────────────────────────────────────
PHASE 6 — CLEAN UP OLD AI TOOL FILES
─────────────────────────────────────────────

Delete every AI tool file for tools NOT in the confirmed list.

Delete map:
  Claude Code removed  → delete CLAUDE.md, .claude/settings.json (leave other .claude/ content)
  Cursor removed       → delete .cursor/rules/agents.mdc  (delete .cursor/ dir if now empty)
  Copilot removed      → delete .github/copilot-instructions.md
  Gemini removed       → delete GEMINI.md
  Windsurf removed     → delete .windsurf/rules/agents.md  (delete .windsurf/ dir if now empty)
  Cline removed        → delete .clinerules
  Aider removed        → delete .aider.conf.yml

Also delete legacy single-file formats replaced by this structure:
  .cursorrules    → replaced by .cursor/rules/agents.mdc
  .windsurfrules  → replaced by .windsurf/rules/agents.md
  CODEX.md        → obsolete; Codex reads AGENTS.md natively

─────────────────────────────────────────────
PHASE 7 — AUTOMATED DOCS SYNC (CI PIPELINE)
─────────────────────────────────────────────

AGENTS.md and docs/ are owned by the CI pipeline, not by local agents.
After this phase, every merge to main automatically updates the docs via
an LLM — no human or local agent should ever write to these files directly.

Step 1: Copy the docs-sync workflow into this repo.
  Create .github/workflows/docs-sync.yml with this content:
  https://github.com/SyntaxWay/agent-ready-repo/blob/main/.github/workflows/docs-sync.yml

Step 2: Add LLM credentials to GitHub Secrets.
  GitHub repo → Settings → Secrets and variables → Actions → New secret

  Choose ONE provider (the workflow auto-detects whichever secrets are present):

  OPTION A — Anthropic Claude (recommended)
    ANTHROPIC_API_KEY      your key from console.anthropic.com/settings/keys

  OPTION B — Azure OpenAI
    AZURE_OPENAI_API_KEY       your key from the Azure portal
    AZURE_OPENAI_ENDPOINT      e.g. https://my-resource.openai.azure.com
    AZURE_OPENAI_DEPLOYMENT    your deployment name, e.g. gpt-4o
    AZURE_OPENAI_API_VERSION   (optional) defaults to 2024-08-01-preview

  OPTION C — OpenAI
    OPENAI_API_KEY         your key from platform.openai.com
    OPENAI_MODEL           (optional) defaults to gpt-4o

  Auto-detection order: Anthropic → Azure OpenAI → OpenAI (first found wins)

Step 3: Allow Actions to push back to main.
  GitHub repo → Settings → Actions → General → Workflow permissions
  → Select "Read and write permissions" → Save

Step 4: Add this read-only notice to the top of AGENTS.md (after the title line,
  before Section 1):

  > ⚠️  Auto-maintained by CI (docs-sync workflow). Do not edit manually.
  > Local agents: read this file and act on its instructions. Never write to it.
  > All doc updates flow through the main branch pipeline only.

Step 5: Ensure .claude/settings.json does NOT contain a Stop hook for docs.
  Local Claude Code sessions must be read-only with respect to AGENTS.md and docs/.
  If a Stop hook exists, remove it. The correct .claude/settings.json is just: {}

Step 6 (optional — recommended for teams): Protect docs from accidental human edits.
  Create .github/CODEOWNERS:
    AGENTS.md    @your-bot-or-maintainer-account
    docs/        @your-bot-or-maintainer-account
  This requires a review from the named account on any PR that touches these paths.

─────────────────────────────────────────────
PHASE 8 — SUMMARY REPORT
─────────────────────────────────────────────

Print a report in this format:

  Created:  [list every new file]
  Updated:  [list every modified file + one-line note on what changed]
  Deleted:  [list every deleted file]
  Skipped:  [files that already had real content and were left alone]

  Next steps:
  1. Fill in the [bracketed placeholders] remaining in AGENTS.md.
  2. Add domain terms to docs/GLOSSARY.md from your database schema.
  3. Write ADRs in docs/decisions/ for decisions already made (stack, auth, DB, etc.).
  4. Copy apps/example-app/AGENTS.md into each real app dir and customise it.
  5. Run your test suite to confirm nothing broke.
