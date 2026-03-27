# Pandas Cheat Sheet: DataFrames and Series

### 1. Getting Started
Essential imports and data loading.

```python
import pandas as pd
import numpy as np

# Loading data
df = pd.read_csv('data.csv')       # From CSV
df = pd.read_excel('data.xlsx')   # From Excel
```

---

### 2. Inspecting Data
Quickly understand the structure and content of your DataFrame.

```python
df.head(5)       # View first 5 rows
df.tail(5)       # View last 5 rows
df.info()        # Data types, memory, and null counts
df.describe()    # Summary stats for numerical columns
df.shape         # (rows, columns)
df.columns       # List of column names
```

---

### 3. Selection and Filtering
How to grab specific rows and columns.

```python
# Selecting Columns
col = df['column_name']           # Single column (Series)
subset = df[['col1', 'col2']]     # Multiple columns (DataFrame)

# Selecting Rows/Cells
df.iloc[0]                        # Selection by position (first row)
df.loc[0, 'col_name']             # Selection by label (row index 0, specific column)

# Filtering
df[df['age'] > 30]                # Rows where age > 30
df[(df['age'] > 20) & (df['score'] < 50)]  # Multiple conditions
```

---

### 4. Data Cleaning
Handling missing values and renaming.

```python
df.rename(columns={'old': 'new'}) # Rename columns
df.dropna()                       # Drop rows with any NULL values
df.fillna(0)                      # Replace NULLs with 0
df['col'].astype(float)           # Change data type
```

---

### 5. Grouping and Aggregation
Summarizing data by categories.

```python
# Group by a column and calculate mean
df.groupby('category')['price'].mean()

# Multiple aggregations
df.groupby('category').agg({'price': 'sum', 'age': 'mean'})
```

---

### 6. Creating DataFrames
Building data from scratch.

```python
# From a Dictionary
data = {'Name': ['Alice', 'Bob'], 'Age': [25, 30]}
df = pd.DataFrame(data)

# Adding a new column
df['status'] = 'Active'
```
