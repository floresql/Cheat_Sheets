# SQL String Functions Cheat Sheet

## ✂️ Basic String Functions

```sql
SELECT
  LENGTH(name),
  UPPER(name),
  LOWER(name),
  TRIM(name),
  SUBSTRING(name FROM 1 FOR 3),
  CONCAT(first_name, ' ', last_name)
FROM users;
```

---

## 🔍 Searching Strings

### LIKE and ILIKE (Postgres)
```sql
SELECT * FROM users WHERE email LIKE '%@gmail.com';
```

### CHARINDEX (SQL Server)
```sql
SELECT CHARINDEX('abc', 'abcde'); -- Returns 1
```

### POSITION (Postgres)
```sql
SELECT POSITION('needle' IN 'haystack and needle'); -- Returns 14
```

---

## 🔄 REPLACE & REGEXP
```sql
SELECT REPLACE('hello world', 'world', 'SQL'); -- hello SQL
```

### REGEXP (Postgres, BigQuery)
```sql
SELECT * FROM users WHERE name ~ '^A'; -- Names starting with A
```

📚 Learn more at [Postgres Regex Guide](https://www.postgresql.org/docs/current/functions-matching.html)
