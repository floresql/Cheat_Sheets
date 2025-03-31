# SQL for Reporting Tools Cheat Sheet

Write efficient and flexible SQL for Power BI, Tableau, SSRS, and other tools.

---

## 🔹 Parameterization

**Description**: Filter queries using dynamic values.

**When to Use**: Making SQL reusable in dashboards.

```sql
SELECT * FROM orders WHERE order_date BETWEEN @StartDate AND @EndDate;
```

---

## 🔸 Aliases and Naming

**Description**: Rename fields for user-friendly display.

**When to Use**: When integrating SQL into visualization tools.

```sql
SELECT customer_id AS 'Customer ID', SUM(sales) AS 'Total Sales' FROM orders GROUP BY customer_id;
```

---

## 🔹 Aggregation Logic

**Description**: Pre-calculate metrics for visuals.

**When to Use**: To reduce dashboard load time.

```sql
SELECT region, SUM(sales) AS total_sales FROM orders GROUP BY region;
```

---

## 🔸 Optimize with Views

**Description**: Save reusable SQL logic as views.

**When to Use**: Simplify report-building and boost performance.

---

## 🧠 Use Cases
- Driving Power BI/Tableau dashboards
- SSRS reports with parameters
- Prepping clean datasets for visualization

---

📚 Learn more at:
- [Power BI SQL Best Practices](https://docs.microsoft.com/en-us/power-bi/)
- [Tableau Custom SQL](https://help.tableau.com/)
