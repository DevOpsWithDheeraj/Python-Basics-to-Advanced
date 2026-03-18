# 📂 06_File_Handling — Reading, Writing & Managing Files in Python for DevOps

## 🧠 1. What is File Handling?

**Definition:**  
File handling allows Python programs to **create, read, write, and delete files** on your system.  
In DevOps, this is vital for managing:

- Log files  
- Configuration files (JSON/YAML)  
- Deployment outputs  
- Backup data

---

## 🧩 2. File Handling Modes in Python

| Mode | Description |
|------|--------------|
| `'r'` | Read (default) |
| `'w'` | Write (overwrite existing content) |
| `'a'` | Append (add new data at end) |
| `'x'` | Create a new file (error if exists) |
| `'r+'` | Read and write |
| `'b'` | Binary mode (e.g., `'rb'`, `'wb'`) |

---

## 🧩 3. Basic File Operations

### ➤ Writing to a File

```python
file = open("devops_notes.txt", "w")
file.write("Python makes DevOps automation easy!\n")
file.write("Logging and monitoring are essential.\n")
file.close()
````

---

### ➤ Reading from a File

```python
file = open("devops_notes.txt", "r")
content = file.read()
print(content)
file.close()
```

Output:

```
Python makes DevOps automation easy!
Logging and monitoring are essential.
```

---

### ➤ Appending to a File

```python
file = open("devops_notes.txt", "a")
file.write("Always secure your servers.\n")
file.close()
```

---

## 🧩 4. Using `with open()` — Context Manager

Using `with` automatically closes the file even if an error occurs.

```python
with open("servers.txt", "w") as file:
    file.write("web01\n")
    file.write("db01\n")
    file.write("cache01\n")

with open("servers.txt", "r") as file:
    print(file.read())
```

💡 **Why Use It:**
Prevents file corruption and resource leaks — especially important in **long-running automation scripts**.

---

## 📋 5. Reading Files Line by Line

```python
with open("servers.txt", "r") as f:
    for line in f:
        print(line.strip())
```

💡 **Use Case:**
Loop through a list of servers from a file and run automation commands.

---

## 🧩 6. Checking if a File Exists

```python
import os

if os.path.exists("servers.txt"):
    print("File exists ✅")
else:
    print("File not found ❌")
```

---

## ⚙️ 7. DevOps Example — Log File Analysis

```python
with open("system.log", "r") as log:
    error_count = 0
    for line in log:
        if "ERROR" in line:
            error_count += 1

print(f"Total Errors Found: {error_count}")
```

💡 **Real-World Use:**
Monitor application or system logs and trigger alerts on high error counts.

---

## 📦 8. Handling JSON Files (Configuration Management)

JSON is heavily used for **configurations** in DevOps tools like Terraform, AWS CLI, and Docker.

### ➤ Writing JSON Data

```python
import json

config = {
    "app_name": "web_app",
    "version": "1.0",
    "servers": ["web01", "web02"],
    "region": "ap-south-1"
}

with open("config.json", "w") as file:
    json.dump(config, file, indent=4)
```

---

### ➤ Reading JSON Data

```python
import json

with open("config.json", "r") as file:
    data = json.load(file)

print("App Name:", data["app_name"])
print("Servers:", data["servers"])
```

💡 **Use Case:**
Automate deployments based on configuration files.

---

## 🧩 9. Handling YAML Files (Common in DevOps)

YAML is used in **Ansible, Kubernetes, and CI/CD** tools.

### ➤ Install PyYAML

```bash
pip install pyyaml
```

### ➤ Example

```python
import yaml

# Writing YAML
config = {
    'app': 'nginx',
    'replicas': 3,
    'env': ['staging', 'production']
}

with open("deployment.yaml", "w") as f:
    yaml.dump(config, f)

# Reading YAML
with open("deployment.yaml", "r") as f:
    data = yaml.safe_load(f)
    print("App:", data['app'])
```

💡 **Use Case:**
Update Kubernetes YAML files dynamically before deployment.

---

## 🔁 10. Automating Log Rotation (Example)

```python
import os
import shutil
from datetime import datetime

def rotate_logs(log_file):
    if os.path.exists(log_file):
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        new_name = f"{log_file}_{timestamp}.bak"
        shutil.move(log_file, new_name)
        print(f"Log rotated: {new_name}")
    else:
        print("No log file found to rotate!")

rotate_logs("app.log")
```

💡 **Use Case:**
Automate log rotation on production servers.

---

## ⚙️ 11. Reading Large Log Files Efficiently

```python
with open("access.log", "r") as log:
    for line in log:
        if "500" in line:
            print("Server Error Found:", line.strip())
```

💡 Use this in **monitoring scripts** that parse log files continuously.

---

## 🧩 12. Working with CSV Files

### ➤ Writing CSV Data

```python
import csv

with open("servers.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Server", "IP", "Status"])
    writer.writerow(["web01", "192.168.1.10", "running"])
```

### ➤ Reading CSV Data

```python
import csv

with open("servers.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

💡 **Use Case:**
Manage server inventory or configuration data in CSV format.

---

## 🧾 13. Exception Handling with Files

```python
try:
    with open("missing.txt", "r") as f:
        data = f.read()
except FileNotFoundError:
    print("File not found. Please check the path.")
```

💡 Always handle file-related exceptions — especially when reading configs or logs in production.

---

## 🧾 14. Summary

| Concept            | Description                         |
| ------------------ | ----------------------------------- |
| File Modes         | `'r'`, `'w'`, `'a'`, `'x'`, `'r+'`  |
| Context Manager    | `with open()` — auto close          |
| JSON               | For structured configuration        |
| YAML               | For deployment files (K8s, Ansible) |
| Log Rotation       | Archive or rename old logs          |
| Exception Handling | Manage missing files safely         |

---
