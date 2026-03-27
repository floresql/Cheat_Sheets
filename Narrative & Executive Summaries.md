# Narrative & Executive Summaries — Dashboard-to-Story Cheat Sheet

## 1. Executive Summary Framework: Strategic (CARE)
Use this structure to prompt an AI to translate complex dashboard data into "Business English."


| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **C** | **Context** | Background and raw data points. | "Q3 Sales grew 12% but Margin dropped 2%." |
| **A** | **Action** | The specific summary task. | "Identify the primary driver of the margin compression." |
| **R** | **Result** | Desired output format. | "Create a 3-bullet executive summary for the CEO." |
| **E** | **Example** | Sample of the tone. | "Use a 'Headline: [Insight]' format; avoid jargon." |

---

## 2. Converting Dashboard Data to Narrative
Don't just paste an image; paste the **summary statistics** or a **CSV export** for the best results.

### The "Data-to-Narrative" Prompt Pattern:
> "Analyze the following data from my Tableau dashboard. Provide a **One-Page Executive Summary** that answers: 
> 1. What is the 'Bottom Line' (the single most important takeaway)?
> 2. What are the top 3 drivers (the 'Why')?
> 3. What is the 'Next Best Action' (the 'So What')?"

---

## 3. The "So What?" Strategy (Prescriptive Summaries)
Executives care about the **implication**, not just the observation. 


| Instead of Reporting... | AI Should Summarize As... |
| :--- | :--- |
| "Churn is up 5% in the Midwest." | "Midwest churn increased 5%, posing a $200k revenue risk; recommend re-allocating Q4 ad spend to retention." |
| "AOV is $150 per user." | "AOV reached a record $150, driven by the new bundle strategy; suggest expanding this to the West region." |

---

## 4. Technical Prompting for Summaries (CODE Framework)
Use this when you need the AI to analyze a specific file or data block.

```text
TASK: Generate an Executive Summary from the attached performance report.
OBJECTIVE: Highlight why the 'Churn' metric deviated from the 2% target.
CONTEXT: We recently changed our subscription pricing model in January.
FORMAT: 
- BLUF (Bottom Line Up Front)
- 3 Bulleted Key Findings
- 1 Recommended Action
- Limit to 250 words total.
```

---

## 5. Refining the Tone & Style
*   **The "Inverted Pyramid":** Tell the AI to put the most important conclusion in the first sentence.
*   **The "BLUF" Method:** Ask for a **Bottom Line Up Front** section.
*   **Constraint Prompting:** "Explain this as if I have only 60 seconds to read it."
*   **Persona:** "Act as a Strategic Consultant for a Fortune 500 company."

---

## 6. Executive Summary Checklist
- [ ] **Clarity:** Did the AI remove technical jargon (e.g., "P-Value," "Standard Deviation")?
- [ ] **Accuracy:** Did I manually verify that the AI didn't "hallucinate" any numbers?
- [ ] **Actionable:** Does the summary end with a specific recommendation?
- [ ] **Brevity:** Is the summary truly "one-page" or "one-slide" compatible?
- [ ] **Alignment:** Does the summary answer the original business question?
