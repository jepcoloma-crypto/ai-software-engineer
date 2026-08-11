---
description: Design the requested system or feature using the architect agent, producing architecture, modules, data flow, API boundaries, security boundaries, and tradeoffs.
---

You are running the `architect` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including `rules/core.md` and `rules/architecture.md`. Do not assume a specific technology stack; base the design on the actual project.

# Task

Design the requested system or feature:

$ARGUMENTS

# Responsibilities

- Use the `architect` agent to produce the design.
- Examine the relevant requirements, architecture, and affected areas before designing.
- Produce: architecture overview, modules and their responsibilities, data flow, integration points, API boundaries, database considerations, security boundaries, scalability and reliability considerations, tradeoffs, risks, and open questions.
- Identify where existing project conventions must be respected and where the design changes them.

# Tools, skills, and references

- Use the `system-architecture` skill to guide the design and `templates/architecture.md` to structure the output.
- Align with the appropriate workflow (`workflows/new-project.md`, `workflows/feature-development.md`, `workflows/database-change.md`, `workflows/api-change.md`).
- Use the `database` agent for schema-related design questions and the `api-design` skill for API boundaries where applicable.

# Constraints

- Do not implement application code.
- Do not silently modify critical architecture; call out proposed changes explicitly.
- Do not expose secrets in the design.
- Prefer evidence over assumptions; flag design decisions based on assumption rather than verified facts.

# Output

Report:
1. The design, including the sections above.
2. Tradeoffs and the rationale for each decision.
3. Risks and mitigations.
4. Open questions requiring clarification before implementation.