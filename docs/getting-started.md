# Getting Started

## What Is the AI Software Engineer Framework?

This repository is an operating framework for autonomous AI software
engineering agents. It codifies how an agent should behave when asked to
design, build, test, review, and improve software. It is **not** a business
application and it does not assume any specific application technology,
language, or framework.

The framework is composed of reusable guidance and structure:

- **AGENTS.md** — the constitution: mission, principles, lifecycle, and safety.
- **Agents** — specialized roles under `.opencode/agents/`.
- **Skills** — specialized knowledge under `.opencode/skills/`.
- **Rules** — enforceable guardrails under `rules/`.
- **Workflows** — repeatable procedures under `workflows/`.
- **Templates** — reusable artifact starting points under `templates/`.
- **Knowledge** — domain reference material under `knowledge/`.
- **Commands** — OpenCode project commands under `.opencode/commands/`:
  `correct`, `research`, `analyze`, `architect`, `plan`, `build`, `test`,
  `review`, `security`, `debug`, and `document`.
- **Documentation** — guidance and decisions under `docs/`, plus
  `README.md` and `CONTRIBUTING.md`.

## What Problem It Solves

Autonomous agents can work inconsistently: skipping verification, inventing
APIs, touching unrelated code, or taking unsafe actions. This framework reduces
that risk by encoding senior engineering discipline as repeatable structure:

- a clear mission and a fixed set of engineering principles (`AGENTS.md`);
- a mandatory development lifecycle with explicit validation gates;
- role separation so research, design, implementation, review, and security
  checks are not collapsed into one unaccountable step;
- safety rules that require verification before completion and approval before
  destructive or high-impact actions;
- reusable knowledge, skills, workflows, and templates so good practice is not
  rediscovered on every task.

## Repository Prerequisites

- **Git** — the repository is version-controlled; changes are proposed and
  reviewed through normal Git flows.
- **OpenCode** — the framework's agents, skills, and AGENTS.md are consumed by
  the OpenCode CLI. Refer to the OpenCode documentation for how the tool
  discovers `AGENTS.md` and the `.opencode/` directory.
- **No build tooling or test suite** — this is a guidance-centric repository.
  There are no dependencies to install and nothing to compile or run for the
  framework itself (see `CONTRIBUTING.md`).

## Repository Structure

| Path | Purpose |
| --- | --- |
| `AGENTS.md` | Mission, core principles, development lifecycle, safety, and source of truth for all tasks. |
| `docs/` | Framework documentation: getting started, architecture, agents, skills, workflows, contributing. |
| `knowledge/` | Domain reference material organized by area: `architecture/`, `backend/`, `databases/`, `devops/`, `frontend/`, `security/`, plus `lessons-learned/` and `research/`. |
| `rules/` | Enforceable engineering and safety rules (core, architecture, api, database, coding, frontend, security, testing, documentation, git). |
| `templates/` | Reusable starting points for common artifacts (requirements, decision, architecture, implementation plan, testing, research, security review, project summary). |
| `workflows/` | Repeatable procedures for recurring task types (new project, feature, bug fix, refactoring, database change, API change, security review, deployment). |
| `.opencode/agents/` | Definitions of the ten specialized agents. |
| `.opencode/skills/` | Specialized skill definitions, one folder per skill. |
| `.opencode/commands/` | OpenCode project commands exposing the framework workflows: `correct`, `research`, `analyze`, `architect`, `plan`, `build`, `test`, `review`, `security`, `debug`, and `document`. |
| `README.md` | Short project overview and layout. |
| `CONTRIBUTING.md` | Guidelines for improving the framework itself. |
| `LICENSE` | MIT License. |

## Role of AGENTS.md

`AGENTS.md` is the constitution. Every agent reads it before undertaking a
task. It defines:

- the **Mission** of an autonomous senior software engineering agent;
- seventeen **Core Engineering Principles** (understand before changing, never
  invent behavior, test important changes, never claim completion without
  verification, protect secrets, and so on);
- the **Development Lifecycle** (`REQUIREMENTS → RESEARCH → ANALYSIS →
  ARCHITECTURE → PLAN → IMPLEMENT → TEST → REVIEW → SECURITY REVIEW →
  DOCUMENT → COMPLETE`);
- **Before Coding** and **Before Completion** checklists;
- the **Safety** boundaries (never expose secrets, never fabricate results,
  never perform destructive operations without approval);
- **Change Management** preferences and the **Source of Truth** ordering for
  technical decisions.

`AGENTS.md` is the top of the framework and shapes everything below it.
Rules, workflows, skills, and agents are all meant to be consistent with it.

## How the Pieces Relate

- **AGENTS.md** sets the identity, principles, and lifecycle.
- **Agents** are the roles that do the work, each with its own permission
  profile (for example, the Developer agent may edit; the Reviewer agent may
  not).
- **Skills** provide specialized, loadable knowledge for a task area and are
  referenced by workflows when that area is touched.
- **Rules** are guardrails referenced throughout workflows; agents apply the
  rules relevant to their step.
- **Workflows** coordinate agents, skills, and rules into an ordered sequence
  with validation gates and human approval points.
