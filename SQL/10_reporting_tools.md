# SQL for Reporting Tools Cheat Sheet (Power BI / Tableau / SSRS)

## 🧱 Structure Your Queries
- Return only the fields needed
- Use readable aliases
```sql
SELECT region AS sales_region, SUM(sales) AS total_sales FROM orders GROUP BY region;
```

## 📊 Use Parameters
Power BI / Tableau can inject values into SQL:
```sql
WHERE order_date BETWEEN @StartDate AND @EndDate
```

## 🧪 Common Patterns
- Aggregations per group
- Date filters and logic
- CASE statements for dynamic categories

## 💡 Performance Tips
- Use indexed columns in filters
- Avoid SELECT *
- Pre-aggregate in views or staging tables

📚 Learn more at:
- [Tableau SQL Best Practices](https://help.tableau.com/)
- [Power BI SQL Optimization](https://docs.microsoft.com/en-us/power-bi/)
