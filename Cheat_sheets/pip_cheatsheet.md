# Python `pip` Cheatsheet

`pip` is Python's package installer. Think of it as the App Store for Python. It allows you to download and install code libraries written by other people (like `requests`, `numpy`, or `django`).

*Note: Always make sure your virtual environment is activated before running these commands!*

## 1. Installing Packages

```bash
# Install the latest version of a package
pip install requests

# Install a specific version
pip install requests==2.28.1

# Upgrade an already installed package to the latest version
pip install --upgrade requests
```

## 2. Uninstalling Packages

```bash
# Remove a package you no longer need
pip uninstall requests
```
*(It will ask you to confirm with `y/n`)*

## 3. Seeing What is Installed

```bash
# Show a nice, readable list of installed packages and versions
pip list

# Show installed packages in a specific format meant for machines
pip freeze
```

## 4. The Magic of `requirements.txt`

When you share your code, you don't share your downloaded packages. Instead, you share a list of what packages your code needs to run.

**To create the list (Do this before sharing your code):**
```bash
# This saves the output of pip freeze into a text file
pip freeze > requirements.txt
```

**To install from the list (Do this when you download someone else's code):**
```bash
# This reads the text file and installs everything in it
pip install -r requirements.txt
```

## 5. Getting Help

```bash
# Show details about a specific package
pip show requests
```