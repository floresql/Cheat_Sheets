# SQL Data Cleaning Cheat Sheet

Clean up messy data with these SQL techniques.

---

## 🔹 NULL Handling

**Description**: Identifying and replacing NULLs.

**When to Use**: To improve data completeness or prepare reports.

```sql
SELECT COALESCE(phone, 'Unknown') AS contact_number FROM customers;
```

---

## 🔸 IS NULL / IS NOT NULL

**Description**: Check for presence of NULLs.

**When to Use**: Data integrity checks and filters.

```sql
SELECT * FROM orders WHERE discount IS NULL;
```

---

## 🔹 DISTINCT

**Description**: Removes duplicate values.

**When to Use**: Getting unique values for analysis.

```sql
SELECT DISTINCT category FROM products;
```

---

## 🔸 CAST / CONVERT

**Description**: Converts data from one type to another.

**When to Use**: Standardizing values or fixing format issues.

```sql
SELECT CAST(order_total AS DECIMAL(10,2)) FROM orders;
```

---

## 🔹 REPLACE

**Description**: Replace bad or inconsistent values.

**When to Use**: Clean typos or standardize text.

```sql
SELECT REPLACE(state, 'Calif.', 'CA') FROM addresses;
```

---

## 🧠 Use Cases
- Cleaning contact info
- Removing duplication
- Formatting values

---

📚 Learn more at [DataCamp SQL Cleaning Guide](https://www.datacamp.com/tutorial/data-cleaning-sql)
