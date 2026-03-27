# SQL Cheat Sheet: CTEs & Hierarchies

### 1. Common Table Expressions (CTEs)
Temporary result sets that exist only during the execution of the query.
```sql
WITH regional_sales AS (
    SELECT region_id, SUM(amount) as total
    FROM orders
    GROUP BY region_id
),
top_regions AS (
    SELECT region_id FROM regional_sales WHERE total > 100000
)
SELECT * FROM top_regions;
```

### 2. Recursive CTEs
Used to query hierarchical data like org charts or bill-of-materials.
```sql
WITH RECURSIVE org_chart AS (
    -- Anchor member: Start with the CEO
    SELECT id, name, manager_id, 1 as level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive member: Join the table back to the CTE
    SELECT e.id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    INNER JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT * FROM org_chart;
```
