# Coding Rules

Constraints on writing and modifying code.

## Readability

- Write code that can be understood in one reading.
- Prefer explicit, linear control flow over clever one-liners.
- Keep functions and methods small and single-purpose.

## Consistency

- Follow existing project conventions and surrounding code style.
- Match the framework, idioms, and patterns already in use.
- Do not introduce a parallel style for new code.

## Naming

- Use clear, descriptive names that state intent.
- Keep naming consistent with the domain and nearby code.
- Avoid abbreviations and single-letter names except in conventional contexts.

## Error Handling

- Make error handling explicit; do not swallow exceptions silently.
- Propagate or translate errors at boundaries; log with context.
- Prefer failing loudly over continuing with corrupt state.

## Input Validation

- Validate all boundary input: externally supplied data, config, and CLI arguments.
- Reject invalid input with clear errors, not silent coercion.
- Validate at trust boundaries, not just inside the core logic.

## Type Safety

- Use the project's type system where it applies.
- Represent invalid states as unrepresentable where reasonably possible.
- Never cast or bypass the type system to silence a legitimate type error.

## Duplication

- Avoid duplicated logic; extract shared behavior into a single named place.
- Do not copy code across modules or services.
- Do not reduce duplication by creating premature abstractions.

## Logging

- Log meaningful events with enough context to investigate failures.
- Structure logs consistently for the project's tooling.
- Never log secrets, tokens, or personal data.

## Configuration

- Externalize configuration that varies between environments.
- Validate configuration at startup; fail fast on invalid values.
- Keep defaults safe and environment-specific overrides explicit.

## Focused Changes

- Keep each change scoped to the requested task.
- Do not mix refactoring, formatting, or unrelated improvements into a functional change.
- Before editing, identify exactly which files and functions a change requires.