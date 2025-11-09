# 🌐 10_Working_with_APIs_and_Networking — Python for DevOps Automation

---

## 🎯 Objective

This chapter teaches how to use **Python for API communication and network automation** — essential for DevOps engineers managing cloud, CI/CD, and infrastructure automation.

By the end of this chapter, you’ll learn to:

- Understand REST APIs and how they work  
- Use the `requests` module to interact with APIs  
- Handle JSON data efficiently  
- Automate DevOps tools (Jenkins, AWS, Kubernetes) via APIs  
- Implement basic socket programming for network communication  

---

## 🔹 1. Introduction to REST APIs

**Definition:**  
A **REST API (Representational State Transfer)** allows communication between systems using HTTP methods such as **GET, POST, PUT, DELETE**.  
It’s the backbone of automation tools like **AWS CLI, Jenkins, Kubernetes, GitHub**, etc.

**Common HTTP Methods:**

| Method | Purpose |
|--------|----------|
| **GET** | Retrieve data |
| **POST** | Create data |
| **PUT** | Update existing data |
| **DELETE** | Remove data |

**Example REST API Endpoint:**
```

[https://api.github.com/users/dheeraj]

````

---

## 🧩 2. Using the `requests` Module

**Definition:**  
The `requests` module is a simple and powerful library for sending HTTP requests.

Install it (if needed):
```bash
pip install requests
````

---

### Example 1: Basic GET Request

```python
import requests

response = requests.get("https://api.github.com")
print("✅ Status Code:", response.status_code)
print("📜 Response:", response.text[:200])
```

**Output:**

```
✅ Status Code: 200
📜 Response: { "current_user_url": "https://api.github.com/user", ... }
```

💡 **DevOps Use Case:**
Check the availability of Jenkins, Grafana, or Prometheus API endpoints.

---

### Example 2: Sending a POST Request

```python
import requests

url = "https://httpbin.org/post"
data = {"app": "webserver", "status": "deployed"}

response = requests.post(url, json=data)
print("🔁 Response JSON:", response.json())
```

💡 **DevOps Use Case:**
Trigger Jenkins jobs or send Slack alerts through a POST API.

---

## 🧠 3. Consuming JSON APIs

**Definition:**
APIs often return data in **JSON (JavaScript Object Notation)** format, which Python can easily process using `.json()`.

### Example:

```python
import requests

url = "https://api.github.com/users/octocat"
response = requests.get(url)
data = response.json()

print("👤 Name:", data["login"])
print("📧 Public Repos:", data["public_repos"])
```

💡 **DevOps Use Case:**
Fetch system metrics or cloud resource details from AWS or Kubernetes APIs.

---

## ⚙️ 4. Automating REST API Calls for DevOps Tools

APIs are the backbone of automation in **DevOps**.
Let’s see how Python interacts with real-world DevOps tools using REST APIs.

---

### 🔸 (a) Jenkins API Automation

**Example:** Trigger a Jenkins job remotely.

```python
import requests

jenkins_url = "http://jenkins.local:8080/job/deploy/build"
auth = ("admin", "your_api_token")

response = requests.post(jenkins_url, auth=auth)
print("🚀 Triggered Jenkins Job! Status:", response.status_code)
```

💡 **Use Case:**
Automate CI/CD pipelines — build or deploy using API calls.

---

### 🔸 (b) AWS API with `boto3`

Although `boto3` is a dedicated AWS SDK, it’s technically an API client library.

**Example:** List S3 Buckets

```python
import boto3

s3 = boto3.client("s3")
for bucket in s3.list_buckets()["Buckets"]:
    print("🪣 Bucket:", bucket["Name"])
```

💡 **Use Case:**
Automate AWS resources — like creating EC2 instances or S3 backups.

---

### 🔸 (c) Kubernetes API

You can interact with the Kubernetes cluster directly via API calls.

**Example:** Get Pods from Kubernetes API

```python
import requests

url = "https://kubernetes.example.com/api/v1/namespaces/default/pods"
headers = {"Authorization": "Bearer <your-token>"}
response = requests.get(url, headers=headers, verify=False)

if response.status_code == 200:
    data = response.json()
    for pod in data["items"]:
        print("🧩 Pod:", pod["metadata"]["name"])
```

💡 **Use Case:**
List, monitor, or delete Kubernetes pods programmatically.

---

### 🔸 (d) Slack API Automation

Send a message to a Slack channel.

```python
import requests

url = "https://hooks.slack.com/services/XXXX/YYYY/ZZZZ"
payload = {"text": "✅ Deployment successful!"}

requests.post(url, json=payload)
print("📣 Slack notification sent.")
```

💡 **Use Case:**
Send automated build or deployment notifications to Slack.

---

## 🔌 5. Socket Programming Basics

**Definition:**
Sockets provide **low-level networking** — enabling direct communication between devices using **IP addresses and ports**.

### Example: Simple TCP Server

```python
import socket

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("localhost", 8080))
server_socket.listen(1)

print("🖥️ Server is listening on port 8080...")
conn, addr = server_socket.accept()
print("🔗 Connection from:", addr)

data = conn.recv(1024).decode()
print("📩 Received:", data)

conn.send("Hello Client!".encode())
conn.close()
```

### Example: TCP Client

```python
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(("localhost", 8080))
client_socket.send("Ping from client".encode())

response = client_socket.recv(1024).decode()
print("💬 Server says:", response)

client_socket.close()
```

💡 **DevOps Use Case:**

* Check network connectivity between servers
* Build simple custom monitoring tools
* Test service ports or network communication

---

## 🧩 6. Handling API Errors and Exceptions

Always include error handling for network issues, invalid tokens, or unavailable endpoints.

### Example:

```python
import requests

try:
    res = requests.get("https://api.github.com/invalid")
    res.raise_for_status()
except requests.exceptions.RequestException as e:
    print("❌ API Error:", e)
```

💡 **Best Practice:**
Use retries, logging, and alerting when automating production APIs.

---

## 🧾 Summary

| Concept                | Description                                 | DevOps Use Case               |
| ---------------------- | ------------------------------------------- | ----------------------------- |
| **REST APIs**          | Standard way to communicate between systems | AWS, Jenkins, Kubernetes APIs |
| **requests**           | Python library to make HTTP calls           | Trigger builds, get metrics   |
| **JSON Parsing**       | Process API data                            | Manage cloud or CI/CD info    |
| **Automation via API** | Automate infrastructure tasks               | Deployments, monitoring       |
| **Socket Programming** | Low-level networking                        | Connectivity testing          |
| **Error Handling**     | Manage API failures                         | Improve script reliability    |

---

## 🧠 Quick Recap

✅ REST APIs = Communication backbone
✅ `requests` = Core library for API calls
✅ JSON = Lightweight data format
✅ Automate Jenkins, AWS, Kubernetes with Python
✅ Sockets = Network-level control for testing

---
