# Framework Architecture

This document describes the layered architecture of the AI Software Engineer
framework: what each layer is, what lives in it, and how the layers relate.
It is framework documentation; it describes how the framework itself is
structured, not the architecture of any application built with it.

## Overall Architecture

The framework is organized into layers that separate distinct concerns:

1. **Constitution layer** â€” `AGENTS.md`: identity, principles, lifecycle, and
   safety.
2. **Agent layer** â€” `.opencode/agents/`: specialized agent roles and their
   permissions.
3. **Skill layer** â€” `.opencode/skills/`: loadable specialized knowledge.
4. **Rules layer** â€” `rules/`: enforceable engineering and safety guardrails.
5. **Workflow layer** â€” `workflows/`: repeatable procedures that orchestrate
   the other layers.
6. **Template layer** â€” `templates/`: reusable starting points for artifacts.
7. **Knowledge layer** â€” `knowledge/`: domain reference material.
8. **Command layer** â€” `.opencode/commands/`: the user-facing orchestration
   interface that exposes the framework workflows through OpenCode commands.
9. **Documentation layer** â€” `docs/`, `README.md`, `CONTRIBUTING.md`, and
   `LICENSE`: explanation, guidance, and licensing.

The constitution sits at the top. Agents, skills, rules, workflows, templates,
and knowledge all operate under it and must remain consistent with it.

## Constitution Layer (`AGENTS.md`)

The constitution defines what the framework is and how it expects an agent to
behave:

- Mission and capabilities;
- seventeen Core Engineering Principles;
- the Development Lifecycle;
- Before Coding and Before Completion requirements;
- Safety boundaries and Change Management preferences;
- a Source of Truth ordering for technical decisions;
- a Continuous Improvement process.

Workflows map their phases to the lifecycle in this file, and every layer
references its principles.

## Agent Layer (`.opencode/agents/`)

Agents are declarative role definitions. Each file defines an agent with a
description of when to use it and a permission profile:

- **Write access** â€” agents that implement work: `developer`, `tester`,
  `debugger`, `database`, `documentation`.
- **Read-only review** â€” agents that must not modify files: `researcher`,
  `architect`, `reviewer`, `security`.

All agents operate as subagents: they are delegated to for a specific role
within a workflow rather than driving the session on their own. The lead agent
(or main session) coordinates the workflow and holds sign-off. See
`docs/agents.md` for the full agent catalog.

## Skill Layer (`.opencode/skills/`)

Skills are specialized, loadable knowledge for a task area. Each skill has a
`SKILL.md` with a description stating when to use it. Skills are loaded when
the relevant area is worked on, and workflows reference the skills that apply
to each phase. See `docs/skills.md` for the full skill catalog.

## Rules Layer (`rules/`)

Rules are enforceable guardrails. Unlike the principles in `AGENTS.md`, rules
are concrete and domain-specific:

- `core.md` â€” fundamental constraints that apply to every task;
- `architecture.md` â€” high-level system structure;
- `api.md` â€” HTTP contract design and implementation;
- `database.md` â€” schema, queries, and data operations;
- `coding.md` â€” writing and modifying code;
- `frontend.md` â€” user-facing UI;
- `security.md` â€” security constraints for every boundary;
- `testing.md` â€” planning, writing, and running tests;
- `documentation.md` â€” creating and keeping documentation honest;
- `git.md` â€” safe use of version control.

Workflows cite the rules that apply to each step instead of restating them.
This keeps rules in one authoritative place and avoids duplication.

## Workflow Layer (`workflows/`)

Workflows are the operating procedures of the framework. Each workflow defines,
for a recurring task type:

- purpose and when to use it;
- an ordered sequence of steps;
- the responsible agents per step;
- the relevant skills and rules per step;
- validation gates (G1, G2, ...) that must have observed evidence;
- required artifacts;
- human approval requirements;
- completion criteria.

