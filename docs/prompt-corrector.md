# Prompt Corrector

This document describes the Prompt Corrector, the framework's recommended
pre-workflow gateway that transforms an unclear, incomplete, ambiguous,
contradictory, or poorly structured user request into a clear, structured,
implementation-ready engineering prompt before the normal framework lifecycle
begins.

## Position

The Prompt Corrector sits between the raw user request and the existing
framework lifecycle, separate from the core lifecycle itself:

```
USER REQUEST
    ↓
PROMPT CORRECTOR   (agent + correct command + prompt-corrector skill)
    ↓
Corrected Prompt   (templates/corrected-prompt.md)
    ↓
Existing Workflow   (REQUIREMENTS → RESEARCH → ANALYSIS → ARCHITECTURE →
                     PLAN → IMPLEMENT → TEST → REVIEW → SECURITY REVIEW →
                     DOCUMENT → COMPLETE)
    ↓
Prompt Loop Engineering   (separate future phase, not implemented)
```

The corrector is a **recommended pre-workflow gateway**, not a mandatory first
step. It is read-only and does not implement, design, research, or review
application work, and it does not replace any of the existing agents. Its
methodology is provider-independent; only its OpenCode integration lives in
`.opencode/`.

## Readiness assessment

The corrector classifies the corrected prompt as:

- **READY** — the request is clear and implementation-ready; no blocking
  clarification is needed.
- **READY WITH ASSUMPTIONS** — the request is usable if its tagged assumptions
  are confirmed; assumptions are surfaced for confirmation before work begins.
- **NEEDS CLARIFICATION** — missing or ambiguous information materially affects
  implementation; the prioritized questions must be answered before the request
  enters a workflow.

## Output markers

- `[CLARIFICATION REQUIRED]` — information is missing or ambiguous in a way that
  materially affects implementation.
- `[ASSUMPTION — REQUIRES CONFIRMATION]` — an inferred fact the user has not
  confirmed. Assumptions are never presented as requirements, and
  contradictions are surfaced for the user rather than silently resolved.

## Methodology

The correction methodology is defined by the `prompt-corrector` skill in ten
steps: understand intent; extract explicit requirements; identify missing
requirements; detect ambiguity; detect contradictions; identify assumptions;
determine clarifications; produce the corrected prompt; define acceptance
criteria; and assess readiness. Irrelevant requirement categories are not
forced onto small requests.

## Components

| Component | Path | Role |
| --- | --- | --- |
| Agent | `.opencode/agents/prompt-corrector.md` | Authoritative (read-only) role definition |
| Command | `.opencode/commands/correct.md` | User-facing entry point (`/correct <user request>`) |
| Skill | `.opencode/skills/prompt-corrector/SKILL.md` | Correction methodology and readiness assessment |
| Template | `templates/corrected-prompt.md` | Canonical corrected prompt structure |

## Integration

The `correct` command is intended to be run before starting an engineering
workflow. `workflows/new-project.md` and `workflows/feature-development.md`
expect the request to be READY or READY WITH ASSUMPTIONS (or to have blocking
NEEDS CLARIFICATION questions resolved) before their requirement steps proceed.
The ready-before-workflow guardrail is also stated in `rules/core.md`. The other
workflows are not modified; the corrector is not embedded into every workflow,
and prompt correction is not mandatory.

## Relation to existing content

- The `requirements-analysis` skill covers detailed requirement gathering
  inside a workflow; the `prompt-corrector` skill does not restate it.
- The `analyze` command performs deeper codebase impact analysis; the corrector
  only prepares the request.
- The output follows `templates/corrected-prompt.md` and its vocabulary aligns
  with `templates/requirements.md` to avoid duplicated artifacts.

## Verification

Verify this documentation against the actual framework: the corrector is
read-only, gated as READY / READY WITH ASSUMPTIONS / NEEDS CLARIFICATION, uses
the `[CLARIFICATION REQUIRED]` and `[ASSUMPTION — REQUIRES CONFIRMATION]`
markers, and never invents requirements, technologies, APIs, libraries,
project behavior, or missing information.