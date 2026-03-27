# Alteryx — Advanced Formulas & Logic

## 1. String & Data Cleansing
*   **Trim:** Use `Trim([Field])` for both sides, or `TrimLeft`/`TrimRight`.
*   **Regex:** Powerful for complex parsing.
*   **Null Handling:** Use `IsNull()` or `Empty()` to check state.

```sql
/* Clean whitespace and handle nulls */
IF IsNull([Customer_Name]) OR Empty([Customer_Name]) 
THEN "Unknown" 
ELSE TitleCase(Trim([Customer_Name])) 
ENDIF

/* Extracting numbers from a string (e.g., "ID: 1234") */
REGEXP_Replace([Field], "\D", "")
```

## 2. Date & Time Calculations
*   **Formatting:** Always use `DateTimeParse` to convert strings to ISO (`yyyy-mm-dd`).
*   **Difference:** Use `DateTimeDiff` for ages or durations.

```sql
/* Calculate age in years */
DateTimeDiff(DateTimeToday(), [Birth_Date], "years")

/* Convert '01-Jan-24' to Alteryx Date */
DateTimeParse([Date_String], "%d-%b-%y")

/* Add 30 days to a date */
DateTimeAdd([Order_Date], 30, "days")
```

## 3. Conditional Logic (IF & Switch)
*   **Nested IF:** Standard logic flow.
*   **Switch:** Cleaner for multiple specific matches.

```sql
/* Multi-tier pricing logic */
IF [Volume] > 1000 THEN [Price] * 0.8
ELSEIF [Volume] > 500 THEN [Price] * 0.9
ELSE [Price]
ENDIF

/* Region mapping using Switch */
Switch([State], "Unknown", "NY", "East", "CA", "West", "TX", "South")
```
