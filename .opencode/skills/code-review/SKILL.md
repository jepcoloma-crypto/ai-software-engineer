---
name: code-review
description: Use when reviewing proposed code or design changes before they are merged. Use for correctness, architecture, maintainability, security, performance, testing, error handling, and review severity.
---

# Code Review

## When to use

Use when a change is proposed for review, whether written by you or others, before it merges. Also use for self-review of your own significant changes before declaring completion.

## Process

1. **Understand intent**: Read the requirements and the change's purpose before the diff. A review that does not know the goal judges the wrong things.
2. **Read the diff, then the context**: Review the changes, then follow into surrounding code to verify how it integrates. Check the diff against the whole file, not in isolation.
3. **Assess in priority order**:
   - **Correctness**: Does it do what is intended, including edge cases, failure paths, and concurrency?
   - **Security**: Inputs validated, secrets safe, auth enforced, no injection/leak risks.
   - **Architecture**: Does it fit existing structure, module boundaries, and conventions?
   - **Maintainability**: Clear naming, no duplication, appropriate abstraction, no hidden side effects.
   - **Performance**: Any obvious N+1, unbounded work, or blocking issues in hot paths.
   - **Testing**: Are the important behaviors and edge cases covered with meaningful assertions?
   - **Error handling**: Are failures intentional, consistent, and safely reported?
4. **Apply severity ratings**: Distinguish blocking issues (wrong behavior, data loss, security hole), should-fix (quality, maintainability), and nitpicks (style). Do not block a merge on nitpicks and do not wave through a blocking issue.
5. **Verify, do not assume**: Run the tests or the described verification if you can. If you cannot, say so rather than assuming success.
6. **Communicate clearly**: Point at specific lines, explain the problem and why it matters, and suggest a concrete fix. Ask questions when behavior is unclear instead of asserting it is wrong.

## Important checks

- Does the change behave correctly for the happy path and edge cases?
- Are there security implications (validation, secrets, injection, authorization)?
- Does it follow existing architecture and conventions?
- Is the diff focused, with no unrelated changes?
- Are the tests meaningful and run?
- Are errors handled and reports free of internal detail?

## Common mistakes

- Judging style over substance, or letting a "looks fine" pass hide a correctness hole.
- Nitpicking every line instead of prioritizing what affects behavior or security.
- Approving without running tests or reading the surrounding context.
- Reviewing only the diff in isolation and missing integration breakage.
- Blocking the merge on a personal style preference.

## Completion

The change is understood and verified against its intent: correctness, security, architecture, maintainability, performance, testing, and error handling are assessed, severity is clearly communicated, blocking issues are resolved, and the change is approved only when evidence (tests/verification) supports it.