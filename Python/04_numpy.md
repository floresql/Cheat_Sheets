# 🔢 NumPy Cheat Sheet

## 📌 Description
Core library for numerical operations in Python. Use it for math-heavy, vectorized computations.

## 📥 Importing
```python
import numpy as np
```

## 🔧 Creating Arrays
```python
arr = np.array([1, 2, 3])
zeros = np.zeros((2, 3))
ones = np.ones((2, 3))
range_arr = np.arange(0, 10, 2)
```

## 🔁 Array Operations
```python
arr + 5
arr1 + arr2
np.sqrt(arr)
```

## 🔄 Reshaping
```python
arr.reshape(3, 2)
arr.flatten()
```

## 🎯 Indexing & Slicing
```python
arr[0], arr[-1]
arr[1:4]
arr[:, 1]
```

## 🧮 Stats
```python
arr.mean(), arr.std(), arr.sum()
```
