# Workflows

This document catalogs the eight workflows defined in `workflows/`. A workflow
is the framework's operating procedure for a recurring task type: it defines an
ordered sequence of steps, the agents responsible for each step, the skills and
rules that apply, the artifacts to produce, the validation gates that must
pass, and the human approvals required. This document summarizes each workflow
and how workflows coordinate the framework's layers; it does not restate the
workflows' step-by-step contents.

## What an Individual Workflow Contains

Every workflow follows the same structure:

- **Purpose** — what the workflow accomplishes and the phase sequence it uses.
- **When to use** — the cases the workflow covers and which workflow to use
  instead for adjacent cases.
- **Preconditions** — what must be true before the workflow starts.
- **Workflow steps** — an ordered sequence, each with the responsible agent(s)
  and the relevant skills and rules.
- **Responsible agents** — a table mapping tasks to agents, including the lead
  agent that coordinates and signs off.
- **Relevant skills and rules** — the skills and rule files cited by the
  workflow.
- **Required artifacts** — what the workflow must produce.
- **Validation gates** — numbered gates (G1, G2, ...) that require observed
  evidence, not assumptions.
- **Approval requirements** — the human approvals required before certain
  steps may proceed.
- **Completion criteria** — the verified conditions required before completion
  may be claimed.

## Workflow Catalog

### new-project
Stands up a new software project from an idea to a working, verified, and
documented foundation. It walks through the full `AGENTS.md` lifecycle
(`REQUIREMENTS → RESEARCH → ANALYSIS → ARCHITECTURE → PLAN → IMPLEMENT →
TEST → REVIEW → SECURITY REVIEW → DOCUMENT → COMPLETE`) and is used for
greenfield work. Use the change-specific workflows instead for work on an
existing project.

### feature-development
Delivers a new feature within an existing project from a vague request to a
verified, reviewed, and documented change. The phase sequence is
`UNDERSTAND → ANALYZE → PLAN → IMPLEMENT → TEST → REVIEW → DOCUMENT`. Use for
additions of new capability, endpoints, screens, or behavior to an existing
system that are larger than a one-line fix but smaller than a new project.

### bug-fix
Repairs a defect from reported symptom to verified fix. The phase sequence is
`REPRODUCE → INVESTIGATE → ROOT CAUSE → FIX → TEST → REGRESSION TEST → REVIEW`.
Use for confirmed bugs, failing tests, crashes, hangs, or incidents where the
root cause is unknown or the failure cannot yet be reproduced on demand.

### refactoring
Restructures existing code to improve internal quality without changing
observable behavior. The phase sequence is
`UNDERSTAND → ANALYZE IMPACT → PLAN → REFACTOR → TEST → REVIEW`. Use for
improving maintainability, readability, structure, or performance while
preserving behavior; use `feature-development.md` when behavior is meant to
change.

### database-change
Makes a safe, reversible, reviewed change to a relational database schema,
queries, or data. The phase sequence is
`ANALYZE → DESIGN → MIGRATION → TEST → VALIDATE → DOCUMENT`. Use when changing
schema, constraints, indexes, views, or stored behavior, or when a migration
will be applied to a shared, staging, or production database. Migrations to
staging or production require human approval.

### api-change
Adds, extends, or changes an HTTP API contract with explicit compatibility
management. The phase sequence is
`ANALYZE → COMPATIBILITY ASSESSMENT → DESIGN → IMPLEMENT → TEST → SECURITY
REVIEW → DOCUMENT`. Use when the API contract is a compatibility boundary with
external consumers; use `feature-development.md` for purely internal changes
with no contract impact.

### security-review
Identifies and remediates security vulnerabilities in a codebase or design. The
phase sequence is `IDENTIFY ATTACK SURFACE → ANALYZE VULNERABILITIES → TEST →
FIX → VERIFY → DOCUMENT`. Use before merging security-sensitive changes, when
introducing authentication or authorization, when handling secrets or user
files, when auditing an existing codebase or dependency set, or when a security
incident is reported. It also serves as the security stage of `new-project.md`,
`feature-development.md`, and `api-change.md`.

### deployment
Releases a verified build to a target environment (staging or production)
safely. The phase sequence is
`VALIDATE → BUILD → TEST → SECURITY CHECK → DEPLOY → VERIFY → DOCUMENT`. Use
when moving software from code to a running environment, including releases,
migrations in a release, environment configuration, and post-deploy
verification. Use only for code that passed its preceding change workflow.
Production deployment requires human approval.

## How Workflows Coordinate the Framework

Workflows are the orchestration point of the framework. Each workflow:

- **Coordinates agents** — assigns every step to a responsible agent defined in
  `.opencode/agents/` (for example, the Developer agent implements, the
  Tester agent tests, the Reviewer agent reviews), while the lead agent
  coordinates and holds sign-off.
- **Loads skills** — references the skills in `.opencode/skills/` that apply to
  each phase (for example, `database-change.md` uses `database-design`, and
  `deployment.md` uses `deployment`, `testing`, and `security-review`).
- **Applies rules** — cites the rule files in `rules/` that govern each step
  instead of restating them (for example, implementation steps cite
  `rules/coding.md`, and deployment steps cite `rules/security.md` and
  `rules/database.md`).
- **Uses templates** — produces required artifacts whose shape is defined by
  `templates/`, keeping artifacts consistent across tasks.
- **Enforces validation gates** — requires observed evidence for each gate. A
  step does not proceed until its gate passes, and completion is claimed only
  when every gate has evidence (see `AGENTS.md`: never claim completion
  without verification).
- **Enforces human approvals** — stops before high-impact or destructive steps
  until a human approves: plans before implementation, migrations on non-local
  databases, breaking API changes, release/deployment, destructive data
  operations, and history rewriting.

The result is that the same agents, skills, and rules are reused consistently
across task types, with the workflow defining the sequence, gates, and
approval boundaries.

## Prompt Correction and the Workflows

The Prompt Corrector (`correct` command, `.opencode/agents/prompt-corrector.md`)
is a recommended pre-workflow gateway that improves a raw user request before
it enters any workflow. It is separate from workflow execution: it does not run
a workflow, delegate to workflow agents, or change the phase sequence of the
workflows above.

- A **READY** or **READY WITH ASSUMPTIONS** corrected prompt flows into the
  workflow that matches the request type — for example, `feature-development.md`
  for a new capability in an existing system, `new-project.md` for greenfield
  work, or `bug-fix.md` for a reported defect.
- A **NEEDS CLARIFICATION** result stops before a workflow starts until the
  prioritized clarifications are answered.
- The corrected prompt feeds the workflow's requirement phase; the workflow
  still owns its own agents, validation gates, and human approval points.
- Prompt correction is recommended, not mandatory. A well-specified request may
  begin a workflow directly without running `correct`.