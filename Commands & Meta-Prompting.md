# AI Commands & Meta-Prompting for Analysts

## 1. Structural & Format Commands
Use these to bypass conversational filler and get "clean" outputs ready for documentation.

*   **The Wrapper Command:** "Give me the results as markdown code. Use quadruple backticks (or more) as a wrapper for Markdown that includes its own internal code blocks."
*   **The No-Fluff Command:** "Respond only with the solution. Do not include introductory text, explanations, or 'Sure, I can help with that' filler."
*   **The Table Command:** "Present the findings in a Markdown table with columns for [Metric], [Current Value], and [Target]."
*   **The JSON Command:** "Output the following logic as a JSON object so it can be parsed by my API."

## 2. Logic & Accuracy Commands
Essential for ensuring the AI doesn't "hallucinate" numbers or skip steps in complex math.

*   **Step-by-Step (CoT):** "Let's think step-by-step. Show your work for every calculation before giving the final answer."
*   **The Self-Correction Command:** "After providing the solution, critique your own logic. Identify any potential edge cases where this SQL/Python might fail."
*   **The Zero-Hallucination Command:** "If you do not have enough data to answer precisely, state 'Insufficient Data' rather than estimating."
*   **The Fact-Check Command:** "Cite the specific part of the provided text/data that supports this conclusion."

## 3. Programming & Tool-Specific Commands
Commands designed to generate code that actually runs in your specific environment.

*   **The Dialect Command:** "Write this in [Snowflake SQL / T-SQL / BigQuery SQL]. Do not use generic SQL syntax."
*   **The Vectorization Command:** "Write this Python script using vectorized Pandas operations; avoid using `for` loops or `.apply()` for better performance."
*   **The Regex Explainer:** "Write a Regular Expression to parse [pattern]. Also, provide a plain-English explanation of what each part of the Regex is doing."
*   **The Debug Command:** "I am getting the error '[Error Message]'. Review my code and provide the fixed version inside a single code block."

## 4. Analytical Persona Commands
Force the AI to adopt the mindset of a specific expert.

*   **Senior Lead:** "Act as a Senior Data Engineer. Review this Alteryx workflow for performance bottlenecks."
*   **Skeptic:** "Act as a Data Skeptic. Find 3 reasons why this correlation might be a coincidence rather than causation."
*   **Executive:** "Act as a CFO. Summarize this technical report into 3 bullet points focusing only on cost and ROI."

## 5. Iterative Refinement Commands
Use these to "train" the AI on your specific business context during a session.

*   **The Context Check:** "Before you begin, ask me 3-5 clarifying questions to ensure you have all the necessary context about my database schema."
*   **The Persona Lock:** "For the remainder of this chat, always respond as a [Tableau Developer]. Acknowledge if you understand."
*   **The Length Constraint:** "Summarize the above in exactly 50 words."

---

## Summary Checklist
- [ ] **Wrapper:** Did I use quadruple backticks to keep the markdown intact?
- [ ] **Persona:** Is the "Role" clearly defined?
- [ ] **Constraint:** Did I tell it what to avoid (e.g., "No subqueries")?
- [ ] **Format:** Is the output type (JSON, Table, CSV) specified?
- [ ] **Verification:** Did I ask it to "think step-by-step"?
