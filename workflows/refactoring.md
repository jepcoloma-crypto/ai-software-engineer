# Workflow: Refactoring

## 1. Purpose

Restructure existing code to improve internal quality without changing its
observable behavior. The workflow is
`UNDERSTAND → ANALYZE IMPACT → PLAN → REFACTOR → TEST → REVIEW` and reuses the
framework's testing and review capabilities to guarantee behavior is preserved.

## 2. When to use

Use when improving maintainability, readability, structure, or performance of
existing code, or when preparing the ground for a new feature. Use only when
the change is intended to preserve behavior; if behavior is meant to change,
use `feature-development.md`. Do not use for architectural redesigns that
change contracts; use `api-change.md` or `new-project.md` where applicable.

## 3. Preconditions

- The code under refactor is understood and has existing tests, or a test
  baseline can be established first.
- The current behavior is defined well enough to verify it is preserved.
- No new user-visible behavior is introduced by the refactor.

## 4. Workflow steps

1. **Understand the code** — **Developer agent / Lead agent.**
   Read the modules, identify existing patterns, dependencies, and any
   behavior contracts. Record the scope of the refactor. Use
   `rules/core.md` and the `system-architecture` skill.
   **Gate G1:** the existing behavior and test baseline are understood before
   any restructuring begins.
2. **Analyze the impact** — **Architect agent / Developer agent.**
   Determine what the refactor touches: public surfaces, dependencies,
   callers, data, and tests. Identify compatibility and risk areas. Use the
   `system-architecture` skill and `rules/architecture.md`.
   **Gate G2:** impact analysis identifies all affected components and
   dependencies before planning.
3. **Plan the refactor** — **Lead agent / Developer agent.**
   Define ordered, small, independently verifiable steps. Decide how behavior
   preservation will be proven at each step.
   **Gate G3:** the refactor plan is approved before restructuring begins.
4. **Refactor** — **Developer agent.**
   Apply the changes step by step. Keep each step small, focused, and
   verified. Preserve existing behavior; avoid mixing functional changes into
   the refactor. Use `rules/coding.md` and `rules/architecture.md`.
   **Gate G4:** each step builds and passes tests before the next begins.
5. **Test that behavior is preserved** — **Tester agent.**
   Run the existing suite plus any behavior-defining tests added as a
   baseline. Confirm behavior is unchanged. Use the `testing` skill and
   `rules/testing.md`.
   **Gate G5:** the full suite passes and no behavior regression is observed.
6. **Review the refactor** — **Reviewer agent.**
   Review for correctness, maintainability, and whether the refactor achieved
   its goal without behavior change or unrelated edits. Use the `code-review`
   skill.
   **Gate G6:** blocking findings are resolved and re-verified.
7. **Confirm completion** — **Lead agent.**
   Confirm the refactor is behavior-preserving and fully verified before
   declaring completion.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Understanding and coordination | Lead agent / Developer agent |
| Impact analysis | Architect agent / Developer agent |
| Refactoring | Developer agent |
| Behavior verification | Tester agent |
| Review | Reviewer agent |
| Documentation updates | Documentation agent |

## 6. Relevant skills and rules

- **Skills:** `system-architecture`, `testing`, `code-review`,
  `backend-development`, `frontend-development`.
- **Rules:** `rules/core.md`, `rules/architecture.md`, `rules/coding.md`,
  `rules/testing.md`, `rules/git.md`.
- **Framework:** the before-coding and before-completion checks in
  `AGENTS.md`; the change-management guidance in `AGENTS.md`.

## 7. Required artifacts

- Impact analysis of the affected code and dependencies.
- Refactor plan with ordered, verifiable steps.
- Code changes that preserve behavior.
- Test baseline and actual test results proving behavior is preserved.
- Review findings and resolutions.
- Documentation updated where the refactor changes structure or contracts.

## 8. Validation gates

- **G1:** behavior and test baseline understood before restructuring.
- **G2:** impact analysis complete and accurate.
- **G3:** refactor plan approved before restructuring begins.
- **G4:** each step builds and passes tests before the next step.
- **G5:** full suite passes; behavior preserved.
- **G6:** blocking review findings resolved and re-verified.

## 9. Approval requirements

- Human approval is required before any refactor that touches a published API
  contract, changes shared interfaces, or requires a schema migration. Such
  cases must follow `api-change.md` or `database-change.md` for the
  contract-bearing parts.
- Human approval is required for any destructive action or history rewriting
  per `rules/git.md`.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- Existing behavior is preserved.
- The executed test suite passes, including the baseline that defines current
  behavior.
- The refactor improves the stated quality attribute (maintainability,
  readability, structure, performance) without unrelated changes.
- Review is complete and blocking findings are resolved.
- Documentation matches the post-refactor structure.
- No secrets were exposed and no destructive action occurred without approval.

Do not claim completion without running the verification steps described
above.