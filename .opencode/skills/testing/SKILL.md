---
name: testing
description: Use when planning, writing, or running tests. Use for unit, integration, API, E2E, regression, edge cases, test strategy, test data, coverage, and verification.
---

# Testing

## When to use

Use before writing a test suite for a feature, when a change needs verification, when a test is flaky or slow, or when deciding what tests a new behavior needs.

## Process

1. **Define the test strategy per layer**: Decide what each layer covers so the suite stays meaningful and fast:
   - **Unit tests**: pure logic, services, helpers, edge cases — fast, no external deps.
   - **Integration tests**: code + real collaborators (database, filesystem, message bus).
   - **API tests**: endpoints end-to-end through HTTP — contracts, status codes, errors.
   - **E2E tests**: whole user journeys through the real UI — the smallest number, covering critical paths only.
2. **Test behavior, not implementation**: Assert outcomes a user or caller observes, not internal call patterns. This keeps tests valid when internals change.
3. **Cover edge cases deliberately**: Boundaries, empty values, malformed input, concurrency, failure paths, authorization failures, and the classic empty/max/off-by-one cases for any numeric boundary.
4. **Design test data explicitly**: Make each test set up its own data; avoid hidden shared state and order-dependent tests. Name fixtures by intent.
5. **Write regression tests for bugs**: When a defect is fixed, add a test that fails before the fix and passes after it.
6. **Keep tests fast and isolated**: No test should depend on another test's execution order. Minimize shared mutable fixtures that make tests flaky.
7. **Verify, not just cover**: Run the suite and confirm the results. Use coverage as a signal for untested branches, not as a finish line.

## Important checks

- Do tests describe the required behavior and its edge cases?
- Are they deterministic, isolated, and independent of run order?
- Do they actually fail when the behavior breaks (mutation check)?
- Are they using existing framework conventions rather than introducing a new one?
- Is the suite fast enough to run often?

## Common mistakes

- Testing implementation details, so refactors break unrelated tests.
- Writing tests that pass because they never assert anything meaningful or never exercise the failure path.
- Test-to-test coupling and reliance on global/shared state.
- E2E tests for everything (slow, brittle) or none of the critical paths.
- Asserting on mocks that mirror the code instead of the real behavior.
- Deleting or weakening a failing test instead of fixing the code.

## Completion

Tests exist for the important behaviors and edge cases, are deterministic and isolated, follow project conventions, fail when the behavior breaks, and have been executed with actual results reported. The suite gives confidence the change works and will keep working.