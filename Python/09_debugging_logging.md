# 🐞 Python Debugging & Logging Cheat Sheet

## 🔍 Try/Except Blocks
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Error:", e)
```

## 🐾 Logging
```python
import logging

logging.basicConfig(level=logging.INFO)
logging.info("This is an info message")
logging.error("Something went wrong!")
```

## 🔧 Debugging Tools
```python
import pdb; pdb.set_trace()
```

📚 Learn more: [Python Logging Docs](https://docs.python.org/3/library/logging.html)
