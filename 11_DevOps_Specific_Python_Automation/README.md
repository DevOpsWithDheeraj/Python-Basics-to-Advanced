## 🧑‍💻 11_DevOps_Specific_Python_Automation

Python is a key language for DevOps engineers. It allows automation across **cloud platforms, CI/CD pipelines, container orchestration, and infrastructure management**.
Below are the essential automation areas every DevOps professional should master using Python.

---

### 🔹 1. AWS Automation using **boto3**

**Definition:**
`boto3` is the **official AWS SDK for Python**, enabling automation of AWS resources such as EC2, S3, Lambda, IAM, CloudWatch, etc.

**Use Case:**
Automatically create and manage AWS resources such as EC2 instances, upload files to S3, and monitor logs.

**Example:** Create an S3 bucket and upload a file.

```python
import boto3

# Create an S3 client
s3 = boto3.client('s3')

bucket_name = "devops-demo-bucket-12345"

# Create a new bucket
s3.create_bucket(Bucket=bucket_name)
print(f"Bucket '{bucket_name}' created successfully!")

# Upload a file
s3.upload_file("demo.txt", bucket_name, "demo.txt")
print("File uploaded to S3 successfully!")
```

✅ *Automation Idea:* Run this as part of your Jenkins job to deploy artifacts automatically to S3.

---

### 🔹 2. File Transfer using **paramiko (SSH & SFTP)**

**Definition:**
`paramiko` allows Python programs to **connect to remote servers via SSH**, execute commands, and transfer files securely.

**Use Case:**
Automate file transfers and remote command execution on Linux servers.

**Example:** Upload a log file to a remote server via SFTP.

```python
import paramiko

hostname = "192.168.1.10"
username = "ec2-user"
password = "mypassword"

# Connect via SSH
ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect(hostname, username=username, password=password)

# Execute a command
stdin, stdout, stderr = ssh.exec_command("ls -l /home/ec2-user")
print(stdout.read().decode())

# File transfer using SFTP
sftp = ssh.open_sftp()
sftp.put("local_log.txt", "/home/ec2-user/logs/log.txt")
print("File transferred successfully!")

sftp.close()
ssh.close()
```

✅ *Automation Idea:* Schedule this to back up server logs nightly.

---

### 🔹 3. Docker Automation using **docker SDK**

**Definition:**
`docker` Python SDK allows you to manage Docker containers, images, and networks programmatically.

**Use Case:**
Automate container creation, image building, and cleanup in CI/CD pipelines.

**Example:** Run a Nginx container using Python.

```python
import docker

client = docker.from_env()

# Pull and run container
container = client.containers.run("nginx:latest", detach=True, ports={'80/tcp': 8080})
print(f"Container {container.short_id} running on port 8080")
```

✅ *Automation Idea:* Use this in Jenkins or GitLab to spin up containers dynamically during testing.

---

### 🔹 4. Kubernetes Automation using **kubernetes client library**

**Definition:**
The `kubernetes` Python client allows you to **interact with Kubernetes clusters** — deploy pods, manage namespaces, and monitor workloads.

**Use Case:**
Automate deployment rollouts and scaling in Kubernetes clusters.

**Example:** List all pods in a namespace.

```python
from kubernetes import client, config

# Load kubeconfig
config.load_kube_config()

v1 = client.CoreV1Api()
pods = v1.list_namespaced_pod(namespace="default")

for pod in pods.items:
    print(pod.metadata.name)
```

✅ *Automation Idea:* Integrate with Jenkins to verify if pods are healthy after deployment.

---

### 🔹 5. CI/CD Integration (GitLab/Jenkins Python Scripts)

**Definition:**
Python can be used to interact with **CI/CD tools** like Jenkins and GitLab via their REST APIs for triggering jobs, fetching build status, or managing pipelines.

**Example:** Trigger a Jenkins job using its API.

```python
import requests

jenkins_url = "http://jenkins.example.com/job/BuildProject/build"
user = "admin"
token = "your_jenkins_token"

response = requests.post(jenkins_url, auth=(user, token))
if response.status_code == 201:
    print("Jenkins job triggered successfully!")
else:
    print(f"Failed to trigger job: {response.status_code}")
```

✅ *Automation Idea:* Schedule this Python script to auto-trigger deployment pipelines after code merges.

---

### 🔹 6. Monitoring and Alerting Automation

**Definition:**
Python scripts can integrate with tools like **CloudWatch, Prometheus, or Grafana APIs** to fetch metrics, detect anomalies, and send alerts via email or Slack.

**Example:** Send an alert if CPU usage exceeds threshold.

```python
import psutil
import smtplib

cpu = psutil.cpu_percent(5)
if cpu > 80:
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.starttls()
    server.login("youremail@gmail.com", "password")
    message = f"ALERT! CPU usage is high: {cpu}%"
    server.sendmail("youremail@gmail.com", "admin@company.com", message)
    print("Alert email sent!")
```

✅ *Automation Idea:* Integrate this with cron jobs or Jenkins to monitor EC2 or on-prem systems.

---

### 🔹 7. Using Python with **Ansible** and **Terraform**

**Definition:**
Python can extend **Ansible** (via custom modules or filters) and **Terraform** (using automation scripts or wrapper tools) for Infrastructure as Code (IaC) management.

**Example:** Automate Terraform commands via Python.

```python
import subprocess

# Initialize and apply Terraform
subprocess.run(["terraform", "init"])
subprocess.run(["terraform", "apply", "-auto-approve"])
print("Terraform infrastructure deployed successfully!")
```

✅ *Automation Idea:* Automate end-to-end environment provisioning from Jenkins or GitLab using Python + Terraform.

---

## 🧾 Summary

| Automation Area | Library                        | Example Task              |
| --------------- | ------------------------------ | ------------------------- |
| AWS             | boto3                          | Create S3, manage EC2     |
| SSH/SFTP        | paramiko                       | Remote file transfers     |
| Docker          | docker SDK                     | Launch containers         |
| Kubernetes      | kubernetes client              | Manage pods & deployments |
| CI/CD           | requests                       | Trigger Jenkins pipelines |
| Monitoring      | psutil, smtplib                | Send alert emails         |
| IaC             | subprocess + Terraform/Ansible | Provision infra           |

---
