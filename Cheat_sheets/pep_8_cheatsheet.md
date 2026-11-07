# Python PEP-8 Style Guide Cheatsheet

PEP-8 is the official rulebook for formatting Python code. Following it makes your code look professional, clean, and easy for other developers to read. 

## 1. Naming Conventions (How to name things)

*   **Variables & Functions:** Use `snake_case` (all lowercase with underscores).
    *   *Good:* `user_age = 25`, `def calculate_total():`
    *   *Bad:* `UserAge = 25`, `def CalculateTotal():`
*   **Constants:** Use `ALL_CAPS_WITH_UNDERSCORES`.
    *   *Good:* `MAX_CONNECTIONS = 100`
*   **Classes:** Use `PascalCase` (Capitalize every word, no underscores).
    *   *Good:* `class UserAccount:`
    *   *Bad:* `class user_account:`

## 2. Indentation (Spacing)

*   Always use **4 spaces** for indentation.
*   **Never** mix tabs and spaces. Configure your code editor to convert tabs to 4 spaces automatically.

## 3. Maximum Line Length

*   Try to keep lines of code to a maximum of **79 characters**.
*   This makes it easier to read code side-by-side on smaller monitors. You can use parentheses `()` or backslashes `\` to break long lines.

## 4. Blank Lines

*   Use **two blank lines** to surround top-level functions and classes.
*   Use **one blank line** to surround methods inside a class.

```python
class MyClass:
    
    def first_method(self):
        pass
        
    def second_method(self):
        pass


def top_level_function():
    pass
```

## 5. Imports

*   Always put imports at the very top of the file.
*   Import things on separate lines.
*   Group them in this order:
    1. Standard library imports (e.g., `import os`, `import sys`)
    2. Third-party imports (e.g., `import requests`)
    3. Local application imports (e.g., `from my_folder import my_file`)

```python
# Good
import os
import sys

# Bad
import os, sys
```

## 6. Whitespace and Math

*   Add spaces around operators (`=`, `+`, `-`, `==`, etc.).
*   Add a space after commas, but not before.
*   Don't put extra spaces directly inside parentheses, brackets, or braces.

```python
# Good
total = (apples + oranges) * 2
my_list = [1, 2, 3]

# Bad
total=(apples+oranges)*2
my_list = [ 1 , 2 , 3 ]
```