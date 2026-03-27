# Python Data Cleaning Cheat Sheet

### 1. Initial Assessment
Check for missing values and data inconsistencies.

```python
import pandas as pd
import numpy as np

# Quick summaries
df.isna().sum()              # Count missing values per column
df.duplicated().sum()        # Count exact duplicate rows
df['col'].value_counts()     # Check for inconsistent labels (e.g., "NY" vs "New York")
df.nunique()                 # Count of unique values per column
```

---

### 2. Handling Missing Data (NaNs)
Decide whether to remove or fill gaps.

```python
# Removing data
df.dropna()                  # Drop rows with any missing values
df.dropna(axis=1)            # Drop columns with any missing values
df.dropna(thresh=3)          # Keep rows with at least 3 non-NA values

# Filling data (Imputation)
df['col'].fillna(0)                     # Fill with a constant
df['col'].fillna(df['col'].mean())      # Fill with mean
df['col'].fillna(method='ffill')        # Forward fill (use previous value)
```

---

### 3. Data Type Conversion
Ensuring numbers are numbers and dates are dates.

```python
# Convert to numeric (coercing errors to NaN)
df['price'] = pd.to_numeric(df['price'], errors='coerce')

# Convert to datetime
df['date'] = pd.to_datetime(df['date'])

# Convert to category (saves memory for repetitive strings)
df['status'] = df['status'].astype('category')
```

---

### 4. Text Cleaning (Strings)
Standardizing string data.

```python
# Basic string operations
df['name'] = df['name'].str.strip()           # Remove whitespace
df['name'] = df['name'].str.lower()           # Lowercase
df['phone'] = df['phone'].str.replace('-', '') # Remove characters

# Extracting info with RegEx
df['zip'] = df['address'].str.extract(r'(\d{5})')
```

---

### 5. Outliers and Mapping
Cleaning values based on logic or thresholds.

```python
# Capping/Clipping outliers
df['age'] = df['age'].clip(lower=0, upper=100)

# Replacing values using a dictionary
mapping = {'M': 'Male', 'F': 'Female'}
df['gender'] = df['gender'].map(mapping)

# Conditional replacement with NumPy
df['score'] = np.where(df['score'] < 0, 0, df['score'])
```

---

### 6. Column & Row Formatting
Renaming and restructuring.

```python
# Renaming
df.columns = [c.lower().replace(' ', '_') for c in df.columns] # Standardize headers

# Resetting index after drops
df.reset_index(drop=True, inplace=True)

# Drop duplicates
df.drop_duplicates(subset=['user_id'], keep='first', inplace=True)
```
