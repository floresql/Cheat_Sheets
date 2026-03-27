# The Data Life Cycle — Managing Data as a Strategic Asset

## 1. Plan
**Goal:** Define the data requirements, standards, and handling procedures before any data is created.
*   **Identify Needs:** What questions are we trying to answer? What data types are required?
*   **Data Governance:** Define who owns the data, who can access it, and how long it must be kept.
*   **Schema Design:** Design the structure (tables, fields, relationships) to ensure scalability.

## 2. Capture
**Goal:** Collect or generate the data from various internal and external sources.
*   **Methods:** Manual entry, automated sensors, web scraping, or importing from existing SQL databases/APIs.
*   **Data Integrity:** Implement validation rules at the point of entry to prevent "Garbage In."
*   **Metadata:** Capture "data about the data" (source, timestamp, author) to ensure future traceability.

## 3. Manage
**Goal:** Store, protect, and maintain the data to ensure it remains available and accurate.
*   **Storage:** Choose the right environment (Cloud Warehouse, On-premise SQL, Data Lake).
*   **Security:** Implement encryption, backups, and access controls (GDPR/SOC2 compliance).
*   **Cleaning:** Continuous maintenance to handle duplicates and "data decay" (e.g., outdated customer addresses).

## 4. Analyze
**Goal:** Process the data to extract insights and drive business value.
*   **Execution:** Apply the [4 Pillars of Analytics](#) (Descriptive, Diagnostic, Predictive, Prescriptive).
*   **Modeling:** Use tools like Alteryx, Python, or SQL to find patterns and trends.
*   **Interpretation:** Translate technical findings into actionable business language.

```sql
-- Example: Managing and Analyzing (Cleaning + Aggregation)
SELECT 
    category, 
    COUNT(*) AS total_items,
    AVG(price) AS avg_price
FROM inventory_master
WHERE status = 'active' -- Management filter
GROUP BY 1;
```

## 5. Archive
**Goal:** Move data that is no longer actively used to long-term, low-cost storage.
*   **Criteria:** Data that is rarely accessed but must be kept for legal, regulatory, or historical reasons.
*   **Cost Optimization:** Move from "Hot" storage (expensive/fast) to "Cold" storage (cheap/slow).
*   **Searchability:** Ensure archived data can still be retrieved if an audit occurs.

## 6. Destroy
**Goal:** Securely and permanently delete data that is no longer needed.
*   **Regulatory Compliance:** Follow "Right to be Forgotten" requests (GDPR) or industry-specific shredding policies.
*   **Method:** Use secure deletion protocols so data cannot be recovered by unauthorized parties.
*   **Audit Trail:** Document when and why data was destroyed to prove compliance.

---

## Life Cycle vs. Analysis Process

| Framework | Primary Focus | Best Used For |
| :--- | :--- | :--- |
| **Data Life Cycle** | Data Management & Governance | IT, Data Engineering, Compliance |
| **Analysis Process** (Google/7-Step) | Problem Solving & Insights | Business Analysis, Research, Strategy |

---

## Summary Checklist
- [ ] **Plan:** Do we have a data dictionary and clear ownership?
- [ ] **Capture:** Is the data being pulled from the "Master" source?
- [ ] **Manage:** Is the data backed up and encrypted?
- [ ] **Analyze:** Have we answered the original business question?
- [ ] **Archive:** Is old data costing us too much in "Hot" storage?
- [ ] **Destroy:** Have we purged data that exceeds our retention policy?
