# SQL Aggregation Cheat Sheet

Aggregation functions summarize multiple rows of data into single values.

---

## 🔹 COUNT()

**Description**: Returns the number of rows.

**When to Use**: To count rows or non-null values.

**Example**:
```sql
SELECT COUNT(*) FROM orders;
```

---

## 🔸 SUM()

**Description**: Adds up the values in a column.

**When to Use**: Totaling numeric values like revenue, quantity, etc.

**Example**:
```sql
SELECT SUM(amount) FROM payments;
```

---

## 🔹 AVG()

**Description**: Returns the average of numeric values.

**When to Use**: To compute mean values.

**Example**:
```sql
SELECT AVG(score) FROM test_results;
```

---

## 🔸 MIN() / MAX()

**Description**: Finds the smallest or largest value.

**When to Use**: To retrieve range extremes or date bounds.

**Example**:
```sql
SELECT MIN(hire_date), MAX(hire_date) FROM employees;
```

---

## 🔺 GROUP BY

**Description**: Groups rows that share a value for aggregation.

**When to Use**: Summarizing data by category (e.g., total per region).

**Example**:
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

---

## 🔻 HAVING

**Description**: Filters grouped results (like WHERE but for aggregates).

**When to Use**: To exclude groups based on conditions.

**Example**:
```sql
SELECT department, SUM(salary) FROM employees GROUP BY department HAVING SUM(salary) > 1000000;
```

---

## 🧠 Use Cases
- Executive summaries
- KPI dashboards
- Frequency analysis

---

📚 Learn more at [Mode Group By](https://mode.com/sql-tutorial/sql-group-by/)
