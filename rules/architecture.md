# Architecture Rules

Constraints governing high-level system structure.

## Separation of Concerns

- Split the system into modules with distinct, single responsibilities.
- Do not mix presentation, business logic, and data access in the same layer.
- Keep cross-cutting concerns (logging, auth, error handling) in dedicated mechanisms.

## Module Boundaries

- Modules communicate through explicit, documented interfaces.
- Do not reach into another module's internals.
- Prefer stable, minimal public surfaces over broad ones.

## Dependency Direction

- Dependencies point inward or downward, never from concrete layers back to their callers.
- No cycles between modules or layers.
- Depend on abstractions and contracts, not concrete implementations, where it reduces coupling.

## Scalability

- Design for the current scale and a clearly stated near-term target.
- Make stateless, horizontally scalable components the default where there is no reason not to.
- Keep scaling-sensitive resources (queues, caches, DB connections) explicit and bounded.

## Reliability

- Handle failure explicitly: fail fast where appropriate, degrade gracefully otherwise.
- Avoid single points of failure in critical paths.
- Design for retries, timeouts, and partial failure.

## Maintainability

- Prefer simple designs that reveal intent over clever ones.
- Make behavior observable through logs and structured output.
- Keep module responsibilities small enough to be understood in one reading.

## Backward Compatibility

- Do not break existing contracts unless a change is intentional and approved.
- When breaking change is required, migrate and communicate it explicitly.
- Design extensible interfaces to reduce future breakage.

## Avoid Unnecessary Complexity

- Do not add layers, abstractions, or infrastructure without a concrete need.
- Prefer the simplest architecture that satisfies current and stated near-term requirements.
- Reject premature distribution, microservices, and speculative generality.