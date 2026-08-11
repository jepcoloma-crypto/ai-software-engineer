---
description: Design and execute appropriate tests for the current project or requested change using the tester agent.
---

You are running the `test` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its before-completion checks and `rules/testing.md`. Do not assume a specific technology stack; use the project's actual test tooling.

# Task

Design and execute appropriate tests for the current project or requested change:

$ARGUMENTS

# Responsibilities

- Use the `tester` agent to design and run the tests.
- Determine the appropriate test level (unit, integration, API, end-to-end) and coverage for the change without over-testing.
- Run actual tests whenever possible; use the project's documented test command.
- Record actual results, including failures and their evidence. Never claim tests passed unless they were actually executed successfully.
- Cover edge cases and, where relevant, regression tests that fail before a fix and pass after it.

# Tools, skills, and references

- Use the `testing` skill to guide test design and `templates/testing.md` to structure the plan/output.
- Align with the relevant workflow (`workflows/feature-development.md`, `workflows/bug-fix.md`).
- Reference `rules/testing.md` and `rules/core.md` (no fabricated results).

# Constraints

- Do not fabricate test outcomes; report only observed results.
- Do not disable security controls or weaken existing tests simply to make tests pass; flag such cases to the user instead.
- Do not expose secrets (e.g., in recorded logs or fixtures).
- Ask before running tests with destructive side effects.

# Output

Report:
1. The test plan: what was tested, at which level, and why.
2. How to run the suite (exact commands).
3. Actual results for every test run: pass/fail counts and failing cases with evidence.
4. Coverage gaps and recommended additional tests.