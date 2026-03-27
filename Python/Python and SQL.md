# Python & SQL Connectivity Cheat Sheet

### 1. SQLite (Built-in Python Library)
Best for local, single-file databases without needing a server.

```python
import sqlite3

# Connect to a database (creates it if it doesn't exist)
conn = sqlite3.connect('my_database.db')
cursor = conn.cursor()

# Create a Table
cursor.execute('''CREATE TABLE IF NOT EXISTS users 
               (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)''')

# Insert Data (Using ? placeholders to prevent SQL Injection)
cursor.execute("INSERT INTO users (name, age) VALUES (?, ?)", ("Alice", 25))
conn.commit()

# Query Data
cursor.execute("SELECT * FROM users WHERE age > 20")
rows = cursor.fetchall()
for row in rows:
    print(row)

# Close connection
conn.close()
```

---

### 2. PostgreSQL (using `psycopg2`)
Standard for connecting Python to professional PostgreSQL servers.

```python
import psycopg2

# Establish connection
conn = psycopg2.connect(
    dbname="test_db", 
    user="postgres", 
    password="password", 
    host="127.0.0.1"
)
cur = conn.cursor()

# Execute and Fetch
cur.execute("SELECT version();")
db_version = cur.fetchone()
print(f"Connected to: {db_version}")

# Clean up
cur.close()
conn.close()
```

---

### 3. SQLAlchemy (ORM Approach)
The "Object-Relational Mapper" way to treat database tables as Python classes.

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Setup
engine = create_engine('sqlite:///example.db')
Base = declarative_base()

# Define Table Schema as a Class
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)

Base.metadata.create_all(engine)

# Add Data
Session = sessionmaker(bind=engine)
session = Session()
new_user = User(name='Bob')
session.add(new_user)
session.commit()
```

---

### 4. Integration with Pandas
Quickly move data between a SQL database and a DataFrame.

```python
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine('sqlite:///data.db')

# SQL to DataFrame
df = pd.read_sql_query("SELECT * FROM users", engine)

# DataFrame to SQL
df.to_sql('new_table', engine, if_exists='replace', index=False)
```

---

### 5. Essential SQL Syntax (Quick Ref)
Commonly used commands within your Python strings:


| Action | SQL Syntax |
| :--- | :--- |
| **Select** | `SELECT col1, col2 FROM table WHERE condition;` |
| **Insert** | `INSERT INTO table (col1) VALUES ('value');` |
| **Update** | `UPDATE table SET col1 = 'new' WHERE id = 1;` |
| **Delete** | `DELETE FROM table WHERE id = 1;` |
| **Join** | `SELECT * FROM t1 JOIN t2 ON t1.id = t2.id;` |
| **Order** | `SELECT * FROM table ORDER BY col1 DESC;` |
