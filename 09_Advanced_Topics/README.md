# ⚡ 09_Advanced_Topics — Powerful Python Concepts for DevOps Automation

---

## 🎯 Objective

By the end of this chapter, you’ll understand and apply:
- **Iterators** and **Generators** for efficient data handling  
- **Decorators** for reusable functionality (logging, retries, authentication)  
- **Context Managers** for managing files, sessions, and resources  
- **Lambda functions, map, filter, reduce**  
- **Practical DevOps use cases** (config management, retries, resource cleanup)

---

## 🧠 1. Iterators

**Definition:**  
An **iterator** is an object that allows you to iterate (loop) over data one element at a time.

### Example:
```python
nums = [10, 20, 30]
it = iter(nums)

print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
````

💡 **Use Case:**
Process log lines, stream data from APIs, or handle huge datasets without loading all into memory.

---

## ⚙️ 2. Custom Iterator Example

```python
class Counter:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= self.end:
            value = self.current
            self.current += 1
            return value
        else:
            raise StopIteration

for num in Counter(1, 5):
    print(num)
```

Output:

```
1
2
3
4
5
```

💡 **Use Case:**
Iterate through server IDs, port numbers, or retry attempts in automation.

---

## 🔁 3. Generators

**Definition:**
A **generator** is a simpler way to create an iterator using the `yield` keyword.

### Example:

```python
def log_reader():
    for i in range(1, 4):
        yield f"Log entry {i}"

for log in log_reader():
    print(log)
```

Output:

```
Log entry 1
Log entry 2
Log entry 3
```

💡 **Use Case:**
Read large log files line by line without loading everything into memory.

---

## ☁️ 4. DevOps Example — Streaming Logs from a File

```python
def stream_logs(filename):
    with open(filename) as f:
        for line in f:
            yield line.strip()

for log_line in stream_logs("system.log"):
    print(log_line)
```

💡 Efficient for monitoring continuous logs (`tail -f` equivalent in Python).

---

## ⚡ 5. Lambda Functions

**Definition:**
A **lambda** is a small anonymous function defined using `lambda` keyword.

### Example:

```python
add = lambda a, b: a + b
print(add(5, 3))  # Output: 8
```

💡 **Use Case:**
Quick data filtering, mapping, or inline functions in DevOps scripts.

---

## 🔍 6. `map()`, `filter()`, and `reduce()`

```python
from functools import reduce

# map
servers = ["web", "db", "cache"]
upper = list(map(lambda s: s.upper(), servers))
print(upper)

# filter
nums = [1, 2, 3, 4, 5]
even = list(filter(lambda n: n % 2 == 0, nums))
print(even)

# reduce
total = reduce(lambda a, b: a + b, nums)
print(total)
```

💡 **Use Case:**
Filter active servers, sum up resource usage, or format lists in automation.

---

## 🧩 7. Decorators

**Definition:**
A **decorator** allows you to modify or extend a function’s behavior **without changing its code**.

### Example:

```python
def log_decorator(func):
    def wrapper():
        print("🔹 Starting function...")
        func()
        print("✅ Function completed.")
    return wrapper

@log_decorator
def deploy():
    print("🚀 Deploying application...")

deploy()
```

Output:

```
🔹 Starting function...
🚀 Deploying application...
✅ Function completed.
```

---

## 🛠️ 8. DevOps Example — Retry Decorator for Failed Operations

```python
import time

def retry(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(1, times + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"⚠️ Attempt {attempt} failed: {e}")
                    time.sleep(2)
            print("❌ All retry attempts failed.")
        return wrapper
    return decorator

@retry(3)
def connect_to_server():
    raise ConnectionError("Unable to reach server")

connect_to_server()
```

💡 **Use Case:**
Retry network/API/SSH operations automatically — common in DevOps automation.

---

## 🔐 9. DevOps Example — Logging Decorator

```python
def log_action(func):
    def wrapper(*args, **kwargs):
        print(f"📝 Executing {func.__name__}() ...")
        result = func(*args, **kwargs)
        print(f"✅ {func.__name__} completed.")
        return result
    return wrapper

@log_action
def update_config():
    print("🔧 Updating configuration file...")

update_config()
```

💡 **Use Case:**
Auto-log steps in CI/CD pipeline scripts.

---

## 🔒 10. Context Managers (`with` Statement)

**Definition:**
A **context manager** is used to manage resources like files, connections, or sessions safely.

### Example:

```python
with open("data.txt", "w") as file:
    file.write("Hello, DevOps!")
```

💡 Automatically closes the file — even if an error occurs.

---

## ⚙️ 11. Custom Context Manager

```python
class ConnectionManager:
    def __enter__(self):
        print("🔌 Connecting to server...")
        return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("🔌 Closing connection...")

with ConnectionManager():
    print("✅ Performing operations...")
```

Output:

```
🔌 Connecting to server...
✅ Performing operations...
🔌 Closing connection...
```

💡 **Use Case:**
Handle connections to databases, APIs, or remote servers.

---

## ☁️ 12. DevOps Example — Temporary File Manager

```python
import tempfile

with tempfile.NamedTemporaryFile(delete=True) as tmp:
    tmp.write(b"Temporary config data")
    tmp.seek(0)
    print(tmp.read())
```

💡 **Use Case:**
Create temp files during CI/CD builds or testing environments.

---

## 🧠 13. Comprehensions Recap (Short Syntax)

```python
# List comprehension
squares = [x**2 for x in range(5)]

# Dict comprehension
env_vars = {"PATH": "/usr/bin", "USER": "devops"}
env_upper = {k: v.upper() for k, v in env_vars.items()}

print(squares)
print(env_upper)
```

💡 **Use Case:**
Quickly transform or filter environment variables or config data.

---

## 🧾 14. Summary Table

| Concept               | Description               | DevOps Use Case       |
| --------------------- | ------------------------- | --------------------- |
| **Iterator**          | Loop through data         | Process logs, retries |
| **Generator**         | Memory-efficient iterator | Stream logs           |
| **Lambda**            | Small inline function     | Filter servers        |
| **map/filter/reduce** | Functional utilities      | Transform data        |
| **Decorator**         | Add features dynamically  | Logging, retry, auth  |
| **Context Manager**   | Manage resources safely   | Files, connections    |
| **Comprehension**     | Short syntax loops        | Transform configs     |

---
