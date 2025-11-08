# 🔁 02_Control_Flow — Conditional Logic & Loops in Python

---

## 🎯 Objective

This module teaches how to **control the execution flow** of your Python scripts using:
- Conditional statements (`if`, `elif`, `else`)
- Loops (`for`, `while`)
- Loop control keywords (`break`, `continue`, `pass`)
- Real-world **DevOps use cases** — such as looping over servers, checking statuses, and conditional deployments.

---

## 🧠 1. What is Control Flow?

Control flow allows your program to **make decisions** and **repeat actions** based on conditions.

Example:
```python
if condition:
    do_something()
else:
    do_something_else()
````

---

## ⚙️ 2. Conditional Statements

### ➤ `if`, `elif`, `else`

```python
server_status = "running"

if server_status == "running":
    print("Server is healthy ✅")
elif server_status == "stopped":
    print("Server is down ❌")
else:
    print("Unknown status ⚠️")
```

💡 **DevOps Use Case:**
Check EC2 instance status and take actions accordingly.

---

### ➤ Nested Conditions

You can put one condition inside another.

```python
cpu_usage = 80
memory_usage = 90

if cpu_usage > 75:
    if memory_usage > 80:
        print("High CPU and memory load — scale up servers 🚀")
    else:
        print("Only CPU is high — monitor closely 👀")
```

---

### ➤ Shorthand `if` Expression

Used for short inline conditions.

```python
status = "up"
print("Server is up") if status == "up" else print("Server is down")
```

---

## 🔁 3. Loops — `for` and `while`

Loops allow you to **repeat actions** — very useful in **automation tasks**.

---

## ➤ `for` Loop

Used for iterating over a **sequence** (like list, tuple, or string).

```python
tools = ["Docker", "Jenkins", "Ansible"]

for tool in tools:
    print(f"Installing {tool}...")
```

💡 **DevOps Example:**
Iterate over multiple servers and run health checks.

```python
servers = ["web01", "db01", "cache01"]

for s in servers:
    print(f"Checking uptime for {s}...")
```

---

### ➤ `range()` Function

Used for numeric loops.

```python
for i in range(1, 4):
    print(f"Deploying service batch {i}...")
```

---

## ➤ `while` Loop

Runs **until a condition becomes False**.

```python
count = 0
while count < 3:
    print("Running build pipeline...")
    count += 1
```

💡 **Use Case:**
Keep retrying a deployment until success.

```python
attempt = 0
success = False

while not success and attempt < 3:
    print(f"Deployment attempt {attempt + 1}")
    success = True  # assume success for demo
    attempt += 1
```

---

## ⏹️ 4. Loop Control Statements

### ➤ `break` — Exit the loop early

```python
for i in range(1, 6):
    if i == 3:
        print("Stopping at 3")
        break
    print(i)
```

---

### ➤ `continue` — Skip the current iteration

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
```

---

### ➤ `pass` — Placeholder (does nothing)

```python
for i in range(5):
    pass  # to be implemented later
```

---

## 🔄 5. Using `else` with Loops

Python allows an optional `else` block after loops, which runs only if the loop **completes normally** (no `break`).

```python
for i in range(3):
    print(f"Checking node {i}")
else:
    print("All nodes checked successfully ✅")
```

---

## 🧰 6. DevOps Automation Examples

### ✅ Example 1: Check Server Status

```python
servers = {
    "web01": "running",
    "db01": "stopped",
    "cache01": "running"
}

for name, status in servers.items():
    if status == "running":
        print(f"{name} is healthy ✅")
    else:
        print(f"{name} is down ❌ — restarting service...")
```

---

### ✅ Example 2: Retry API Call Until Success

```python
import time

attempt = 0
max_attempts = 5
success = False

while attempt < max_attempts and not success:
    print(f"Attempt {attempt + 1}: Sending request to API...")
    # Simulate success in 3rd attempt
    if attempt == 2:
        success = True
        print("API call successful ✅")
    else:
        print("Failed — retrying in 2 seconds...")
        time.sleep(2)
    attempt += 1
```

---

### ✅ Example 3: Loop Over Docker Containers

```python
containers = ["nginx", "mysql", "redis"]

for c in containers:
    print(f"Checking logs for {c} container...")
```

---

### ✅ Example 4: Conditional Deployment Script

```python
env = "production"

if env == "production":
    print("Deploying to Production servers 🚀")
elif env == "staging":
    print("Deploying to Staging servers 🧪")
else:
    print("Unknown environment ❌")
```

---

## 🧩 7. Practical Exercises

1. **Server Health Checker**

   * Create a list of 5 servers with random statuses (`running`, `stopped`).
   * Loop through them and print whether each server is healthy or needs restart.

2. **Retry Logic Script**

   * Simulate 3 retry attempts for a failed deployment.
   * Use `while` loop and `break` once success is achieved.

3. **Even/Odd Counter**

   * Use a `for` loop to count even and odd numbers from 1–20.

4. **Tool Installation Automation**

   * Given a list `["Docker", "Ansible", "Jenkins"]`, print installation messages for each.

---

## 🧾 Summary

| Concept          | Description                   | Example                     |
| ---------------- | ----------------------------- | --------------------------- |
| `if-elif-else`   | Conditional branching         | `if status == "running":`   |
| `for` loop       | Iterates over sequences       | `for s in servers:`         |
| `while` loop     | Runs until condition is false | `while attempt < 3:`        |
| `break`          | Exit loop early               | Stop retrying               |
| `continue`       | Skip current iteration        | Skip failed servers         |
| `pass`           | Placeholder                   | Empty loop body             |
| `else` with loop | Executes if no `break` occurs | Check all servers completed |

---
