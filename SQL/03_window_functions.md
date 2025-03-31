# SQL Window Functions Cheat Sheet

Window functions allow calculations across rows related to the current row, without collapsing the result set.

---

## 🟢 ROW_NUMBER()

**Description**: Assigns a unique, sequential number to rows within a partition.

**When to Use**: Useful for ranking or selecting one row per group.

**Example**:
```sql
SELECT *, ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```

---

## 🔵 RANK()

**Description**: Assigns rank to rows with gaps in ranking for ties.

**When to Use**: When tied ranks should result in skipped positions.

**Example**:
```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

---

## 🟣 DENSE_RANK()

**Description**: Like RANK() but without gaps for tied values.

**When to Use**: When ties should not cause gaps in rank order.

**Example**:
```sql
SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

---

## 🟤 NTILE(n)

**Description**: Distributes rows into `n` buckets as evenly as possible.

**When to Use**: When you want to split data into quantiles.

**Example**:
```sql
SELECT name, NTILE(4) OVER (ORDER BY score) AS quartile
FROM test_results;
```

---

## 🟠 LAG() and LEAD()

**Description**: Accesses values from previous or next rows in the same result set.

**When to Use**: Comparing a row’s value with its neighbors (e.g., change over time).

**Examples**:
```sql
SELECT month, sales, LAG(sales) OVER (ORDER BY month) AS previous_month_sales
FROM sales_data;

SELECT month, sales, LEAD(sales) OVER (ORDER BY month) AS next_month_sales
FROM sales_data;
```

---

## 🔺 FIRST_VALUE() and LAST_VALUE()

**Description**: Returns the first or last value in the window frame.

**When to Use**: To retrieve boundary values for a group.

**Example**:
```sql
SELECT employee, department, 
  FIRST_VALUE(hire_date) OVER (PARTITION BY department ORDER BY hire_date) AS first_hired
FROM employees;
```

---

## 🧠 Use Cases
- Running totals
- Ranking competitors or customers
- Time-based comparisons (YoY, MoM)
- Finding earliest/latest records

---

📚 Learn more at [Mode SQL Window Functions](https://mode.com/sql-tutorial/sql-window-functions/)
