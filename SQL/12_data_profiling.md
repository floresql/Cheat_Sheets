# SQL for Data Profiling & Auditing Cheat Sheet

Use SQL to assess data quality, completeness, and patterns—especially before analysis or modeling.

---

## 🔹 Record Counts

**Description**: Check total number of rows.

```sql
SELECT COUNT(*) FROM your_table;
```

**When to Use**: To verify load or data presence.

---

## 🔸 NULL & Missing Values

**Description**: Count missing values by column.

```sql
SELECT
  COUNT(*) AS total_rows,
  SUM(CASE WHEN column_name IS NULL THEN 1 ELSE 0 END) AS null_count
FROM your_table;
```

**When to Use**: Identifying incomplete data.

---

## 🔹 Distinct Values

**Description**: Check uniqueness and spot potential enums.

```sql
SELECT column_name, COUNT(DISTINCT column_name) FROM your_table;
```

**When to Use**: Find cardinality or potential dimensions.

---

## 🔸 Outlier Detection (Simple)

**Description**: Find numeric outliers using z-score logic.

```sql
SELECT *
FROM your_table
WHERE column_name > (SELECT AVG(column_name) + 3 * STDEV(column_name) FROM your_table);
```

**When to Use**: To detect suspicious values.

---

## 🔹 Pattern & Format Checks

**Description**: Identify bad formats using LIKE or regex.

```sql
SELECT *
FROM customers
WHERE email NOT LIKE '%@%.%';
```

**When to Use**: Data validation and quality control.

---

## 🔸 Duplicate Checks

**Description**: Detect duplicate rows or keys.

```sql
SELECT customer_id, COUNT(*)
FROM orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

**When to Use**: Ensure data integrity.

---

## 🔹 Referential Integrity

**Description**: Find orphan records in foreign key relationships.

```sql
SELECT o.*
FROM orders o
LEFT JOIN customers c ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

**When to Use**: Validate join logic or missing foreign keys.

---

## 🧠 Use Cases
- QA for data ingestion
- Health checks before reporting
- Debugging dirty datasets

---

📚 Learn more at [DataCamp - Data Profiling](https://www.datacamp.com/)
