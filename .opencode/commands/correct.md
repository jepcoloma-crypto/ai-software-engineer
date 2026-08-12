---
description: Correct and normalize an unclear, incomplete, ambiguous, contradictory, or poorly structured user request into a clear, structured, implementation-ready engineering prompt before starting an engineering workflow. Invoke the prompt-corrector agent to determine intent, extract requirements, mark clarification gaps and assumptions, and assess readiness.
---

You are running the `correct` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its core principles and `rules/core.md`. This command is read-only: you must NOT modify files or implement anything. The Prompt Corrector is a recommended pre-workflow gateway, not a mandatory lifecycle step and not an implementation agent.

# Task

Correct the following user request:

$ARGUMENTS

Expected usage: `/correct <user request>`

# Responsibilities

- Invoke the `prompt-corrector` agent (and the `prompt-corrector` skill methodology) to process the request.
- Determine the user's original intent and the actual requested outcome. Preserve the intent rather than expanding scope.
- Extract explicit requirements and separate them from assumptions.
- Detect ambiguity, missing requirements, contradictions, and unrealistic assumptions.
- Identify users and actors, functional and non-functional requirements, integrations, data requirements, security considerations, reporting and audit requirements, acceptance criteria, and stated technical and business constraints.
- Mark missing information as `[CLARIFICATION REQUIRED]` and unconfirmed inferences as `[ASSUMPTION — REQUIRES CONFIRMATION]`.
- Assess implementation readiness and classify the request as READY, READY WITH ASSUMPTIONS, or NEEDS CLARIFICATION.

# Tools, skills, and references

- Delegate the correction to the `prompt-corrector` agent.
- Use the `prompt-corrector` skill for the methodology and the `requirements-analysis` skill for requirement-gathering detail.
- Use `templates/corrected-prompt.md` to structure the output.
- Use the `explore` agent or direct reads to confirm project context when needed; do not assume project behavior.

# Constraints

- Do not modify files or implement anything.
- Do not make final architecture decisions or choose technologies without evidence.
- Do not invent requirements, technologies, APIs, libraries, or project behavior.
- Do not pretend missing information is known; mark it as `[CLARIFICATION REQUIRED]`.
- Do not proceed to implementation; the command ends with the corrected prompt and readiness assessment.
- Do not expose secrets or credentials discovered during correction.

# Output

Report:
1. The corrected engineering prompt following `templates/corrected-prompt.md` (original request, intent, desired outcome, context, users/actors, explicit requirements, functional and non-functional requirements, business rules, data requirements, integrations, security requirements, reporting/audit requirements, technical constraints, assumptions, clarifications required, out of scope, acceptance criteria).
2. The implementation readiness assessment: READY, READY WITH ASSUMPTIONS, or NEEDS CLARIFICATION.
3. The final corrected prompt suitable for the engineering framework.