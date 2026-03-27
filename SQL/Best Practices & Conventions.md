# SQL Style Guide — Best Practices & Conventions

## 1. General Formatting
*   **Keywords:** Use **UPPERCASE** for all SQL keywords (`SELECT`, `FROM`, `WHERE`).
*   **Identifiers:** Use **snake_case** (lowercase with underscores) for table and column names.
*   **Indentation:** Use a new line for each major clause and indent columns/conditions for readability.

```sql
-- Good: Readable and structured
SELECT
    user_id,
    first_name,
    last_name
FROM users
WHERE status = 'active'
    AND created_at >= '2023-01-01';
```

## 2. Naming Conventions


| Entity | Convention | Example |
| :--- | :--- | :--- |
| **Tables** | Collective or Plural snake_case | `user_accounts`, `orders` |
| **Columns** | snake_case | `created_at`, `total_amount` |
| **Primary Keys** | `id` or `table_name_id` | `user_id` |
| **Foreign Keys** | `referenced_table_id` | `order_id` (in `payments` table) |
| **Aliasing** | Meaningful short names | `users AS u` |

## 3. Selecting Data
*   **Avoid `SELECT *`:** Explicitly name columns to improve performance and prevent breaking code if the schema changes.
*   **Aliasing:** Use the `AS` keyword explicitly for clarity when renaming columns or tables.

```sql
-- Good
SELECT 
    u.first_name AS given_name,
    u.email
FROM users AS u;

-- Bad
SELECT * FROM users;
```

## 4. Joins
*   **Be Explicit:** Use `INNER JOIN` instead of just `JOIN`.
*   **Join Conditions:** Always use the `ON` keyword. Avoid comma-separated tables in the `FROM` clause.

```sql
-- Good
SELECT
    o.order_id,
    u.email
FROM orders AS o
INNER JOIN users AS u 
    ON o.user_id = u.id;
```

## 5. Filtering & Logic
*   **Alignment:** Indent `AND` and `OR` logical operators under the `WHERE` clause.
*   **In-Lists:** When using `IN` with many values, put them on separate indented lines.

```sql
-- Good
SELECT product_name
FROM products
WHERE category_id IN (
        101,
        102,
        103
    )
    AND price < 50.00;
```

## 6. Common Table Expressions (CTEs)
*   **Preference:** Use CTEs (`WITH` clauses) instead of nested subqueries for complex logic. They act as "readable variables" for SQL.

```sql
-- Good: Highly readable
WITH active_users AS (
    SELECT id, email
    FROM users
    WHERE last_login > '2023-12-01'
)
SELECT 
    au.email,
    o.total_price
FROM active_users AS au
LEFT JOIN orders AS o 
    ON au.id = o.user_id;
```

## 7. Comments
*   **Single Line:** Use `--` followed by a space.
*   **Multi-line:** Use `/* ... */` for longer explanations or logic headers.

```sql
-- Get the total revenue per month
SELECT 
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount) AS revenue
FROM sales
GROUP BY 1 -- Group by the first column
ORDER BY 1 DESC;
```
