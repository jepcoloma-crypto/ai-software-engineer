---
description: Create a detailed implementation plan from approved requirements and architecture, covering phases, tasks, affected areas, validation gates, risks, and rollback.
---

You are running the `plan` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including `rules/core.md`. Do not assume a specific technology stack; base the plan on the actual project and approved design.

# Task

Create a detailed implementation plan for:

$ARGUMENTS

# Responsibilities

- Base the plan on the approved requirements and architecture (which you must inspect—do not invent them). If requirements or architecture are unclear or missing, stop and ask for clarification.
- Identify implementation phases and the tasks within each phase.
- Identify affected files/modules and the nature of each change.
- Identify database changes (e.g., migrations) and API changes, noting compatibility impact.
- Define the testing strategy and validation gates for each phase.
- Identify risks and rollback considerations.
- Identify what requires human approval before execution (destructive or high-risk operations, breaking changes, non-local migrations).

# Tools, skills, and references

- Use `templates/implementation-plan.md` to structure the output.
- Align with the appropriate workflow (`workflows/feature-development.md`, `workflows/new-project.md`, `workflows/refactoring.md`, `workflows/database-change.md`, `workflows/api-change.md`).
- Reference, but do not duplicate, the relevant skills and `rules/` content (e.g., `rules/testing.md`, `rules/database.md`, `rules/api.md`).

# Constraints

- Do not implement code.
- Keep the plan reusable across projects: no technology-specific assumptions beyond what the project establishes.
- Do not expose secrets.

# Output

Report:
1. The plan with phases and ordered tasks.
2. Affected files/modules, database changes, and API changes.
3. Testing strategy and validation gates.
4. Risks and mitigations.
5. Rollback considerations.
6. A list of items needing human approval before execution.