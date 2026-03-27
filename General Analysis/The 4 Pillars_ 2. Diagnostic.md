# Diagnostic Analytics — The "Why Did It Happen?" Deep Dive

## 1. Core Objectives
Diagnostic analytics moves from observation to investigation. It is the "detective work" of data analysis used to uncover root causes and relationships.
*   **Anomaly Detection:** Identifying exactly where and when a metric deviated from the norm.
*   **Discovery:** Finding hidden patterns and correlations between variables.
*   **Causal Identification:** Distinguishing between what *seems* related (correlation) and what actually *drives* the result (causation).

---

## 2. Essential Diagnostic Techniques
Analysts use specific "drill-down" methods to isolate the drivers of change.



| Technique | Definition | Use Case Example |
| :--- | :--- | :--- |
| **Drill-Down** | Breaking a metric into sub-segments (e.g., Region > Store). | Finding which specific store caused a 10% regional sales drop. |
| **Data Mining** | Using algorithms to find patterns or anomalies in large sets. | Identifying that customers who buy milk also buy cereal 80% of the time. |
| **Correlation** | Measuring the strength of the relationship between two variables. | Checking if higher website load times correlate with lower sales. |
| **Hypothesis Testing** | Statistical testing to confirm or challenge an assumption. | Testing if a new UI layout actually caused a spike in sign-ups. |
| **Regression** | Determining how much one variable affects another. | Measuring how much a $1 price increase affects total volume. |

---

## 3. The "5 Whys" Root Cause Framework
The **5 Whys** is a structured interrogative technique to peel away layers of symptoms to find the root cause.

**Scenario: A data pipeline failed to deliver the morning report.**
1.  **Why?** The extraction process from the source system was delayed.
2.  **Why?** The source system was experiencing high latency.
3.  **Why?** A recent software update consumed excessive resources.
4.  **Why?** The update was not optimized for the current hardware.
5.  **Why? (Root Cause):** The testing environment did not mirror the production environment closely.

---

## 4. Technical Implementation (SQL & Python)

### SQL: Comparative Drill-Downs
Use subqueries or Common Table Expressions (CTEs) to compare "Affected" vs. "Normal" groups.

```sql
-- Diagnostic: Comparing Churned vs. Active users on a specific behavior
WITH churned_users AS (
    SELECT user_id, AVG(session_duration) AS avg_duration
    FROM user_activity
    WHERE status = 'Churned'
    GROUP BY 1
),
active_users AS (
    SELECT user_id, AVG(session_duration) AS avg_duration
    FROM user_activity
    WHERE status = 'Active'
    GROUP BY 1
)
-- See if session duration is a "Why" for churn
SELECT 
    'Churned' AS group, AVG(avg_duration) AS group_avg FROM churned_users
UNION ALL
SELECT 
    'Active' AS group, AVG(avg_duration) AS group_avg FROM active_users;
```

### Python: Anomaly & Relationship Detection
Use libraries like `Seaborn` to visualize relationships.

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Identify relationships between variables using a Pairplot
# This helps spot which variable moves in lockstep with your target
sns.pairplot(df, vars=['revenue', 'marketing_spend', 'bounce_rate', 'discount_pct'])
plt.show()

# Isolate the specific anomaly point
df['z_score'] = (df['metric'] - df['metric'].mean()) / df['metric'].std()
anomalies = df[df['z_score'].abs() > 3] # Outliers beyond 3 standard deviations
```

---

## 5. Diagnostic Checklist
- [ ] **Precision:** Is the problem defined specifically? (e.g., "Revenue is down" vs. "Conversion rate for iOS users dropped 5%").
- [ ] **Comparison:** Have I compared the "Affected" group against a stable baseline?.
- [ ] **Context:** Did I check for external factors like holidays, competitor moves, or tracking bugs?.
- [ ] **Mechanism:** Can I explain the *how*? (e.g., "Cans are heavy, so they crush the soft produce in transit").
- [ ] **Causation Check:** Is this just a coincidence, or is there a direct link?.
