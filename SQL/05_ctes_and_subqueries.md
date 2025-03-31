# SQL CTEs & Subqueries Cheat Sheet

## 📌 Description
Covers subqueries and Common Table Expressions (CTEs), including recursive CTEs.

## 🚀 When to Use
Use for breaking down complex logic or working with hierarchical data.


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