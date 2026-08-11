# Database Rules

Constraints on schema, queries, and data operations.

## Data Integrity

- Consider data integrity in every schema change.
- Model the schema to prevent logically invalid data from being stored.
- Apply constraints at the database, not just in application code.

## Keys

- Every table has a primary key; choose it deliberately.
- Use foreign keys to enforce relationships between tables.
- Match key types and collation exactly across joined and referenced columns.

## Constraints

- Enforce invariants with NOT NULL, UNIQUE, CHECK, and exclusion constraints where they hold.
- Do not rely on application validation alone for critical invariants.
- Give constraints explicit, meaningful names for debuggability.

## Indexes

- Create indexes to support actual query patterns, not speculative ones.
- Verify queries with an execution plan when performance matters.
- Avoid redundant and overlapping indexes.

## Transactions

- Wrap multi-statement operations that must be atomic in a transaction.
- Keep transactions short and scoped to the work they protect.
- Never hold user input or network I/O open inside a transaction.

## Migrations

- Make every schema change through a versioned, reviewed migration.
- Write migrations that are safe to apply and roll back.
- Never edit a production database schema outside a migration.

## Concurrency

- Use explicit locking and constraints to handle concurrent writes on shared rows.
- Document the transaction isolation behavior your code relies on.
- Round-trip expected values (optimistic concurrency) where lost-update risk matters.

## Query Performance

- Avoid full scans on hot paths; use indexes to serve filtered and sorted queries.
- Fetch only the rows and columns the operation needs.
- Beware of N+1 patterns and load-bearing queries in transactions.

## Backups

- Verify backups are taken and restorable before relying on them.
- Treat backup restoration as a process to be tested, not assumed.

## Safe Destructive Operations

- Never delete or truncate production data without approval.
- Use soft delete or staging tables before irreversible operations.
- Prefer reversible changes whenever possible.

## Resource Discipline

- Close connections and release resources explicitly.
- Use connection pools sized to the load, not unbounded.