# Python File I/O Cheat Sheet

### 1. Basic Text Files (`txt`, `log`)
Always use the `with` statement to ensure files are closed automatically.

```python
# Modes: 'r' (read), 'w' (write/overwrite), 'a' (append), 'r+' (read/write)

# Reading a file
with open('data.txt', 'r') as file:
    content = file.read()          # Read entire file as string
    # lines = file.readlines()     # Read as a list of lines

# Writing to a file (Overwrites existing content)
with open('output.txt', 'w') as file:
    file.write("Hello World\n")
    file.write("Second line\n")

# Appending to a file (Adds to the end)
with open('log.txt', 'a') as file:
    file.write("New log entry\n")
```

---

### 2. Working with JSON
Standard for configuration files and API data.

```python
import json

data = {"id": 1, "name": "Alice", "active": True}

# Writing JSON to a file (Serialization)
with open('user.json', 'w') as f:
    json.dump(data, f, indent=4)

# Reading JSON from a file (Deserialization)
with open('user.json', 'r') as f:
    user_data = json.load(f)
```

---

### 3. Working with CSV (Standard Library)
Best for simple CSV tasks without the overhead of Pandas.

```python
import csv

# Reading CSV
with open('data.csv', 'r') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row) # Each row is a list of strings

# Writing CSV
rows = [['Name', 'Age'], ['Bob', 30], ['Joe', 25]]
with open('output.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerows(rows)
```

---

### 4. File & Directory Management (`os` and `pathlib`)
Managing paths and checking for file existence.

```python
import os
from pathlib import Path

# Check if file exists
if os.path.exists('data.txt'):
    print("File found!")

# Get current working directory
cwd = os.getcwd()

# Join paths (cross-platform safe)
path = os.path.join('folder', 'subfolder', 'file.txt')

# Modern Pathlib approach
path = Path("folder/file.txt")
print(path.name)    # file.txt
print(path.stem)    # file
print(path.suffix)  # .txt
print(path.parent)  # folder
```

---

### 5. Binary Files & Pickling
For saving and loading complex Python objects directly.

```python
import pickle

# Save/Dump object to binary file
my_list = [1, 2, 3, {"key": "val"}]
with open('data.pkl', 'wb') as f:
    pickle.dump(my_list, f)

# Load object from binary file
with open('data.pkl', 'rb') as f:
    loaded_list = pickle.load(f)
```
