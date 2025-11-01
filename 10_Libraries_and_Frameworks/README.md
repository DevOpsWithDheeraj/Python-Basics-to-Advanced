# 🧰 10_Libraries_and_Frameworks — Essential Python Libraries for DevOps Automation

---

## 🎯 Objective

By the end of this chapter, you’ll understand and use key Python libraries that help automate **DevOps workflows**, such as:

- Managing OS and system-level operations  
- Running Linux commands via scripts  
- Handling AWS and cloud automation  
- Working with remote servers using SSH  
- Interacting with APIs and Docker containers  

---

## 🧠 1. Introduction

DevOps engineers rely on Python libraries to automate tasks like:

✅ Infrastructure provisioning  
✅ CI/CD pipeline scripting  
✅ Server monitoring  
✅ Log management  
✅ Cloud service operations (AWS, Docker, etc.)  

Below are **the most important Python libraries** every DevOps professional should master.

---

## ⚙️ 2. `os` — Operating System Interface

**Definition:**  
The `os` module lets you interact with the operating system — managing files, directories, and environment variables.

### Example:
```python
import os

# Get current working directory
print("📁 Current Directory:", os.getcwd())

# List files
print("📄 Files:", os.listdir())

# Create and remove directory
os.mkdir("logs")
print("✅ Folder created: logs")
os.rmdir("logs")
print("🗑️ Folder deleted: logs")

# Access environment variable
print("👤 USER:", os.getenv("USER"))
````

💡 **Use Case:**
Automate file operations, manage directories, and configure system environments.

---

## 🔧 3. `subprocess` — Running Shell Commands

**Definition:**
The `subprocess` module is used to run shell commands and scripts directly from Python.

### Example:

```python
import subprocess

result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print("📜 Command Output:\n", result.stdout)
```

### With Error Handling:

```python
try:
    subprocess.run(["cat", "/invalid/file"], check=True)
except subprocess.CalledProcessError:
    print("❌ Command failed!")
```

💡 **Use Case:**
Automate Linux commands (e.g., deploy scripts, restart services, check system health).

---

## 🔑 4. `paramiko` — SSH and Remote Server Automation

**Definition:**
`paramiko` allows you to SSH into remote servers and execute commands securely.

### Example:

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(hostname="192.168.1.10", username="ubuntu", key_filename="/path/to/key.pem")

stdin, stdout, stderr = ssh.exec_command("uptime")
print(stdout.read().decode())

ssh.close()
```

💡 **Use Case:**
Run commands, deploy applications, or collect logs on remote servers.

---

## ☁️ 5. `boto3` — AWS Automation SDK

**Definition:**
`boto3` is the official AWS SDK for Python — used for managing AWS resources like EC2, S3, Lambda, IAM, and CloudWatch.

### Example: List S3 Buckets

```python
import boto3

s3 = boto3.client("s3")
for bucket in s3.list_buckets()["Buckets"]:
    print("🪣", bucket["Name"])
```

### Example: Start/Stop EC2 Instance

```python
ec2 = boto3.client("ec2")
ec2.stop_instances(InstanceIds=["i-0abcd1234efgh5678"])
print("🛑 Instance stopped.")
```

💡 **Use Case:**
Automate AWS infrastructure tasks, cost optimization, or resource management.

---

## 🐍 6. `requests` — API Interaction

**Definition:**
The `requests` library allows you to make HTTP calls to APIs.

### Example: GET Request

```python
import requests

response = requests.get("https://api.github.com")
print("🌐 Status Code:", response.status_code)
```

### Example: POST Request

```python
payload = {"name": "DevOpsBot", "language": "Python"}
response = requests.post("https://httpbin.org/post", json=payload)
print(response.json())
```

💡 **Use Case:**
Integrate REST APIs — e.g., Jenkins, Slack, AWS, Grafana, Prometheus.

---

## 🐳 7. `docker` — Manage Docker Containers

**Definition:**
The `docker` SDK lets you manage containers, images, and volumes programmatically.

### Example:

```python
import docker

client = docker.from_env()

# List containers
for container in client.containers.list(all=True):
    print(f"📦 {container.name} | Status: {container.status}")

# Start a container
container = client.containers.get("nginx")
container.start()
print("🚀 Container started.")
```

💡 **Use Case:**
Automate Docker container management and deployment pipelines.

---

## 🧰 8. `json` — Working with JSON Data

**Definition:**
Used for reading/writing JSON configuration files or API responses.

### Example:

