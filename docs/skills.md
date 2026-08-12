# Skills

This document catalogs the skills defined under `.opencode/skills/`. Skills
provide specialized knowledge for a task area and are loaded when that area
is relevant. Workflows reference the skills that apply to each phase, so a
skill's content lives in one place and is reused rather than duplicated.

Each skill is a directory containing a `SKILL.md` whose description states when
to use it. The descriptions below summarize that guidance; they do not restate
the skills' full contents.

## Skill Catalog

### requirements-analysis
Used when gathering and refining requirements for a feature or system: functional
and non-functional requirements, acceptance criteria, constraints, assumptions,
and ambiguity detection before design or implementation begins.

### prompt-corrector
Used to transform a raw, imperfect user request into a clear, structured,
verifiable engineering request before an engineering workflow begins: request
classification, intent extraction, evidence labeling, ambiguity, contradiction
and scope detection, clarification, and readiness decisions.

### system-architecture
Used when designing or reviewing a system's high-level structure: architecture
styles, module boundaries, system components, scalability, reliability, security
boundaries, trade-offs, and architecture decisions.

### database-design
Used when modeling or changing relational data in PostgreSQL: relational
modeling, keys, relationships, constraints, indexes, transactions, migrations,
data integrity, and query performance.

### api-design
Used when designing, extending, or reviewing HTTP/REST APIs: contracts,
validation, errors, authentication, authorization, versioning, idempotency,
pagination, and compatibility.

### frontend-development
Used when building or modifying user-facing UI: UI architecture, component
design, state management, forms, validation, accessibility, performance,
responsive design, and API integration.

### backend-development
Used when building or modifying server-side services: service architecture,
business logic, validation, authentication, authorization, errors, transactions,
logging, observability, and performance.

### testing
Used when planning, writing, or running tests: unit, integration, API, E2E,
regression, edge cases, test strategy, test data, coverage, and verification.

### debugging
Used when investigating a defect or unexpected behavior: reproduction, evidence
collection, logs, root-cause analysis, minimal fixes, and regression testing.

### code-review
Used when reviewing proposed code or design changes before they are merged:
correctness, architecture, maintainability, security, performance, testing,
error handling, and review severity.

### security-review
Used when auditing code or designs for security vulnerabilities: authentication,
authorization, secrets, input validation, SQL injection, XSS, CSRF, API security,
dependencies, file handling, rate limiting, and session security.

### git-workflow
Used when planning or executing Git operations: branching, commits, pull
requests, conflict resolution, history quality, safe Git operations, and
avoiding destructive operations.

### deployment
Used when releasing software to any environment: build validation, environments,
configuration, secrets, migrations, deployment checks, health checks, rollback,
and post-deployment verification.

## How Skills Are Used

- Skills are referenced by the workflows in `workflows/` at the phase where the
  relevant task area applies. For example, `feature-development.md` references
  `api-design` when the feature touches an API contract.
- Skills complement rules: rules are enforceable guardrails, while skills carry
  the specialized how-to knowledge for a task area (see `docs/architecture.md`).
- A skill is loaded when its area is relevant; it does not replace the core
  principles in `AGENTS.md`, which still apply to every task.