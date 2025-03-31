# SQL String Functions Cheat Sheet

String manipulation techniques to clean, search, and transform text.

---

## 🔹 UPPER / LOWER

**Description**: Converts text to uppercase or lowercase.

**When to Use**: Standardizing or formatting text.

```sql
SELECT UPPER(name), LOWER(name) FROM users;
```

---

## 🔸 LENGTH

**Description**: Returns the number of characters.

**When to Use**: Validating text length or truncation checks.

```sql
SELECT LENGTH(name) FROM customers;
```

---

## 🔹 TRIM / LTRIM / RTRIM

**Description**: Removes whitespace from strings.

**When to Use**: Cleaning dirty data entries.

```sql
SELECT TRIM('   hello   ');
```

---

## 🔸 SUBSTRING

**Description**: Extracts part of a string.

**When to Use**: Getting specific tokens (e.g., area codes, domain names).

```sql
SELECT SUBSTRING(email FROM 1 FOR 10) FROM users;
```

---

## 🔹 REPLACE

**Description**: Substitutes occurrences of a substring.

**When to Use**: Normalizing inconsistent values.

```sql
SELECT REPLACE(name, 'Inc.', '') FROM companies;
```

---

## 🔸 CONCAT

**Description**: Joins two or more strings together.

**When to Use**: Merging name fields or building dynamic values.

```sql
SELECT CONCAT(first_name, ' ', last_name) FROM employees;
```

---

## 🧠 Use Cases
- Data cleaning and prep
- Pattern searches and transformations
- Text parsing for reporting

---

📚 Learn more at [W3Schools SQL String Functions](https://www.w3schools.com/sql/sql_ref_string_functions.asp)
