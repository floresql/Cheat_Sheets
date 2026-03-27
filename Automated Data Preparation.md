# AI-Powered Automated Data Preparation Cheat Sheet

## 1. AI Prompting Framework: Prep-Specific (ROCE)
Use this structured approach when asking an LLM (ChatGPT, Claude, etc.) to handle your data wrangling.


| Letter | Component | Description | Example |
| :--- | :--- | :--- | :--- |
| **R** | **Role** | Define the AI's persona. | "Act as a Python Data Engineer." |
| **O** | **Objective** | The specific cleaning goal. | "Identify data types and suggest a cleaning strategy." |
| **C** | **Context** | Background and schema info. | "I have a messy 10k-row CSV of retail transactions." |
| **E** | **Expectation**| Desired output format. | "Provide a Python script with inline comments." |

---

## 2. Automated Identification & Type Casting
AI can scan a sample of your data to determine the "true" intent of a column beyond what a standard CSV reader sees.

**The Prompt:**
> "Analyze this data sample. For each column, identify the **intended data type** (e.g., Categorical, DateTime, Integer, Boolean) and flag any columns where the current format prevents analysis."

**The Code (Python/Pandas):**
```python
import pandas as pd

# Automated inference of data types
df = pd.read_csv('messy_data.csv')
df = df.convert_dtypes() # AI-like inference for best possible types

# Force specific cleaning based on AI suggestion
df['timestamp'] = pd.to_datetime(df['timestamp'], errors='coerce')
df['is_active'] = df['is_active'].map({'Yes': True, 'No': False, '1': True, '0': False})
```

---

## 3. Handling Missing Values (Imputation Strategy)
Ask the AI to suggest the best statistical method for filling gaps based on the column's distribution.

**The Prompt:**
> "Review the null counts for [Column_Name]. Based on the distribution, should I use **Mean**, **Median**, **Mode**, or a **Forward Fill**? Explain why and provide the code."

**The Code Snippet:**
```python
# Strategy: Median for skewed numerical data, Mode for categorical
df['price'] = df['price'].fillna(df['price'].median())
df['category'] = df['category'].fillna(df['category'].mode()[0])

# Strategy: Interpolation for Time-Series
df['sensor_reading'] = df['sensor_reading'].interpolate(method='linear')
```

---

## 4. Outlier Detection & Handling
AI can suggest the threshold for what constitutes an "outlier" in your specific business context.

**The Prompt:**
> "Using the **Interquartile Range (IQR)** method, write a script to flag outliers in the 'Transaction_Amount' column. Suggest whether I should **cap** them at the 95th percentile or **remove** them."

**The Code Snippet:**
```python
# IQR Method for Outlier Detection
Q1 = df['amount'].quantile(0.25)
Q3 = df['amount'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Capping (Winsorizing) instead of deleting
df['amount_clean'] = df['amount'].clip(lower=lower_bound, upper=upper_bound)
```

---

## 5. Summary Checklist: Automated Prep
- [ ] **Data Profiling:** Did the AI identify hidden nulls (e.g., "N/A", "0", or "?" strings)?
- [ ] **Constraint Check:** Are "ID" columns treated as Strings to prevent accidental math?
- [ ] **Methodology:** Did the AI explain *why* it chose Median over Mean for imputation?
- [ ] **Scalability:** Will the suggested cleaning script work on the full dataset or just the sample?
- [ ] **Audit Trail:** Is every automated change logged or kept in a separate 'cleaned' column?
