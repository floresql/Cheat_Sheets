# Natural Language Querying (NLQ) — Prompting for SQL & Python

## 1. NLQ Prompting Framework: Analytical (RISEN)
To generate accurate code, the AI needs to understand your data "map" as much as your question.



| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **R** | **Role** | Define the technical persona. | "Act as a Senior Snowflake SQL Expert." |
| **I** | **Input** | Provide the Schema/Metadata. | "Table 'sales' has 'id', 'amt', and 'date'." |
| **S** | **Scenario** | The business logic context. | "We only consider 'completed' orders." |
| **E** | **Expectation**| The specific code goal. | "Calculate the 30-day retention rate." |
| **N** | **Nuance** | Dialect or style constraints. | "Use CTEs and avoid subqueries." |

---

## 2. Best Practices for SQL Generation (Text-to-SQL)
*   **Provide the Schema:** Never assume the AI knows your column names. Paste your `CREATE TABLE` statement or a list of column names and types.
*   **Specify the Dialect:** State if you need **PostgreSQL**, **MySQL**, **T-SQL**, or **BigQuery** syntax to avoid library errors.
*   **Define Complex Joins:** If your database uses cryptic IDs, tell the AI how tables relate (e.g., "Join 'users' to 'orders' on 'users.id = orders.user_id'").
*   **Ask for a "Dry Run":** Ask the AI to explain the logic of the query before providing the code to verify its understanding.

---

## 3. Best Practices for Python Generation (Text-to-Python)
*   **Declare Your Libraries:** Specify if you want to use **Pandas**, **Polars**, or **PySpark**.
*   **Commented Logic:** Request inline comments so you can audit the transformations.
*   **Error Handling:** Ask the AI to include `try-except` blocks or checks for empty dataframes.

```python
# Prompt: "Write a Pandas script to find the top 5 customers. Use 'df' as the dataframe."
# The AI output will be more reliable if you define the input name.
top_customers = df.groupby('customer_id')['spend'].sum().nlargest(5)
```

---

## 4. Advanced Techniques: Shot Prompting & Chain-of-Thought
*   **Few-Shot Prompting:** Provide 1-2 examples of "Question -> Correct SQL" to help the AI learn your specific business logic.
*   **Chain-of-Thought:** Use the phrase **"Let's think step-by-step"** to ensure the AI breaks down complex multi-step aggregations correctly.
*   **Iteration:** If the code fails, paste the error message back into the AI. It is often better at debugging than writing perfectly the first time.

---

## 5. Security & Guardrails Checklist
- [ ] **No Secrets:** Never paste real API keys or connection strings into a public LLM.
- [ ] **PII Masking:** Use "dummy" column names if your database contains sensitive personal info.
- [ ] **Read-Only:** Only execute AI-generated SQL on **Read-Only** database clones to prevent accidental deletions.
- [ ] **Limit Clause:** Always include a `LIMIT 100` in the prompt to prevent massive data pulls that crash your session.
- [ ] **Audit:** Manually review every JOIN and WHERE clause before execution.
