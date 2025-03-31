# SQL Basics Cheat Sheet

## 🧠 SELECT Statement Structure
```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1 [ASC|DESC]
LIMIT n OFFSET m;
```

---

## 🔍 SELECT & FROM
- Pull specific columns or use `*` to select all.
```sql
SELECT * FROM employees;
SELECT first_name, last_name FROM customers;
```

---

## 🎯 WHERE Clause
- Filter rows based on condition(s).
```sql
SELECT * FROM orders WHERE amount > 100;
```

### Operators:
- `=`, `!=`, `<`, `<=`, `>=`, `<>`
- `BETWEEN`, `IN`, `LIKE`, `IS NULL`, `IS NOT NULL`
```sql
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

---

## 🔄 ORDER BY
- Sort results by one or more columns.
```sql
SELECT * FROM sales ORDER BY sale_date DESC, region ASC;
```

---

## 🎯 LIMIT / OFFSET
- Control how many rows you return and where to start.
```sql
SELECT * FROM products LIMIT 10 OFFSET 20;
```

---

## 🔄 Aliases
- Rename columns or tables for readability.
```sql
SELECT first_name AS fname, last_name AS lname FROM customers;
```

---

## 🔢 Arithmetic & Expressions
```sql
SELECT price * quantity AS total_price FROM order_items;
SELECT salary + bonus AS total_compensation FROM employees;
```

---

## 🧹 DISTINCT
- Remove duplicate rows.
```sql
SELECT DISTINCT country FROM customers;
```

---

## 🧰 Built-in Functions

### Numeric:
- `ROUND()`, `CEIL()`, `FLOOR()`, `ABS()`

### String:
- `UPPER()`, `LOWER()`, `LENGTH()`, `SUBSTRING()`, `TRIM()`, `CONCAT()`

### Date/Time:
- `CURRENT_DATE`, `NOW()`, `DATE_TRUNC()`, `EXTRACT()`

---

## 🧪 CASE Statement
- Conditional logic in SELECT
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

## 🧠 Comments
```sql
-- This is a single-line comment

/*
  This is a 
  multi-line comment
*/
```

---

📚 Learn more at [SQLBolt](https://sqlbolt.com) or [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
