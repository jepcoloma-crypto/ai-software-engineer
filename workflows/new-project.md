# Workflow: New Project

## 1. Purpose

Stand up a new software project from an idea to a working, verified, and
documented foundation. The workflow follows the Development Lifecycle defined
in `AGENTS.md` and produces the architecture, plan, code, tests, security
review, and documentation required before a project can be considered
production-ready at its initial scope.

## 2. When to use

Use when starting a new software project or repository. Use when requirements
are an idea rather than a specification, when no implementation exists yet, or
when a greenfield effort must be brought to its first verifiable milestone.
Do not use for changes to an existing project; use `feature-development.md`,
`bug-fix.md`, or the workflow that matches the change type.

## 3. Preconditions

- The project goal and business intent have been stated.
- The request has passed the Prompt Corrector gate (`correct` command): it is
  READY or READY WITH ASSUMPTIONS, or any blocking NEEDS CLARIFICATION
  questions are resolved.
- Stakeholders or the requesting user are available for clarification.
- Writing an implementation plan may precede coding.
- No assumption of an existing codebase, framework, or language is made unless
  explicitly stated by the user.

## 4. Workflow steps

The steps mirror the lifecycle in `AGENTS.md`:
`REQUIREMENTS → RESEARCH → ANALYSIS → ARCHITECTURE → PLAN → IMPLEMENT →
TEST → REVIEW → SECURITY REVIEW → DOCUMENT → COMPLETE`.

1. **Clarify requirements** — **Lead agent.**
   Restate the requested goal, gather functional and non-functional
   requirements, record constraints, capture assumptions, and define testable
   acceptance criteria. Follow the `requirements-analysis` skill and
   `rules/core.md`. Ask for missing critical information before proceeding.
   If the request has not already been corrected, run the `correct` command
   first; do not proceed while the request is NEEDS CLARIFICATION.
   **Gate G1:** requirements and acceptance criteria are recorded and
   unambiguous.
2. **Research open questions** — **Research agent.**
   Investigate any uncertain technical decisions: technology choices,
   frameworks, libraries, and platform behavior. Prefer official
   documentation. Follow the `requirements-analysis` and `system-architecture`
   skills and `rules/core.md`.
   **Gate G2:** open questions are resolved or explicitly deferred with a
   stated impact.
3. **Analyze the problem** — **Architect agent / Lead agent.**
   Convert requirements and research into a clear statement of what must be
   built: scope, boundaries, actors, data, and the main flows. Record
   assumptions and risks. Follow the `system-architecture` skill.
   **Gate G3:** the problem analysis documents scope, boundaries, and risks.
4. **Design the architecture** — **Architect agent.**
   Select an architecture style, define module boundaries and components,
   design the data model, design API and data contracts, and define security
   boundaries. Evaluate tradeoffs and record architecture decisions. Follow
   the `system-architecture`, `database-design`, and `api-design` skills and
   `rules/architecture.md`. Engage the **Database agent** to design or review
   the data model and migrations. The Architect agent must NOT implement code.
5. **Plan the implementation** — **Architect agent / Lead agent.**
   Produce an implementation plan: milestones, ordered increments, the
   components each increment touches, and how each increment is verified.
   Identify dependencies between work items.
   **Gate G4:** the plan must be approved before implementation begins.
6. **Implement the foundation** — **Developer agent.**
   Build each planned increment: project scaffolding, configuration, core
   modules, database migrations, APIs, and the user-facing surface. Follow
   existing conventions where any exist; otherwise establish minimal, clear
    conventions. Apply the `backend-development`, `frontend-development`,
    `database-design`, and `api-design` skills and `rules/coding.md`.
   Running of tests, builds, and tooling is eligible here.
   **Gate G5:** implementation must pass its own build and test run before
   being considered complete.
7. **Test the implementation** — **Tester agent.**
   Design and execute unit, integration, API, and any appropriate end-to-end
   tests per the `testing` skill and `rules/testing.md`. Report actual results
   only; never fabricate passing runs.
   **Gate G6:** the suite must be executed and pass before review.
