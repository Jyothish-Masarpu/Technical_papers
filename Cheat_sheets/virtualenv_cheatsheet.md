# Python Virtual Environments (`venv`) Cheatsheet

A virtual environment is like an isolated "bubble" for your Python project. It keeps your project's dependencies separate from other projects and your main system. This prevents version conflicts (e.g., Project A needs Django 3, but Project B needs Django 4).

## 1. Creating a Virtual Environment

Modern Python comes with a built-in tool called `venv`. You don't usually need to download anything extra!

Open your terminal or command prompt, navigate to your project folder, and run:

```bash
# Syntax: python -m venv <environment_name>
python -m venv myenv
```
*(Note: `myenv` is just a popular name for the folder it creates. You can name it `.venv` or `env` too.)*

## 2. Activating the Environment

You MUST activate the environment every time you work on your project. Your terminal prompt will usually change to show `(myenv)` when it's active.

**On Windows:**
```cmd
myenv\Scripts\activate
```

**On Mac / Linux:**
```bash
source myenv/bin/activate
```

## 3. Working Inside the Environment

Once activated, any Python package you install (using `pip`) will ONLY be installed inside this `myenv` folder, not on your whole computer.

```bash
# Check which Python is running (it should point to your myenv folder)
# Windows:
where python
# Mac/Linux:
which python
```

## 4. Deactivating

When you are done working on your project and want to leave the "bubble", just type:

```bash
deactivate
```
Your terminal will return to normal.

---
💡 **Pro Tip:** NEVER commit your virtual environment folder (like `myenv`) to GitHub. Add `myenv/` to your `.gitignore` file.