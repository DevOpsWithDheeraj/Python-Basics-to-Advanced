## 🧩 **15. Popular DevOps Libraries**

Python provides a wide range of **libraries** that simplify automation and integration tasks across DevOps tools like AWS, Docker, Kubernetes, Jenkins, and more.
These libraries allow you to manage infrastructure, perform CI/CD operations, monitor systems, and handle configuration files — all through Python scripts.

---

### 🟡 **1. AWS Cloud Automation – boto3**

**Definition:**
`boto3` is the official AWS SDK for Python that enables developers to create, configure, and manage AWS services such as EC2, S3, IAM, Lambda, and more.

**Use Case:**
Automating AWS resource provisioning, backups, or monitoring.

**Example: Create an S3 bucket**

```python
import boto3

s3 = boto3.client('s3')
s3.create_bucket(Bucket='devops-demo-bucket')
print("✅ S3 bucket created successfully!")
```

**Example: List EC2 Instances**

```python
import boto3

ec2 = boto3.client('ec2')
instances = ec2.describe_instances()
for reservation in instances['Reservations']:
    for instance in reservation['Instances']:
        print(instance['InstanceId'], instance['State']['Name'])
```

---

### 🟡 **2. SSH / SFTP – paramiko, fabric**

**Definition:**

* `paramiko` provides SSH and SFTP capabilities for remote server management.
* `fabric` builds on top of `paramiko` for higher-level deployment and automation.

**Use Case:**
Running remote commands, transferring files, automating deployments.

**Example (Paramiko – Run remote command):**

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect('192.168.1.10', username='ubuntu', password='password')

stdin, stdout, stderr = ssh.exec_command('uptime')
print(stdout.read().decode())

ssh.close()
```

**Example (Fabric – Run command on remote server):**

```python
from fabric import Connection

conn = Connection('ubuntu@192.168.1.10')
conn.run('ls -l /var/www/')
```

---

### 🟡 **3. REST APIs – requests**

**Definition:**
`requests` is a simple and powerful HTTP library for sending REST API calls.

**Use Case:**
Integrate with cloud services, Jenkins, or Kubernetes APIs.

**Example (GET Request):**

```python
import requests

response = requests.get('https://api.github.com/users/octocat')
print(response.json())
```

**Example (POST Request):**

```python
import requests

data = {'name': 'demo', 'description': 'Test Repo'}
headers = {'Authorization': 'token YOUR_GITHUB_TOKEN'}
response = requests.post('https://api.github.com/user/repos', json=data, headers=headers)
print(response.status_code)
```

---

### 🟡 **4. Docker Automation – docker**

**Definition:**
`docker` SDK for Python allows programmatic management of Docker containers, images, and networks.

**Use Case:**
Automate container deployment, build images, or monitor containers.

**Example:**

```python
import docker

client = docker.from_env()
container = client.containers.run("nginx", detach=True, ports={'80/tcp': 8080})
print(f"Started container: {container.id}")
```

---

### 🟡 **5. Kubernetes Automation – kubernetes**

**Definition:**
The `kubernetes` Python client allows you to interact with Kubernetes clusters programmatically (e.g., creating pods, deployments, services).

**Use Case:**
Automate deployment, scaling, or health checks in a Kubernetes cluster.

**Example:**

```python
from kubernetes import client, config

config.load_kube_config()
v1 = client.CoreV1Api()
pods = v1.list_pod_for_all_namespaces(watch=False)

for pod in pods.items:
    print(f"{pod.metadata.namespace}: {pod.metadata.name}")
```

---

### 🟡 **6. YAML Parsing – pyyaml**

**Definition:**
`pyyaml` is used to read and write YAML configuration files, which are common in DevOps tools like Kubernetes, Ansible, and Terraform.

**Use Case:**
Modify or create configuration files programmatically.

**Example:**

```python
import yaml

data = {
    'apiVersion': 'v1',
    'kind': 'Pod',
    'metadata': {'name': 'mypod'},
    'spec': {'containers': [{'name': 'nginx', 'image': 'nginx:latest'}]}
}

with open('pod.yaml', 'w') as file:
    yaml.dump(data, file)
print("✅ pod.yaml created successfully!")
```

---

### 🟡 **7. Monitoring – psutil, prometheus_client**

**Definition:**

* `psutil`: monitors system resources like CPU, memory, and disk usage.
* `prometheus_client`: exposes metrics to Prometheus for monitoring.

**Use Case:**
Monitor system health, generate metrics, or trigger alerts.

**Example (psutil – System Metrics):**

```python
import psutil

print("CPU Usage:", psutil.cpu_percent(), "%")
print("Memory Usage:", psutil.virtual_memory().percent, "%")
```

**Example (prometheus_client – Export Metrics):**

```python
from prometheus_client import start_http_server, Gauge
import psutil, time

cpu_gauge = Gauge('cpu_usage_percent', 'CPU usage percentage')

start_http_server(8000)
while True:
    cpu_gauge.set(psutil.cpu_percent())
    time.sleep(5)
```

---

### ✅ **Summary Table**

| **Purpose**           | **Library**                   | **Use Case**                              |
| --------------------- | ----------------------------- | ----------------------------------------- |
| AWS Cloud Automation  | `boto3`                       | Manage AWS resources like EC2, S3, Lambda |
| SSH / SFTP            | `paramiko`, `fabric`          | Remote command execution, file transfers  |
| REST APIs             | `requests`                    | Interact with APIs (AWS, Jenkins, etc.)   |
| Docker Automation     | `docker`                      | Create/manage containers                  |
| Kubernetes Automation | `kubernetes`                  | Automate K8s resources                    |
| YAML Parsing          | `pyyaml`                      | Read/write YAML config files              |
| Monitoring            | `psutil`, `prometheus_client` | System monitoring and alerting            |

---
