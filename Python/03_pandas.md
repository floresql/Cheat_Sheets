# 🐼 Pandas Cheat Sheet

## 📌 Description
High-performance data manipulation tool for tabular data. Use it when cleaning, transforming, or analyzing datasets.

## 📥 Importing
```python
import pandas as pd
df = pd.read_csv("file.csv")
```

## 🧾 Inspecting Data
```python
df.head()
df.info()
df.describe()
```

## 🎯 Selecting Data
```python
df["column"]
df[["col1", "col2"]]
df.loc[0]
df.iloc[0:5]
```

## 🧹 Filtering
```python
df[df["age"] > 30]
df[(df["gender"] == "F") & (df["age"] < 40)]
```

## 🧮 Aggregations
```python
df.groupby("department")["salary"].mean()
df["score"].sum()
```

## 🔧 Modifying Data
```python
df["bonus"] = df["salary"] * 0.1
df.rename(columns={"old": "new"}, inplace=True)
```

## 🔗 Merging & Joining
```python
pd.merge(df1, df2, on="id", how="left")
```
