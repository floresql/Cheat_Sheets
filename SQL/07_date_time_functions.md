# SQL Date & Time Functions Cheat Sheet

## 🗓️ Current Date & Time
```sql
SELECT CURRENT_DATE, CURRENT_TIME, NOW();
```

---

## 📆 Date Arithmetic
```sql
SELECT order_date + INTERVAL '7 days' AS delivery_date FROM orders;
```

## 🔍 Extracting Date Parts
```sql
SELECT
  EXTRACT(YEAR FROM order_date) AS order_year,
  EXTRACT(MONTH FROM order_date) AS order_month
FROM orders;
```

## ⏱️ Truncating Dates
```sql
SELECT DATE_TRUNC('month', order_date) FROM orders;
```

## 🔁 DATEDIFF & DATEADD
```sql
-- SQL Server
SELECT DATEDIFF(day, start_date, end_date) AS days_between FROM events;

-- Postgres
SELECT end_date - start_date AS days_between FROM events;
```

📚 Learn more at [Mode SQL Date Tutorial](https://mode.com/sql-tutorial/sql-date-functions/)
