# API Rules

Constraints on HTTP contract design and implementation.

## Contracts

- Define the request and response shape explicitly before implementing.
- Keep the contract in sync with its documentation.
- Treat the API contract as a compatibility boundary that changes require care.

## Validation

- Validate all request input at the boundary, before business logic runs.
- Validate types, format, ranges, and required fields with clear errors.
- Reject unknown or malformed fields rather than silently ignoring them when correctness matters.

## Authentication

- Authenticate every request that touches protected resources.
- Do not place authentication trust in client-supplied values.
- Never bypass authentication for debugging or convenience.

## Authorization

- Authorize per resource and per action, not just at the endpoint level.
- Base decisions on verified identity and context, never on unverified client claims.
- Fail closed: deny by default when authorization state is missing or unclear.

## HTTP Semantics

- Use standard HTTP methods, status codes, and headers for their intended meaning.
- Do not overload method semantics or encode state in URLs.
- Follow the project's convention for code 2xx, 4xx, and 5xx usage.

## Error Handling

- Return structured, machine-readable errors with stable error identifiers.
- Include enough detail for the caller to act without leaking internals.
- Do not leak stack traces, SQL, or internal paths in responses.
- Use consistent error shapes across endpoints.

## Versioning

- Version the API before removing or changing existing behavior.
- Document the supported versions and their compatibility guarantees.
- Never silently change behavior within a published version.

## Pagination

- Paginate list endpoints with explicit, bounded page sizes.
- Use stable cursors or offsets that do not break under concurrent writes.
- Return the same item set consistently within a single paged query.

## Idempotency

- Design mutating operations to be safe to retry where the caller may retry.
- Use idempotency keys for operations that trigger side effects.
- Ensure retries of the same logical request do not duplicate side effects.

## Compatibility

- Additive changes (new fields, new endpoints) take priority over breaking ones.
- Never remove or rename existing fields or endpoints without versioning or approval.
- Preserve the meaning of existing values when extending enums.

## Security

- Assume all input is untrusted; treat every endpoint as a trust boundary.
- Rate limit sensitive and expensive endpoints.
- Apply the security rules for input validation, injection prevention, and session handling at every API boundary.