- **Templates** standardize the artifacts workflows produce (requirements,
  plans, decision records, review reports).
- **Knowledge** supplies reusable reference material that research can promote
  into verified guidance.
- **Commands** are OpenCode project commands under `.opencode/commands/` that
  expose the framework workflows: `correct`, `research`, `analyze`, `architect`,
  `plan`, `build`, `test`, `review`, `security`, `debug`, and `document`.

## Basic Usage Flow

For a significant task, the flow follows the Development Lifecycle in
`AGENTS.md`. Before the workflow begins, run the `correct` command so the
Prompt Corrector normalizes the request and confirms it is ready:

1. **Requirements** — restate the goal, gather functional and non-functional
   requirements, record constraints and assumptions, define acceptance
   criteria. Ask for missing critical information.
2. **Research** — resolve uncertain technical decisions using official
   documentation.
3. **Analysis** — define scope, boundaries, actors, data, and main flows.
4. **Architecture** — design modules, data model, APIs, and security
   boundaries; record trade-offs and decisions.
5. **Plan** — produce an approved implementation plan with ordered increments.
6. **Implement** — build each increment, following existing conventions.
7. **Test** — design and run the appropriate tests; report actual results.
8. **Review** — review correctness, fit, maintainability, and edge cases.
9. **Security Review** — map the attack surface and audit security-relevant
   concerns.
10. **Document** — document what actually exists.
11. **Complete** — confirm every gate has observed evidence before claiming
    completion.

The eight workflows in `workflows/` specialize this lifecycle for recurring
task types; each defines the phases, responsible agents, skills, rules,
validation gates, and approval requirements for that type of change.

## Using the Framework with OpenCode

1. Clone or copy this repository.
2. Open the repository in OpenCode. `AGENTS.md` is picked up as the project
   instruction file, and the agent and skill definitions under `.opencode/`
   are available to the session.
3. Read `AGENTS.md` before any task.
4. Run the `correct` command to normalize the request into a verified
   engineering prompt, then identify the matching workflow in `workflows/`
   (for example, `feature-development.md` for a new capability in an existing
   system) and follow it.
5. Delegate specialized work to the appropriate agent defined in
   `.opencode/agents/` (for example, the Architect agent for design, the
   Developer agent for implementation, the Reviewer agent for review).
6. Load the relevant skills when their area applies (for example,
   `api-design` when touching an API contract). Skills are specialized
   knowledge; they are referenced by the workflows.
7. Apply the relevant rules and templates for the artifacts produced.
8. Respect the human approval points defined in the workflow and in
   `AGENTS.md` before proceeding with high-impact or destructive steps.

## Prompt Correction (`/correct`)

Before starting an engineering workflow, you may run:

`/correct <user request>`

The Prompt Corrector returns a structured corrected prompt built from
`templates/corrected-prompt.md` — the understood intent, desired outcome,
context, users and actors, explicit, functional, and non-functional
requirements, business rules, data, integrations, security, reporting and
audit requirements, technical constraints, assumptions, clarifications
required, out-of-scope items, and proposed acceptance criteria — plus an
implementation readiness assessment:

- **READY** — the request is clear and implementation-ready.
- **READY WITH ASSUMPTIONS** — the request is usable if its tagged assumptions
  are confirmed.
- **NEEDS CLARIFICATION** — missing or ambiguous information must be answered
  before the request enters a workflow.

The Prompt Corrector is a **recommended pre-workflow gateway**, not a mandatory
first step. It is read-only and never implements anything. Use it when a request
is unclear, incomplete, ambiguous, contradictory, or poorly structured;
well-specified requests may proceed directly through the normal framework entry
points.

## Safely Inspecting and Validating Framework Changes

The framework itself is subject to its own principles, especially
"understand before changing" and "never claim completion without
verification." When inspecting or changing it:

- Read `AGENTS.md`, the affected layer(s), and any content already covering
  the topic before editing.
- Follow the directory conventions; add or edit content in the appropriate
  layer rather than duplicating it elsewhere.
- Validate changes against the repository's own verification guidance in
  `CONTRIBUTING.md`: contributions must be complete, free of placeholders,
  consistent in style, and free of secrets and accidental artifacts.
- Keep documentation synchronized with the actual repository structure and
  never document features that do not exist.

## Important Safety and Approval Principles

- **Verification before completion** — a result is unverified until it has
  been observed. Never fabricate or claim unobserved results.
- **Secrets** — never expose credentials; never commit secrets to the
  repository.
- **Destructive operations** — never delete data, force-push, rewrite history,
  or run other destructive operations without explicit approval.
- **Human approval** — high-impact steps require approval: applying migrations
  to a non-local database, deploying to production, breaking published API
  contracts, changing core framework behavior, and any destructive action.
- **Commit and push** — never commit, push, or merge unless the user
  explicitly asks.
- **No silent changes** — never silently modify critical architecture or
  framework behavior; propose the change first.

See `AGENTS.md`, `rules/core.md`, `rules/git.md`, and `rules/security.md` for
the authoritative statements of these boundaries.