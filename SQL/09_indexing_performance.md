# SQL Indexing & Performance Cheat Sheet

Speed up query performance using indexing and smart practices.

---

## 🔹 CREATE INDEX

**Description**: Adds an index to a column for faster searches.

**When to Use**: On columns used in WHERE, JOIN, or ORDER BY.

```sql
CREATE INDEX idx_customer_name ON customers (last_name);
```

---

## 🔸 UNIQUE INDEX

**Description**: Enforces uniqueness constraint on column values.

**When to Use**: Preventing duplicates in key fields.

```sql
CREATE UNIQUE INDEX idx_email ON users(email);
```

---

## 🔹 EXPLAIN

**Description**: Shows query execution plan.

**When to Use**: Analyze performance bottlenecks.

```sql
EXPLAIN SELECT * FROM orders WHERE customer_id = 123;
```

---

## 🔸 COVERING INDEX

**Description**: Index that includes all columns needed by the query.

**When to Use**: For highly optimized read operations.

---

## 🧠 Use Cases
- Speeding up lookups
- Preventing table scans
- Optimizing JOIN conditions

---

📚 Learn more at [Use the Index, Luke](https://use-the-index-luke.com/)
