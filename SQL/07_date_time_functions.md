# SQL Date & Time Functions Cheat Sheet

Manipulating and formatting dates for time-based reporting and analysis.

---

## 🔹 CURRENT_DATE / NOW()

**Description**: Returns the current date/time.

**When to Use**: For dynamic filtering or logging.

```sql
SELECT CURRENT_DATE, NOW();
```

---

## 🔸 DATE_ADD / DATE_SUB

**Description**: Adds or subtracts time intervals.

**When to Use**: Calculating due dates or timeframes.

```sql
SELECT order_date, DATE_ADD(order_date, INTERVAL 7 DAY) AS delivery_date FROM orders;
```

---

## 🔹 DATEDIFF

**Description**: Returns the number of days between two dates.

**When to Use**: Measuring duration or aging.

```sql
SELECT DATEDIFF(CURRENT_DATE, order_date) AS days_since_order FROM orders;
```

---

## 🔸 EXTRACT

**Description**: Gets a part of a date (year, month, etc.).

**When to Use**: Grouping or filtering by time components.

```sql
SELECT EXTRACT(YEAR FROM order_date) AS order_year FROM orders;
```

---

## 🔹 DATE_TRUNC

**Description**: Truncates date to a specified precision (e.g., month).

**When to Use**: Monthly, quarterly, or yearly rollups.

```sql
SELECT DATE_TRUNC('month', order_date) FROM orders;
```

---

## 🧠 Use Cases
- Rolling date windows
- Time series analysis
- Dynamic filtering

---

📚 Learn more at [SQL Date Tutorial – Mode](https://mode.com/sql-tutorial/sql-date-functions/)
