# Python Debugging and Logging Cheat Sheet

### 1. Simple Debugging (Print & Type)
Quick checks for values and data structures.

```python
# Print variable values
print(f"DEBUG: Current value of x is {x}")

# Check data type and available methods
print(type(my_var))
print(dir(my_var)) 

# Pretty print complex dictionaries/lists
from pprint import pprint
pprint(large_dictionary)
```

---

### 2. The Python Debugger (`pdb`)
Pause execution and inspect the environment interactively.

```python
import pdb

def complex_logic(a, b):
    # Set a breakpoint (execution stops here)
    breakpoint()  # Modern Python 3.7+ way
    # pdb.set_trace() # Older way
    
    result = a / b
    return result

# Common PDB Commands:
# n (next line) | s (step into function) | c (continue to end)
# p variable (print variable) | q (quit)
```

---

### 3. Error Handling (`try`, `except`, `finally`)
Preventing crashes and capturing specific error messages.

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
except ValueError:
    print("Error: Please enter a valid integer.")
except ZeroDivisionError as e:
    print(f"Error: Cannot divide by zero. Details: {e}")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
else:
    print(f"Success! Result is {result}")
finally:
    print("Execution complete (runs regardless of errors).")
```

---

### 4. Logging (The `logging` Module)
Better than `print()` for production; tracks events with timestamps and levels.

```python
import logging

# Basic Configuration
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s',
    filename='app.log', # Saves to file (remove to print to console)
    filemode='w'        # 'w' overwrites, 'a' appends
)

logging.debug("Detailed info for developers")
logging.info("General confirmation of program progress")
logging.warning("Something unexpected happened, but app still works")
logging.error("Serious problem; some functions failed")
logging.critical("Fatal error; program may shut down")
```

---

### 5. Inspecting Call Stacks
Find out exactly where an error originated in nested code.

```python
import traceback

try:
    # Some nested function call that fails
    1 / 0
except ZeroDivisionError:
    # Print the full path of the error
    traceback.print_exc()
```

---

### 6. Assertions
Sanity checks that throw an error if a condition is `False`.

```python
def calculate_age(year):
    assert year > 0, "Year must be a positive number!"
    return 2024 - year
```
