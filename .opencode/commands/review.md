---
description: Review the current implementation or specified change using the reviewer agent for correctness, architecture, maintainability, security, performance, testing, and edge cases.
---

You are running the `review` command of the AI Software Engineer framework.

First, read and follow AGENTS.md and `rules/core.md`. Do not assume a specific technology stack; review against the project's actual conventions and stated requirements.

# Task

Review the current implementation or specified change:

$ARGUMENTS

# Responsibilities

- Use the `reviewer` agent to perform the review.
- Review for: correctness, architecture fit, maintainability, security, performance, testing coverage, error handling, and edge cases.
- Check that the change respects the intended scope, follows existing conventions, and preserves existing behavior.
- Do not modify any files.
- Report findings by severity (blocking / major / minor / nit) and identify recommended fixes for each.

# Tools, skills, and references

- Use the `code-review` skill to guide the review and `rules/` content relevant to the area under review (e.g., `rules/coding.md`, `rules/security.md`, `rules/testing.md`, `rules/api.md`, `rules/database.md`).
- Align with the relevant workflow's review stage (`workflows/feature-development.md`, `workflows/bug-fix.md`).

# Constraints

- Do not modify files; this command produces an assessment and recommendations only.
- Do not expose secrets discovered during review (report their presence without leaking values).
- Prefer evidence over assumptions; only report findings you can substantiate from the code.

# Output

Report:
1. A summary of the review scope (files/change reviewed).
2. Findings grouped by severity, each with the specific evidence (file/line or behavior) and a recommended fix.
3. What is verified vs. assumed.
4. An overall verdict, including whether the change is ready or what must be resolved first.