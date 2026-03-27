# Gap Analysis — Bridging Current State to Future State

## 1. The Core Concept
Gap Analysis is the process of identifying the "space" between where a business is now and where it wants to be. For a Data Analyst, this usually involves identifying missing data, broken processes, or untapped opportunities.


| Component | Focus | Analyst Action |
| :--- | :--- | :--- |
| **Current State** | The "As-Is" | Perform **Descriptive Analytics** to audit current performance. |
| **Future State** | The "To-Be" | Work with stakeholders to define **SMART** goals. |
| **Gap** | The "Missing Link" | Identify the delta (e.g., -15% Revenue, missing API data). |
| **Action Plan** | The "Bridge" | Propose **Prescriptive** steps (e.g., "Build Alteryx workflow"). |

---

## 2. Steps to Perform a Gap Analysis

### Step 1: Identify the Target (Future State)
Define exactly what success looks like. Use a metric-driven goal.
*   *Example:* "Achieve 98% data accuracy in the CRM by Q4."

### Step 2: Audit the Reality (Current State)
Use SQL or Tableau to quantify where you are today.
*   *Example:* "Current CRM accuracy is 74% due to manual entry errors."

### Step 3: Analyze the Gaps
Categorize why the gap exists. Common categories:
*   **Data Gap:** We aren't collecting the necessary fields.
*   **Skill Gap:** The team needs training in Alteryx/SQL.
*   **Process Gap:** Data is being overwritten by a faulty sync.
*   **Technology Gap:** The current server is too slow for real-time reporting.

### Step 4: Propose the Bridge (Action Plan)
Create a prioritized list of tasks to close the gap.

---

## 3. Gap Analysis Matrix (Template)


| Focus Area | Current State (As-Is) | Future State (To-Be) | The Gap | Action/Bridge |
| :--- | :--- | :--- | :--- | :--- |
| **Reporting** | Manual Excel files (4hrs/wk) | Automated Tableau Dashboard | 4 hours of manual labor | Build Alteryx ETL to Tableau |
| **Data Quality** | 15% Null Email fields | 0% Null Email fields | 5,000 missing emails | Implement required field in UI |
| **Insights** | Hindsight only | Predictive Churn Scores | No foresight capability | Develop Random Forest model |

---

## 4. SQL for Gap Detection
Use SQL to find "The Gap" in data integrity or business targets.

```sql
-- Finding "Missing Data" Gaps
SELECT 
    COUNT(*) AS total_records,
    SUM(CASE WHEN customer_email IS NULL THEN 1 ELSE 0 END) AS missing_emails,
    (SUM(CASE WHEN customer_email IS NULL THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) AS gap_percentage
FROM crm_data;

-- Comparing Actuals vs. Target (The Business Gap)
SELECT 
    region,
    actual_sales,
    target_sales,
    (target_sales - actual_sales) AS revenue_gap,
    (actual_sales / target_sales) * 100 AS percent_to_target
FROM sales_performance
WHERE actual_sales < target_sales;
```

---

## 5. Visualizing the Gap
*   **Waterfall Chart:** Shows the starting point, the factors adding/subtracting, and the ending point.
*   **Bullet Graph:** Best for showing a single measure (Current) against a target (Future).
*   **Side-by-Side Bar:** Compares "Last Year" vs. "This Year" to show growth gaps.

---

## 6. Summary Checklist
- [ ] Did I quantify the **Current State** with hard data?
- [ ] Is the **Future State** tied to a specific business KPI?
- [ ] Have I identified the **Root Cause** of the gap (Process, Data, or Tech)?
- [ ] Is my **Action Plan** realistic given the current resources?
