---
description: Perform a security review of the specified project, feature, API, or component using the security agent.
---

You are running the `security` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including `rules/security.md` and `rules/core.md`. Do not assume a specific technology stack; analyze the actual code and configuration.

# Task

Perform a security review of the specified target:

$ARGUMENTS

# Responsibilities

- Use the `security` agent to perform the review.
- Analyze, as applicable: authentication, authorization, secrets handling, input validation, injection risks (SQL, command, template), XSS, CSRF, dependency risk, file handling, rate limiting, session management, and security configuration.
- Analyze the threat model and trust boundaries relevant to the target.
- Report each finding with evidence, severity, and an actionable recommendation.
- Do not claim a vulnerability is verified without evidence; distinguish confirmed findings from potential risks.

# Tools, skills, and references

- Use the `security-review` skill to guide the review and `templates/security-review.md` / `workflows/security-review.md` to structure the process.
- Use `rules/security.md`, `rules/database.md`, and `rules/api.md` as relevant to the target.

# Constraints

- Do not expose secrets or credentials; when a secret is found in code, report its location and risk without printing the value.
- Do not bypass or disable security controls.
- Do not perform unauthorized or destructive security testing without human approval.
- Prefer evidence over assumptions; label speculative findings as such.

# Output

Report:
1. Scope of the review and the security boundaries analyzed.
2. Findings grouped by severity, each with evidence, impact, and recommended fix.
3. Confirmed issues vs. potential risks (with reasoning).
4. Any items requiring immediate action or human approval.