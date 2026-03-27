# PEP 8 — The Style Guide for Python Code (Complete)

## 1. Indentation, Tabs & Line Length
* **Indent:** Use ~~**4 spaces**~~ **1 tab** per level. Never mix tabs and spaces.
* **Maximum Line Length:** Limit code to **79 characters**; docstrings/comments to **72**.
* **Hanging Indents:** Continuation lines should align elements vertically or use a ~~4-space~~ tab indent.

```python
# Vertical alignment
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# Hanging indent (extra level to distinguish from body)
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
```

## 2. Imports
* Group imports: Standard library, Third-party, then Local. Use absolute imports.

```python
import os
import sys

# Third-party
import flask
import pandas as pd

# Local
from my_package import my_module
```

## 3. Whitespace & Operators
* Surround binary operators (`=`, `+`, `-`, `==`, `!=`, `in`, `is`, `and`, `or`) with one space.
* **Exceptions:** No spaces around `=` for keyword arguments or default parameter values.
* **Line Breaks:** Break *before* binary operators.

```python
# Good: Operator alignment
income = (gross_wages
          + taxable_interest
          - ira_deduction)

# Good: Keyword arguments
def complex_func(real, imag=0.0):
    return magic(r=real, i=imag)
```

## 4. Naming Conventions


| Entity | Convention | Example |
| :--- | :--- | :--- |
| **Packages** | short, lowercase, no underscores | `mypackage` |
| **Modules** | lowercase, underscores allowed | `my_module` |
| **Classes** | CapWords (PascalCase) | `UserProfile` |
| **Functions / Variables** | lowercase_with_underscores | `calculate_total()` |
| **Constants** | ALL_CAPS_WITH_UNDERSCORES | `MAX_TIMEOUT` |
| **Exceptions** | CapWords with "Error" suffix | `ConnectionError` |

## 5. Programming Recommendations
* **Singletons:** Always use `is` or `is not` for `None`.
* **Booleans:** Use truthiness for sequences (strings, lists).
* **String Methods:** Use `.startswith()` and `.endswith()` instead of slicing.

```python
# Good
if x is None:
    pass

if not my_list:
    print("List is empty")

if name.startswith('Py'):
    pass
```

## 6. Comments & Docstrings
* **Docstrings:** Use `"""Triple Double Quotes"""`.
* **Inline Comments:** Separate from code by at least two spaces.

```python
def get_user_id(username):
    """Retrieve the unique ID for a given username.
    
    Args:
        username (str): The name to lookup.
    Returns:
        int: The user's ID.
    """
    user_id = db.fetch(username)  # Inline comment
    return user_id
```

## 7. Closing Braces
* Closing braces can align with the first non-whitespace character of the last line or the first character of the starting line.

```python
# Option 1
my_list = [
    1, 2, 3,
    ]

# Option 2
my_list = [
    1, 2, 3,
]
```
