# Python General Cheatsheet

A comprehensive, professional reference guide covering Python operators, syntax, data types, collections, mutability, dictionaries, control flow, functions, file handling, and error management with extensive examples.

---

## 1. Getting Started & I/O

### Basic Input & Output
```python
# Standard print output
print("Hello, World!")
print("Python", "is", "awesome", sep="-")
print("Loading", end="...\n")

# Modern string formatting using f-strings
username = "Alice"
score = 95.5
print(f"User {username} achieved a score of {score}%")

# Taking user input (Always returns a string)
name = input("Enter your name: ")
age = int(input("Enter your age: "))  # Casting string input to integer
print(f"Hello {name}, next year you will be {age + 1} years old.")
```

### Comments
```python
# This is a single-line comment

"""
This is a multi-line string block 
commonly used as a docstring to document 
functions, classes, or modules.
"""
```

---

## 2. Python Operators

Python provides several built-in operator categories for computation, comparison, and logic.

### A. Arithmetic Operators
```python
a = 10
b = 3

print(a + b)   # Addition: 13
print(a - b)   # Subtraction: 7
print(a * b)   # Multiplication: 30
print(a / b)   # Division: 3.3333333333333335
print(a // b)  # Floor Division (rounds down): 3
print(a % b)   # Modulus (remainder): 1
print(a ** b)  # Exponentiation (10 to the power of 3): 1000
```

### B. Assignment & Augmented Assignment Operators
```python
x = 5       # Assigns 5 to x
x += 3      # Equivalent to x = x + 3 (x is now 8)
x -= 2      # Equivalent to x = x - 2 (x is now 6)
x *= 4      # Equivalent to x = x * 4 (x is now 24)
x /= 3      # Equivalent to x = x / 3 (x is now 8.0)
```

### C. Comparison Operators (Return True or False)
```python
p = 10
q = 20

print(p == q)   # Equal to: False
print(p != q)   # Not equal to: True
print(p > q)    # Greater than: False
print(p < q)    # Less than: True
print(p >= 10)  # Greater than or equal to: True
print(q <= 20)  # Less than or equal to: True
```

### D. Logical Operators
```python
is_logged_in = True
has_permission = False

print(is_logged_in and has_permission)  # Logical AND: False
print(is_logged_in or has_permission)   # Logical OR: True
print(not is_logged_in)                 # Logical NOT: False
```

### E. Membership & Identity Operators
```python
# Membership operators (in, not in)
fruits = ["apple", "banana", "cherry"]
print("banana" in fruits)      # True
print("grape" not in fruits)   # True

# Identity operators (is, is not) - checks if variables point to the exact same memory object
x = [1, 2, 3]
y = [1, 2, 3]
z = x
print(x is z)   # True (same memory reference)
print(x is y)   # False (different objects in memory despite same content)
```

---

## 3. Python Data Types & Type Checking

Python is dynamically typed. Use `type()` or `isinstance()` to inspect objects.

```python
# Core Built-in Types
x_int = 42              # int (Integer)
x_float = 3.14159       # float (Floating point)
x_str = "Data Science"  # str (String)
x_bool = False          # bool (Boolean)
x_none = None           # NoneType (Absence of value)

# Type Inspection & Casting
print(type(x_int))              # <class 'int'>
print(isinstance(x_float, float)) # True

# Explicit Type Conversion (Casting)
num_str = "250"
num_int = int(num_str)          # Converted to int: 250
num_float = float(num_str)      # Converted to float: 250.0
back_to_str = str(42)           # Converted to string: "42"
```

---

## 4. Mutable vs. Immutable Objects

* **Immutable:** Objects whose state **cannot** be modified after creation (`int`, `float`, `str`, `tuple`, `bool`). Any modification creates a brand new object in memory.
* **Mutable:** Objects whose content **can** be modified in-place after creation (`list`, `dict`, `set`).

### Summary Table

| Data Type | Category | Mutable? | Example Declaration |
| :--- | :--- | :--- | :--- |
| `int`, `float` | Numeric | **No** | `x = 10` |
| `str` | Sequence | **No** | `s = "hello"` |
| `tuple` | Sequence | **No** | `t = (1, 2, 3)` |
| `list` | Sequence | **Yes** | `l = [1, 2, 3]` |
| `dict` | Mapping | **Yes** | `d = {"key": "val"}` |
| `set` | Collection | **Yes** | `st = {1, 2, 3}` |

### Code Demonstration
```python
# 1. Immutable Demonstration (Strings)
name = "Python"
# name[0] = "J"  # TypeError: 'str' object does not support item assignment
name = "Jython"   # This works because we are reassigning the variable to a brand new string object

# 2. Mutable Demonstration (Lists)
scores = [80, 85, 90]
scores[0] = 95    # Modifies the list directly in-place; memory address remains identical
print(scores)     # Output: [95, 85, 90]
```

---

## 5. Collections & Data Structures

