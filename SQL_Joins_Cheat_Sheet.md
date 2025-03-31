# SQL Joins & Set Operators Cheat Sheet

## 🔑 Key Concepts
- **Primary Key**: Uniquely identifies each record in a table.
- **Foreign Key**: References the primary key in another table.
- **Relationships**:
  - One-to-One
  - One-to-Many
  - Many-to-Many

---

## 🤝 SQL Joins

### 🔹 INNER JOIN
Returns records with matching keys in both tables.
```sql
SELECT * 
FROM artist AS art
INNER JOIN album AS alb 
ON art.artist_id = alb.artist_id;
```

### 🔹 LEFT JOIN
Keeps all records from the left table, fills NULLs where no match in right.
```sql
SELECT * 
FROM artist AS art
LEFT JOIN album AS alb 
ON art.artist_id = alb.artist_id;
```

### 🔹 RIGHT JOIN
Keeps all records from the right table, fills NULLs where no match in left.
```sql
SELECT * 
FROM artist AS art
RIGHT JOIN album AS alb 
ON art.artist_id = alb.artist_id;
```

### 🔹 FULL JOIN
Returns all records when there's a match in one of the tables.
```sql
SELECT * 
FROM artist AS art
FULL OUTER JOIN album AS alb 
ON art.artist_id = alb.artist_id;
```

### 🔹 CROSS JOIN
Creates all combinations of rows from both tables.
```sql
SELECT art.name, alb.title
FROM artist AS art
CROSS JOIN album AS alb;
```

### 🔹 SELF JOIN
Joins a table to itself.
```sql
SELECT 
  alb1.artist_id, 
  alb1.title AS alb1_title, 
  alb2.title AS alb2_title
FROM album AS alb1
INNER JOIN album AS alb2 
ON alb1.artist_id = alb2.artist_id 
WHERE alb1.album_id <> alb2.album_id;
```

---

## 🔍 Semi & Anti Joins

### 🔹 SEMI JOIN
Returns rows from the left where a match exists in the right.
```sql
SELECT * 
FROM album 
WHERE artist_id IN (SELECT artist_id FROM artist);
```

### 🔹 ANTI JOIN
Returns rows from the left where no match exists in the right.
```sql
SELECT * 
FROM album 
WHERE artist_id NOT IN (SELECT artist_id FROM artist);
```

---

## 🧮 Set Operators

### 🔹 UNION
Combines results and removes duplicates.
```sql
SELECT artist_id FROM artist
UNION
SELECT artist_id FROM album;
```

### 🔹 UNION ALL
Combines results and includes duplicates.
```sql
SELECT artist_id FROM artist
UNION ALL
SELECT artist_id FROM album;
```

### 🔹 INTERSECT
Returns common rows between two queries.
```sql
SELECT artist_id FROM artist
INTERSECT
SELECT artist_id FROM album;
```

### 🔹 EXCEPT
Returns rows from the first query not in the second.
```sql
SELECT artist_id FROM artist
EXCEPT
SELECT artist_id FROM album;
```

---

## 📌 Tips
- Always match column count and types for set operations.
- Use `USING(column)` for shorthand joins when column names match.
- `JOIN ON` is more flexible when column names differ.

---

📚 Learn more at [DataCamp](https://www.datacamp.com)
