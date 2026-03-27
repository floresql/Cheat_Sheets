# Tableau Cheat Sheet: String Shortcuts

### 1. Parsing Names (First and Last)
Extract parts of a string based on a delimiter (like a space or comma).
```sql
// Extract First Name
SPLIT([Full Name], " ", 1)

// Extract Last Name
SPLIT([Full Name], " ", 2)
```

### 2. Standardizing Case & Whitespace
Clean up user-entered data before grouping.
```sql
// Remove extra spaces and force uppercase
UPPER(TRIM([Region Name]))
```

### 3. Check if String Contains a Keyword
A more efficient way to build "Search" logic than using wildcards in filters.
```sql
// Returns True if "Urgent" is found anywhere in the string
CONTAINS(UPPER([Comments]), "URGENT")
```

### 4. Shorthand Dimensions (Initials)
Turn "North America" into "NA".
```sql
LEFT([Region], 1) + RIGHT(SPLIT([Region], " ", 2), 1)
```
