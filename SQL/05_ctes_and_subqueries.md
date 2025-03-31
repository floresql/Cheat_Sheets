# SQL CTEs & Subqueries Cheat Sheet
## 📌 Description
Explains subqueries and Common Table Expressions (CTEs), including recursion.

## 🚀 When to Use
Use to break complex queries into logical parts or handle hierarchical data.



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