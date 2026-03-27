# SQL Cheat Sheet: Performance Tuning

### 1. Indexing Strategies
*   **Clustered Index:** Defines the physical order of data (one per table).
*   **Non-Clustered Index:** A "lookup table" pointing to the data.
*   **Covering Index:** An index that includes all columns needed for a query.

```sql
-- Create a composite index for a common filter
CREATE INDEX idx_user_status ON users (last_login, status);
```

### 2. Execution Plans (EXPLAIN)
Use `EXPLAIN` or `EXPLAIN ANALYZE` to see if the engine is doing a "Table Scan" (slow) or an "Index Seek" (fast).
```sql
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 500;
```

### 3. SARGable Queries (Search ARGumentable)
Avoid functions on columns in the `WHERE` clause; they break indexes.
*   **SLOW:** `WHERE YEAR(order_date) = 2023`
*   **FAST:** `WHERE order_date >= '2023-01-01' AND order_date < '2024-01-01'`

### 4. Common Tuning Tips
*   **Avoid SELECT *:** Pulling extra columns increases I/O.
*   **Exists vs In:** Use `EXISTS` for subqueries to stop the search as soon as a match is found.
*   **Join Order:** Join smaller tables to larger tables to reduce the size of intermediate results.
