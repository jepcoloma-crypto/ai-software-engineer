---
name: backend-development
description: Use when building or modifying server-side services. Use for service architecture, business logic, validation, authentication, authorization, errors, transactions, logging, observability, and performance.
---

# Backend Development

## When to use

Use when implementing or changing server-side functionality: endpoints, business logic, services, background jobs, or anything that validates and processes data before it reaches a database or another system.

## Process

1. **Follow the existing service architecture**: Match the project's framework, layering, dependency patterns, and error conventions. Inspect neighboring services before writing new code.
2. **Place business logic where it belongs**: Keep rules in a service/domain layer rather than scattered across controllers, routes, and ORM callbacks. A controller should translate HTTP; the service should apply rules.
3. **Validate everything at the boundary**: Validate request shape and business rules server-side with the project's validation tooling. Reject invalid input early with a consistent error response. Treat all client input as untrusted.
4. **Enforce authentication and authorization**: Authenticate the caller on every protected path and authorize each action (never just "logged in"). Apply the same enforcement to internal jobs where relevant.
5. **Define consistent error handling**: Map failures to intentional responses (4xx for client errors, 5xx for server errors). Never leak stack traces, SQL, or internals to clients. Log the detail server-side.
6. **Use transactions for multi-step writes**: Wrap operations that must be all-or-nothing in a transaction. Consider idempotency and concurrency (races, duplicate submissions) for mutating operations.
7. **Log and observe**: Log meaningful, structured events — request outcomes, business events, and failures — with enough context to debug. Export metrics/traces per the project's observability setup. Avoid logging secrets or sensitive data.
8. **Mind performance**: Avoid N+1 queries, fetching columns you do not need, and synchronous work that blocks the request path unnecessarily. Use indexes and query plans for hot paths.

## Important checks

- Are inputs validated and never trusted as-is?
- Is every protected operation authenticated and authorized?
- Do multi-step writes stay atomic and handle duplicate/re-entrant calls?
- Are errors intentional, consistent, and free of internal detail leakage?
- Is there enough logging to trace a request end-to-end?
- Are hot code paths query-efficient?

## Common mistakes

- Business rules duplicated across controllers and queries instead of living in one service layer.
- Validation only in the frontend or middleware, not at the service boundary.
- Returning 500 for expected client mistakes, or a bare `400` with no detail.
- Holding DB connections or transactions during slow external calls.
- Logging request bodies that contain passwords, tokens, or PII.
- Making blocking calls that stall the web worker pool.

## Completion

The service follows existing architecture, business logic lives in the right layer, inputs are validated at the boundary, authentication/authorization are enforced on every protected action, errors are consistent and safe, writes are transactional, and there is sufficient logging and observability to operate and debug the feature in production.