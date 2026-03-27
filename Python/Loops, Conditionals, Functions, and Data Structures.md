# Python Basics: Loops, Conditionals, Functions, and Data Structures

### 1. Conditionals (`if`, `elif`, `else`)
Used to run code based on whether a condition is `True` or `False`.

```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
else:
    print("Grade: C")

# Logical Operators
if score > 70 and score <= 100:
    print("Passing grade")

# Ternary Operator (One-liner)
status = "Pass" if score >= 60 else "Fail"
```

---

### 2. Loops (`for`, `while`)
Loops repeat a block of code until a specific condition is met.

#### For Loops
```python
# Loop through a range (0 to 4)
for i in range(5):
    print(i)

# Loop through a list
items = ["apple", "banana", "cherry"]
for item in items:
    print(item)

# With index using enumerate
for index, item in enumerate(items):
    print(f"{index}: {item}")
```

#### While Loops
```python
count = 0
while count < 5:
    print(count)
    count += 1
```

#### Loop Control
- `break`: Stops the loop entirely.
- `continue`: Skips the current iteration.

---

### 3. Functions
Functions are reusable blocks of code defined with `def`.

```python
# Function with parameters and a default value
def greet(name, message="Hello"):
    return f"{message}, {name}!"

# Calling the function
print(greet("Alice"))           # Hello, Alice!
print(greet("Bob", "Welcome"))  # Welcome, Bob!

# Lambda (Anonymous) Functions
square = lambda x: x * x
print(square(5)) # 25
```

---

### 4. Data Structures (Lists, Dictionaries, Sets, Tuples)

#### Lists (Ordered, Changeable, Allows Duplicates)
```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")      # Add to end
fruits[1] = "blueberry"      # Change item
last_item = fruits.pop()     # Remove and return last item
```

#### Dictionaries (Key:Value Pairs, Ordered, Changeable)
```python
user = {"name": "Alice", "age": 25}
print(user["name"])          # Access value
user["email"] = "a@b.com"    # Add new pair
keys = user.keys()           # Get all keys
```

#### Sets (Unordered, Unindexed, No Duplicates)
```python
tags = {"python", "coding", "git"}
tags.add("python")           # Won't add (already exists)
is_coding = "coding" in tags # Check existence (True)
```

#### Tuples (Ordered, Unchangeable, Allows Duplicates)
```python
coordinates = (10.0, 20.0)
# coordinates[0] = 15.0      # Error! Tuples cannot be changed
point_x = coordinates[0]
```