Workflows are the coordination point: they select which agents run which steps,
pull in the right skills and rules, reference templates for artifacts, and
enforce gates and approvals. See `docs/workflows.md` for the full workflow
catalog.

## Template Layer (`templates/`)

Templates are reusable starting points for the artifacts a workflow produces:

- `requirements.md` â€” problem, goals, and requirements;
- `decision.md` â€” architecture decision records;
- `implementation-plan.md` â€” milestones, scope, and increments;
- `architecture.md` â€” architecture context and goals;
- `testing.md` â€” testing reports;
- `research.md` â€” research question, context, and findings;
- `security-review.md` â€” review scope and findings;
- `project-summary.md` â€” project overview and objectives.

Templates keep artifacts consistent across tasks. They are kept generic and
reusable rather than project-specific.

## Knowledge Layer (`knowledge/`)

Knowledge is reusable reference material organized by domain:

- `architecture/`, `backend/`, `databases/`, `devops/`, `frontend/`,
  `security/` â€” domain reference material;
- `research/` â€” recorded technical research with sources, evidence, and
  uncertainty (supports the `RESEARCH` lifecycle step);
- `lessons-learned/` â€” lessons extracted from completed work that point to
  framework improvements.

Research may be promoted into reusable knowledge after verification. Lessons
must not silently change core framework behavior; they record the lesson and
proposed improvement until a human approves the change.

## Command Layer (`.opencode/commands/`)

The command layer is the user-facing orchestration interface. It exposes the
framework workflows through OpenCode project commands located under
`.opencode/commands/` (`correct`, `research`, `analyze`, `architect`, `plan`,
`build`, `test`, `review`, `security`, `debug`, `document`), and connects user
requests to the appropriate agents, skills, rules, workflows, and templates.

## Prompt Corrector (pre-workflow gateway)

The Prompt Corrector is a recommended pre-workflow gateway, not a lifecycle
stage and not part of workflow execution. It transforms an unclear,
incomplete, ambiguous, contradictory, or poorly structured user request into a
clear, structured, implementation-ready engineering prompt before the normal
framework lifecycle (REQUIREMENTS through COMPLETE) begins.

- It is read-only and separate from the implementation, architecture, review,
  research, and documentation agents.
- Its methodology (`.opencode/skills/prompt-corrector/SKILL.md`) is
  provider-independent; only its OpenCode integration lives in `.opencode/`.
- It classifies the corrected prompt as READY, READY WITH ASSUMPTIONS, or
  NEEDS CLARIFICATION and never proceeds to implementation itself.
- It is recommended, not mandatory: well-specified requests may still enter a
  workflow directly through the normal entry points; `correct` improves the
  request before they do.
- The corrected prompt is an input to the workflow's requirement phase; the
  workflow keeps its own agents, gates, and approval points.
- See `docs/prompt-corrector.md` for the capability description.

## Documentation Layer (`docs/`, `README.md`, `CONTRIBUTING.md`, `LICENSE`)

The documentation layer explains the framework and governs contributions to
it:

- `docs/` â€” structured framework documentation (getting started, architecture,
  agents, skills, workflows, contributing);
- `README.md` â€” overview and repository layout;
- `CONTRIBUTING.md` â€” how to contribute to the framework;
- `LICENSE` â€” MIT License.

These documents describe the framework itself, not any application built with
it.

## Relationship Between the Layers

Flow of authority and reuse:

- **Authority:** `AGENTS.md` â†’ `rules/` â†’ `workflows/`. The constitution sets
  principles; rules turn them into enforceable constraints; workflows apply the
  relevant rules in sequence.
- **Execution:** `workflows/` â†’ `.opencode/agents/`. Workflows delegate steps
  to the responsible agents.
- **Knowledge:** `workflows/` â†’ `.opencode/skills/` + `knowledge/`. Workflows
  load the skills and draw on the knowledge relevant to each phase.
