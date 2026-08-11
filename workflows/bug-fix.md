# Workflow: Bug Fix

## 1. Purpose

Repair a defect or unexpected behavior in an existing system from reported
symptom to verified fix. The workflow is
`REPRODUCE → INVESTIGATE → ROOT CAUSE → FIX → TEST → REGRESSION TEST →
REVIEW` and uses the framework's debugging, testing, and review capabilities.

## 2. When to use

Use when behavior does not match expectations: a failing test, a wrong result,
a crash, a hang, or a production incident. Use for confirmed bugs rather than
new work; for new behavior use `feature-development.md`. Use when the root
cause is unknown or the failure cannot yet be reproduced on demand.

## 3. Preconditions

- The defect is reported with enough context to attempt reproduction.
- Evidence gathering may start without any code change.
- The affected subsystem is identifiable or discoverable.

## 4. Workflow steps

1. **Reproduce the failure** — **Debugger agent.**
   Find the smallest reliable way to trigger the defect. Confirm the actual
   behavior, capture inputs, expected output, actual output, and relevant
   logs. Use the `debugging` skill and `rules/testing.md`.
   **Gate G1:** the failure is reproducible on demand, or the inability to
   reproduce is documented as evidence of an environmental or build issue.
2. **Investigate the cause** — **Debugger agent.**
   Read the relevant code, tests, logs, and data flow. Trace actual values
   from source to failure point. Form and check hypotheses against evidence.
   Use the `debugging` skill and `rules/core.md`.
   **Gate G2:** root cause identified from evidence, not guesswork.
3. **Fix the root cause** — **Debugger agent / Developer agent.**
   Apply the minimal change that restores correct behavior and the violated
   invariant. Do not introduce unrelated refactors while fixing. Do not mask
   the symptom. Use `rules/coding.md` and `rules/core.md`.
   **Gate G3:** the fix changes the smallest amount of code needed.
4. **Test the fix** — **Tester agent.**
   Run the reproduction against the fix, then run the surrounding suite.
   Report actual results. Use the `testing` skill and `rules/testing.md`.
   **Gate G4:** the original failure is resolved and the surrounding suite
   passes.
5. **Add a regression test** — **Tester agent.**
   Add a test that fails on the old code and passes on the fixed code, and
   keep it in the suite to prevent recurrence. Use `rules/testing.md`.
   **Gate G5:** the regression test is verified to fail before and pass after
   the fix.
6. **Review the fix** — **Reviewer agent.**
   Review the fix for correctness, scope, side effects, and whether it
   addresses the root cause rather than the symptom. Use the `code-review`
   skill.
   **Gate G6:** blocking findings are resolved and re-verified.
7. **Confirm completion** — **Lead agent.**
   Confirm the failure is reproduced, fixed, and verified before closing the
   bug.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Reproduction and investigation | Debugger agent |
| Root-cause fix | Debugger agent / Developer agent |
| Testing and regression test | Tester agent |
| Review | Reviewer agent |
| Coordination and sign-off | Lead agent |

## 6. Relevant skills and rules

- **Skills:** `debugging`, `testing`, `code-review`.
- **Rules:** `rules/core.md`, `rules/coding.md`, `rules/testing.md`,
  `rules/security.md`, `rules/git.md`.
- **Framework:** the safety and before-completion checks in `AGENTS.md`.

## 7. Required artifacts

- Reproduction steps and captured evidence (inputs, outputs, logs).
- Root-cause description supported by evidence.
- The minimal fix applied.
- Actual test results showing the fix works.
- A regression test that guards against recurrence.
- Review findings and resolutions.

## 8. Validation gates

- **G1:** failure reproduced on demand, or non-reproducibility documented.
- **G2:** root cause identified from evidence.
- **G3:** the fix is minimal and scoped to the defect.
- **G4:** original failure resolved and surrounding suite passes.
- **G5:** regression test fails before the fix and passes after it.
- **G6:** blocking review findings resolved and re-verified.

## 9. Approval requirements

- Human approval is required before any destructive operation on production
  data, database rollback outside the migration system, or history
  rewriting per `rules/database.md` and `rules/git.md`.
- Hotfixes or production changes must be approved before execution.
- Do not remove or weaken an existing failing test without justification and
  approval per `rules/testing.md`.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- The defect is reproduced on demand (or non-reproducibility is documented).
- The root cause is identified from evidence.
- A minimal fix restores correct behavior without unrelated changes.
- The executed test suite passes, and the regression test fails before / passes
  after the fix.
- Review is complete and blocking findings are resolved.
- No security regression was introduced and no destructive action occurred
  without approval.

Do not claim completion without running the verification steps described
above.