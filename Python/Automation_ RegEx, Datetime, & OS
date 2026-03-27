# Python Automation: RegEx, Datetime, & OS

### 1. Regular Expressions (re)
```python
import re

text = "Contact us at support@example.com or info@test.org"
emails = re.findall(r'[\w\.-]+@[\w\.-]+', text)

# Common Patterns:
# \d = digit, \w = alphanumeric, \s = whitespace
# + = 1 or more, * = 0 or more, ? = optional
```

### 2. Datetime Management
```python
from datetime import datetime, timedelta

now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S")) # Format to string

# Math with dates
yesterday = now - timedelta(days=1)
future = datetime.strptime("2025-12-31", "%Y-%m-%d") # String to object
```

### 3. OS & Pathlib (File System)
```python
import os
from pathlib import Path

# Create directory if missing
os.makedirs("new_folder", exist_ok=True)

# List files in directory
files = os.listdir(".")

# Modern path handling
p = Path("data/results.csv")
print(p.exists())
print(p.absolute())
```
