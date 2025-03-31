# 🧱 Python Data Structures Cheat Sheet

## 📌 Description
Overview of core data containers in Python. Use this when organizing or transforming collections of data.

## 🧾 Lists
Ordered, mutable sequences.
```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
fruits[1] = "kiwi"
```

## 🧾 Tuples (Immutable)
Fixed-size, ordered collection.
```python
point = (3, 4)
x, y = point
```

## 🧾 Sets (Unique values)
Fast membership checks, no duplicates.
```python
unique_numbers = {1, 2, 3}
unique_numbers.add(4)
```

## 🧾 Dictionaries (Key-Value Pairs)
Flexible mapping structures.
```python
person = {"name": "Alice", "age": 30}
person["age"] += 1
```

## 🔁 Loops with Collections
```python
for fruit in fruits:
    print(fruit)

for key, value in person.items():
    print(key, value)
```
