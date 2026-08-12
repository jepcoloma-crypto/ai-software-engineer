# Workflow: Feature Development

## 1. Purpose

Deliver a new feature within an existing project from vague request to a
verified, reviewed, and documented change. The workflow is
`UNDERSTAND → ANALYZE → PLAN → IMPLEMENT → TEST → REVIEW → DOCUMENT` and
reuses the framework's agents, skills, and rules without duplicating them.

## 2. When to use

Use when adding a new capability, endpoint, screen, or behavior to an existing
system. Use when the change is larger than a one-line fix but smaller than a
new project. Do not use for: new projects (`new-project.md`), bug repairs
(`bug-fix.md`), database-only changes (`database-change.md`), API-only changes
that carry a compatibility impact (`api-change.md`), refactors with no behavior
change (`refactoring.md`), or releases (`deployment.md`).

## 3. Preconditions

- The project exists and its conventions are discoverable.
- The feature request states the goal and the problem it solves.
- The request has passed the Prompt Corrector gate (`correct` command): it is
  READY_FOR_WORKFLOW or any blocking clarification is resolved.
- The affected surface (modules, endpoints, data, UI) is identifiable.
- The relevant subsystems have been inspected before coding begins.

## 4. Workflow steps

1. **Understand the request** — **Lead agent.**
   Restate the goal, gather functional and non-functional requirements,
   identify constraints and assumptions, and write testable acceptance
   criteria. Use the `requirements-analysis` skill and `rules/core.md`. If the
   request has not already been corrected, run the `correct` command first; do
   not proceed while the request is NEEDS_CLARIFICATION. If requirements are
   unclear, ask before continuing.
2. **Analyze the change** — **Architect agent.**
   Identify how the feature fits the existing architecture. Determine the
   impacted modules, data model, API surface, and user flows. Record the
   impact analysis and any tradeoffs. Use the `system-architecture` skill and
   `rules/architecture.md`. The Architect agent does not implement code.
   **Gate G1:** the impact analysis must be complete before planning.
3. **Plan the implementation** — **Lead agent / Architect agent.**
   Define the work items, ordering, and how each item is verified. Identify
   database, API, or UI work so the right agents are engaged.
   **Gate G2:** the plan must be approved before implementation starts.
4. **Implement the feature** — **Developer agent.**
   Implement each work item following existing conventions. Reuse existing
   components, keep changes small and focused, and never expose secrets.
   Engage the **Database agent** for schema changes and the **Developer
   agent** using the `frontend-development` skill where UI/frontend work is
   required. Use the
   `backend-development`, `frontend-development`, `database-design`, and
   `api-design` skills and `rules/coding.md`.
   **Gate G3:** the change builds, type-checks, and passes its targeted tests
   before proceeding.
5. **Test the feature** — **Tester agent.**
   Design and run unit, integration, API, and end-to-end tests that cover the
   feature and its edge cases. Report actual results only. Use the `testing`
   skill and `rules/testing.md`.
   **Gate G4:** the executed suite passes before review.
6. **Review the change** — **Reviewer agent.**
   Review correctness, architecture fit, security implications, edge cases,
   and test coverage. Apply the `code-review` skill.
   **Gate G5:** blocking findings are resolved and re-verified.
7. **Document the change** — **Documentation agent.**
   Update API, setup, architecture, or change documentation to match the
   actual implementation. Use `rules/documentation.md`.
8. **Confirm completion** — **Lead agent.**
   Confirm all gates have observed evidence before declaring the feature done.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Understanding and coordination | Lead agent |
| Impact analysis | Architect agent |
| Data model changes | Database agent |
| Implementation | Developer agent |
| Testing | Tester agent |
| Review | Reviewer agent |
| Documentation | Documentation agent |

## 6. Relevant skills and rules

- **Skills:** `requirements-analysis`, `system-architecture`,
  `backend-development`, `frontend-development`, `database-design`,
  `api-design`, `testing`, `code-review`.
- **Rules:** `rules/core.md`, `rules/architecture.md`, `rules/coding.md`,
  `rules/database.md`, `rules/api.md`, `rules/frontend.md`,
  `rules/security.md`, `rules/testing.md`, `rules/documentation.md`,
  `rules/git.md`.
- **Framework:** the before-coding and before-completion checks in
  `AGENTS.md`.

## 7. Required artifacts

- Feature requirements and acceptance criteria.
- Impact analysis of affected modules, data, and APIs.
- Implementation plan (work items and order).
- Code changes scoped to the feature.
- Database migrations where the feature touches the data model.
- Automated tests for the new behavior and its edge cases.
- Record of actual test results.
- Review findings and resolutions.
- Documentation updated to match the implementation.

## 8. Validation gates

- **G1:** impact analysis complete and accurate; acceptance criteria are
  testable.
- **G2:** implementation plan approved before any code is written.
- **G3:** build, type-check, and targeted tests pass on the implementation.
- **G4:** the full relevant suite is executed and passes; results are observed,
  not assumed.
- **G5:** blocking review findings resolved and re-verified.

## 9. Approval requirements

- Human approval is required before: applying migrations to any non-local
  database, changing a published API contract in a breaking way, and any
  release or deployment.
- Human approval is required for any destructive action (data deletion,
  force-push, history rewriting) per `rules/git.md` and `rules/database.md`.
- Scope changes beyond the approved plan require approval before continuing.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- Requirements and acceptance criteria are recorded.
- The feature is implemented within the existing conventions.
- The executed test suite passes, including new coverage for the feature and
  its edge cases.
- Review is complete and blocking findings are resolved.
- Any data model or API changes are compatible or explicitly approved as
  breaking.
- Documentation matches the implementation.
- No secrets were exposed and no destructive action occurred without approval.

Do not claim completion without running the verification steps described
above.