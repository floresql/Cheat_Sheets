# 🛢️ Python for SQL Analysts Cheat Sheet

## 📌 Description
Connect Python to databases and query with SQL. Ideal for integrating Python analysis with data warehouses or reporting layers.

## 🔌 Connecting to SQL
```python
import pyodbc
conn = pyodbc.connect('DRIVER={SQL Server};SERVER=server;DATABASE=db;UID=user;PWD=password')
```

## 📄 Running Queries
```python
cursor = conn.cursor()
cursor.execute("SELECT * FROM employees")
for row in cursor:
    print(row)
```

## 🐼 Load into Pandas
```python
import pandas as pd
df = pd.read_sql("SELECT * FROM employees", conn)
```

## 💾 SQLite Example
```python
import sqlite3
conn = sqlite3.connect("data.db")
pd.read_sql("SELECT * FROM my_table", conn)
```
