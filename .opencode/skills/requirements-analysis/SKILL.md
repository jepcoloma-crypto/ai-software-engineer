---
name: requirements-analysis
description: Use when gathering and refining requirements for a feature or system. Use for functional and non-functional requirements, acceptance criteria, constraints, assumptions, and ambiguity detection before design or implementation begins.
---

# Requirements Analysis

## When to use

Use when a request is underspecified, when starting a new feature or system, or when you must translate a vague idea into testable requirements. Both coding tasks and review tasks may require this skill when the acceptance bar is unclear.

## Process

1. **Clarify intent**: Identify the problem and the user's goal before proposing solutions. Restate the request in your own words and confirm.
2. **Gather requirements**: Ask focused questions to surface missing facts. Distinguish:
   - **Functional requirements** — what the system must do.
   - **Non-functional requirements** — performance, availability, security, scalability, usability, maintainability.
3. **Identify constraints**: Note technical, organizational, legal, and time constraints that bound the solution.
4. **Document assumptions**: Record every assumption explicitly. Mark assumptions that are risky or could invalidate the design.
5. **Write acceptance criteria**: Define observable, testable conditions that prove the requirement is met. Prefer the Given/When/Then form where possible.
6. **Detect ambiguity**: Check for vague terms ("fast", "user-friendly", "handle errors"), unstated actors, and undefined edge cases. Ask for clarification or propose a sensible default and flag it.
7. **Confirm scope**: Agree on what is in scope and, importantly, what is out of scope for the current effort.

## Important checks

- Are both functional and non-functional requirements captured?
- Is every acceptance criterion testable and unambiguous?
- Are constraints recorded as constraints, not assumptions?
- Are actors and edge cases defined (empty input, concurrency, failure)?
- Would a second engineer reach the same understanding from the written requirements?

## Common mistakes

- Diving into implementation before the goal is clear.
- Recording assumptions silently instead of flagging them.
- Confusing nice-to-haves with requirements.
- Skipping non-functional requirements until they become production incidents.
- Leaving acceptance criteria as prose that cannot be verified.

## Completion

Requirements are unambiguous, cover functional and non-functional needs, have testable acceptance criteria, and explicitly list constraints and assumptions. You can state clearly what will be built, who uses it, and how success is measured.