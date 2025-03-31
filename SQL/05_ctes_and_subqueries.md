# SQL CTEs & Subqueries Cheat Sheet

## 📌 Description
Use CTEs and subqueries to break down complex logic and reuse query structures.

## 🔄 Common Table Expressions (CTEs)
### Simple CTE
Good for breaking logic into steps, similar to a SQL variable.

### Recursive CTE
Used for hierarchical or tree-structured data, such as organizational charts or parent-child tables.

```sql
WITH RECURSIVE nums AS (
  SELECT 1 AS n
  UNION ALL
  SELECT n + 1 FROM nums WHERE n < 10
)
SELECT * FROM nums;
```

📚 Learn more at [DataCamp](https://www.datacamp.com/tutorial/sql-cte-recursive)
---

## 📌 More Examples
### Nested Subquery Example
```sql
SELECT name FROM employees WHERE department_id = (
  SELECT department_id FROM departments WHERE name = 'Sales'
);
```

### Recursive CTE for factorial:
```sql
WITH RECURSIVE factorial(n, fact) AS (
  SELECT 1, 1
  UNION ALL
  SELECT n + 1, (n + 1) * fact FROM factorial WHERE n < 5
)
SELECT * FROM factorial;
```
