# SQL Cheat Sheet: Procedures & Transactions

### 1. Stored Procedures
Pre-compiled SQL code that can be called repeatedly.
```sql
CREATE PROCEDURE UpdateInventory (IN prod_id INT, IN qty INT)
BEGIN
    UPDATE products SET stock = stock - qty WHERE id = prod_id;
    INSERT INTO audit_log (action, prod_id) VALUES ('Purchase', prod_id);
END;
```

### 2. ACID Transactions
Ensure multiple steps succeed together or fail together.
```sql
BEGIN TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- If both succeed:
COMMIT;

-- If an error occurs:
ROLLBACK;
```

### 3. User-Defined Functions (UDFs)
Custom logic that returns a single value.
```sql
CREATE FUNCTION GetTax (price DECIMAL) RETURNS DECIMAL
AS
BEGIN
    RETURN price * 0.08;
END;
```
