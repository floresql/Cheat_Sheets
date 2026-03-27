# NumPy Cheat Sheet: Arrays and Vectorized Operations

### 1. Basics & Creation
Fundamental ways to initialize NumPy arrays.

```python
import numpy as np

# Creating Arrays
arr = np.array([1, 2, 3])            # From list
arr_2d = np.array([[1, 2], [3, 4]])  # 2D Array (Matrix)

# Fast Initialization
np.zeros((3, 4))                     # 3x4 array of zeros
np.ones((2, 2))                      # 2x2 array of ones
np.full((2, 2), 7)                   # 2x2 array filled with 7
np.eye(3)                            # 3x3 Identity matrix

# Sequences
np.arange(0, 10, 2)                  # 0 to 8, stepping by 2
np.linspace(0, 1, 5)                 # 5 values evenly spaced between 0 and 1
```

---

### 2. Inspecting Arrays
Checking the metadata of your data.

```python
arr.shape    # Dimensions (rows, cols)
arr.ndim     # Number of dimensions
arr.size     # Total number of elements
arr.dtype    # Data type (int64, float64, etc.)
```

---

### 3. Array Operations
Vectorized math (no loops required!).

```python
a = np.array([1, 2])
b = np.array([3, 4])

# Element-wise Math
a + b        # [4, 6]
a * b        # [3, 8]
a ** 2       # [1, 4]

# Statistics
np.mean(a)   # Average
np.median(a) # Median
np.std(a)    # Standard Deviation
arr.sum()    # Sum of all elements
```

---

### 4. Indexing & Slicing
Accessing and modifying data.

```python
arr = np.array([10, 20, 30, 40])

arr[0]       # First element (10)
arr[1:3]     # Slicing (20, 30)
arr[::-1]    # Reverse array

# 2D Slicing [row, col]
matrix = np.array([[1, 2], [3, 4]])
matrix[0, 1] # Row 0, Col 1 (Value: 2)
matrix[:, 0] # All rows, first column ([1, 3])
```

---

### 5. Reshaping & Manipulating
Changing the structure of data.

```python
# Change shape (must have same total elements)
arr = np.arange(6)       # [0, 1, 2, 3, 4, 5]
new_arr = arr.reshape((2, 3))

# Flattening
flat = new_arr.flatten()

# Transpose (Swap rows and columns)
matrix.T

# Joining
np.concatenate((a, b))   # Combine two arrays
```

---

### 6. Filtering & Boolean Logic
Using masks to select data.

```python
arr = np.array([1, 5, 10, 15])

mask = arr > 8           # [False, False, True, True]
filtered = arr[mask]     # [10, 15]

# Replace values based on condition
np.where(arr > 8, 1, 0)  # If > 8, return 1, else 0
```
