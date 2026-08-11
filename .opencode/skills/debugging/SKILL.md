---
name: debugging
description: Use when investigating a defect or unexpected behavior. Use for reproduction, evidence collection, logs, root-cause analysis, minimal fixes, and regression testing.
---

# Debugging

## When to use

Use when behavior does not match expectations: a failing test, a wrong result, a crash, a hang, or a production incident. Also use before opening the code, to form a hypothesis rather than guessing.

## Process

1. **Reproduce first**: Find the smallest reliable way to trigger the defect. A reproducible case halves the problem; impossible-to-reproduce symptoms are usually environmental, timing, or stale-build issues.
2. **Collect evidence**: Gather the actual inputs, expected outputs, actual outputs, and relevant logs/stack traces before changing anything. Record timestamps and environment details.
3. **Form hypotheses from evidence**: Use logs, traces, and data to narrow the cause. Look for the first deviation from correct behavior, not the first suspicious code you encounter.
4. **Trace the data flow**: Follow the actual values from source to failure point. Check assumptions at each boundary — parsing, type coercion, timezones, encodings, null vs empty.
5. **Rule out the cheap causes**: Rebuild/restart where stale binaries matter; check for environment drift, missing dependencies, and state contamination before deep diving.
6. **Find the root cause, not the symptom**: Identify why the invariant was violated. A fix at the wrong layer (e.g., patching the UI to hide a bad value) will resurface.
7. **Apply a minimal fix**: Change the smallest amount of code that restores correct behavior and restores the violated invariant. Avoid introducing refactors while debugging.
8. **Verify and lock it in**: After the fix, run the reproduction, then the surrounding suite. Add a regression test that fails before and passes after the fix.

## Important checks

- Can I reproduce the defect on demand?
- Do logs and stack traces support my hypothesis, or am I guessing?
- Have I confirmed the actual data values rather than assuming them?
- Did I fix the root cause, or only mask the symptom?
- Does the fix break any related behavior, and is there a regression test?

## Common mistakes

- Changing code before reproducing or understanding the failure.
- Fixing the symptom and declaring victory while the underlying invariant stays broken.
- Rewriting unrelated code during the hunt, blurring what fixed the bug.
- Ignoring evidence (logs, exact versions) in favor of a favorite theory.
- Fixing hard-coded without a regression test, so the bug returns.

## Completion

The defect is reliably reproduced, its root cause is identified from evidence, a minimal fix restores correct behavior and the violated invariant, the related test suite passes, and a regression test guards against recurrence.