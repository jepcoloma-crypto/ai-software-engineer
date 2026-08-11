# Workflow: Database Change

## 1. Purpose

Make a safe, reversible, reviewed change to a relational database schema,
queries, or data from analysis through verified migration and documentation.
The workflow is
`ANALYZE → DESIGN → MIGRATION → TEST → VALIDATE → DOCUMENT` and reuses the
framework's database, testing, and documentation capabilities.

## 2. When to use

Use when changing schema, constraints, indexes, views, or stored behavior, or
when a query or write path is slow or returns wrong data. Use when a migration
will be applied to a shared, staging, or production database. Do not use for
application-only changes that do not touch the database.

## 3. Preconditions

- The current schema and its data are understood.
- The change's purpose and expected impact are stated.
- Access to a non-production environment for testing exists.
- Any destructive operation on production data requires prior human approval.

## 4. Workflow steps

1. **Analyze the change** — **Database agent / Lead agent.**
   Identify the entities, access patterns, relationships, and volume involved.
   Clarify the goal of the change. Use the `database-design` skill and
   `rules/database.md`.
   **Gate G1:** the analysis records the affected tables, queries, and data
   before design begins.
2. **Design the change** — **Database agent.**
   Model keys, constraints, indexes, and relationships. Write forward and
   rollback paths. Consider data integrity, concurrency, and query performance.
   Use the `database-design` skill and `rules/database.md`.
   **Gate G2:** the design is reviewed and approved before a migration is
   written.
3. **Write the migration** — **Database agent.**
   Create a versioned, reviewed migration with a forward and a rollback path.
   Never edit an applied migration; add a new one. Use the `database-design`
   skill and `rules/database.md`.
   **Gate G3:** the migration is complete, reversible, and ordered.
4. **Test the migration** — **Tester agent / Database agent.**
   Apply the migration to a non-production environment. Test the forward path,
   the rollback path, and the affected queries. Use the `testing` skill and
   `rules/testing.md`.
   **Gate G4:** the migration applies cleanly, rolls back cleanly, and the
   affected queries behave correctly.
5. **Validate data and integrity** — **Database agent.**
   Validate that existing data remains correct, constraints hold, and the
   schema matches the design. Confirm query performance on the new structure.
   Use `rules/database.md`.
   **Gate G5:** data integrity and query behavior are validated before any
   production application.
6. **Document the change** — **Documentation agent.**
   Update schema, migration, and any API or setup documentation that reflects
   the database change. Use `rules/documentation.md`.
7. **Apply to higher environments (with approval)** — **Lead agent.**
   Apply the migration to staging or production only with human approval and
   per the project's release process. This step may be deferred to
   `deployment.md` when part of a release.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Analysis and design | Database agent |
| Migration authoring | Database agent |
| Migration and query testing | Tester agent / Database agent |
| Integrity and performance validation | Database agent |
| Documentation | Documentation agent |
| Coordination and approval | Lead agent |

## 6. Relevant skills and rules

- **Skills:** `database-design`, `testing`, `deployment`.
- **Rules:** `rules/database.md`, `rules/testing.md`, `rules/core.md`,
  `rules/documentation.md`, `rules/git.md`.
- **Framework:** the data-integrity and safety guidance in `AGENTS.md`.

## 7. Required artifacts

- Analysis of affected tables, queries, and data.
- Database design with keys, constraints, indexes, and relationships.
- A versioned migration with forward and rollback paths.
- Actual test results from applying and rolling back the migration in a
  non-production environment.
- Integrity and performance validation results.
- Documentation reflecting the new schema.

## 8. Validation gates

- **G1:** analysis complete; affected data and queries identified.
- **G2:** design reviewed and approved before the migration is written.
- **G3:** migration is versioned, reversible, and ordered.
- **G4:** migration applies and rolls back cleanly in a non-production
  environment.
- **G5:** data integrity and query behavior validated before any production
  application.

## 9. Approval requirements

- Human approval is required before applying any migration to a staging or
  production database.
- Human approval is required before any destructive or irreversible data
  operation (drop table, truncate, batch delete, column type change that
  alters meaning). Prefer reversible changes per `rules/database.md`.
- Never edit a production database schema outside a migration per
  `rules/database.md`.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- The change is analyzed and designed with data integrity as a first-class
  concern.
- A versioned, reversible migration exists and was never retroactively edited.
- The migration applied and rolled back cleanly in a non-production
  environment, with results observed.
- Data integrity and query performance are validated on the new structure.
- Documentation reflects the actual schema.
- No destructive production operation occurred without approval.

Do not claim completion without running the verification steps described
above.