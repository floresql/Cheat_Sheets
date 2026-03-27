# Descriptive Analytics — The "What Happened?" Deep Dive

## 1. Core Objectives
Descriptive analytics is the foundation of the analytical maturity model. It transforms raw data into a coherent historical narrative.
*   **Summarization:** Condensing millions of rows into key metrics (KPIs).
*   **Comparison:** Measuring performance against a baseline (Target, Last Year, or Average).
*   **Snapshotting:** Providing a clear picture of the business at a specific point in time.

---

## 2. Essential Statistical Methods
To describe data accurately, you must understand its distribution and central tendency.


| Method | Definition | When to Use |
| :--- | :--- | :--- |
| **Mean (Average)** | Sum of values divided by count. | For normally distributed data without extreme outliers. |
| **Median** | The middle value in a sorted list. | When data is skewed (e.g., Household Income, Home Prices). |
| **Mode** | The most frequently occurring value. | For categorical data (e.g., "Most Popular Product Category"). |
| **Standard Deviation** | Measures how spread out numbers are. | To determine data volatility or consistency. |
| **Percentiles** | Indicates the value below which a percentage of data falls. | For "Top 10%" analysis or identifying "Normal" ranges. |

---

## 3. Technical Implementation (SQL & Python)

### SQL: Aggregations & Window Functions
SQL is the primary tool for descriptive summaries. Use `GROUP BY` for dimensions and Window Functions for comparisons.

```sql
-- Calculating Total Sales, Avg Order Value, and % of Total
SELECT 
    region,
    COUNT(order_id) AS total_orders,
    SUM(revenue) AS total_revenue,
    AVG(revenue) AS avg_order_value,
    -- Window Function to see regional share of total company revenue
    SUM(revenue) * 100.0 / SUM(SUM(revenue)) OVER () AS pct_of_total_company_rev
FROM sales_fact
WHERE status = 'Completed'
GROUP BY 1
ORDER BY total_revenue DESC;
```

### Python: Distribution & Profiling
Python is excellent for identifying the "shape" of your historical data.

```python
import pandas as pd

# Rapid descriptive profiling
summary = df['sales_amount'].describe()

# Binning data for a Frequency Distribution (Histogram logic)
df['price_tier'] = pd.cut(df['price'], bins=[0, 20, 50, 100, 1000], 
                         labels=['Budget', 'Mid', 'Premium', 'Luxury'])

# Pivot Table for multi-dimensional summary
pivot = df.pivot_table(index='Region', columns='Year', values='Revenue', agg_agg='sum')
```

---

## 4. Key Descriptive Frameworks

### Time-Series Analysis (The "When")
*   **YoY (Year-over-Year):** Compares a period (e.g., March 2024) to the same period in the previous year (March 2023). Accounts for seasonality.
*   **WoW/MoM:** Measures short-term momentum.
*   **Rolling Averages:** Smooths out daily "noise" to see the true trend line (e.g., 7-day or 30-day moving average).

### Segmentation (The "Who")
*   **Cohort Analysis:** Grouping users by a shared event date (e.g., "The January 2024 Signup Cohort") to track behavior over time.
*   **Pareto Analysis (80/20 Rule):** Identifying the 20% of causes (products/customers) that drive 80% of the effects (revenue).

---

## 5. Visualization Best Practices
*   **Line Charts:** Best for showing a continuous variable (Revenue) over time.
*   **Bar Charts:** Best for comparing discrete categories (Sales by Region).
*   **Tables:** Use only when the specific exact number is more important than the trend.
*   **Don't truncate the Y-axis:** Always start at zero for bar charts to avoid exaggerating differences.

---

## 6. Descriptive Checklist
- [ ] **Grain:** Is the data at the right level (Daily vs. Monthly)?
- [ ] **Filters:** Have I excluded test accounts, internal transactions, or outliers?
- [ ] **Benchmarking:** Does this number have context (e.g., "Up 5% vs. Last Month")?
- [ ] **Data Freshness:** Is the "Last Refreshed" timestamp clearly visible?
- [ ] **Definition:** Does everyone agree on what "Active User" or "Gross Margin" means?
