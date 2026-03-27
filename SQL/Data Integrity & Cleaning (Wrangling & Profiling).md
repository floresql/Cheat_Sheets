# SQL Cheat Sheet: Data Cleaning & Profiling

### 1. Data Profiling Queries
Check the health of your dataset.
```sql
-- Check for NULL percentages
SELECT 
    COUNT(*) as total_rows,
    COUNT(column_name) as non_null_count,
    (COUNT(*) - COUNT(column_name)) * 100.0 / COUNT(*) as percent_missing
FROM table_name;

-- Check for distribution/outliers
SELECT column_name, COUNT(*) 
FROM table_name 
GROUP BY 1 ORDER BY 2 DESC;
```

### 2. Cleaning & Standardizing
*   **COALESCE:** Returns the first non-null value.
*   **NULLIF:** Returns NULL if two expressions are equal (prevents divide-by-zero).
```sql
-- Divide by zero protection
SELECT revenue / NULLIF(units_sold, 0) FROM sales;

-- Standardizing strings
SELECT 
    TRIM(LOWER(email)) as clean_email,
    REPLACE(phone, '-', '') as numeric_phone
FROM users;
```

### 3. Handling Case Logic
```sql
SELECT 
    order_id,
    CASE 
        WHEN status = 'D' THEN 'Delivered'
        WHEN status = 'P' THEN 'Pending'
        ELSE 'Unknown' 
    END as status_label
FROM orders;
```
