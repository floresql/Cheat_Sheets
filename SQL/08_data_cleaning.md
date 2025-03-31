# SQL Data Cleaning Cheat Sheet

## 🔍 Handling NULLs
```sql
SELECT * FROM customers WHERE phone IS NULL;
SELECT COALESCE(phone, 'N/A') FROM customers;
```

## 🔄 Type Conversion
```sql
SELECT CAST(order_total AS INT), 
       TRY_CAST(order_total AS FLOAT)
FROM orders;
```

## 🔁 Removing Duplicates
```sql
SELECT DISTINCT name FROM customers;
```

## 🧹 Replacing Values
```sql
SELECT REPLACE(name, 'Inc.', '') FROM companies;
```

## ✅ Validating Patterns
```sql
SELECT * FROM users WHERE email NOT LIKE '%@%.%';
```

📚 Learn more at [DataCamp Data Cleaning in SQL](https://www.datacamp.com/courses/data-cleaning-in-sql)
