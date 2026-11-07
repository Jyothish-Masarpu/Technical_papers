# Python Dictionaries Cheatsheet

A dictionary in Python stores information in **key:value** pairs. Think of it like a real-world dictionary where you look up a word (the key) to find its definition (the value). Keys must be unique and "hashable" (like strings or numbers).

---

## 1. Creating Dictionaries
Here are the most common ways to make a dictionary.

```python
# The standard way
student = {"name": "Ravi", "age": 21}

# Creating empty dictionaries
empty_dict = {}
another_empty = dict()

# Using zip (combining two lists)
from_zip = dict(zip(["a", "b"], [1, 2])) # Result: {'a': 1, 'b': 2}

# Dictionary comprehension (e.g., making squares)
squares = {n: n*n for n in range(1, 4)}  # Result: {1: 1, 2: 4, 3: 9}
```

*💡 **Pro Tip:** Be careful with `dict.fromkeys(["x", "y"], [])` if you plan to append to the lists later. All keys will share the exact same list!*

---

## 2. Accessing, Updating, and Deleting
How to get your data out, change it, or remove it.

```python
d = {"name": "Ravi", "age": 21}

# Accessing values
print(d["name"])          # Output: Ravi (Note: crashes with KeyError if key doesn't exist)
print(d.get("email"))     # Output: None (Safe way to access, doesn't crash)
print(d.get("email", "NA")) # Output: NA (Returns "NA" if key is missing)

# Adding and Updating
d["city"] = "Pune"        # Adds a new key-value pair
d["age"] = 22             # Updates an existing key
d.update({"age": 23})     # Updates multiple pairs at once

# Removing values
d.pop("age")              # Removes "age" and returns its value
d.popitem()               # Removes and returns the last inserted pair
del d["name"]             # Deletes the "name" key
d.clear()                 # Empties the entire dictionary
```

---

## 3. Looping Through Dictionaries
You can loop through keys, values, or both at the same time.

```python
marks = {"Math": 90, "Python": 95}

# Loop through keys (default behavior)
for key in marks:
    print(key) 

# Loop through values only
for value in marks.values():
    print(value)

# Loop through BOTH (super useful!)
for key, value in marks.items():
    print(key, value)
```

---

## 4. Math and Sorting
How to find the biggest, smallest, or total values.

```python
scores = {"A": 70, "B": 95, "C": 80}

# Min/Max (By default, this looks at the KEYS)
max(scores)               # Output: "C" (because alphabetically C is highest)
min(scores)               # Output: "A"

# Min/Max/Sum (Looking at the VALUES)
max(scores.values())      # Output: 95
sum(scores.values())      # Output: 245

# Find the KEY that has the highest VALUE
max(scores, key=scores.get) # Output: "B" (because B has 95)

# Sorting
sorted(scores.items())    # Sorts alphabetically by key
sorted(scores.items(), key=lambda x: x[1]) # Sorts by value
```

---

## 5. Common Coding Patterns
These are heavily used in interviews and coding tests.

### Frequency Counting (Counting how many times something appears)
```python
numbers = [1, 2, 2, 3, 1, 2]
freq = {}

for number in numbers:
    # Get current count (or 0 if not seen yet), then add 1
    freq[number] = freq.get(number, 0) + 1 
    
# Result: {1: 2, 2: 3, 3: 1}
```

### Grouping Values (Organizing items by a common trait)
```python
words = ["ant", "apple", "bat"]
groups = {}

for word in words:
    first_letter = word[0]
    if first_letter not in groups:
        groups[first_letter] = [] # Create an empty list first
    groups[first_letter].append(word)
    
# Result: {'a': ['ant', 'apple'], 'b': ['bat']}
```

---

## 6. Taking Keyboard Input
How to build a dictionary from user input.

```python
# Read 'n' number of key-value pairs from the user
n = int(input("How many entries? "))
data = {}

for _ in range(n):
    # Expecting input like: "Ravi 90"
    key, value = input().split() 
    data[key] = int(value)

# Example input: 
# 2
# Ravi 90
# Maya 95
# Resulting dictionary: {'Ravi': 90, 'Maya': 95}
```