- **Artifacts:** `workflows/` â†’ `templates/`. Workflows produce artifacts in
  the shape defined by templates.
- **Explanation:** all of the above are documented in the documentation layer.

## Portable vs OpenCode Runtime Layers

The framework has a deliberate portability boundary.

The **portable framework layers** are provider-independent and should remain
usable without OpenCode:

- `AGENTS.md` — mission, principles, lifecycle, and global guardrails.
- `rules/` — enforceable engineering and safety rules.
- `workflows/` — repeatable engineering procedures.
- `templates/` — reusable artifact structures.
- `knowledge/` — verified engineering knowledge and lessons learned.
- `docs/` — framework documentation and architectural guidance.

The **`.opencode/` layer** is the OpenCode-specific runtime integration:

- `.opencode/agents/` — OpenCode agent definitions.
- `.opencode/commands/` — OpenCode project commands.
- `.opencode/skills/` — OpenCode skill definitions.

The portable layers must not depend on OpenCode-specific runtime features.
The `.opencode/` layer may reference and orchestrate the portable framework
layers, but OpenCode-specific syntax, frontmatter, commands, or runtime
behavior should remain inside `.opencode/`.

This boundary implements Core Engineering Principle #17: engineering
knowledge must remain portable and usable independently of a specific AI
model or provider. Rehosting the framework on another AI engineering runtime
should therefore require replacing or adapting the runtime integration layer,
not rewriting the framework's core engineering guidance.

---
## Separation of Concerns

Each concern lives in exactly one layer:

| Concern | Layer |
| --- | --- |
| Identity, principles, lifecycle, safety | Constitution (`AGENTS.md`) |
| Roles, capabilities, permissions | Agents (`.opencode/agents/`) |
| Specialized task knowledge | Skills (`.opencode/skills/`) |
| Enforceable guardrails | Rules (`rules/`) |
| Procedures and orchestration | Workflows (`workflows/`) |
| Artifact formats | Templates (`templates/`) |
| Reference material | Knowledge (`knowledge/`) |
| Reusable commands | Commands (`.opencode/commands/`) |
| Explanation and contribution guidance | Documentation (`docs/`, etc.) |

The separation keeps content non-duplicated and authoritative in one place.
For example, a workflow references `rules/database.md` rather than restating
database rules, and references `database-design` skill rather than restating
it. This mirrors the project convention in `rules/architecture.md`: keep module
responsibilities small and avoid duplicating logic.

## Learning / Improvement Lifecycle

The framework improves itself through a controlled loop:

1. **Reflection** â€” after significant work, identify what worked, what failed,
   what was difficult, and what was missing (`AGENTS.md` â†’
   Continuous Improvement).
2. **Recording** â€” record lessons in `knowledge/lessons-learned/` and verified
   research in `knowledge/research/`.
3. **Proposal** â€” propose improvements (a new skill, rule, knowledge entry,
   or workflow change) with rationale and evidence.
4. **Promotion** â€” research is promoted into reusable knowledge only after it
   is verified and accepted.
5. **Approval** â€” changes to core framework behavior require explicit human
   approval before they are applied.

This lifecycle is itself governed by the human approval boundary described
below.

## Human Approval Boundary

Some actions are never taken silently. The framework requires human approval
for, at minimum:

- approving an implementation plan before implementation begins;
- applying database migrations to a staging or production database;
- breaking a published API contract, or deprecating/removing exposed
  endpoints or fields;
- deploying to production or releasing software;
- destructive or irreversible operations (deleting or truncating production
  data, force-push, history rewriting, schema alterations that change meaning);
- secret rotation performed as part of remediation;
- changing core framework behavior (rules, workflows, principles, or other
  governing behavior);
- leaving a blocking vulnerability unresolved without a documented risk
  decision.

The reasoning is consistent with `AGENTS.md` safety and the per-domain rules:
fail closed on uncertainty, prefer reversible operations, and never claim
completion without verification.

