---
description: Create or update technical documentation for the specified project, feature, architecture, API, deployment, decision, or change using the documentation agent.
---

You are running the `document` command of the AI Software Engineer framework.

First, read and follow AGENTS.md and `rules/documentation.md`. Do not assume a specific technology stack; document the actual implementation.

# Task

Create or update documentation for:

$ARGUMENTS

# Responsibilities

- Use the `documentation` agent to produce or update the documentation.
- Inspect the actual code, configuration, and architecture before writing; document only what exists or is decided.
- Keep documentation synchronized with the actual implementation; update existing docs when the implementation changes.
- Do not fabricate undocumented behavior, APIs, or configuration.
- Identify the correct location (e.g., `docs/`) and the appropriate template for the artifact.

# Tools, skills, and references

- Use `rules/documentation.md` for conventions.
- Use the matching template for the artifact type: `templates/architecture.md`, `templates/decision.md` (ADR), `templates/implementation-plan.md`, `templates/project-summary.md`, `templates/requirements.md`, `templates/research.md`, `templates/security-review.md`, `templates/testing.md`.
- Align with the relevant workflow (`workflows/feature-development.md`, `workflows/api-change.md`, `workflows/database-change.md`, `workflows/deployment.md`, `workflows/refactoring.md`).

# Constraints

- Never fabricate technical facts; attribute claims to the actual implementation.
- Do not expose secrets or credentials in documentation.
- Keep documentation scope aligned with the requested artifact.

# Output

Report:
1. The documentation created or updated and where it lives.
2. The source material (files, decisions, requirements) used.
3. Any gaps where documentation could not be verified against the implementation.
4. Any existing docs that should be updated but were out of scope.