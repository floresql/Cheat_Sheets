# Tableau Cheat Sheet: Date & Time Logic

### 1. YTD vs. Previous YTD Comparison
The standard way to build Year-over-Year (YoY) metrics.
```sql
// Current Year to Date (CYTD)
[Order Date] <= TODAY() 
AND DATEDIFF('year', [Order Date], TODAY()) = 0

// Previous Year to Date (PYTD)
[Order Date] <= DATEADD('year', -1, TODAY()) 
AND DATEDIFF('year', [Order Date], TODAY()) = 1
```

### 2. Custom Date Parts (DTRUNC)
Force dates to the first of the month/week regardless of the specific day.
```sql
// Always returns the first day of the month
DATETRUNC('month', [Order Date])
```

### 3. Relative Date Filters
*   **The Trick:** Drag a date field to the **Filters** shelf and select **Relative Date**. This allows users to easily choose "Last 3 Months," "Last 30 Days," or "Current Year" without manual date entry.
