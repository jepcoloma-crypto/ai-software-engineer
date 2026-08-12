# Corrected Engineering Prompt — <SLUG>

## Request Status

- READY_FOR_WORKFLOW | NEEDS_CLARIFICATION | INVALID_REQUEST

## Request Type

- <new-project | feature-development | bug-fix | refactoring | database-change | api-change | security-review | deployment | research | documentation | other>

## User Intent

<The underlying goal or problem in the user's own framing.>

## Objective

<A single, unambiguous statement of the intended outcome.>

## Project Context

<Verified repository facts only. Each fact is tagged REPOSITORY FACT and cites the file or line it was observed in. Do not include assumptions here.>

- <Fact> — <file reference>
- <Fact> — <file reference>

## Explicit Requirements

### Functional

- FR-01: <Requirement as stated by the user>

### Non-functional

- NFR-01: <Requirement> — <target or metric>

## Evidence Table

| Claim | Source | Status |
| --- | --- | --- |
| <Claim> | <user statement / file reference / official source / inference> | USER REQUIREMENT / REPOSITORY FACT / CONFIRMED FACT / INFERRED ASSUMPTION / UNKNOWN / REQUIRES RESEARCH |

## Constraints

- <Constraint: technical, organizational, regulatory, or temporal>

## Assumptions

<Unconfirmed inferences only. Each is tagged INFERRED ASSUMPTION and states what would confirm or invalidate it. Assumptions must not be treated as requirements.>

- <Assumption> — <what confirms or invalidates>

## Unknowns

### Blocking

- <Unknown> — <question that resolves it>

### Non-blocking

- <Unknown> — <defer to research or a later phase>

## Ambiguities

- <Ambiguous term or scope> — <interpretations>

## Contradictions

- <Conflict> — <options for the user to adjudicate>

## Dependencies

- <Dependency: system, library, data, or team>

## Risks

- <Risk> — <suggested mitigation>

## Out of Scope

- <Explicit non-goal>

## Acceptance Criteria

<Proposed, observable, testable conditions. Mark as proposals pending user confirmation; never invent requirements.>

- [ ] <Criterion 1>
- [ ] <Criterion 2>

## Clarification Questions

### Blocking

- <Question required before the request can enter a workflow>

### Optional

- <Question> — <default if unanswered>

## Recommended Workflow

- <workflows/<file>.md> — <reasoning>

## Corrected Engineering Prompt

<Normative, self-contained prompt for the recommended workflow and its agents. Preserve the user's original intent while using the structured sections above.>