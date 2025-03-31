# 🐞 Python Debugging & Logging Cheat Sheet

## 📌 Description
Track issues and errors in code. Use when troubleshooting, testing, or deploying apps.

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
