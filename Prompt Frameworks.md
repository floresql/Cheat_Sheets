# AI Prompting Frameworks for Analysts

## 1. The ROCE Framework
**Best For:** Standardizing technical requests and workflow optimizations.


| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **R** | **Role** | Define the persona. | "Act as an Alteryx Lead Developer." |
| **O** | **Objective** | The specific goal. | "Optimize this workflow for the AMP engine." |
| **C** | **Context** | Background info. | "The current workflow joins 5 tables from Snowflake." |
| **E** | **Expectation**| The final format. | "Provide a list of 5 specific tool changes." |

---

## 2. The RISEN Framework
**Best For:** Deep strategic research and complex data problem-solving.


| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **R** | **Role** | Define the persona. | "You are a Senior Business Analyst." |
| **I** | **Input** | The data or resources. | "I have a CSV of Q3 churn data." |
| **S** | **Scenario** | The specific situation. | "Competitors just launched a 50% discount." |
| **E** | **Expectation**| The desired outcome. | "Identify the top 3 segments likely to switch." |
| **N** | **Nuance** | Constraints or style. | "Keep it professional; avoid technical ML terms." |

---

## 3. The CARE Framework
**Best For:** Communicating results and drafting executive summaries.


| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **C** | **Context** | Project background. | "We just finished the year-end financial audit." |
| **A** | **Action** | The specific task. | "Summarize findings regarding operational spend." |
| **R** | **Result** | Goal of the response. | "Create a 3-bullet summary for the CFO." |
| **E** | **Example** | Tone or format sample. | "Use: [Category] - [Status] - [Delta]." |

---

## 4. The CODE Framework (Technical Tasks)
**Best For:** Generating SQL, Python, or automated logic.

```text
TASK: Write a Snowflake SQL query.
OBJECTIVE: Calculate 7-day rolling revenue per customer.
ENVIRONMENT: Table 'orders' with columns 'cust_id', 'order_date', and 'total'.
FORMAT: Use a Common Table Expression (CTE) and include inline comments.
```

---

## 5. Advanced Prompting Techniques

### Chain-of-Thought (CoT)
Forces the AI to "think step-by-step," reducing errors in math or logic.
*   **The Magic Phrase:** "Let's work through this step-by-step."
*   **Usage:** Essential when asking the AI to interpret a statistical result or debug complex code.

### N-Shot Prompting
Providing examples within the prompt to steer the AI toward a specific pattern.
*   **Zero-Shot:** "Write a Python script to clean this date column."
*   **One-Shot:** "Write a Python script. Example: [Input Format] -> [Cleaned Format]."
*   **Few-Shot:** Providing 3+ examples. (Best for complex parsing like Regex).

---

## 6. Analyst’s "Prompt Refinement" Checklist
- [ ] **Persona:** Did I tell the AI who it is (e.g., "Act as a Tableau Expert")?
- [ ] **Constraints:** Did I tell it what *not* to do (e.g., "Do not use subqueries")?
- [ ] **Format:** Did I specify the output (e.g., "Table," "Markdown," "JSON")?
- [ ] **Clarification:** Did I end with "Ask me 3 questions to ensure you have enough context"?
