## 🚀 **16. Hands-on Projects (Python for DevOps)**

These projects combine all the concepts learned throughout the course — from Python fundamentals to DevOps-specific automation.
Each project focuses on **real-world DevOps automation**, helping you practice working with AWS, Docker, Kubernetes, monitoring, and CI/CD systems.

---

### ✅ **1. Automate AWS EC2 Instance Start/Stop using boto3**

**Goal:**
Automatically start or stop EC2 instances based on time or load conditions.

**Skills Covered:**
AWS automation, boto3, IAM permissions, scheduling.

**Example Code:**

```python
import boto3

ec2 = boto3.client('ec2')

def start_instances():
    ec2.start_instances(InstanceIds=['i-0abcd1234ef567890'])
    print("✅ EC2 instance started")

def stop_instances():
    ec2.stop_instances(InstanceIds=['i-0abcd1234ef567890'])
    print("🛑 EC2 instance stopped")

# Call the function manually or via cron/scheduler
start_instances()
```

---

### ✅ **2. Log File Analyzer Script**

**Goal:**
Parse and analyze log files (e.g., `/var/log/syslog`, Nginx logs) to extract errors, warnings, and statistics.

**Skills Covered:**
File handling, regex (`re`), automation, reporting.

**Example Code:**

```python
import re

error_count = 0
with open("/var/log/syslog", "r") as log:
    for line in log:
        if re.search(r"error|failed|critical", line, re.IGNORECASE):
            error_count += 1

print(f"⚠️ Total errors found: {error_count}")
```

---

### ✅ **3. Automated Backup using Python**

**Goal:**
Backup important files or directories to a remote server or S3 bucket automatically.

**Skills Covered:**
File handling, `shutil`, `boto3`, `paramiko`.

**Example Code:**

```python
import shutil, datetime, boto3

# Create local backup
backup_file = f"/tmp/backup_{datetime.date.today()}.zip"
shutil.make_archive("/tmp/backup", "zip", "/etc")

# Upload to S3
s3 = boto3.client('s3')
s3.upload_file(backup_file, "devops-backup-bucket", "backup.zip")
print("✅ Backup completed and uploaded to S3.")
```

---

### ✅ **4. CI/CD Pipeline Trigger via Python Script**

**Goal:**
Trigger Jenkins or GitLab CI/CD pipelines programmatically using REST APIs.

**Skills Covered:**
REST API, `requests`, authentication, DevOps integration.

**Example Code (Jenkins Example):**

```python
import requests

jenkins_url = "http://jenkins-server:8080/job/deploy/build"
response = requests.post(jenkins_url, auth=('admin', 'password'))
print("✅ CI/CD Pipeline Triggered:", response.status_code)
```

---

### ✅ **5. Docker Image Cleaner Automation**

**Goal:**
Automatically delete old or unused Docker images to save disk space.

**Skills Covered:**
Docker SDK, automation, system monitoring.

**Example Code:**

```python
import docker

client = docker.from_env()
for image in client.images.list():
    if "<none>" in image.tags:
        client.images.remove(image.id, force=True)
        print(f"🧹 Removed dangling image: {image.id}")
```

---

### ✅ **6. Kubernetes Pod Status Checker**

**Goal:**
Monitor the status of pods in a Kubernetes cluster and report failed pods.

**Skills Covered:**
Kubernetes Python client, automation, alerting.

**Example Code:**

```python
from kubernetes import client, config

config.load_kube_config()
v1 = client.CoreV1Api()
pods = v1.list_pod_for_all_namespaces()

for pod in pods.items:
    if pod.status.phase != "Running":
        print(f"⚠️ Pod {pod.metadata.name} in {pod.metadata.namespace} is {pod.status.phase}")
```

---

### ✅ **7. Server Health Monitoring Tool**

**Goal:**
Monitor CPU, memory, and disk usage, and trigger alerts if thresholds are crossed.

**Skills Covered:**
`psutil`, alerting, system monitoring, automation.

**Example Code:**

```python
import psutil, smtplib

cpu = psutil.cpu_percent()
memory = psutil.virtual_memory().percent

if cpu > 80 or memory > 80:
    print("⚠️ High usage detected!")
else:
    print(f"✅ CPU: {cpu}% | Memory: {memory}%")
```

---

## 🧠 **Learning Outcomes**

By completing these projects, you’ll gain hands-on experience in:

* Automating cloud (AWS) operations
* Managing infrastructure with Docker & Kubernetes
* Integrating Python with DevOps CI/CD pipelines
* Building monitoring and backup scripts
* Applying automation in real-world DevOps workflows

---
