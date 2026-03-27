# Prescriptive Analytics — The "How Can We Make It Happen?" Deep Dive

## 1. Core Objectives
Prescriptive analytics is the final and most valuable stage of the analytical maturity model. It doesn't just predict the future; it recommends specific **actions** to achieve a desired outcome or mitigate a predicted risk.
*   **Optimization:** Finding the best way to allocate limited resources (Time, Budget, Inventory).
*   **Decision Automation:** Using logic-based engines to trigger actions without manual intervention.
*   **Strategy Testing:** Running "What-If" simulations to see the impact of different business decisions.

---

## 2. Essential Prescriptive Techniques
These methods turn "foresight" into "instructions."


| Technique | Definition | Use Case Example |
| :--- | :--- | :--- |
| **Linear Programming** | Mathematical modeling to find the best result under constraints. | Determining the cheapest delivery route that hits all 50 stops on time. |
| **Monte Carlo Simulation**| Running thousands of scenarios using random variables to see outcomes. | Testing how a 5% price increase affects total revenue across 10 different regions. |
| **Decision Trees** | A map of possible outcomes used to guide a specific choice. | Automatically approving a credit limit increase based on score and history. |
| **Heuristics / Rules** | Rule-based logic ("If X, then do Y") derived from data. | If a customer's churn score is >0.8, auto-send a 20% discount code. |

---

## 3. The Prescriptive Workflow
How to bridge the gap from a "Score" to an "Action."

1.  **Define the Objective:** What is the specific goal? (e.g., "Minimize Shipping Cost" or "Maximize Lifetime Value").
2.  **Define Constraints:** What are the limits? (e.g., "Budget is $10k," "Staff can only work 40 hours," "Warehouse is full").
3.  **Apply Logic/Algorithm:** Use an optimization solver or a business rules engine.
4.  **Feedback Loop:** Track the results of the recommended action to refine the rules.

---

## 4. Technical Implementation (SQL & Python)

### SQL: Rule-Based Recommendation Engine
Once a **Predictive Score** exists, SQL is used to categorize and prescribe the "Next Best Action."

```sql
-- Prescriptive: Automated Customer Retention Actions
WITH predicted_risk AS (
    SELECT 
        user_id, 
        churn_probability -- From Predictive Model
    FROM model_outputs
)
SELECT 
    user_id,
    CASE 
        WHEN churn_probability >= 0.90 THEN 'Tier 1: Personal Phone Call from Account Manager'
        WHEN churn_probability BETWEEN 0.70 AND 0.89 THEN 'Tier 2: High-Value Discount Email (25%)'
        WHEN churn_probability BETWEEN 0.50 AND 0.69 THEN 'Tier 3: Educational Content & Feature Tips'
        ELSE 'Tier 4: No Intervention (Standard Marketing)'
    END AS prescriptive_action
FROM predicted_risk;
```

### Python: What-If Simulation
Using Python to simulate how changing one variable (Price) affects another (Profit).

```python
import numpy as np

# Simulation: Impact of Price Increase on Profit
current_price = 100
units_sold = 1000
cost_per_unit = 60

def simulate_profit(price_increase_pct):
    new_price = current_price * (1 + price_increase_pct)
    # Assume 1% price increase leads to 2% drop in volume (Price Elasticity)
    new_units = units_sold * (1 - (price_increase_pct * 2))
    profit = (new_price - cost_per_unit) * new_units
    return profit

# Test a 10% price increase vs. a 5% increase
print(f"Profit at +10%: ${simulate_profit(0.10):,.2f}")
print(f"Profit at +5%:  ${simulate_profit(0.05):,.2f}")
```

---

## 5. Prescriptive Checklist
- [ ] **Actionable:** Does the result provide a clear "Do This" instruction, or just more data?
- [ ] **Feasible:** Is the recommendation possible within the current business constraints (Budget/Legal)?
- [ ] **Validated:** Have we run a "What-If" simulation to see the potential downside of this action?
- [ ] **Monitored:** Is there a way to track if the recommended action actually worked?
- [ ] **Ethical:** Does the automated decision-making logic avoid unfair bias or discrimination?