### A. Lists (`[...]`) — Ordered, Mutable, Allows Duplicates
```python
# Creating and modifying lists
colors = ["red", "green", "blue"]
colors.append("yellow")         # Adds to end: ["red", "green", "blue", "yellow"]
colors.insert(1, "purple")      # Inserts at index 1: ["red", "purple", "green", "blue", "yellow"]
colors.remove("green")          # Removes first matching item
popped_color = colors.pop()     # Removes and returns last item

# Slicing and indexing
print(colors[0])    # First item: "red"
print(colors[-1])   # Last item: "blue"
print(colors[1:3])  # Slice from index 1 to 2: ["purple", "green"]
```

### B. Tuples (`(...)`) — Ordered, Immutable
```python
# Useful for fixed data collections like coordinates or database records
point = (10.5, 20.2)
print(point[0])     # Accessing element: 10.5

# Tuple unpacking
x, y = point
print(f"X: {x}, Y: {y}")

# point[0] = 15.0   # Raises TypeError because tuples are immutable
```

### C. Sets (`{...}`) — Unordered, Unique Elements Only
```python
# Automatically removes duplicate elements
permissions = {"read", "write", "execute", "read"}
print(permissions)  # Output: {'read', 'write', 'execute'} (order may vary)

permissions.add("delete")
permissions.remove("write")

# Set operations
set_a = {1, 2, 3}
set_b = {3, 4, 5}
print(set_a.union(set_b))         # {1, 2, 3, 4, 5}
print(set_a.intersection(set_b))  # {3}
```

---

## 6. Mastering Dictionaries (`dict`)

Dictionaries store data as **`key: value` pairs**. Keys must be unique and immutable (like strings or numbers), while values can be any data type.

```python
# Creating a dictionary representing a user profile
employee = {
    "id": 1042,
    "name": "Sarah Connor",
    "department": "Engineering",
    "skills": ["Python", "Linux", "Docker"],
    "is_active": True
}

# 1. Accessing values
print(employee["name"])                 # "Sarah Connor"
print(employee.get("department"))       # "Engineering"
print(employee.get("salary", 50000))    # Returns default 50000 since "salary" key doesn't exist

# 2. Adding and modifying key-value pairs
employee["email"] = "sarah@company.com" # Adds new key-value pair
employee["department"] = "AI Research"  # Updates existing value

# 3. Removing elements
deleted_status = employee.pop("is_active")  # Removes key and returns its value
del employee["id"]                          # Deletes key directly

# 4. Dictionary methods & iteration
print(employee.keys())    # View all keys
print(employee.values())  # View all values

# Iterating over dictionaries
for key, value in employee.items():
    print(f"{key} -> {value}")
```

---

## 7. Control Flow

### A. Conditionals (`if`, `elif`, `else`)
```python
score = 82

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"

print(f"Final Grade: {grade}")
```

### B. For Loops
```python
# Iterating over sequence items
languages = ["Python", "JavaScript", "Rust"]
for lang in languages:
    print(f"Language: {lang}")

# Iterating using range(start, stop, step)
for i in range(1, 6, 2):  # Prints 1, 3, 5
    print(i)

# Iterating with index using enumerate()
for idx, lang in enumerate(languages):
    print(f"Index {idx}: {lang}")
```

### C. While Loops
```python
countdown = 3
while countdown > 0:
    print(f"Countdown: {countdown}")
    countdown -= 1
print("Liftoff!")
```

---

## 8. Functions

Functions encapsulate reusable logic blocks.

```python
# Defining a function with parameters, default values, and return value
def calculate_salary(base_rate, hours=40, bonus=0.0):
    """Calculates total weekly earnings."""
    regular_pay = base_rate * hours
    total = regular_pay + bonus
    return total

# Calling functions
pay1 = calculate_salary(25, 35, 200)  # Positional & keyword arguments
pay2 = calculate_salary(30)           # Uses default hours=40 and bonus=0.0
print(f"Pay 1: ${pay1}, Pay 2: ${pay2}")

# Lambda (Anonymous) Functions - Small inline one-line functions
multiply = lambda x, y: x * y
print(multiply(5, 4))  # Output: 20
```

---

## 9. File I/O & Exception Handling

### A. File Handling (`open()`)
```python
# Writing text to a file (creates or overwrites file)
with open("notes.txt", "w") as file:
    file.write("Line 1: Learn Python basics\n")
    file.write("Line 2: Practice data structures\n")

# Appending text to an existing file
with open("notes.txt", "a") as file:
    file.write("Line 3: Master database integrations\n")

# Reading from a file line by line
with open("notes.txt", "r") as file:
    content = file.read()
    print("--- File Contents ---")
    print(content)
```

### B. Exception Handling (`try`, `except`, `else`, `finally`)
```python
try:
    user_input = input("Enter a number to divide 100 by: ")
    number = float(user_input)
    result = 100 / number
except ValueError:
    print("Error: Please enter a valid number.")
except ZeroDivisionError:
    print("Error: Division by zero is not permitted.")
else:
    print(f"Success! Result is: {result}")
finally:
    print("Execution complete. Cleaning up resources.")
```