# SQL CTEs & Subqueries Cheat Sheet

## 🧠 Subqueries

### Scalar Subquery
Returns a single value.
```sql
SELECT name
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### Correlated Subquery
Depends on outer query.
```sql
SELECT name
FROM employees e
WHERE salary > (
  SELECT AVG(salary) 
  FROM employees 
  WHERE department_id = e.department_id
);
```

---

## 🔄 Common Table Expressions (CTEs)

### Simple CTE
```sql
WITH high_salary AS (
  SELECT * FROM employees WHERE salary > 100000
)
SELECT name FROM high_salary;
```

### Recursive CTE
```sql
WITH RECURSIVE nums AS (
  SELECT 1 AS n
  UNION ALL
  SELECT n + 1 FROM nums WHERE n < 10
)
SELECT * FROM nums;
```

---

## 🧩 Use Cases
- Breaking down complex queries
- Improving readability
- Recursive hierarchies

📚 Learn more at [DataCamp](https://www.datacamp.com/tutorial/sql-cte-recursive)
