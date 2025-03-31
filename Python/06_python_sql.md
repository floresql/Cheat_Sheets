# 🛢️ Python for SQL Analysts Cheat Sheet

## 🔌 Connecting to SQL
```python
import pyodbc

conn = pyodbc.connect('DRIVER={SQL Server};SERVER=server;DATABASE=db;UID=user;PWD=password')
cursor = conn.cursor()
```

## 📄 Running Queries
```python
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

📚 Learn more: [SQLite in Python](https://docs.python.org/3/library/sqlite3.html)
