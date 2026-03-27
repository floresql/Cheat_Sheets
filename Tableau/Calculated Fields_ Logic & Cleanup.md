# Tableau Cheat Sheet: Logic & Cleanup

### 1. CASE vs. IF Statements
Use `CASE` for exact matches (it is slightly faster and easier to read).
```sql
CASE [Status Code]
    WHEN 1 THEN "Active"
    WHEN 2 THEN "Pending"
    ELSE "Inactive"
END
```

### 2. Handling Nulls in Concatenation
Standard addition `+` with a Null results in a Null. Use `IFNULL` to prevent this.
```sql
// Ensures the result isn't blank if one field is missing
IFNULL([First Name], "") + " " + IFNULL([Last Name], "")
```

### 3. Dimension vs. Measure Toggle
Create a parameter to let users choose what metric they see in a chart.
```sql
// Parameter [Select Metric] has values: "Sales", "Profit", "Quantity"
CASE [Select Metric]
    WHEN "Sales" THEN [Sales]
    WHEN "Profit" THEN [Profit]
    ELSE [Quantity]
END
```

### 4. Minimum/Maximum of Two Fields
Compare two columns and return the larger/smaller value.
```sql
// Returns the higher of the two values for each row
MAX([Shipping Date], [Delivery Date])
```