```python
import json

data = {"app": "web", "version": "1.2"}
json_string = json.dumps(data)
print("JSON String:", json_string)

# Load JSON from string
parsed = json.loads(json_string)
print("App Name:", parsed["app"])
```

💡 **Use Case:**
Handle config files (e.g., Terraform outputs, CI/CD settings).

---

## 📦 9. `yaml` — Reading Configuration Files (DevOps Favorite)

**Definition:**
Used for reading and writing YAML files — common in **Kubernetes, Ansible, Jenkins**, etc.

### Example:

```python
import yaml

with open("config.yaml") as f:
    data = yaml.safe_load(f)

print("Cluster Name:", data["cluster_name"])
```

💡 **Use Case:**
Parse YAML-based configuration files like `kubeconfig`, `docker-compose.yml`, or `playbooks`.

---

## 🪣 10. `psutil` — System Monitoring

**Definition:**
Provides system and process monitoring capabilities.

### Example:

```python
import psutil

print("🧠 CPU Usage:", psutil.cpu_percent(), "%")
print("💾 Memory:", psutil.virtual_memory().percent, "%")
print("🖥️ Disk Usage:", psutil.disk_usage('/').percent, "%")
```

💡 **Use Case:**
Monitor server health, performance metrics, and resource utilization.

---

## 🧩 11. `logging` — Log Management

**Definition:**
Used to log errors, warnings, and system information for debugging and monitoring.

### Example:

```python
import logging

logging.basicConfig(filename="app.log", level=logging.INFO)
logging.info("Pipeline started.")
logging.warning("Low disk space.")
logging.error("Deployment failed.")
```

💡 **Use Case:**
Centralized logging for scripts, pipelines, and automation tools.

---

## 🔍 12. `argparse` — Command-Line Arguments

**Definition:**
Allows scripts to accept parameters from the command line.

### Example:

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--env", help="Environment name")
args = parser.parse_args()

print(f"Deploying to {args.env} environment...")
```

💡 **Use Case:**
Parameterize automation scripts — e.g., `python deploy.py --env=prod`

---

## 🧩 13. `smtplib` — Email Notifications

**Definition:**
Send emails automatically from your scripts.

### Example:

```python
import smtplib

server = smtplib.SMTP("smtp.gmail.com", 587)
server.starttls()
server.login("youremail@gmail.com", "password")
server.sendmail("youremail@gmail.com", "receiver@gmail.com", "Build Successful ✅")
server.quit()
```

💡 **Use Case:**
Send alerts or build notifications after CI/CD runs.

---

## 🔗 14. Integration Example — DevOps Automation Script

```python
import os, boto3, requests, logging

logging.basicConfig(filename="devops.log", level=logging.INFO)

def get_instance_list():
    ec2 = boto3.client("ec2")
    instances = ec2.describe_instances()
    for res in instances["Reservations"]:
        for inst in res["Instances"]:
            print("🖥️", inst["InstanceId"], inst["State"]["Name"])

def notify_slack(message):
    url = "https://hooks.slack.com/services/XXXXX/XXXXX/XXXXX"
    requests.post(url, json={"text": message})

try:
    get_instance_list()
    notify_slack("✅ AWS EC2 instances listed successfully.")
except Exception as e:
    logging.error("Error: %s", e)
    notify_slack(f"❌ Script failed: {e}")
```

💡 **Use Case:**
Integrated AWS + Slack automation with error handling and logging.

---

## ✅ 15. Best Practices

✔️ Use `virtualenv` to manage dependencies
✔️ Store secrets securely (not in code)
✔️ Log every important action
✔️ Use exception handling for network/API operations
✔️ Combine libraries effectively (e.g., `boto3` + `logging` + `yaml`)
✔️ Keep config data outside scripts (in YAML/JSON)

---

## 🧾 16. Summary

| Library        | Purpose               | Example Use Case      |
| -------------- | --------------------- | --------------------- |
| **os**         | File & env management | Create/delete folders |
| **subprocess** | Run shell commands    | Execute bash scripts  |
| **paramiko**   | SSH automation        | Remote deployments    |
| **boto3**      | AWS SDK               | Cloud automation      |
| **requests**   | REST API calls        | Slack/Jenkins APIs    |
| **docker**     | Container management  | Start/stop containers |
| **yaml/json**  | Config parsing        | K8s & Ansible         |
| **psutil**     | System monitoring     | CPU/memory metrics    |
| **logging**    | Log handling          | Error tracking        |
| **argparse**   | CLI interface         | Parameterized scripts |

---
