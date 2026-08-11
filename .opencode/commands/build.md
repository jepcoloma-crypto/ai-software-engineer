---
description: Implement the approved plan using the developer agent, following existing conventions and verifying changes before claiming completion.
---

You are running the `build` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its before-coding and before-completion checks, and `rules/core.md` and `rules/coding.md`. Do not assume a specific technology stack; follow the actual project conventions.

# Task

Implement the approved plan or requested change:

$ARGUMENTS

# Responsibilities

- Use the `developer` agent to implement the change.
- Before changing code: inspect the repository, understand the architecture, identify relevant files, patterns, dependencies, database structures, and API contracts, and read the relevant skills and rules.
- Make focused changes that preserve existing behavior; follow existing conventions; reuse existing components.
- Validate changes: run relevant tests, type checks, linting, and build verification as applicable, and report actual results.
- Never claim completion without verification. Never claim tests or validation passed unless they were actually executed.
- If requirements or architecture are unclear, stop and ask for clarification rather than inventing decisions.
- Ask for human approval before destructive or high-risk operations (e.g., non-local database migrations, breaking API changes).

# Tools, skills, and references

- Use the relevant development skills (`backend-development`, `frontend-development`, `database-design`, `api-design`) and rules (`rules/database.md`, `rules/api.md`, `rules/frontend.md`, `rules/testing.md`, `rules/git.md`) as applicable to the change.
- Align with the appropriate workflow (`workflows/feature-development.md`, `workflows/bug-fix.md`, `workflows/database-change.md`, `workflows/api-change.md`).

# Constraints

- Never expose credentials or secrets in code, logs, or output.
- Keep changes focused on the requested task; avoid unrelated edits and premature abstraction.
- Prefer evidence over assumptions; do not fabricate technical facts.

# Output

Report:
1. What was implemented and the files changed.
2. How each change was verified (actual test/typecheck/lint/build results, not assumptions).
3. Anything left unverified or requiring follow-up.
4. Any safety or approval concerns encountered.