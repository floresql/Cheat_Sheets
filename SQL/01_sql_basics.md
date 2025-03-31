# SQL Basics Cheat Sheet

A quick reference for the most commonly used SQL commands. This guide covers core syntax, when to use each concept, and practical examples.

---

## 🟦 SELECT

**Description**: Retrieves data from a table.

**When to Use**: Anytime you want to query data.

**Example**:
```sql
SELECT first_name, last_name FROM employees;
```

---

## 🟩 FROM

**Description**: Specifies the table to select or delete data from.

**When to Use**: Every time you run a SELECT, DELETE, or UPDATE.

**Example**:
```sql
SELECT * FROM customers;
```

---

## 🟨 WHERE

**Description**: Filters records based on specific conditions.

**When to Use**: To limit rows returned by a query.

**Example**:
```sql
SELECT * FROM orders WHERE amount > 100;
```

---

## 🟥 ORDER BY

**Description**: Sorts the result set by one or more columns.

**When to Use**: When you need results in a specific order.

**Example**:
```sql
SELECT name, salary FROM employees ORDER BY salary DESC;
```

---

## 🟪 LIMIT / OFFSET

**Description**: Restricts the number of rows returned (LIMIT) and skips rows (OFFSET).

**When to Use**: Pagination or previewing data.

**Example**:
```sql
SELECT * FROM products LIMIT 10 OFFSET 20;
```

---

## 🟫 ALIASES (AS)

**Description**: Renames columns or tables temporarily.

**When to Use**: For clarity or when using functions.

**Example**:
```sql
SELECT first_name AS fname, last_name AS lname FROM employees;
```

---

## ⚫ DISTINCT

**Description**: Removes duplicate values.

**When to Use**: When only unique values are needed.

**Example**:
```sql
SELECT DISTINCT department FROM employees;
```

---

## 🔵 COMPARISON OPERATORS

**Description**: Used in WHERE clauses to compare values.

**When to Use**: Filtering data based on logic.

**Example**:
```sql
SELECT * FROM items WHERE price >= 50 AND price <= 100;
```

---

## 🔺 LOGICAL OPERATORS (AND, OR, NOT)

**Description**: Combine multiple conditions.

**When to Use**: Complex filtering scenarios.

**Example**:
```sql
SELECT * FROM users WHERE age > 18 AND status = 'active';
```

---

## 🔻 IN / NOT IN

**Description**: Checks if a value exists in a list.

**When to Use**: Multi-value filters.

**Example**:
```sql
SELECT * FROM countries WHERE region IN ('Europe', 'Asia');
```

---

## 🟤 LIKE / ILIKE

**Description**: Performs pattern matching.

**When to Use**: Searching text data.

**Example**:
```sql
SELECT * FROM customers WHERE email LIKE '%@gmail.com';
```

---

## 🟥 NULL Handling (IS NULL / IS NOT NULL / COALESCE)

**Description**: Deals with missing values.

**When to Use**: To clean or identify incomplete data.

**Example**:
```sql
SELECT name, COALESCE(phone, 'N/A') AS phone_number FROM contacts;
```

---

## 🔷 COMMENTS

**Description**: Adds documentation to queries.

**When to Use**: Any time you need to clarify logic.

**Example**:
```sql
-- This query finds top spenders
SELECT name, total_spent FROM customers;
```

---

## 🧮 ARITHMETIC OPERATIONS

**Description**: Performs math in queries.

**When to Use**: Calculating totals, averages, etc.

**Example**:
```sql
SELECT price * quantity AS total_cost FROM order_items;
```

---

## 🎭 CASE Statement

**Description**: Adds conditional logic in queries.

**When to Use**: Categorizing data, creating flags.

**Example**:
```sql
SELECT name,
  CASE 
    WHEN score >= 90 THEN 'A'
    WHEN score >= 80 THEN 'B'
    ELSE 'C'
  END AS grade
FROM test_scores;
```

---

## 🧠 Use Cases
- Exploratory data analysis
- Business reporting
- Application backend queries

---

📚 Learn more at [SQLBolt](https://sqlbolt.com) or [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
