# 📂 Python File I/O Cheat Sheet

## 📌 Description
How to read/write files in different formats. Use for loading data or saving outputs.

## 📄 Read/Write CSV
```python
import pandas as pd
df = pd.read_csv("data.csv")
df.to_csv("out.csv", index=False)
```

## 📘 Read/Write Excel
```python
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")
df.to_excel("output.xlsx", index=False)
```

## 📃 Read JSON
```python
df = pd.read_json("data.json")
```

## 📁 Plain Text Files
```python
with open("file.txt", "r") as file:
    content = file.read()
```
