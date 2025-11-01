# 🐍 01_Basics — Python Fundamentals 

---

## 🎯 Objective

By the end of this section, you’ll:

* Understand the **core syntax** and **structure** of Python.
* Be able to write **basic scripts** for automation tasks.
* Know how to **run Python programs** on Linux or Windows.

---

## 🧩 1. Introduction to Python

**Python** is a high-level, interpreted, and object-oriented programming language.
It is widely used in **DevOps** for automation, scripting, CI/CD, and cloud operations.

### ✅ Why DevOps Engineers Use Python

* Automate repetitive tasks (e.g., deployment, backup)
* Integrate APIs (AWS, Docker, Kubernetes)
* Manage servers via SSH
* Write monitoring and reporting scripts

### Example:

```bash
# Run a Python script
python3 my_script.py
```

---

## ⚙️ 2. Python Setup

### 🖥️ Installing Python

* **Windows:** Download from [python.org/downloads](https://www.python.org/downloads/)
* **Linux:**

  ```bash
  sudo apt install python3
  ```
* **Verify installation:**

  ```bash
  python3 --version
  ```

---

## 🏗️ 3. Python Syntax & Indentation

Python uses **indentation (spaces or tabs)** to define code blocks instead of `{}`.

### Example:

```python
# Correct indentation
if True:
    print("Automation works!")

# Incorrect indentation
if True:
print("This will throw an error!")  # ❌ IndentationError
```

---

## 🧮 4. Variables and Data Types

### What are Variables?

Variables are **containers** for storing data.

### Example:

```python
name = "Dheeraj"
age = 25
is_devops = True
salary = 55000.50
```

### Data Types in Python:

| Type    | Example                             | Description        |
| ------- | ----------------------------------- | ------------------ |
| `int`   | `5`                                 | Integer            |
| `float` | `3.14`                              | Decimal number     |
| `str`   | `"AWS"`                             | Text/String        |
| `bool`  | `True` / `False`                    | Boolean            |
| `list`  | `[1,2,3]`                           | Ordered, mutable   |
| `tuple` | `(1,2,3)`                           | Ordered, immutable |
| `set`   | `{1,2,3}`                           | Unordered, unique  |
| `dict`  | `{"name":"DevOps","tool":"Docker"}` | Key-value pairs    |

---

## 🔄 5. Input and Output

### Input Example:

```python
name = input("Enter your name: ")
print("Welcome,", name)
```

### Output Example:

```python
tool = "Ansible"
print(f"{tool} is a popular configuration management tool.")
```

---

## 🔢 6. Type Conversion

You can convert between data types using casting functions.

### Example:

```python
num_str = "10"
num_int = int(num_str)
print(num_int + 5)  # Output: 15
```

---

## 🔠 7. Comments and Documentation

Comments are used to explain code.
They are ignored by the interpreter.

### Example:

```python
# This script prints a welcome message
print("Hello DevOps Engineer!")  # Inline comment
```

**Multi-line comment (docstring):**

```python
"""
This script connects to a remote server
and fetches system information.
"""
```

---

## ➗ 8. Operators

### Arithmetic Operators

```python
a = 10
b = 3
print(a + b)  # Addition
print(a - b)  # Subtraction
print(a * b)  # Multiplication
print(a / b)  # Division
print(a % b)  # Modulus
```

### Comparison Operators

```python
print(a == b)  # False
print(a > b)   # True
print(a != b)  # True
```

### Logical Operators

```python
x = True
y = False
print(x and y)  # False
print(x or y)   # True
print(not x)    # False
```

---

## 🧠 9. Strings and String Operations

### Example:

```python
msg = "Python for DevOps"
print(msg.upper())   # PYTHON FOR DEVOPS
print(msg.lower())   # python for devops
print(msg.split())   # ['Python', 'for', 'DevOps']
print(msg.replace("DevOps", "Automation"))  # Python for Automation
```

### String Formatting:

```python
name = "Dheeraj"
tool = "Docker"
print(f"{name} uses {tool} for container management.")
```

---

## 🧮 10. Example Script — DevOps Context

### Problem:

Write a Python script that takes a server name as input and prints a formatted message.

```python
# server_info.py
server = input("Enter server name: ")
print(f"Connecting to {server}... Please wait!")
```

**Output:**

```
Enter server name: prod-web01
Connecting to prod-web01... Please wait!
```

---

## 💻 11. Running Python Scripts in DevOps

In **Linux environments**, automation scripts often use a *shebang* line.

```python
#!/usr/bin/env python3
print("Script executed successfully!")
```

Make script executable:

```bash
chmod +x script.py
./script.py
```

---

## 🧰 12. Real DevOps Example — Check Python Version on Servers

```python
import os

# Check Python version
print("Checking Python version on local system...")
os.system("python3 --version")
```

**Use Case:**
You can extend this script to check Python installation across multiple servers using SSH automation.

---

## ✅ Summary

| Concept      | Key Point                   | Example               |
| ------------ | --------------------------- | --------------------- |
| Variables    | Store data                  | `x = 10`              |
| Data Types   | int, float, str, list, dict | `"Hello"`             |
| Input/Output | Take and print data         | `input()`             |
| Indentation  | Defines code block          | `if True: print()`    |
| Operators    | Perform actions             | `+`, `>`, `and`       |
| Comments     | Explain code                | `# This is a comment` |

---
