# Python Arrays Cheatsheet

In Python, the term "array" usually refers to the built-in **`list`** data structure, which is a dynamic array. For strict, C-style typed arrays, Python provides the **`array`** module. For mathematical and scientific computing, **NumPy** arrays are the standard.

## Table of Contents
- [1. Python Lists (Dynamic Arrays)](#1-python-lists-dynamic-arrays)
- [2. Iterating & List Comprehensions](#2-iterating--list-comprehensions)
- [3. Multi-dimensional Arrays (Matrices)](#3-multi-dimensional-arrays-matrices)
- [4. The array Module (Strictly Typed Arrays)](#4-the-array-module-strictly-typed-arrays)
- [5. NumPy Arrays (Scientific Computing)](#5-numpy-arrays-scientific-computing)

---

## 1. Python Lists (Dynamic Arrays)

Lists are ordered, mutable (changeable), and can contain mixed data types.

### A. Creation & Initialization

```python
# Empty list
empty_list = []
empty_list_alt = list()

# List with initial values
numbers = [10, 20, 30, 40, 50]
mixed = [1, "Hello", 3.14, True]

# Initializing a list of a specific size with default values
zeros = [0] * 5          # [0, 0, 0, 0, 0]
```

### B. Accessing Elements (Indexing & Slicing)

```python
letters = ['a', 'b', 'c', 'd', 'e']

# Indexing (0-based)
print(letters[0])        # 'a' (First element)
print(letters[-1])       # 'e' (Last element - negative indexing)

# Slicing [start : stop : step] (stop is exclusive)
print(letters[1:4])      # ['b', 'c', 'd']
print(letters[:3])       # ['a', 'b', 'c'] (From beginning to index 2)
print(letters[2:])       # ['c', 'd', 'e'] (From index 2 to end)
print(letters[::-1])     # ['e', 'd', 'c', 'b', 'a'] (Reverses the list)
```

### C. Adding Elements

```python
fruits = ["apple", "banana"]

# append(): Adds a single element to the end
fruits.append("cherry")           # ["apple", "banana", "cherry"]

# insert(): Adds an element at a specific index
fruits.insert(1, "orange")        # ["apple", "orange", "banana", "cherry"]

# extend(): Appends elements from another list (or iterable)
fruits.extend(["mango", "kiwi"])  # ["apple", "orange", "banana", "cherry", "mango", "kiwi"]
```

### D. Removing Elements

```python
nums = [10, 20, 30, 40, 50, 20]

# remove(): Removes the first matching value
nums.remove(20)          # [10, 30, 40, 50, 20]

# pop(): Removes and returns the element at a specific index (default is last item)
last_item = nums.pop()   # Returns 20. List becomes: [10, 30, 40, 50]
first_item = nums.pop(0) # Returns 10. List becomes: [30, 40, 50]

# del: Deletes an element by index, or a slice
del nums[1]              # Removes 40. List becomes: [30, 50]

# clear(): Empties the entire list
nums.clear()             # []
```

### E. List Methods & Operations Summary

```python
lst = [3, 1, 4, 1, 5, 9]

length = len(lst)        # 6 (Number of elements)
count_1 = lst.count(1)   # 2 (Occurrences of value '1')
index_4 = lst.index(4)   # 2 (First index of value '4')

lst.sort()               # Sorts in ascending order in-place: [1, 1, 3, 4, 5, 9]
lst.sort(reverse=True)   # Sorts descending: [9, 5, 4, 3, 1, 1]
lst.reverse()            # Reverses the current order in-place
```

---

## 2. Iterating & List Comprehensions

### A. Looping Through a List

```python
colors = ["red", "green", "blue"]

# Standard for loop
for color in colors:
    print(color)

# Looping with index using enumerate()
for index, color in enumerate(colors):
    print(f"Index {index}: {color}")
```

### B. List Comprehensions

A concise, Pythonic way to create lists based on existing iterables.
**Syntax:** `[expression for item in iterable if condition]`

```python
# Create a list of squares
squares = [x**2 for x in range(1, 6)]  # [1, 4, 9, 16, 25]

# Filter a list (only even numbers)
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]

# Modify existing list
shouted = [color.upper() for color in colors] # ["RED", "GREEN", "BLUE"]
```

---

## 3. Multi-dimensional Arrays (Matrices)

You can create lists containing other lists to represent 2D arrays.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Accessing elements: matrix[row][column]
print(matrix[0][1])  # 2 (Row 0, Col 1)
print(matrix[2][2])  # 9 (Row 2, Col 2)

# Iterating through a 2D array
for row in matrix:
    for item in row:
        print(item, end=" ")
    print()
```

---

## 4. The array Module (Strictly Typed Arrays)

If you need a highly memory-efficient array of basic C-style types (like all integers or all floats), use the built-in `array` module.

```python
import array as arr

# 'i' stands for signed integer. All elements MUST be integers.
numbers = arr.array('i', [10, 20, 30])

# Accessing and modifying are identical to lists
print(numbers[0])     # 10
numbers.append(40)

# numbers.append("hello") # TypeError: integer argument expected, got str
```

*Common Type Codes:* `'i'` (signed int), `'I'` (unsigned int), `'f'` (float), `'d'` (double).

---

## 5. NumPy Arrays (Scientific Computing)

For heavy mathematical operations or large datasets, use the third-party `numpy` library. It is significantly faster and more memory-efficient than standard Python lists.

```python
# Requires installation: pip install numpy
import numpy as np

# Create a numpy array
np_arr = np.array([1, 2, 3, 4])

# NumPy allows vectorized operations (operations applied to every element)
print(np_arr * 2)      # [2 4 6 8]
print(np_arr + 10)     # [11 12 13 14]

# 2D NumPy Array
np_matrix = np.array([[1, 2], [3, 4]])
print(np_matrix.shape) # (2, 2)
```
