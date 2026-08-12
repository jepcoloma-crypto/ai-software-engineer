# Prompt Corrector

This document describes the Prompt Corrector, the framework's front-of-pipeline
gateway that transforms an imperfect user request into a clear, structured,
verifiable engineering request before the existing engineering workflows begin.

## Position

The Prompt Corrector sits between the raw user request and the existing
framework lifecycle:

```
USER REQUEST
    ↓
PROMPT CORRECTOR   (agent + correct command + prompt-corrector skill)
    ↓
Corrected / Clarified Prompt   (templates/corrected-prompt.md)
    ↓
Existing Workflow   (REQUIREMENTS → RESEARCH → ANALYSIS → ARCHITECTURE →
                     PLAN → IMPLEMENT → TEST → REVIEW → SECURITY REVIEW →
                     DOCUMENT → COMPLETE)
    ↓
Prompt Loop Engineering   (separate future phase, not implemented)
```

The corrector is a **recommended gateway**, not a mandatory lifecycle stage.
It is not a coding agent: it does not implement, design, research, or review
application work, and it does not replace any of the existing agents. It
prepares the request so that the correct existing workflow can begin.

## Output states

- **READY_FOR_WORKFLOW** — the readiness gate is satisfied; the corrector emits
  a corrected engineering prompt and recommends an existing workflow.
- **NEEDS_CLARIFICATION** — blocking uncertainty remains; the corrector emits
  minimal, targeted questions and does not start engineering work.
- **INVALID_REQUEST** — the request is not engineering work, is vacuous, or is
  safety-incompatible; the corrector stops without reinterpreting it silently.

`REQUIRES_RESEARCH` is a non-blocking annotation: a request can be
READY_FOR_WORKFLOW with an evidence gap deferred to the RESEARCH step.

## Readiness gate

A request is READY_FOR_WORKFLOW only when all of the following hold:

- Intent and objective are unambiguous.
- No blocking unknowns remain.
- Every contradiction is resolved or explicitly accepted by the user.
- Scope is bounded (stated in/out of scope, or the request is single-purpose).
- Provisional, testable acceptance criteria exist and the user can confirm them.
- A concrete existing workflow can be recommended.
- The request is not safety-incompatible.

## Evidence taxonomy

Every claim is labeled: USER REQUIREMENT (stated by the user), REPOSITORY FACT
(verified by repository inspection, with a file/line citation), CONFIRMED FACT
(verified against an authoritative source), INFERRED ASSUMPTION (unconfirmed,
surfaced for user agreement), UNKNOWN (blocking or non-blocking), or
REQUIRES RESEARCH (deferred to the RESEARCH step). Assumptions are never
converted into facts, and contradictions are never silently resolved.

## Clarification strategy

Questions are minimal, specific, and grouped into blocking and optional. The
corrector does not ask what the repository or existing documentation can
answer, and does not ask preference questions where the repository already
establishes the answer. Optional questions carry a proposed default so the user
may answer none and still proceed.

## Components

| Component | Path | Role |
| --- | --- | --- |
| Agent | `.opencode/agents/prompt-corrector.md` | Authoritative (read-only) role definition |
| Command | `.opencode/commands/correct.md` | User-facing entry point |
| Skill | `.opencode/skills/prompt-corrector/SKILL.md` | Correction method and readiness gate |
| Template | `templates/corrected-prompt.md` | Canonical output structure |

## Integration

The `correct` command is intended to be run before starting an engineering
workflow. `workflows/new-project.md` and `workflows/feature-development.md`
require the request to pass the corrector's gate (or to have blocking
clarification resolved) before their requirement steps proceed. The guardrail
is also stated in `rules/core.md`. The other workflows are not modified; the
corrector is not embedded into every workflow.

## Relation to existing content

- The `requirements-analysis` skill covers detailed requirement gathering
  inside a workflow; the `prompt-corrector` skill does not restate it.
- The `analyze` command performs deeper codebase impact analysis; the corrector
  only labels repository facts and detects contradictions.
- The output follows `templates/corrected-prompt.md` and its vocabulary aligns
  with `templates/requirements.md` to avoid duplicated artifacts.

## Verification

Authenticate this documentation against the actual framework: the corrector is
read-only, gated as READY_FOR_WORKFLOW / NEEDS_CLARIFICATION / INVALID_REQUEST,
and never invents requirements, technologies, APIs, or project behavior.