# Agents

This document catalogs the ten agents defined in .opencode/agents/.

The files under .opencode/agents/ are the **authoritative agent definitions**.
This document is summary-only and must not duplicate their full instructions.
When an agent definition changes, update its authoritative file first.

All ten agents are subagents. The lead agent (the main session) coordinates
workflows, delegates specialized tasks, holds final sign-off, and confirms
completion.

## Agent Permissions

| Agent         | File Editing |
| ------------- | ------------ |
| developer     | Can edit     |
| tester        | Can edit     |
| debugger      | Can edit     |
| database      | Can edit     |
| documentation | Can edit     |
| prompt-corrector | Cannot edit  |
| researcher    | Cannot edit  |
| architect     | Cannot edit  |
| reviewer      | Cannot edit  |
| security      | Cannot edit  |

Permission settings are defined in each authoritative agent file.

---
## Agent Catalog

### prompt-corrector

Transforms an unclear, incomplete, ambiguous, contradictory, or poorly
structured user request into a clear, structured, implementation-ready
engineering prompt before the engineering workflow begins. Determines intent,
extracts explicit requirements, marks missing information and unconfirmed
assumptions, identifies users, constraints, and acceptance criteria, and
assesses readiness.

**Typical use:** Running `/correct` before a workflow, normalizing a raw user
request, surfacing missing or ambiguous information, and classifying the
request as READY, READY WITH ASSUMPTIONS, or NEEDS CLARIFICATION.

**Authoritative definition:** .opencode/agents/prompt-corrector.md

---

### researcher

Investigates technical questions and provides evidence-based recommendations
before uncertain technical decisions.

**Typical use:** Researching technologies, libraries, APIs, platforms,
constraints, risks, and trade-offs.

**Authoritative definition:** .opencode/agents/researcher.md

---

### architect

Transforms requirements into technical architecture, system design, data
flows, API contracts, boundaries, trade-offs, and implementation plans.

**Typical use:** Requirements analysis, architecture design, impact analysis,
and implementation planning.

**Authoritative definition:** .opencode/agents/architect.md

---

### developer

Implements approved plans while following existing project architecture,
coding conventions, and verification requirements.

**Typical use:** Feature implementation, approved fixes, refactoring, and
release builds.

**Authoritative definition:** .opencode/agents/developer.md

---

### reviewer

Reviews implementations and architectural changes for correctness,
maintainability, security, performance, compatibility, and edge cases.

**Typical use:** Pre-merge reviews and verification of completed changes.

**Authoritative definition:** .opencode/agents/reviewer.md

---

### tester

Designs and executes tests and reports actual verification results without
fabricating or assuming test outcomes.

**Typical use:** Feature testing, regression testing, API testing, migration
verification, and release testing.

**Authoritative definition:** .opencode/agents/tester.md

---

### debugger

Reproduces defects, determines root causes, implements focused fixes, and
verifies that the original failure has been resolved.

**Typical use:** Bug reproduction, root-cause investigation, minimal fixes, and
regression verification.

**Authoritative definition:** .opencode/agents/debugger.md

---

### security

Audits systems and code for security vulnerabilities, configuration risks,
authentication and authorization issues, injection risks, and other
security concerns.

**Typical use:** Security reviews of applications, APIs, deployments, and
architectural changes.

**Authoritative definition:** .opencode/agents/security.md

---

### database

Handles relational data modeling, schema changes, migrations, queries,
indexes, transactions, concurrency, and data-integrity concerns.

**Typical use:** Database design, migrations, query optimization, and
database-change workflows.

**Authoritative definition:** .opencode/agents/database.md

---

### documentation

Creates and maintains accurate documentation that reflects the actual system,
including architecture, APIs, setup, deployment, and important decisions.

**Typical use:** Documentation updates after implementation, architecture
documentation, API documentation, and release documentation.

**Authoritative definition:** .opencode/agents/documentation.md

---

## Agent Selection

Workflows determine which specialized agents should participate in each
lifecycle stage.

The lead agent should delegate specialized work rather than duplicating the
responsibilities of the specialized agents.

Agent definitions must remain focused, reusable, and independent of any
specific AI model or provider.

For the complete role, responsibilities, restrictions, and permissions of an
agent, always refer to its authoritative file under .opencode/agents/.

