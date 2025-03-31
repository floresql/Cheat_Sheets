# SQL Joins Cheat Sheet

A practical guide to understanding and using SQL JOIN operations to combine data across tables.

---

## 🔹 INNER JOIN

**Description**: Returns only rows with matching values in both tables.

**When to Use**: To retrieve records that have corresponding matches in both tables.

**Example**:
```sql
SELECT a.name, b.title
FROM artist a
INNER JOIN album b ON a.artist_id = b.artist_id;
```

---

## 🔸 LEFT JOIN

**Description**: Returns all rows from the left table and matched rows from the right table. Unmatched rows return NULLs.

**When to Use**: When you want all rows from one table regardless of matches in the other.

**Example**:
```sql
SELECT a.name, b.title
FROM artist a
LEFT JOIN album b ON a.artist_id = b.artist_id;
```

---

## 🔹 RIGHT JOIN

**Description**: Returns all rows from the right table and matched rows from the left table. Unmatched rows return NULLs.

**When to Use**: When you want all rows from the right table regardless of matches in the left.

**Example**:
```sql
SELECT a.name, b.title
FROM artist a
RIGHT JOIN album b ON a.artist_id = b.artist_id;
```

---

## 🔸 FULL OUTER JOIN

**Description**: Returns all rows when there is a match in one of the tables. NULLs are returned for non-matching rows from either side.

**When to Use**: When you want a complete set of data from both tables, regardless of matches.

**Example**:
```sql
SELECT a.name, b.title
FROM artist a
FULL OUTER JOIN album b ON a.artist_id = b.artist_id;
```

---

## 🔹 CROSS JOIN

**Description**: Returns the Cartesian product of the two tables.

**When to Use**: When every row in the first table should join with every row in the second.

**Example**:
```sql
SELECT a.name, b.title
FROM artist a
CROSS JOIN album b;
```

---

## 🔸 SELF JOIN

**Description**: Joins a table to itself using table aliases.

**When to Use**: Comparing rows within the same table.

**Example**:
```sql
SELECT a1.artist_id, a1.name, a2.name AS collaborator
FROM artist a1
JOIN artist a2 ON a1.label_id = a2.label_id
WHERE a1.artist_id <> a2.artist_id;
```

---

## 🔹 SEMI JOIN

**Description**: Returns rows from the left table that have a match in the right table (similar to WHERE EXISTS).

**When to Use**: Filtering rows based on existence in another table.

**Example**:
```sql
SELECT * 
FROM album 
WHERE artist_id IN (SELECT artist_id FROM artist);
```

---

## 🔸 ANTI JOIN

**Description**: Returns rows from the left table that do **not** have a match in the right table.

**When to Use**: To identify unmatched records.

**Example**:
```sql
SELECT * 
FROM album 
WHERE artist_id NOT IN (SELECT artist_id FROM artist);
```

---

## 🧠 Use Cases
- Joining transactional data with dimensions
- Combining related data across normalized tables
- Performing data quality checks (anti joins)
- Building full data exports (outer joins)

---

📚 Learn more at [Mode Analytics Join Guide](https://mode.com/sql-tutorial/sql-joins/)
