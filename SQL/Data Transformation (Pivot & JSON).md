# SQL Cheat Sheet: PIVOT & Semi-Structured Data

### 1. PIVOT (Rows to Columns)
Transforming category rows into individual columns.
```sql
SELECT * FROM (
    SELECT year, category, sales FROM sales_data
) 
PIVOT (
    SUM(sales) FOR category IN ('Electronics', 'Clothing', 'Home')
);
```

### 2. JSON Manipulation
Querying nested JSON objects stored in the DB.
```sql
-- PostgreSQL syntax
SELECT 
    user_data->>'name' as user_name,
    user_data->'address'->>'zipcode' as zip
FROM users_json;

-- Extracting from JSON array
SELECT jsonb_array_elements(tags) FROM products;
```

### 3. Self-Joins
Joining a table to itself to compare rows within the same set.
```sql
-- Find pairs of employees in the same city
SELECT a.name, b.name, a.city
FROM employees a
JOIN employees b ON a.city = b.city AND a.id <> b.id;
```
