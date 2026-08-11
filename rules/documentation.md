# Documentation Rules

Constraints on creating and keeping documentation honest.

## Accuracy

- Document what the system actually does, not what it should do.
- Never document features that do not exist.
- Verify claims in documentation against the code before writing them.

## Keep Documentation in Sync with Implementation

- Update documentation when the behavior it describes changes.
- Treat stale documentation as a defect to fix, not a footnote.
- Review documentation in the same change as the implementation it explains.

## Architecture Decisions

- Record significant architecture decisions with context, reasoning, and consequences.
- Use the project's chosen decision-record format where one exists.
- Reference the decision record from the code it affects when convenient.

## APIs

- Document every public endpoint: purpose, request shape, response shape, errors, and version.
- Keep examples copy-pasteable and verified against the real contract.
- Update API documentation when the contract changes.

## Setup

- Document how to obtain, install, configure, and run the system.
- Record exact commands and required environment so a fresh setup works.
- Document prerequisites and environment-specific steps.

## Deployment

- Document build, release, and rollback procedures.
- List required environment variables and how they are provided.
- Record migration and seed steps that production must run.

## Changes

- Document user-visible and behavior-affecting changes where the project tracks them.
- Note breaking changes and the migration path.
- Keep changelog entries accurate and dated.

## Avoid Undocumented Assumptions

- State non-obvious prerequisites and limitations explicitly.
- Do not leave behavior to be inferred from code alone when it matters.
- If a constraint is project-specific, record it rather than assuming it.

## Scope

- Keep documentation close to the thing it describes.
- Reuse and reference existing documents instead of duplicating them.