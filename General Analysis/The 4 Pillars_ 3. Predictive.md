# Predictive Analytics — The "What Will Happen?" Deep Dive

## 1. Core Objectives
Predictive analytics uses historical data and statistical algorithms to identify the likelihood of future outcomes. It shifts the focus from **historical reporting** to **probabilistic forecasting**.
*   **Forecasting:** Predicting future trends (e.g., Sales for next quarter).
*   **Propensity Modeling:** Scoring individuals on their likelihood to act (e.g., Churn, Purchase, Fraud).
*   **Risk Assessment:** Identifying potential future failures or bottlenecks.

---

## 2. Essential Predictive Techniques
Analysts select models based on the type of target variable they are trying to predict.


| Technique | Target Variable Type | Use Case Example |
| :--- | :--- | :--- |
| **Linear Regression** | Continuous Number | Predicting the specific dollar amount a customer will spend. |
| **Logistic Regression** | Binary (Yes/No) | Predicting if a customer will churn (1) or stay (0). |
| **Time Series (ARIMA)** | Time-based Trends | Forecasting inventory needs for the holiday season. |
| **Decision Trees** | Categorical/Numerical | Determining credit approval based on multiple "if/then" rules. |
| **Clustering (K-Means)** | Groupings | Segmenting customers into "High Value" vs. "Budget" groups. |

---

## 3. The Modeling Workflow
Predictive analytics follows a strict process to ensure the model is reliable and generalizes to new data.

1.  **Feature Engineering:** Creating variables that help the model learn (e.g., "Days Since Last Login").
2.  **Data Splitting:** Dividing data into **Training** (to build) and **Testing** (to validate).
3.  **Training:** Feeding the algorithm the training data to find patterns.
4.  **Evaluation:** Measuring accuracy using the test data.
5.  **Deployment:** Using the model to score new, incoming data.

---

## 4. Technical Implementation (Python & SQL)

### Python: Machine Learning Lifecycle
Python’s `scikit-learn` is the industry standard for building predictive models.

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# 1. Prepare Features (X) and Target (y)
X = df[['age', 'total_spend', 'days_since_last_login', 'support_tickets']]
y = df['did_churn']

# 2. Split into Train (80%) and Test (20%)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 3. Train the Model
model = RandomForestClassifier()
model.fit(X_train, y_train)

# 4. Evaluate Performance
predictions = model.predict(X_test)
print(f"Model Accuracy: {accuracy_score(y_test, predictions):.2%}")
```

### SQL: Scoring Data
Once a model is built, analysts often "score" new data directly in SQL using coefficients.

```sql
-- Scoring customers based on a simplified "Likelihood to Buy" formula
SELECT 
    customer_id,
    (0.5 * days_active) + (1.2 * page_views) - (2.0 * bounce_count) AS propensity_score
FROM web_activity
ORDER BY propensity_score DESC;
```

---

## 5. Model Evaluation Metrics
How do we know if our prediction is "Good"?

*   **RMSE (Root Mean Square Error):** For numbers. Measures the average distance between predicted and actual values.
*   **Precision:** For categories. "When the model says Yes, how often is it right?" (Avoids False Positives).
*   **Recall:** For categories. "Did we find all the actual Yes cases?" (Avoids False Negatives).
*   **R-Squared:** For regression. Tells you how much of the variance in the data is explained by your model.

---

## 6. Predictive Checklist
- [ ] **Data Quality:** Is my training data free of "future leakage" (data the model wouldn't have at the time of prediction)?
- [ ] **Validation:** Did I test the model on a "Hold-out" set it hasn't seen before?
- [ ] **Bias:** Does the training data represent the actual population we are predicting for?
- [ ] **Interpretability:** Can I explain *why* the model made a certain prediction?
- [ ] **Confidence:** Did I provide a range or probability, or just a single "guess"?
