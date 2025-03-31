# SQL CTEs & Subqueries Cheat Sheet

A guide to writing modular, readable SQL with Common Table Expressions and subqueries.

---

## 🔹 Subqueries

**Description**: A query nested inside another SQL statement.

**When to Use**: When you need to compute a value or filter based on results of another query.

**Example (Scalar Subquery)**:
```sql
SELECT name 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Example (Correlated Subquery)**:
```sql
SELECT e.name 
FROM employees e 
WHERE salary > (
  SELECT AVG(salary) 
  FROM employees 
  WHERE department_id = e.department_id
);
```

---

## 🔸 Common Table Expressions (CTE)

**Description**: Temporary result set defined with `WITH`, used within a single query.

**When to Use**: Simplifying complex queries, making them easier to read and reuse.

**Example (Simple CTE)**:
```sql
WITH high_earners AS (
  SELECT * FROM employees WHERE salary > 100000
)
SELECT name FROM high_earners;
```

---

## 🔺 Recursive CTE

**Description**: A CTE that calls itself to process hierarchical or iterative data.

**When to Use**: When dealing with tree-like data structures or sequential data.

**Example**:
```sql
WITH RECURSIVE nums(n) AS (
  SELECT 1
  UNION ALL
  SELECT n + 1 FROM nums WHERE n < 5
)
SELECT * FROM nums;
```

---

## 🧠 Use Cases
- Replacing derived tables
- Hierarchical reporting
- Modularizing complex logic

---

📚 Learn more at [CTE Tutorial – Mode](https://mode.com/sql-tutorial/sql-cte/)
