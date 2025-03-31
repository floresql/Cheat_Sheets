# SQL Performance Tuning for Analysts Cheat Sheet

Learn quick wins to write faster, more efficient queries without being a DBA.

---

## 🔹 Use SELECT Columns (Avoid SELECT *)

**Why**: SELECT * fetches unnecessary data and slows performance.

```sql
-- Bad
SELECT * FROM orders;

-- Better
SELECT order_id, order_date FROM orders;
```

---

## 🔸 Index Awareness

**Why**: Queries run faster on indexed columns.

```sql
-- Use WHERE, JOIN, or ORDER BY on indexed fields
SELECT * FROM customers WHERE email = 'test@example.com';
```

---

## 🔹 Use WHERE to Filter Early

**Why**: Reduce the dataset before aggregation or joining.

```sql
SELECT AVG(sales)
FROM transactions
WHERE region = 'West';
```

---

## 🔸 Avoid Functions on Indexed Columns in WHERE

**Why**: Breaks index usage.

```sql
-- Bad
WHERE YEAR(order_date) = 2023

-- Better
WHERE order_date >= '2023-01-01' AND order_date < '2024-01-01'
```

---

## 🔹 Use EXISTS or JOIN over IN

**Why**: IN can be slow for subqueries.

```sql
-- Better
SELECT * FROM orders o
WHERE EXISTS (
  SELECT 1 FROM customers c WHERE o.customer_id = c.customer_id
);
```

---

## 🔸 EXPLAIN Plans

**Why**: Reveals how the query is executed (table scans, index usage, etc.)

```sql
-- SQL Server
SET SHOWPLAN_ALL ON;
GO
-- Then run your query
```

---

## 🔹 Limit Rows When Testing

**Why**: Prevent unnecessary load while debugging.

```sql
SELECT TOP 100 * FROM transactions;
```

---

## 🧠 Use Cases
- Dashboards with large datasets
- ETL pipeline bottlenecks
- Ad-hoc report optimization

---

📚 Learn more at [Use the Index, Luke](https://use-the-index-luke.com/)
