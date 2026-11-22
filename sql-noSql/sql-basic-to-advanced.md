# SQL: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [SQL and NoSQL questions](questions.md): joins, `WHERE` vs `HAVING`, nth salary, duplicates, indexes, ACID, normalization, views, sharding vs partitioning, `RANK` vs `DENSE_RANK`
- [Tech lead mock interview](../java/techlead-mock-interview.md): DB migrations, storing sensitive data

## Basic

1. `UNION` vs `UNION ALL`?
   - `UNION` removes duplicates, which costs a sort or hash. Use `UNION ALL` when rows are already distinct.
2. `COUNT(*)` vs `COUNT(column)` vs `COUNT(DISTINCT column)`?
   - `COUNT(column)` skips `NULL` values.
3. How does `NULL` behave in comparisons and `NOT IN`?
   - `NULL = NULL` is unknown, so use `IS NULL`. `NOT IN` with a `NULL` in the list returns no rows; use `NOT EXISTS`.

## Intermediate

1. Find the top 3 salaries in each department.

   ```sql
   SELECT * FROM (
     SELECT e.*, DENSE_RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rnk
     FROM employees e
   ) t
   WHERE rnk <= 3;
   ```

2. Use `LAG` / `LEAD` and a running total with `SUM() OVER (ORDER BY ...)`.
3. Recursive CTE: list every employee under a given manager.
4. When is an index not used?
   - A function on the column, a leading wildcard `LIKE '%x'`, a type cast, low selectivity, or the planner thinks a scan is cheaper.
5. Composite index column order: why does it matter?
   - The index is sorted by the first column, so `(a, b)` helps `WHERE a = ?` and `WHERE a = ? AND b = ?`, not `WHERE b = ?` alone.
6. Covering, partial and expression indexes?
7. How do you read an execution plan?
   - `EXPLAIN (ANALYZE, BUFFERS)`: look at scan types, estimated vs actual rows, join type, and sorts spilling to disk.
8. Isolation levels and the anomalies each prevents?
   - Read uncommitted (dirty reads), read committed (non-repeatable reads), repeatable read (phantoms in the SQL standard), serializable.
9. Offset vs keyset (cursor) pagination?
   - `OFFSET 100000` reads and throws away 100,000 rows. Keyset uses `WHERE (created_at, id) < (?, ?)` with an index.
10. Views vs materialized views?

## Advanced

1. How does MVCC work in PostgreSQL?
   - Each update writes a new row version. Readers see a snapshot and don't block writers. `VACUUM` removes dead versions.
2. How do deadlocks happen in a database and how do you avoid them?
   - Two transactions lock rows in opposite order. Lock in a fixed order, keep transactions short, and retry on deadlock errors.
3. `SELECT ... FOR UPDATE` vs `FOR UPDATE SKIP LOCKED`?
   - `SKIP LOCKED` lets many workers pull jobs from a table without waiting on each other.
4. How do you prevent overselling the last item in stock?
   - A conditional update `UPDATE stock SET qty = qty - 1 WHERE id = ? AND qty > 0`, a row lock, or a unique constraint.
5. Read replicas: what is replication lag and how does it affect users?
   - A user may not see their own write. Read your own writes from the primary for a short time.
6. How do you choose a shard key?
   - High cardinality, even load, and present in most queries, so a query hits one shard.
7. How do you run a zero-downtime schema change on a big table?
   - Expand and contract: add a nullable column, dual-write, backfill in batches, switch reads, then drop the old column.
   - Create indexes with `CREATE INDEX CONCURRENTLY`.
8. Why is a bigger connection pool often slower?
   - The DB has a few cores; hundreds of active connections fight for CPU, locks and memory.
9. How do you store money and time correctly?
   - `NUMERIC` (or integer minor units) for money, `timestamptz` in UTC for time.
10. When do you denormalize?
11. How do you audit changes to rows? (triggers, change data capture with Debezium, an append-only history table)

## Scenario

1. A query that took 50 ms now takes 10 s after the table grew. Walk through your investigation.
2. Design the tables for orders, order items, payments and refunds. Which indexes do you add?
3. A report query slows down the production database every morning. What are your options?
4. Two users book the same seat at the same moment. Show how the database stops a double booking.
