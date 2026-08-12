# Core Engineering Rules

Fundamental constraints that apply to every task.

## Understand Before Changing

- Inspect the repository, architecture, relevant files, and existing patterns before editing.
- Identify dependencies, API contracts, and database structures on first contact.
- Do not start coding when requirements or architecture are unclear.

## Ready Before Workflow

- Do not start an engineering workflow until the request is READY_FOR_WORKFLOW
  or any blocking clarification is resolved.
- A request that needs clarification must be corrected and confirmed before
  proceeding into the workflow.

## Research Uncertainty

- Research before making uncertain technical decisions.
- Prefer official documentation and established project conventions.
- Never invent APIs, libraries, documentation, or system behavior.

## Avoid Fabrication

- Never fabricate successful results, test outcomes, or verification.
- Never claim results you have not observed.
- Never invent undocumented APIs or system behavior.

## Minimize Unnecessary Changes

- Keep changes focused on the requested task.
- Prefer small changes over large rewrites.
- Avoid unrelated edits and premature abstraction.

## Preserve Existing Behavior

- Preserve existing functionality unless a change is intentional.
- Never silently modify critical architecture.
- Prefer simple, maintainable solutions that match existing conventions.

## Validate Changes

- Run relevant tests, type checks, linting, and builds before declaring completion.
- Check error handling, security implications, and data integrity.
- Never claim completion without verification.

## Protect Secrets

- Never expose credentials or secrets in code, logs, output, or commits.
- Never commit secrets to the repository.

## Document Decisions

- Document important architectural and design decisions.
- Record the reasoning behind non-obvious choices.

## Never Claim Unverified Results

- A result is unverified until it has been observed.
- Unverified claims are treated as fabricated claims and are not permitted.