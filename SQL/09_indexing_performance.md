# SQL Indexing & Performance Cheat Sheet

## ⚡ Why Index?
Indexes improve the speed of data retrieval but may slow down INSERT/UPDATE operations.

---

## 🔍 Creating Indexes
```sql
CREATE INDEX idx_customer_name ON customers (last_name);
```

---

## 🔎 Unique Index
```sql
CREATE UNIQUE INDEX idx_email_unique ON users (email);
```

---

## 🧪 Analyze with EXPLAIN
```sql
EXPLAIN SELECT * FROM orders WHERE customer_id = 123;
```

## 💡 Covering Index
An index that includes all columns needed by a query.

---

## ⚠️ Best Practices
- Don't over-index
- Index columns used in WHERE, JOIN, ORDER BY
- Use composite indexes wisely

📚 Learn more at [Use The Index, Luke](https://use-the-index-luke.com/)
