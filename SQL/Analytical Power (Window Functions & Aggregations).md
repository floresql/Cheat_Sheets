# SQL Cheat Sheet: Window Functions & Analytics

### 1. The `OVER` Clause
Defines the window (set of rows) the function operates on.
*   **PARTITION BY:** Divides the result set into partitions.
*   **ORDER BY:** Sorts rows within each partition.

```sql
SELECT 
    employee_id, 
    department, 
    salary,
    -- Calculate average salary per department for every row
    AVG(salary) OVER(PARTITION BY department) as dept_avg,
    -- Running total of salary within the department
    SUM(salary) OVER(PARTITION BY department ORDER BY hire_date) as running_total
FROM employees;
```

### 2. Ranking Functions
*   **ROW_NUMBER():** Unique ID for each row (1, 2, 3, 4).
*   **RANK():** Leaves gaps for ties (1, 2, 2, 4).
*   **DENSE_RANK():** No gaps for ties (1, 2, 2, 3).
*   **NTILE(n):** Divides rows into `n` buckets (e.g., quartiles).

### 3. Positional Functions (Lead/Lag)
Compare the current row with a previous or subsequent row.
```sql
SELECT 
    order_date, 
    revenue,
    -- Get revenue from the previous day
    LAG(revenue, 1) OVER(ORDER BY order_date) as prev_day_revenue,
    -- Calculate growth
    revenue - LAG(revenue, 1) OVER(ORDER BY order_date) as daily_growth
FROM sales;
```

### 4. Advanced Aggregations (Rollup/Cube)
Create subtotal rows automatically.
```sql
SELECT region, city, SUM(sales)
FROM sales_data
GROUP BY ROLLUP(region, city); -- Generates city totals, region totals, and grand total
```
