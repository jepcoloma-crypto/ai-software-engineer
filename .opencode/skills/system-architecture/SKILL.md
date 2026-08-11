---
name: system-architecture
description: Use when designing or reviewing a system's high-level structure. Use for architecture styles, module boundaries, system components, scalability, reliability, security boundaries, tradeoffs, and architecture decisions.
---

# System Architecture

## When to use

Use before and during implementation of any non-trivial system: when deciding structure, when a feature crosses module boundaries, or when reviewing whether existing structure still fits the requirements.

## Process

1. **Reuse before design**: Prefer to extend an existing, working architecture over designing a new one. Understand the current system first.
2. **Choose an architecture style deliberately**: Monolith, modular monolith, microservices, event-driven, layered — each has costs. Justify the choice against the actual requirements, not fashion.
3. **Define module boundaries**: Each module should have a single responsibility, a clear owned surface (public APIs), and explicit dependencies. Avoid tangled or cyclic dependencies.
4. **Identify components**: List components, their responsibilities, data flow, and the interfaces between them. Document the contract at each boundary.
5. **Address cross-cutting concerns**:
   - **Scalability**: how the system grows (vertical, horizontal, caching, partitioning).
   - **Reliability**: failure modes, retries, timeouts, graceful degradation, redundancy.
   - **Security boundaries**: trust zones, authentication and authorization enforcement points, data sensitivity.
6. **Evaluate tradeoffs**: For each decision, state what is gained and what is lost. Record decisions (ADR-style) so the rationale is preserved.
7. **Validate the design**: Run the main flows and failure scenarios through the architecture on paper before writing code.

## Important checks

- Does each component have a clear owner and contract?
- Are dependencies acyclic and justified?
- Are security boundaries explicit and enforced at the module edge?
- Does the design handle failure, not just the happy path?
- Is complexity justified by a concrete requirement?

## Common mistakes

- Over-engineering: distributed systems, queues, and caches added without a requirement.
- Premature abstraction: generic layers with no current consumer.
- Ignoring the existing architecture and silently restructuring it.
- Choosing microservices when a monolith would be simpler to operate.
- Leaking implementation details across module boundaries.

## Completion

A validated architecture exists that fits the requirements, component boundaries and contracts are clear, cross-cutting concerns (scalability, reliability, security) are addressed, the tradeoffs of each decision are documented, and the design is simple enough for a team to implement and maintain.