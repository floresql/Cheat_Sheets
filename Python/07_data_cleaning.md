# 🧹 Python Data Cleaning Cheat Sheet

## 🔍 Missing Values
```python
df.isnull().sum()
df.dropna()
df.fillna(0)
```

## 🧪 `apply()` for Custom Logic
```python
df["col"] = df["col"].apply(lambda x: x.strip().lower())
```

## 🔠 String Cleanup
```python
df["col"] = df["col"].str.replace(",", "").str.upper()
```

## 🔢 Type Casting
```python
df["col"] = df["col"].astype(int)
```

## 🧽 Deduplication
```python
df.drop_duplicates(inplace=True)
```

📚 Learn more: [Pandas Cleaning Docs](https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html)
