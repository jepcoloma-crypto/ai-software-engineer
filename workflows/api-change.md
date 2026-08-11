# Workflow: API Change

## 1. Purpose

Add, extend, or change an HTTP API contract with explicit compatibility
management, from analysis through implementation, testing, security review,
and documentation. The workflow is
`ANALYZE → COMPATIBILITY ASSESSMENT → DESIGN → IMPLEMENT → TEST → SECURITY
REVIEW → DOCUMENT` and reuses the framework's API, testing, and security
capabilities.

## 2. When to use

Use when adding a new endpoint, changing a request or response shape, altering
validation or semantics, or deprecating and versioning an existing API. Use
when the API contract is a compatibility boundary with external consumers. Do
not use for purely internal changes with no contract impact; use
`feature-development.md`.

## 3. Preconditions

- The current API contract and its consumers are understood.
- The change's purpose and intended impact on consumers are stated.
- The compatibility policy of the project is known.
- Any breaking change requires prior human approval.

## 4. Workflow steps

1. **Analyze the change** — **Lead agent / Architect agent.**
   Identify the endpoints, request and response shapes, validation rules, and
   error behavior involved. Clarify the goal. Use the `api-design` skill and
   `rules/api.md`.
   **Gate G1:** the analysis identifies the affected contract and its
   consumers before design begins.
2. **Assess compatibility** — **Architect agent / Reviewer agent.**
   Classify the change as additive, deprecating, or breaking. Determine what
   existing consumers rely on. Use the `api-design` skill and `rules/api.md`.
   **Gate G2:** compatibility classification is documented; breaking changes
   are flagged for approval.
3. **Design the contract** — **Architect agent.**
   Define the request and response shape, status codes, error format,
   validation, pagination, idempotency, and authentication or authorization
   requirements. Use the `api-design` skill and `rules/api.md`.
   **Gate G3:** the contract is documented and reviewed before implementation.
4. **Implement the change** — **Developer agent.**
   Implement the contract following the design and existing conventions.
   Validate all input at the boundary and apply authentication and
   authorization. Use the `backend-development` and `api-design` skills and
   `rules/api.md`, `rules/coding.md`.
   **Gate G4:** the implementation builds and passes its targeted tests.
5. **Test the change** — **Tester agent.**
   Test the new contract, edge cases, validation, error responses, and
   authorization. Confirm additive changes keep existing consumers working.
   Use the `testing` skill and `rules/testing.md`.
   **Gate G5:** the executed API tests pass and compatibility expectations
   hold.
6. **Perform a security review** — **Security agent.**
   Review input validation, injection, authentication, authorization,
   rate limiting, and information leakage for the changed surface. Use the
   `security-review` skill and `rules/security.md`.
   **Gate G6:** no blocking vulnerability remains; findings are recorded.
7. **Document the change** — **Documentation agent.**
   Update the API contract documentation, endpoint reference, changelog, and
   any migration guidance for consumers. Use `rules/api.md` and
   `rules/documentation.md`.
8. **Confirm completion** — **Lead agent.**
   Confirm all gates have observed evidence before declaring completion.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Analysis and coordination | Lead agent / Architect agent |
| Compatibility assessment | Architect agent / Reviewer agent |
| Contract design | Architect agent |
| Implementation | Developer agent |
| Testing | Tester agent |
| Security review | Security agent |
| Documentation | Documentation agent |

## 6. Relevant skills and rules

- **Skills:** `api-design`, `backend-development`, `testing`,
  `security-review`, `code-review`.
- **Rules:** `rules/api.md`, `rules/core.md`, `rules/security.md`,
  `rules/testing.md`, `rules/documentation.md`, `rules/git.md`.
- **Framework:** the before-coding and before-completion checks in
  `AGENTS.md`.

## 7. Required artifacts

- Analysis of the affected contract and consumers.
- Compatibility assessment classifying the change as additive, deprecating, or
  breaking.
- Documented contract design (request/response, errors, validation,
  versioning, idempotency, pagination).
- Implementation scoped to the contract.
- Automated tests for the contract, edge cases, and error paths.
- Security review findings and resolutions.
- Updated API documentation and changelog.

## 8. Validation gates

- **G1:** affected contract and consumers identified.
- **G2:** compatibility classification documented; breaking changes flagged.
- **G3:** contract design documented and reviewed before implementation.
- **G4:** implementation builds and passes targeted tests.
- **G5:** API tests pass and compatibility expectations hold.
- **G6:** no blocking security vulnerability remains.

## 9. Approval requirements

- Human approval is required for any breaking change to a published contract
  per `rules/api.md`.
- Human approval is required before deprecating or removing an existing
  endpoint or field, and before changing the meaning of existing values.
- Human approval is required before any release or deployment of the change.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- The change is classified as additive, deprecating, or breaking, with
  compatibility documented.
- The contract is documented and matches the implementation.
- Inputs are validated at the boundary; authentication and authorization are
  enforced per `rules/api.md`.
- The executed API test suite passes, including edge cases and error paths.
- Additive changes preserve existing consumers; breaking changes are approved.
- Security review found no blocking vulnerability.
- Documentation is updated and matches the actual contract.

Do not claim completion without running the verification steps described
above.