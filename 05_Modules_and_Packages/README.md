# 📦 05_Modules_and_Packages 

## 🧠 1. What is a Module?

**Definition:**  
A **module** is a Python file (`.py`) that contains **functions, variables, or classes** you can reuse in other scripts.

👉 Think of it as a **toolbox** you can import anywhere.

---

### 🧩 Example 1: Creating and Importing a Custom Module

Create a file named **`devops_utils.py`**

```python
# devops_utils.py

def start_server(server_name):
    print(f"Starting {server_name}... ✅")

def stop_server(server_name):
    print(f"Stopping {server_name}... 🛑")

def get_status(server_name):
    print(f"Checking status of {server_name}... OK ✅")
````

Now create another script **`main.py`**

```python
# main.py

import devops_utils

devops_utils.start_server("web-server-1")
devops_utils.get_status("web-server-1")
devops_utils.stop_server("web-server-1")
```

📘 Output:

```
Starting web-server-1... ✅
Checking status of web-server-1... OK ✅
Stopping web-server-1... 🛑
```

---

## 🧱 2. Built-in Python Modules for DevOps

Python provides several **standard libraries** that are extremely helpful in DevOps automation.

| Module       | Description                       | Example Use Case            |
| ------------ | --------------------------------- | --------------------------- |
| `os`         | Interact with Operating System    | File & directory operations |
| `sys`        | Access system-specific parameters | Path, exit codes            |
| `subprocess` | Run shell commands                | Execute Linux commands      |
| `shutil`     | High-level file operations        | Copy, move, delete          |
| `json`       | Work with JSON data               | API or config parsing       |
| `datetime`   | Handle time/date                  | Logs, timestamps            |
| `platform`   | System info                       | Identify OS, architecture   |

---

### 🧩 Example 2: Using `os` Module

```python
import os

print("Current Directory:", os.getcwd())
os.mkdir("logs")
print("Directory 'logs' created successfully!")
```

💡 **Use Case (DevOps):**
Automatically create a log directory before deploying an application.

---

### 🧩 Example 3: Using `sys` Module

```python
import sys

print("Python version:", sys.version)
print("System Path:", sys.path)
sys.exit("Exiting Script 🚫")
```

💡 **Use Case:**
Stop execution of a script if a required environment variable is missing.

---

### 🧩 Example 4: Using `subprocess` Module

```python
import subprocess

output = subprocess.getoutput("uptime")
print("Server Uptime:", output)
```

💡 **Use Case (DevOps):**
Run shell commands, start services, or manage system resources directly from Python.

---

### 🧩 Example 5: Using `json` Module

```python
import json

data = '{"server": "web01", "status": "running"}'
parsed = json.loads(data)
print("Server:", parsed["server"])
```

💡 **Use Case:**
Handle **API responses**, **Terraform outputs**, or **Kubernetes manifests**.

---

### 🧩 Example 6: Using `datetime` Module

```python
from datetime import datetime

now = datetime.now()
print("Deployment Timestamp:", now.strftime("%Y-%m-%d %H:%M:%S"))
```

💡 **Use Case:**
Add timestamps to **logs**, **backups**, or **audit trails**.

---

## 📦 3. What is a Package?

**Definition:**
A **package** is a collection of modules stored in a directory that contains an `__init__.py` file.

📁 Example Folder Structure:

```
devops_tools/
    __init__.py
    aws_utils.py
    docker_utils.py
    monitor_utils.py
```

---

### 🧩 Example 7: Creating a DevOps Package

#### 1️⃣ Folder: `devops_tools/`

**`__init__.py`**

```python
# Marks this folder as a package
```

**`aws_utils.py`**

```python
def deploy_ec2(instance_name):
    print(f"Deploying EC2 instance: {instance_name}")
```

**`docker_utils.py`**

```python
def start_container(container):
    print(f"Starting Docker container: {container}")
```

#### 2️⃣ Main Script:

```python
from devops_tools import aws_utils, docker_utils

aws_utils.deploy_ec2("web-instance-1")
docker_utils.start_container("nginx-container")
```

---

## 🌐 4. Third-Party Libraries for DevOps

You can install external libraries using **pip**:

```bash
pip install boto3 paramiko requests psutil
```

| Library      | Purpose           | Example                             |
| ------------ | ----------------- | ----------------------------------- |
| **boto3**    | AWS Automation    | Manage EC2, S3, Lambda              |
| **paramiko** | SSH Automation    | Remote login, run commands          |
| **requests** | REST API          | Interact with Jenkins, GitHub, etc. |
| **psutil**   | System Monitoring | CPU, memory, process stats          |

---

### 🧩 Example 8: AWS Automation with `boto3`

```python
import boto3

ec2 = boto3.resource('ec2')

instance = ec2.create_instances(
    ImageId='ami-0abcdef1234567890',  # Example AMI ID
    InstanceType='t2.micro',
    MinCount=1,
    MaxCount=1,
    KeyName='my-key-pair'
)

print("Launched EC2 Instance:", instance[0].id)

```

💡 **Use Case:**
List all EC2 instances and their states (running/stopped).

---

### 🧩 Example 9: Remote SSH with `paramiko`

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect('192.168.1.10', username='ec2-user', key_filename='key.pem')

stdin, stdout, stderr = ssh.exec_command('uptime')
print(stdout.read().decode())

ssh.close()
```

💡 **Use Case:**
Run shell commands remotely for **configuration management** or **server monitoring**.

---

### 🧩 Example 10: REST API with `requests`

```python
import requests

response = requests.get("https://api.github.com")
print("GitHub API Status:", response.status_code)
```

💡 **Use Case:**
Monitor APIs or integrate with CI/CD tools like **Jenkins, GitLab, GitHub Actions**.

---

## 🧠 5. Organizing Your DevOps Automation Project

**Example Folder Structure:**

```
devops_automation/
│
├── main.py
├── devops_utils/
│   ├── __init__.py
│   ├── aws_utils.py
│   ├── docker_utils.py
│   ├── monitoring_utils.py
│
├── configs/
│   └── app_config.json
│
└── logs/
    └── deployment.log
```

**main.py**

```python
from devops_utils import aws_utils, docker_utils

aws_utils.deploy_ec2("prod-web")
docker_utils.start_container("nginx")
```

---

## ✅ 6. Best Practices

✔️ Keep **related functions in one module** (e.g., `aws_utils`, `docker_utils`) <br>
✔️ Use **meaningful names** for modules and packages <br>
✔️ Add **docstrings** to explain functions <br>
✔️ Store **configuration files** separately (`.json` or `.yaml`) <br>
✔️ Use **virtual environments** for dependency management <br>
✔️ Maintain **requirements.txt** for all libraries <br>

---

## 🧾 8. Summary

| Concept                 | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| **Module**              | Single `.py` file with reusable code                  |
| **Package**             | Directory with multiple modules                       |
| **Built-in Modules**    | Already available in Python (e.g., `os`, `sys`)       |
| **Third-party Modules** | Installed via pip (`boto3`, `paramiko`)               |
| **Importing**           | `import module_name` or `from module import function` |

---
