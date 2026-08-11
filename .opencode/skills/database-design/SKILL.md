---
name: database-design
description: Use when modeling or changing relational data in PostgreSQL. Use for relational modeling, keys, relationships, constraints, indexes, transactions, migrations, integrity, and query performance.
---

# Database Design

## When to use

Use when designing a schema, adding a table or column, writing a migration, or when a query or write path is slow or returns wrong data. Applies to relational modeling in PostgreSQL.

## Process

1. **Understand the data and access patterns first**: What entities exist, how they relate, how data is read and written, and at what volume. The schema should serve the query patterns you actually need.
2. **Model relationships intentionally**: Determine cardinality (1:1, 1:N, M:N) and how each relationship is represented (FK column, join table). Model the domain, then adapt to reality — avoid over-normalizing or denormalizing without reason.
3. **Design keys**:
   - Prefer an `id bigint GENERATED ALWAYS AS IDENTITY` or `uuid` primary key on every table.
   - Use natural keys only when they are truly stable and unique.
   - Add foreign keys with explicit `ON DELETE` behavior aligned to your data lifecycle.
4. **Apply constraints as data integrity guarantees**: `NOT NULL`, `UNIQUE`, `CHECK`, `FOREIGN KEY`, `DEFAULT`. Enforce invariants in the database, not just in application code.
5. **Index with intent**: Index columns used in `WHERE`, joins, `ORDER BY`, and uniqueness. Consider composite indexes that match query filters. Avoid indexing low-selectivity columns; drop indexes that are never used.
6. **Write migrations as versioned, reversible steps**: One migration per committed change, forward and rollback paths, and migration ordering that reflects dependencies. Never edit an applied migration; add a new one.
7. **Use transactions correctly**: Wrap multi-statement operations that must be atomic in a single transaction with appropriate isolation level. Keep transactions short; avoid holding them across network or user interaction.
8. **Validate query performance**: Run `EXPLAIN ANALYZE` on important queries in the workload. Check for sequential scans on large tables, missing/never-used indexes, and N+1 access from ORMs.

## Important checks

- Is the schema normalized to avoid update anomalies without losing needed performance?
- Are constraints preventing invalid data at the database level?
- Are all FKs indexed where they are frequently joined?
- Are migrations replayable, reversible, and safe for running databases?
- Are transactions atomic, short, and using the right isolation level?
- Do hot queries use indexes?

## Common mistakes

- Storing values that should be relationships (comma-separated lists, JSON as a universal container).
- Missing constraints and relying on application code for integrity.
- Indexing everything (write amplification) or nothing (slow reads).
- Mutating applied migrations instead of adding new ones.
- Long-running transactions that increase lock contention and bloat.
- Renaming or type-changing a column without a data migration.

## Completion

The schema correctly models the entities and their relationships, integrity is enforced by constraints, key queries are indexed and verified, transactions are correct and short, and migrations are versioned, reversible, and documented. Data integrity and query performance are both accounted for.