---
name: api-design
description: Use when designing, extending, or reviewing HTTP/REST APIs. Use for contracts, validation, errors, authentication, authorization, versioning, idempotency, pagination, and compatibility.
---

# API Design

## When to use

Use when creating a new API endpoint, changing an existing one, defining request/response contracts, or reviewing an API surface for correctness and compatibility.

## Process

1. **Design the contract first**: Define resources, their representations, HTTP methods, status codes, and request/response bodies before implementing. Document the contract in an OpenAPI spec or equivalent definition that serves as the source of truth.
2. **Follow REST conventions sensibly**: Use nouns for resources, plural collections, resource IDs in the path, and correct method semantics (GET read, POST create, PUT/PATCH update, DELETE). Do not force REST where another shape is a better fit.
3. **Validate inputs at the boundary**: Validate structure (required fields, types, formats) and business rules. Return a consistent, structured validation error. Never trust client-supplied data.
4. **Define an error contract**: Consistent error envelope (e.g., `{"error": {"code", "message", "details"}}`), appropriate HTTP status codes for the failure class, and documentation of error codes so clients can react programmatically.
5. **Enforce authentication and authorization**: Every endpoint that touches protected data must authenticate the caller and authorize the specific action. Reject unauthorized access before doing work.
6. **Plan for evolution — versioning and compatibility**: Version the API or accept additive changes (new optional fields, new endpoints) without breaking existing clients. Never silently change the meaning of existing fields.
7. **Support idempotency where a request can be retried safely**: For non-idempotent operations (POST creates, payments), accept an idempotency key, deduplicate retries, and return the original result.
8. **Paginate list endpoints**: Use cursor or offset pagination with a bounded page size and return stable metadata (total, next cursor). Apply the same rules to every collection endpoint.
9. **Consider caching**: Safe, cacheable responses (GET) may set `Cache-Control`/`ETag`. Never cache responses that vary per user or contain sensitive data.

## Important checks

- Is the contract documented and reviewed for naming, types, and semantics?
- Is every input validated server-side with a consistent error format?
- Is authentication performed on every protected endpoint, before any processing?
- Does authorization follow least privilege for each action?
- Can existing clients keep working after the change (compatibility)?
- Are mutating operations protected from duplicate execution?
- Is pagination bounded and consistent across collections?
- Are secrets, keys, and internal details never exposed in responses or errors?

## Common mistakes

- Returning generic 500s for client errors or leaking stack traces/DB details in error messages.
- PUT/PATCH semantics that surprise callers (partial vs. full replace).
- Versioning by path without a deprecation plan.
- Idempotency implemented as "retry the work" rather than "deduplicate".
- Breaking changes sneaked into a release: renamed fields, changed types, tightened validation.
- Omitting pagination until a list grows large enough to break.

## Completion

The API has a documented contract with validated inputs, a consistent error format, authentication and authorization on every protected endpoint, planned versioning and compatibility, safe idempotency and pagination, and no sensitive data leakage. Clients can integrate correctly from the documentation alone.