# Alteryx — In-Database (In-DB) Best Practices

## 1. Why Use In-DB?
*   **Processing Power:** It uses the **Database Engine** (SQL Server, Snowflake, Oracle) instead of pulling data into your local RAM.
*   **Speed:** Critical for datasets with billions of rows.

## 2. In-DB Workflow Tips
*   **Filter Early:** Use the **Filter In-DB** tool immediately after the connection.
*   **Formula In-DB:** Use **SQL Syntax** instead of Alteryx functions (e.g., use `GETDATE()` instead of `DateTimeToday()`).
*   **Data Stream In:** Use this to bring a small local list (like an Excel lookup) *into* the database for joining.
*   **Data Stream Out:** The final step to bring results back into Designer for outputting to Excel/Tableau.
