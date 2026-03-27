# SMART Framework — Goal Setting & Problem Definition

## 1. The SMART Criteria
The SMART framework ensures that business objectives are clear, reachable, and trackable.


| Letter | Criteria | Definition | Key Question |
| :--- | :--- | :--- | :--- |
| **S** | **Specific** | Well-defined, clear, and unambiguous. | What exactly do we want to accomplish? |
| **M** | **Measurable** | Specific criteria that measure progress. | How will we know when it is accomplished? |
| **A** | **Achievable** | Attainable and not impossible to achieve. | Do we have the resources/skills to do this? |
| **R** | **Relevant** | Fits within broader business goals. | Does this matter to the current business need? |
| **T** | **Time-bound** | Has a clearly defined start and end date. | When will we achieve this goal? |

---

## 2. Converting Vague Goals to SMART Goals

### Example 1: Sales Improvement
*   **Vague:** "We need to increase our sales."
*   **SMART:** "The sales team will increase **subscription revenue** by **15%** ($200k) by **Q4 2024** by upselling existing enterprise clients, using the new **Alteryx automated lead score** model."

### Example 2: Data Quality
*   **Vague:** "Clean up the customer database."
*   **SMART:** "Reduce **duplicate customer records** in the CRM from **8% to <1%** by **June 30th** using a SQL deduplication script to improve marketing attribution accuracy."

---

## 3. The Analyst's "SMART" Checklist
Before starting a SQL query, Tableau dashboard, or Alteryx workflow, verify these points:

- [ ] **Specific:** Is the "Target Variable" clearly defined (e.g., "Gross Revenue" vs "Net Profit")?
- [ ] **Measurable:** Is there a numeric baseline and a numeric target?
- [ ] **Achievable:** Is the data actually available in the source system (Snowflake, Excel, etc.)?
- [ ] **Relevant:** If I solve this, will it actually change a business decision?
- [ ] **Time-bound:** Is the look-back period (e.g., "Last 12 Months") and the deadline clearly set?

---

## 4. Implementation Template
Use this structure for project documentation:

```text
GOAL STATEMENT:
By [Date/Time], [Who/What] will [Action/Verb] [Metric] 
from [Baseline] to [Target] because [Business Reason/Relevance].

RESOURCES REQUIRED:
- Data Sources: [e.g., SQL Server, API]
- Tools: [e.g., Alteryx, Tableau]
- Stakeholders: [e.g., Marketing VP]
```

---

## 5. Potential Pitfalls
*   **Too Many Metrics:** Focusing on 10 things means you focus on 0. Pick **one** primary SMART goal.
*   **Lack of Authority:** A goal is only *Achievable* if the analyst has access to the necessary data.
*   **Ignoring the "R":** Don't spend 40 hours analyzing data that no one plans to act upon.
