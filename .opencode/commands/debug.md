---
description: Investigate a reported problem using the debugger agent: reproduce, find the root cause, apply the smallest fix, and run regression tests.
---

You are running the `debug` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including `rules/core.md` and `rules/coding.md`. Do not assume a specific technology stack; inspect the actual project.

# Task

Investigate and fix the following problem:

$ARGUMENTS

# Responsibilities

- Use the `debugger` agent to investigate the problem.
- Reproduce the issue when possible; find the smallest reliable trigger and capture inputs, expected behavior, actual behavior, and relevant logs.
- Inspect logs and relevant code, trace actual values from source to failure point, and identify the root cause from evidence rather than guesswork.
- Implement the smallest appropriate fix that restores correct behavior. Do not mask the symptom and do not introduce unrelated refactors.
- Run regression tests and the surrounding suite, and report actual results.
- Never claim the issue is fixed unless reproduction and tests were actually run and passed.

# Tools, skills, and references

- Use the `debugging` skill and `workflows/bug-fix.md` to guide the process.
- Use `rules/testing.md` for test execution and regression-test expectations; use `rules/coding.md` for the fix itself.

# Constraints

- Keep the fix minimal and scoped to the defect.
- Do not remove or weaken an existing failing test without justification and approval.
- Never expose secrets in logs or output.
- Ask for human approval before destructive operations (e.g., changes to production data or history rewriting).
- Prefer evidence over assumptions; document what was verified.

# Output

Report:
1. Reproduction steps and captured evidence.
2. Root-cause description supported by evidence.
3. The fix applied and why it is minimal.
4. Actual test results (original issue resolved, surrounding suite, regression test).
5. Any unresolved aspects or required follow-up.