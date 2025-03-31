# Data Quality Profiling Cheat Sheet

## Step 1: Gather Data
- **SQL Server (SSMS):** Use basic SELECT statements to extract data.
```sql
SELECT * FROM your_table WHERE created_date >= '2024-01-01';
```
- **Python (Pandas):**
```python
import pandas as pd
df = pd.read_csv("your_data.csv")
```
- **SSIS:** Use Data Flow Task to pull from source into staging.
- **Alteryx:** Input Data tool to connect and extract.
- **Excel/Tableau:** Import data from CSV, Excel, or database connectors.

---

## Step 2: Check for Missing or NULL Values
- **SQL Server:**
```sql
SELECT 
    COUNT(*) AS total_rows, 
    SUM(CASE WHEN column_name IS NULL THEN 1 ELSE 0 END) AS null_count
FROM your_table;
```
- **Python (Pandas):**
```python
missing_values = df.isnull().sum() / len(df) * 100
print(missing_values)
```
- **Tableau:** Use COUNTD([Column]) to compare distinct vs. total.

---

## Step 3: Identify Duplicates
- **SQL Server:**
```sql
SELECT column_name, COUNT(*) FROM your_table GROUP BY column_name HAVING COUNT(*) > 1;
```
- **Python (Pandas):**
```python
duplicates = df[df.duplicated()]
print(duplicates)
```
- **Tableau:**
```text
IF { FIXED [ID] : COUNT([ID]) } > 1 THEN "Duplicate" ELSE "Unique"
```

---

## Step 4: Check Data Type & Format Consistency
- **SQL Server:**
```sql
SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'your_table';
```
- **Python:**
```python
print(df.dtypes)
```
- **Excel:** Use Data Validation.
- **SSIS:** Use Data Profiling Task.

---

## Step 5: Detect Outliers and Anomalies
- **SQL Server:**
```sql
SELECT AVG(column_name) AS avg_val, STDEV(column_name) AS std_dev FROM your_table;
```
- **Python (Pandas + Seaborn):**
```python
import seaborn as sns
sns.boxplot(x=df["column_name"])
```
- **Tableau:** Use Box-and-Whisker Plot from "Show Me".

---

## Step 6: Validate Business Rules
- **SQL Server:**
```sql
SELECT * FROM your_table WHERE order_date > GETDATE();
```
- **Python:**
```python
invalid = df[df['order_date'] > pd.to_datetime("today")]
print(invalid)
```

---

## Step 7: Generate Reports
- **SSRS:** Build a custom report with missing values, duplicates, etc.
- **Excel:** Pivot tables to summarize profiling results.
- **Tableau:** Create a dashboard showing data quality KPIs.

---

## Tools Summary
- **Exploration:** SQL, Pandas, Tableau
- **Automation:** SSIS, Alteryx
- **Reporting:** SSRS, Tableau, Excel

---

### Next Steps:
- Automate checks in Alteryx or SSIS.
- Build Python script for reusable profiling.
- Create Tableau dashboard template to track data health.
