# 🔎 Python Regex Cheat Sheet

## 📌 Description
Find and manipulate text using patterns. Use in validation, extraction, or complex filtering.

## 📥 Importing
```python
import re
```

## 🔍 Basic Functions
```python
re.search(pattern, string)
re.match(pattern, string)
re.findall(pattern, string)
```

## 🧹 Replace with `sub`
```python
re.sub(r"\d+", "", "abc123")  # Output: 'abc'
```

## ⚙️ Patterns
- `\d` → digit
- `\w` → word character
- `.` → any character
- `*`, `+`, `?` → quantifiers
- `^`, `$` → start/end of string
- `[]` → character set
- `()` → capture group

## 🧪 Example
```python
pattern = r"\b[A-Za-z]+@\w+\.com\b"
emails = re.findall(pattern, text)
```
