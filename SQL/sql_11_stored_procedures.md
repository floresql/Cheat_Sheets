# SQL Server Stored Procedures Cheat Sheet

Stored procedures in SQL Server allow you to encapsulate logic and reuse it across applications and users.

---

## 🔹 What Is a Stored Procedure?

**Description**: A named set of SQL statements stored in the database.

**When to Use**:
- Reuse complex SQL logic
- Improve performance via execution plan reuse
- Secure and audit operations
- Automate recurring tasks

---

## 🔸 Basic Syntax

**Create a Procedure**:
```sql
CREATE PROCEDURE usp_GetAllEmployees
AS
BEGIN
    SELECT * FROM Employees;
END;
```

**Execute a Procedure**:
```sql
EXEC usp_GetAllEmployees;
```

---

## 🔹 Parameters in Stored Procedures

**IN Parameter** (default in SQL Server):
```sql
CREATE PROCEDURE usp_GetEmployeeByID @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;

EXEC usp_GetEmployeeByID @EmployeeID = 3;
```

**OUT Parameter**:
```sql
CREATE PROCEDURE usp_GetTotalEmployees @TotalCount INT OUTPUT
AS
BEGIN
    SELECT @TotalCount = COUNT(*) FROM Employees;
END;

DECLARE @Count INT;
EXEC usp_GetTotalEmployees @TotalCount = @Count OUTPUT;
PRINT @Count;
```

---

## 🔸 Control Flow

**IF / ELSE**:
```sql
IF EXISTS (SELECT 1 FROM Employees WHERE EmployeeID = 5)
    PRINT 'Employee exists';
ELSE
    PRINT 'Employee does not exist';
```

**BEGIN / END and Variables**:
```sql
DECLARE @BonusRate FLOAT;
SET @BonusRate = 0.10;

BEGIN
    UPDATE Employees
    SET Bonus = Salary * @BonusRate
    WHERE Department = 'Sales';
END;
```

---

## 🔹 Error Handling

**TRY...CATCH**:
```sql
BEGIN TRY
    -- risky operation
    DELETE FROM Employees WHERE EmployeeID = 999;
END TRY
BEGIN CATCH
    PRINT 'An error occurred:';
    PRINT ERROR_MESSAGE();
END CATCH;
```

---

## 🔸 Transactions

```sql
BEGIN TRANSACTION;

BEGIN TRY
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 1;
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 2;
    COMMIT;
END TRY
BEGIN CATCH
    ROLLBACK;
    PRINT ERROR_MESSAGE();
END CATCH;
```

---

## 🔹 Dynamic SQL

```sql
DECLARE @SQL NVARCHAR(MAX);
SET @SQL = 'SELECT * FROM ' + QUOTENAME(@TableName);
EXEC sp_executesql @SQL;
```

---

## 🔸 Permissions

**Grant Execute Permission**:
```sql
GRANT EXECUTE ON usp_GetAllEmployees TO ReportingUser;
```

---

## 🧠 Use Cases
- Data cleanup tasks
- Automating reports or imports
- Enforcing complex business rules
- Securing sensitive logic
- Auditing data changes

---

📚 Learn more at [Microsoft Docs](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-procedure-transact-sql)
