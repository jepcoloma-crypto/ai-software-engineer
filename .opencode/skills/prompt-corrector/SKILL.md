---
name: prompt-corrector
description: Use to transform an unclear, incomplete, ambiguous, contradictory, or poorly structured user request into a clear, structured, implementation-ready engineering prompt before the engineering workflow begins. Use for intent determination, requirement extraction, ambiguity and contradiction and assumption detection, clarification, acceptance criteria, and readiness assessment.
---

# Prompt Corrector

## When to use

Use as a recommended pre-workflow gateway before starting an engineering
workflow when a request is unclear, incomplete, ambiguous, contradictory, or
poorly structured. The Prompt Corrector is read-only and its methodology is
provider-independent. It does not implement, design, research, or review
application work, and it does not modify files. It prepares the request so the
correct existing workflow can begin.

## Step 1 — Understand Intent

Determine:

- what the user wants
- why they want it
- the expected outcome
- the primary users
- the system and business context

## Step 2 — Extract Explicit Requirements

Separate everything explicitly stated by the user. Preserve the user's
original intent rather than unnecessarily expanding scope.

## Step 3 — Identify Missing Requirements

Check the relevant categories:

- users
- roles
- permissions
- workflows
- business rules
- data
- integrations
- notifications
- reports
- audit trail
- security
- performance
- scalability
- deployment
- technology constraints

Do not force irrelevant categories onto small requests.

## Step 4 — Detect Ambiguity

Identify statements that could have multiple interpretations. Mark unresolved
ambiguity as `[CLARIFICATION REQUIRED]`.

## Step 5 — Detect Contradictions

Identify requirements that conflict with each other. Surface the conflict for
the user; do not silently pick a resolution.

## Step 6 — Identify Assumptions

Clearly separate assumptions from confirmed requirements. Mark inferred facts
as `[ASSUMPTION — REQUIRES CONFIRMATION]`. Never present an assumption as a
requirement.

## Step 7 — Determine Clarifications

Create a prioritized list of questions only when answers materially affect
implementation. Do not ask what the repository or existing documentation can
establish.

## Step 8 — Produce Corrected Prompt

Generate an implementation-ready prompt that preserves the user's intent, using
`templates/corrected-prompt.md`.

## Step 9 — Define Acceptance Criteria

Create measurable, testable acceptance criteria where possible. Mark any
criteria inferred from assumptions as requiring confirmation.

## Step 10 — Readiness Assessment

Classify the request as:

- READY
- READY WITH ASSUMPTIONS
- NEEDS CLARIFICATION

Do not proceed to implementation. The corrected prompt and readiness assessment
are the final output.

## Output markers

- `[CLARIFICATION REQUIRED]` — information is missing or ambiguous in a way
  that materially affects implementation.
- `[ASSUMPTION — REQUIRES CONFIRMATION]` — an inferred fact the user has not
  confirmed.

## Readiness definitions

- **READY** — the request is clear and implementation-ready; no blocking
  clarification is needed.
- **READY WITH ASSUMPTIONS** — the request is usable if its tagged assumptions
  are confirmed; surface the assumptions for confirmation before work begins.
- **NEEDS CLARIFICATION** — missing or ambiguous information materially affects
  implementation; the prioritized questions must be answered before the request
  enters a workflow.

## Relationship to other framework content

- Use `templates/corrected-prompt.md` for the corrected prompt structure.
- Use `requirements-analysis` for detailed requirement gathering inside a
  workflow; the Prompt Corrector does not restate it.
- The `analyze` command performs deeper codebase impact analysis; the Prompt
  Corrector only prepares the request.
- Apply `rules/core.md`, including the ready-before-workflow guardrail.

## Completion

The request has been transformed into a clear, structured, implementation-ready
prompt that preserves the user's intent. Explicit requirements are separated
from assumptions, missing or ambiguous information is marked
`[CLARIFICATION REQUIRED]`, inferred facts are marked
`[ASSUMPTION — REQUIRES CONFIRMATION]`, acceptance criteria are proposed, and
the readiness assessment (READY, READY WITH ASSUMPTIONS, or NEEDS CLARIFICATION)
is stated. No implementation has been started.