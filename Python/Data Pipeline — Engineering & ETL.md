# Python Data Pipeline — Engineering & ETL Cheat Sheet

## 1. Extract: Efficient Data Ingestion
Focus on reducing memory overhead and handling large files by processing in chunks or streams.

```python
import pandas as pd
import json

# Efficient CSV Loading: Process in chunks to avoid RAM overflow
def extract_csv_in_chunks(file_path, chunk_size=10000):
    for chunk in pd.read_csv(file_path, chunksize=chunk_size):
        yield transform(chunk)  # Pass to next step in pipeline

# Efficient JSON Loading: Streaming large nested files
def extract_json_stream(file_path):
    with open(file_path, 'r') as f:
        for line in f:
            yield json.loads(line)
```

---

## 2. Transform: Vectorization & Logic
Move away from slow `for` loops and toward high-performance vectorized operations.


| Technique | Method | Benefit |
| :--- | :--- | :--- |
| **Vectorization** | `df['col'] * 1.1` | Uses C-level optimization; 100x faster than loops. |
| **Broadcasting** | `df['total'] - df['cost']` | Efficiently applies operations across entire arrays. |
| **Mapping** | `df['cat'].map(dict)` | Rapidly replaces categorical values using a hash map. |
| **Type Casting** | `df.astype('category')` | Reduces memory usage by up to 90% for repetitive strings. |

```python
def transform_data(df: pd.DataFrame) -> pd.DataFrame:
    # Vectorized cleaning
    df['timestamp'] = pd.to_datetime(df['timestamp'], errors='coerce')
    df['margin'] = (df['revenue'] - df['cost']) / df['revenue'].replace(0, 1)
    
    # Downcasting for memory efficiency
    df['status'] = df['status'].astype('category')
    return df.dropna(subset=['timestamp'])
```

---

## 3. Load: Database Integrity & Performance
Ensure data is written efficiently and handles failures without corrupting the destination.

```python
from sqlalchemy import create_engine

# Batch Loading into SQL
engine = create_engine('postgresql://user:pass@host:port/db')

def load_to_postgres(df: pd.DataFrame, table_name: str):
    # 'append' adds data; 'replace' drops table first
    # method='multi' improves speed for large inserts
    df.to_sql(table_name, engine, if_exists='append', index=False, method='multi')
```

---

## 4. Pipeline Resilience (Decorators & Logging)
Use standard Python modules to handle network retries and track pipeline health.

```python
import logging
import time
from functools import wraps

# Setup Logging
logging.basicConfig(level=logging.INFO, filename='pipeline.log')

# Retry Decorator for API/DB connections
def retry(exceptions, tries=3, delay=2):
    def decorator(f):
        @wraps(f)
        def wrapper(*args, **kwargs):
            for i in range(tries):
                try:
                    return f(*args, **kwargs)
                except exceptions as e:
                    logging.warning(f"Attempt {i+1} failed: {e}")
                    time.sleep(delay)
            return f(*args, **kwargs)
        return wrapper
    return decorator
```

---

## 5. Pipeline Architecture Checklist
- [ ] **Idempotency:** If I run this script twice on the same data, does it create duplicates? (Use `upsert` or `delete-then-insert`).
- [ ] **Atomicity:** Does the pipeline fail "gracefully" so that a partial load doesn't ruin the database?
- [ ] **Environment Variables:** Are database credentials stored in a `.env` file rather than hardcoded?
- [ ] **Logging:** Can I tell exactly where a failure occurred without opening the code?
- [ ] **Type Hinting:** Are function inputs and outputs clearly defined for future maintenance?

---

## 6. Recommended Standard Library Tools
*   **`pathlib`**: Better than `os.path` for handling cross-platform file paths.
*   **`itertools`**: Efficient looping and memory-friendly data manipulation.
*   **`datetime`**: The standard for timezone-aware date handling.
*   **`configparser`**: For managing configuration files (credentials, file paths).
