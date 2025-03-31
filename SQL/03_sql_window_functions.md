# SQL Window Functions Cheat Sheet

## 🧠 What Are Window Functions?
Window functions perform calculations across a set of table rows that are somehow related to the current row—without collapsing them into groups (unlike GROUP BY).

---

## 🧰 Common SQL Window Functions

### 🔹 `ROW_NUMBER()`
Assigns a unique number to each row based on the order.
```sql
SELECT *, 
  ROW_NUMBER() OVER (ORDER BY sales DESC) AS row_num
FROM sales_data;
```

### 🔹 `RANK()`
Gives the same rank to identical values but skips subsequent numbers.
```sql
SELECT *, 
  RANK() OVER (ORDER BY score DESC) AS rank_pos
FROM exam_results;
```

### 🔹 `DENSE_RANK()`
Similar to `RANK()` but does not skip numbers.
```sql
SELECT *, 
  DENSE_RANK() OVER (ORDER BY score DESC) AS dense_rank
FROM exam_results;
```

### 🔹 `NTILE(n)`
Divides ordered rows into `n` approximately equal groups.
```sql
SELECT *, 
  NTILE(4) OVER (ORDER BY score DESC) AS quartile
FROM exam_results;
```

---

## 📊 Aggregate Window Functions

### 🔹 `SUM()`, `AVG()`, `MIN()`, `MAX()`
Calculates aggregates over a window of rows.
```sql
SELECT *,
  SUM(sales) OVER (PARTITION BY region ORDER BY month) AS running_total
FROM sales_data;
```

```sql
SELECT *,
  AVG(score) OVER (PARTITION BY subject) AS avg_score
FROM exam_results;
```

---

## ⏪ Lag/Lead Functions

### 🔹 `LAG()`
Accesses previous row's value.
```sql
SELECT *,
  LAG(sales, 1) OVER (PARTITION BY region ORDER BY month) AS prev_month_sales
FROM sales_data;
```

### 🔹 `LEAD()`
Accesses next row's value.
```sql
SELECT *,
  LEAD(sales, 1) OVER (PARTITION BY region ORDER BY month) AS next_month_sales
FROM sales_data;
```

---

## 🧱 FIRST_VALUE() / LAST_VALUE()

### 🔹 `FIRST_VALUE()`
Gets the first value in the window frame.
```sql
SELECT *,
  FIRST_VALUE(sales) OVER (PARTITION BY region ORDER BY month) AS first_month_sales
FROM sales_data;
```

### 🔹 `LAST_VALUE()`
Gets the last value in the window frame (can be tricky—frame settings matter).
```sql
SELECT *,
  LAST_VALUE(sales) OVER (
    PARTITION BY region ORDER BY month 
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  ) AS last_month_sales
FROM sales_data;
```

---

## 🪟 Anatomy of a Window Function
```sql
function_name(expression) 
OVER (
  [PARTITION BY partition_expression]
  [ORDER BY order_expression]
  [ROWS frame_specification]
)
```

---

## 📝 Frame Clauses
- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Cumulative calculations
- `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`: Rolling calculations

---

## 💡 Use Cases
- Running totals
- Ranking within groups
- Comparing current vs previous or next row
- Calculating percent change
- Filtering top-N per group using `ROW_NUMBER()`

---

📚 Learn more at [Mode SQL Tutorial](https://mode.com/sql-tutorial/sql-window-functions/)
