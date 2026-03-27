# AI Commands for SQL & Python — Debugging & Refactoring

## 1. SQL Debugging & Optimization
Use AI to break down complex errors, optimize execution plans, and modernize legacy scripts for better readability and performance.


| Task | Prompt Strategy | Example Command |
| :--- | :--- | :--- |
| **Error Diagnosis** | Paste error + code. | "I am getting a 'Division by zero' error in this Snowflake SQL. Identify the problematic column and add a `NULLIF` fix." |
| **Refactoring** | Convert to CTEs. | "Rewrite this nested subquery using Common Table Expressions (CTEs) to improve readability and maintainability." |
| **Performance** | Optimize joins. | "This query is hitting a memory limit. Explain why and rewrite it using a more efficient join strategy or filtering logic." |
| **Dialect Swap** | Convert syntax. | "Translate this T-SQL (SQL Server) script to BigQuery Standard SQL, ensuring all date functions are compatible." |

```sql
-- AI Output: Refactored with CTEs for Performance
WITH FilteredSales AS (
    -- Filter early to reduce memory overhead
    SELECT 
        user_id, 
        amount 
    FROM raw_sales 
    WHERE transaction_date >= '2024-01-01'
),
UserTotals AS (
    SELECT 
        user_id, 
        SUM(amount) AS total_spend
    FROM FilteredSales
    GROUP BY 1
)
SELECT * FROM UserTotals WHERE total_spend > 5000;
```

---

## 2. Python Debugging & Refactoring
Leverage AI to vectorize slow loops, handle edge cases (Nulls/Inf), and adhere to PEP 8 standards.


| Task | Prompt Strategy | Example Command |
| :--- | :--- | :--- |
| **Vectorization** | Replace loops. | "Act as a Senior Python Dev. Rewrite this `for` loop using vectorized Pandas operations for a 10x speedup." |
| **Logic Cleanup** | Simplify conditions. | "Simplify this nested `if-else` logic using a dictionary mapping or a helper function to reduce cognitive load." |
| **Bug Fixing** | Handle Nulls/NaN. | "This function crashes when it encounters a NaN value. Update the code to handle missing values by filling them with the column mean." |
| **Standardization** | PEP 8 Alignment. | "Refactor this script to comply with PEP 8 naming conventions and add type hinting to the function signatures." |

```python
# AI Output: Refactored with Vectorization and Type Hinting
import pandas as pd

def calculate_discounted_price(df: pd.DataFrame, discount_rate: float) -> pd.Series:
    """
    Refactored from a loop to a vectorized Pandas operation.
    Handles potential NaN values by filling with 0.
    """
    return df['price'].fillna(0) * (1 - discount_rate)

# Usage
# df['new_price'] = calculate_discounted_price(df, 0.15)
```

---

## 3. Advanced Troubleshooting Commands
*   **The "Explain" Command:** "Explain this code line-by-line to a Junior Analyst so they understand the logic."
*   **The "Edge Case" Command:** "Identify 3 edge cases (e.g., empty strings, negative values) where this logic might fail and provide a robust fix."
*   **The "Dry Run" Command:** "Describe the expected output of this script given the following input data: [Paste Sample Data]."

---

## 4. Debugging Checklist
- [ ] **SQL:** Did I check for "Implicit Conversions" that slow down joins?
- [ ] **Python:** Did I avoid using `.apply()` for large datasets in favor of native Pandas methods?
- [ ] **Validation:** Did I verify the AI's logic on a small sample before running it on production data?
- [ ] **Security:** Did the AI accidentally suggest hardcoding a password or API key?
