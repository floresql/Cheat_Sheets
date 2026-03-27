# Data & Business Analyst — General Best Practices

## 1. Problem Definition (The "Why")
*   **The Stakeholder "Why":** Never start a project without a clear business question. Ask: "What decision will be made based on this data?"
*   **KPI Alignment:** Ensure your metrics (Primary vs. Secondary) actually track the business objective, not just "vanity" numbers (e.g., use *Conversion Rate* instead of just *Page Views*).
*   **Success Criteria:** Define what "good" looks like before you analyze.

## 2. Data Quality & Integrity
*   **GIGO (Garbage In, Garbage Out):** Always validate your row counts, null values, and data types before starting analysis.
*   **Source of Truth:** Identify which system is the "Master" (e.g., CRM vs. Finance ERP) to avoid conflicting numbers.
*   **Documentation:** Maintain a Data Dictionary. Define what "Active User" or "Gross Margin" means so everyone is using the same language.
*   **Sanity Checks:** Compare aggregated totals against high-level reports from the previous month to ensure logical consistency.

## 3. Analysis Workflow & Accuracy
*   **Segmented Analysis:** Never rely solely on averages; they hide the "tails" of your data. Break data down by region, cohort, or behavior.
*   **Edge Case Identification:** Actively look for "Test" accounts, "Internal" IP addresses, and outliers that can skew results.
*   **Reproducibility:** Write clean, commented code. If you perform a task in Excel, document the steps so someone else can replicate the exact same result.

## 4. Visual Communication & Storytelling
*   **Headline-Driven Insights:** Instead of titling a chart "Monthly Sales," use "Sales Increased 12% in March due to Promo X."
*   **Data-Ink Ratio:** Remove unnecessary gridlines, borders, and bold colors that don't represent actual data.
*   **Cognitive Load:** Stick to 3–4 key takeaways per dashboard. Don't force users to "work" to find the answer.

## 5. Analyst Soft Skills


| Skill | Best Practice |
| :--- | :--- |
| **Skepticism** | If the data looks too good to be true, it’s probably a tracking bug. |
| **Communication** | Translate "P-values" and "Standard Deviations" into "Business Risk" and "Confidence." |
| **Curiosity** | Don't just report that sales are down; dig into *which* region or product is driving it. |
| **Iteration** | Treat your first dashboard as a draft. Get user feedback early and often. |
| **Empathy** | Understand the stakeholder's pressure. Are they trying to save costs or grow revenue? |

## 6. The "Analyst's Toolbox" Logic
*   **Excel:** Best for quick "what-if" modeling and small, ad-hoc data cleaning.
*   **SQL:** Best for large-scale data extraction and transformation (The Foundation).
*   **Tableau/PowerBI:** Best for recurring, interactive storytelling and monitoring.
*   **Python/R:** Best for advanced statistics, automation, and machine learning.

## 7. Data Privacy & Ethics
*   **Anonymization:** Always mask PII (Personally Identifiable Information) like names, emails, and phone numbers in your working datasets.
*   **Avoid Confirmation Bias:** Don't go looking for data that proves your boss's "hunch"; look for the truth, even if it's uncomfortable.
*   **Compliance:** Be aware of GDPR, CCPA, or internal retention policies before storing sensitive data locally.

## 8. Final Checklist before Presenting
1. [ ] **Verification:** Did I double-check my totals against a known source?
2. [ ] **Visuals:** Are my axes labeled and do they start at zero (unless there's a reason not to)?
3. [ ] **Objective:** Did I answer the original business question?
4. [ ] **Hierarchy:** Is the most important insight the biggest thing on the page?
5. [ ] **Actionable:** Did I include a "Next Best Action" recommendation?
