# Testing Rules

Constraints on planning, writing, and running tests.

## Appropriate Test Levels

- Match the test level to the risk: unit tests for logic, integration for boundaries, end-to-end for critical user flows.
- Focus automated coverage where failures are expensive and behavior is stable.
- Do not force full coverage of trivial or throwaway code.

## Deterministic Tests

- Write tests that pass or fail consistently on every run.
- Avoid time, randomness, and network dependence; freeze, inject, or replace them.
- Never rely on unchecked order assumptions.

## Edge Cases

- Include boundary values, empty collections, and error paths in tests.
- Test the contract, not just the happy path.
- Cover the input validation and authorization rules that guard the code.

## Regression Testing

- Reproduce a bug with a failing test before or at the same time as the fix.
- Keep the failing test in the suite to prevent recurrence.
- Confirm the test fails on the old code and passes on the fixed code.

## Test Isolation

- Each test starts from a known state and does not depend on other tests.
- Clean up data and resources created by a test.
- Parallel test execution must not share mutable state.

## Failure Investigation

- Investigate a failing test to find the cause before changing anything.
- Report the actual failure and evidence, not an assumption.
- Never delete, weaken, or skip a failing test to make it pass without a justified and approved reason.

## Never Claim Tests Passed Without Running Them

- Only report a test as passing after the test run actually executed and reported it as passing.
- Do not report results from memory, inference, or prior runs.
- If tests could not be run, say so explicitly.

## Verify with the Project's Tooling

- Run tests through the project's documented command, not ad hoc equivalents.
- A green suite on a full run is the only acceptable definition of "tests pass".