8. **Review the implementation** — **Reviewer agent.**
   Review correctness, architecture fit, maintainability, edge cases, API
   compatibility, and test coverage. Apply the `code-review` skill and
   `rules/core.md`. Deliver prioritized, actionable findings.
   **Gate G7:** blocking findings must be resolved and re-verified.
9. **Perform a security review** — **Security agent.**
   Map trust boundaries and audit authentication, authorization, secrets,
   input validation, injection, XSS, CSRF, dependency security, file
   handling, rate limiting, and session handling. Apply the `security-review`
   skill and `rules/security.md`.
   **Gate G8:** no blocking vulnerability may remain; findings are recorded
   with severity and remediation.
10. **Document the project** — **Documentation agent.**
    Create or update setup, architecture, API, and decision documentation
    covering what actually exists. Apply `rules/documentation.md`.
11. **Confirm completion** — **Lead agent.**
    Confirm every validation gate passed, verification actually ran, and all
    artifacts exist before declaring completion.

## 5. Responsible agents

| Role | Agent |
| --- | --- |
| Requirements, coordination, final sign-off | Lead agent |
| Research | Research agent |
| Architecture and planning | Architect agent |
| Data model and migrations design | Database agent |
| Implementation | Developer agent |
| Testing | Tester agent |
| Review | Reviewer agent |
| Security | Security agent |
| Documentation | Documentation agent |

## 6. Relevant skills and rules

- **Skills:** `requirements-analysis`, `system-architecture`,
  `database-design`, `api-design`, `backend-development`,
  `frontend-development`, `testing`, `code-review`, `security-review`.
- **Rules:** `rules/core.md`, `rules/architecture.md`, `rules/coding.md`,
  `rules/database.md`, `rules/api.md`, `rules/frontend.md`,
  `rules/security.md`, `rules/testing.md`, `rules/documentation.md`.
- **Framework:** the Development Lifecycle in `AGENTS.md`; the safety and
  before-completion checks in `AGENTS.md`.

## 7. Required artifacts

- Requirements and acceptance criteria (recorded in the issue tracker or
  requirements document).
- Research notes or decision-record entries for open questions.
- Architecture decision records covering the key structural choices.
- Implementation plan with milestones and increments.
- Source code, configuration, and initial project scaffolding.
- Database migrations and schema definition.
- API contract documentation (or OpenAPI style definition where applicable).
- Automated tests and the record of actual test results.
- Review findings and resolutions.
- Security review report with severity and remediation.
- Setup and architecture documentation.
- Verification log showing each gate's outcome with evidence.

## 8. Validation gates

- **G1 (after requirements):** requirements and acceptance criteria are
  recorded and unambiguous.
- **G2 (after research):** all expensive-to-change decisions are backed by
  evidence; open questions are resolved or explicitly deferred with a stated
  impact.
- **G3 (after analysis):** scope, boundaries, and risks are documented before
  architecture design.
- **G4 (after planning):** the implementation plan is concrete, ordered, and
  approved before coding starts.
- **G5 (after each increment):** the increment builds and passes its targeted
  tests before the next increment begins.
- **G6 (after testing):** the full relevant suite is executed and passes;
  results are real, not assumed.
- **G7 (after review):** all blocking review findings are resolved and
  re-verified.
- **G8 (after security review):** no blocking vulnerabilities remain; all
  findings are recorded with severity and remediation.

## 9. Approval requirements

- Human approval is required before: writing any plan that gets implemented,
  creating a database against a shared or production instance, applying
  migrations to any non-local database, and before any release or deployment.
- Human approval is required for any destructive action (dropping data,
  force-push, deleting branches, rewriting history) per `rules/git.md` and
  `rules/database.md`.
- Breaking architecture decisions and scope changes require approval before
  implementation proceeds.

## 10. Completion criteria

Completion is claimed only when all of the following are verified:

- Requirements and acceptance criteria are recorded and unambiguous.
- Architecture, decisions, and plan are documented.
- The implementation exists, builds, and passes the executed test suite.
- Review is complete and blocking findings are resolved.
- Security review is complete with no blocking vulnerabilities.
- Documentation matches the actual implementation.
- Every validation gate in section 8 has observed evidence of passing.

Do not claim completion without running the verification steps described
above.