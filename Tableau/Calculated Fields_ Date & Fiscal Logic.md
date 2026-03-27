# Tableau Cheat Sheet: Date & Fiscal Logic

### 1. Fiscal Year Offset (Custom Start Month)
If your fiscal year starts in July, shift the date by 6 months.
```sql
// Returns the Fiscal Year as an integer
YEAR(DATEADD('month', 6, [Order Date]))
```

### 2. Period-to-Date (YTD, QTD, MTD)
Create a single boolean filter to handle all "To-Date" logic.
```sql
// YTD: Current year up to today's date
YEAR([Order Date]) = YEAR(TODAY()) 
AND [Order Date] <= TODAY()

// MTD: Current month up to today's date
DATEDIFF('month', [Order Date], TODAY()) = 0 
AND [Order Date] <= TODAY()
```

### 3. Finding the Last Day of the Previous Month
Great for monthly closing reports.
```sql
// Step 1: Go to the first of this month. Step 2: Go back 1 day.
DATEADD('day', -1, DATETRUNC('month', TODAY()))
```

### 4. Grouping by Week (Always Starting Monday)
Tableau's default week start can vary; force it to Monday.
```sql
DATETRUNC('week', [Order Date], 'monday')
```
