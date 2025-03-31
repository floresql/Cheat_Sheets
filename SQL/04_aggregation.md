# SQL Aggregation Cheat Sheet

## 🧮 Basic Aggregate Functions
- `COUNT()` - Number of rows
- `SUM()` - Total value
- `AVG()` - Average value
- `MIN()` - Minimum
- `MAX()` - Maximum

```sql
SELECT 
  COUNT(*) AS total_orders,
  SUM(amount) AS total_sales,
  AVG(amount) AS avg_sale
FROM orders;
```

---

## 🔀 GROUP BY
Groups rows that have the same values in specified columns into summary rows.
```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id;
```

---

## 🧾 HAVING Clause
Filters grouped data (like WHERE, but for groups).
```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 1000;
```

---

## 🔁 GROUPING SETS / ROLLUP / CUBE
Advanced aggregations (SQL Server, Postgres, Oracle)
```sql
-- GROUP BY with ROLLUP
SELECT region, product, SUM(sales)
FROM sales_data
GROUP BY ROLLUP (region, product);

-- GROUPING SETS
SELECT region, product, SUM(sales)
FROM sales_data
GROUP BY GROUPING SETS ((region), (product));
```

---

📚 Learn more at [Mode Analytics](https://mode.com/sql-tutorial/sql-group-by/)
