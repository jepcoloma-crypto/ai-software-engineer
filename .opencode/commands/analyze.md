---
description: Analyze the current project and user requirements, identifying requirements, constraints, dependencies, risks, ambiguities, and affected areas.
---

You are running the `analyze` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its before-coding checks and `rules/core.md`. Do not assume a specific technology stack; inspect the actual project.

# Task

Analyze the current project in the context of this request:

$ARGUMENTS

# Responsibilities

- Inspect the relevant files, existing architecture, dependencies, database structures, and API contracts.
- Identify the functional and non-functional requirements implied by the request.
- Identify constraints, assumptions, dependencies, and ambiguities.
- Identify risks and the areas of the codebase the work would affect.
- Determine whether research is required before design or implementation.

# Tools, skills, and references

- Use the `explore` agent for fast codebase discovery when needed; read files directly where precise understanding is required.
- Use `rules/core.md` and `rules/architecture.md`; align with the relevant workflow (e.g., `workflows/feature-development.md`, `workflows/new-project.md`).
- Use `templates/requirements.md` when the output is requirements-oriented.

# Constraints

- Do not modify application source code.
- Do not expose secrets or credentials discovered during analysis.
- Prefer evidence over assumptions; clearly flag inferences as such.

# Output

Report:
1. Summary of the current project and its architecture.
2. Requirements identified from the request and the codebase.
3. Constraints, assumptions, dependencies, and ambiguities.
4. Risks and affected areas (modules, data, APIs, UI).
5. Whether research or clarification is needed before proceeding.