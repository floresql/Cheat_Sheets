# The 4 Pillars of Analytics — The Data Maturity Model

## 1. Overview of the 4 Pillars
This framework represents the journey from raw data to optimized business decisions. Each pillar builds on the previous one, increasing in both **complexity** and **business value**.


| Pillar | Focus | Question | Complexity | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Descriptive** | Hindsight | **What happened?** | Low | Low |
| **Diagnostic** | Insight | **Why did it happen?** | Medium | Medium |
| **Predictive** | Foresight | **What will happen?** | High | High |
| **Prescriptive** | Optimization | **How can we make it happen?** | Very High | Strategic |

---

## 2. Descriptive Analytics: "The Mirror"
**Goal:** Summarize historical data to provide context.
*   **Tools:** Tableau, Power BI, Excel, SQL.
*   **Examples:** Monthly revenue reports, Year-over-year (YoY) sales growth, active user counts.

```sql
-- Example: Descriptive SQL (Total Sales per Region)
SELECT 
    region, 
    SUM(sales_amount) AS total_revenue
FROM sales_fact
WHERE transaction_date >= '2023-01-01'
GROUP BY region;
```

---

## 3. Diagnostic Analytics: "The Drill"
**Goal:** Identify patterns and root causes through data discovery.
*   **Techniques:** Data mining, drill-downs, correlations, and A/B testing.
*   **Examples:** Why did sales drop in March? (Answer: A supply chain delay in the Midwest region).

```python
# Example: Diagnostic Python (Correlation Matrix)
import seaborn as sns
import matplotlib.pyplot as plt

# Identify relationship between 'marketing_spend' and 'conversions'
correlation = df[['marketing_spend', 'conversions', 'page_load_speed']].corr()
sns.heatmap(correlation, annot=True)
```

---

## 4. Predictive Analytics: "The Crystal Ball"
**Goal:** Use statistical models and ML to forecast future outcomes.
*   **Techniques:** Regression, Time-series analysis, Propensity scoring (Churn prediction).
*   **Examples:** Forecasting next month's inventory needs; predicting which customers are likely to cancel.

```python
# Example: Simple Linear Regression Forecast
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
future_prediction = model.predict(X_upcoming_month)
```

---

## 5. Prescriptive Analytics: "The GPS"
**Goal:** Recommend specific actions to achieve a desired goal or solve a problem.
*   **Techniques:** Optimization algorithms, simulation, business rules engines.
*   **Examples:** "To hit our 15% growth target, we should reallocate $50k from TV ads to Instagram influencers."

```sql
-- Logic-based Prescriptive Flag (in Alteryx or SQL)
CASE 
    WHEN inventory_count < safety_stock AND lead_time > 5 THEN 'Urgent Reorder - Air Freight'
    WHEN inventory_count < safety_stock THEN 'Standard Reorder'
    ELSE 'Maintain'
END AS recommended_action
```

---

## 6. Implementation Checklist for Analysts
- [ ] **Descriptive:** Is my dashboard reporting accurate, "clean" history?
- [ ] **Diagnostic:** Can the user click a chart to see *why* a number changed?
- [ ] **Predictive:** Have I validated my model accuracy on a hold-out test set?
- [ ] **Prescriptive:** Does my analysis end with a "Next Best Action" for the stakeholder?
