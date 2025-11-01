# ⚙️ 04_Functions — Reusable and Modular Scripting in Python for DevOps

---

## 🎯 Objective

By the end of this section, you’ll be able to:
- Define and use **functions** effectively.
- Pass arguments and return data.
- Create **modular and reusable scripts**.
- Apply functions in **real DevOps automation** (AWS, Docker, Monitoring, etc.).

---

## 🧩 1. What is a Function?

**Definition:**  
A **function** is a reusable block of code that performs a specific task.  
Functions make scripts **modular, readable, and maintainable** — which is critical for large DevOps projects.

---

## 🧠 2. Syntax of a Function

```python
def function_name(parameters):
    # block of code
    return value
````

### Example:

```python
def greet():
    print("Welcome to Python for DevOps!")
```

**Call the function:**

```python
greet()
```

---

## 🧩 3. Function with Parameters

### Example:

```python
def greet_user(name):
    print(f"Hello {name}, welcome to the DevOps world!")
```

**Call:**

```python
greet_user("Dheeraj")
```

---

## 📤 4. Function with Return Values

Functions can **return values** to the caller using `return`.

```python
def add(a, b):
    return a + b

result = add(10, 20)
print("Sum:", result)
```

💡 **Use Case (DevOps):** Return a status code after performing an action.

```python
def check_service(status):
    if status == "running":
        return "Healthy ✅"
    else:
        return "Issue Detected ❌"

print(check_service("running"))
```

---

## ⚙️ 5. Types of Function Arguments

Python supports several types of arguments.

### ➤ Positional Arguments

```python
def deploy(env, version):
    print(f"Deploying version {version} to {env}")
    
deploy("production", "v2.3")
```

---

### ➤ Keyword Arguments

```python
deploy(env="staging", version="v2.3")
```

---

### ➤ Default Arguments

```python
def start_server(region="ap-south-1"):
    print(f"Starting server in region: {region}")

start_server()               # Uses default
start_server("us-east-1")    # Overrides default
```

---

### ➤ Variable-Length Arguments (`*args` and `**kwargs`)

#### `*args` — For multiple positional arguments

```python
def install_tools(*tools):
    for t in tools:
        print(f"Installing {t}...")

install_tools("Docker", "Jenkins", "Terraform")
```

#### `**kwargs` — For multiple keyword arguments

```python
def show_server_details(**server):
    for key, value in server.items():
        print(f"{key}: {value}")

show_server_details(name="web01", ip="192.168.1.10", status="running")
```

---

## 🔁 6. Scope of Variables

### Local vs Global

```python
count = 5  # global

def increase():
    count = 10  # local
    print("Inside function:", count)

increase()
print("Outside function:", count)
```

Output:

```
Inside function: 10
Outside function: 5
```

💡 Use `global` keyword to modify global variable if required (use cautiously).

---

## 💡 7. Lambda (Anonymous) Functions

**Definition:**
Lambda functions are **small, one-line anonymous functions** often used for short, simple operations.

```python
square = lambda x: x * x
print(square(4))
```

💡 **DevOps Use Case:**
Filter running servers quickly.

```python
servers = ["running", "stopped", "running", "terminated"]
running = list(filter(lambda s: s == "running", servers))
print("Active Servers:", running)
```

---

## 🧰 8. DevOps-Focused Examples

### ✅ Example 1: Check Server Health

```python
def check_health(server_name, status):
    if status == "running":
        print(f"{server_name} is healthy ✅")
    else:
        print(f"{server_name} is down ❌ - Restart required!")
```

**Call:**

```python
check_health("web01", "running")
check_health("db01", "stopped")
```

---

### ✅ Example 2: Automate EC2 Start/Stop (Simulated)

```python
def manage_ec2(action, instance_id):
    if action == "start":
        print(f"Starting EC2 instance {instance_id}")
    elif action == "stop":
        print(f"Stopping EC2 instance {instance_id}")
    else:
        print("Invalid action!")

manage_ec2("start", "i-0abc12345")
```

---

### ✅ Example 3: Disk Space Checker

```python
import random

def check_disk_space(server):
    usage = random.randint(50, 95)
    print(f"{server}: Disk usage = {usage}%")
    if usage > 85:
        print("⚠️ High Disk Usage - Cleanup Required!")

check_disk_space("prod-server-1")
```

---

### ✅ Example 4: Log Analyzer

```python
def count_errors(logs):
    error_count = 0
    for line in logs:
        if "ERROR" in line:
            error_count += 1
    return error_count

logs = [
    "INFO: Server started",
    "ERROR: Disk full",
    "INFO: Restart complete",
    "ERROR: Memory exceeded"
]

print("Total Errors:", count_errors(logs))
```

---

### ✅ Example 5: Dynamic Resource Allocator

```python
def allocate_resource(resource_type, quantity):
    print(f"Allocating {quantity} {resource_type}(s)...")
    return f"{quantity} {resource_type}(s) allocated successfully ✅"

result = allocate_resource("EC2 instance", 3)
print(result)
```

---

## 🧩 9. Nested Functions

You can define functions **inside other functions**.

```python
def devops_pipeline():
    def build():
        print("Building code...")
    def deploy():
        print("Deploying to server...")
    build()
    deploy()

devops_pipeline()
```

---

## ⚡ 10. Best Practices

✅ Keep functions **small and focused**
✅ Use **meaningful names** (e.g., `deploy_to_aws`, not `fun1`)
✅ Add **docstrings** for clarity
✅ Return values instead of printing whenever possible
✅ Avoid global variables
✅ Reuse functions across automation scripts

---

## 🧾 12. Summary

| Concept          | Description            | Example           |
| ---------------- | ---------------------- | ----------------- |
| Function         | Reusable block of code | `def func():`     |
| Arguments        | Pass values            | `def add(a,b)`    |
| Return           | Send value back        | `return x`        |
| Default args     | Predefined values      | `def f(x=10)`     |
| *args / **kwargs | Multiple args          | `def f(*a, **kw)` |
| Lambda           | One-line function      | `lambda x: x*2`   |
| Scope            | Variable visibility    | Local vs Global   |

---
