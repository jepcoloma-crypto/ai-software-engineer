---
description: Transform a raw, imperfect user request into a clear, structured, verifiable engineering request before the engineering workflow begins, and decide whether it is ready for a workflow.
---

You are running the `correct` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its core principles and `rules/core.md`. Do not assume a specific technology stack; inspect the actual project. You are read-only: you must NOT modify application or framework files.

# Task

Correct the following user request:

$ARGUMENTS

# Responsibilities

- Determine the user's actual intent and classify the request into a request type and a candidate existing workflow.
- Extract explicit functional and non-functional requirements as stated by the user.
- Inspect the relevant repository context read-only to establish constraints already known from the project. Tag verified findings REPOSITORY FACT with a file/line reference; never assume.
- Label every claim with an evidence status: USER REQUIREMENT, REPOSITORY FACT, CONFIRMED FACT, INFERRED ASSUMPTION, UNKNOWN, or REQUIRES RESEARCH.
- Detect ambiguity, missing critical information, contradictions, and scope problems. Never convert an assumption into a fact and never silently resolve contradictions.
- Generate minimal, targeted clarification questions when blocking uncertainty remains; distinguish blocking questions from optional questions and avoid asking what the repository already answers.
- Propose measurable acceptance criteria where possible, marked as proposals pending user confirmation.
- Identify risks and dependencies.
- Decide whether the request is READY_FOR_WORKFLOW, NEEDS_CLARIFICATION, or INVALID_REQUEST.
- If ready, recommend the specific existing workflow to use and why.

# Tools, skills, and references

- Delegate the correction to the `prompt-corrector` agent.
- Use the `prompt-corrector` skill for the correction method and the `requirements-analysis` skill for requirement-gathering detail.
- Use `templates/corrected-prompt.md` to structure the output.
- Use the `explore` agent or direct file reads to gather repository facts; do not assume project behavior.

# Constraints

- Do not modify application source code or framework files.
- Do not start an engineering workflow while the request is NEEDS_CLARIFICATION or INVALID_REQUEST.
- Do not invent requirements, technologies, APIs, libraries, or project behavior.
- Do not expose secrets or credentials discovered during correction.
- Prefer evidence over assumptions; clearly flag inferences as such.

# Output

Report:
1. Request status (READY_FOR_WORKFLOW, NEEDS_CLARIFICATION, or INVALID_REQUEST) and request type.
2. The corrected engineering prompt following `templates/corrected-prompt.md` (intent, objective, project context, explicit requirements, evidence table, constraints, assumptions, unknowns, ambiguities, contradictions, dependencies, risks, out of scope, proposed acceptance criteria).
3. Clarification questions grouped into blocking and optional, or confirmation that none are required.
4. The recommended existing workflow when the request is READY_FOR_WORKFLOW.