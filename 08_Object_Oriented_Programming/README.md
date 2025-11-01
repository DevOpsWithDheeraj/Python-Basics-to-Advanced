# 🧱 08_Object_Oriented_Programming (OOP) — Building Modular & Scalable DevOps Scripts

---

## 🎯 Objective

By the end of this chapter, you’ll learn to:

- Understand the **concepts of Object-Oriented Programming** (OOP) in Python.  
- Create and use **classes and objects** effectively.  
- Implement **encapsulation, inheritance, polymorphism**, and **abstraction**.  
- Design **modular and reusable automation tools** for DevOps workflows.  
- Apply OOP principles in **real DevOps projects** — CI/CD tools, AWS automation, log management, etc.

---

## 🧠 1. What is OOP?

**Definition:**  
**Object-Oriented Programming (OOP)** is a programming paradigm that organizes code into **objects** — entities that combine **data (attributes)** and **behavior (methods)**.

💡 **Why OOP in DevOps?**
- Helps you **reuse automation logic** (e.g., EC2 operations, monitoring tasks).  
- Makes scripts **cleaner, modular, and scalable**.  
- Improves **error handling** and maintainability.

---

## 🧩 2. Key OOP Concepts

| Concept | Description | Example |
|----------|--------------|----------|
| **Class** | Blueprint for creating objects | `class Server:` |
| **Object** | Instance of a class | `web_server = Server()` |
| **Encapsulation** | Hiding internal details | Private variables, methods |
| **Inheritance** | Reusing code from another class | `class EC2(Server):` |
| **Polymorphism** | Using same method differently | Overriding methods |
| **Abstraction** | Hiding complexity from users | Abstract classes |

---

## 🧱 3. Creating a Class and Object

```python
class Server:
    def __init__(self, name, ip):
        self.name = name
        self.ip = ip

    def start(self):
        print(f"🚀 Server {self.name} started at {self.ip}")

# Creating Object
web_server = Server("Web-01", "192.168.1.10")
web_server.start()
````

Output:

```
🚀 Server Web-01 started at 192.168.1.10
```

---

## ⚙️ 4. `__init__()` Method (Constructor)

**Definition:**
The `__init__()` method initializes object attributes automatically when the object is created.

```python
class DevOpsEngineer:
    def __init__(self, name, project):
        self.name = name
        self.project = project

    def display(self):
        print(f"👨‍💻 Engineer: {self.name} | Project: {self.project}")

eng1 = DevOpsEngineer("Dheeraj", "AWS Automation")
eng1.display()
```

---

## 🧩 5. Encapsulation — Hiding Internal Data

```python
class JenkinsPipeline:
    def __init__(self, job_name):
        self.__job_name = job_name  # Private variable

    def __build(self):  # Private method
        print(f"Building {self.__job_name}")

    def trigger_pipeline(self):
        print("🔁 Triggering pipeline...")
        self.__build()

pipeline = JenkinsPipeline("DeployApp")
pipeline.trigger_pipeline()
```

💡 **Use Case:**
Keep internal operations private — like secrets, credentials, or internal build steps.

---

## 🧬 6. Inheritance — Reusing Code

```python
class Server:
    def __init__(self, name):
        self.name = name

    def start(self):
        print(f"Starting server: {self.name}")

class WebServer(Server):
    def deploy(self):
        print(f"Deploying web app on {self.name}")

# Example usage
web = WebServer("NginxServer")
web.start()
web.deploy()
```

Output:

```
Starting server: NginxServer
Deploying web app on NginxServer
```

💡 **Use Case:**
Common in DevOps — base `Server` class reused by EC2, Jenkins, or Docker classes.

---

## 🧩 7. Polymorphism — One Interface, Many Forms

```python
class Server:
    def restart(self):
        print("Restarting generic server...")

class WebServer(Server):
    def restart(self):
        print("Restarting Nginx web server...")

class DatabaseServer(Server):
    def restart(self):
        print("Restarting MySQL database server...")

for srv in [WebServer(), DatabaseServer()]:
    srv.restart()
```

Output:

```
Restarting Nginx web server...
Restarting MySQL database server...
```

💡 **Use Case:**
Uniform operations (e.g., restart) for different server types.

---

## 🧩 8. Abstraction — Hiding Implementation Details

```python
from abc import ABC, abstractmethod

class CloudProvider(ABC):
    @abstractmethod
    def create_instance(self):
        pass

class AWS(CloudProvider):
    def create_instance(self):
        print("☁️ Launching EC2 instance on AWS...")

class Azure(CloudProvider):
    def create_instance(self):
        print("☁️ Launching VM on Azure...")

aws = AWS()
aws.create_instance()
```

💡 **Use Case:**
Used in multi-cloud automation scripts — enforce structure for providers.

---

## ☁️ 9. DevOps Example — AWS EC2 Manager

```python
import boto3

class EC2Manager:
    def __init__(self):
        self.ec2 = boto3.client("ec2")

    def list_instances(self):
        instances = self.ec2.describe_instances()
        for res in instances["Reservations"]:
            for inst in res["Instances"]:
                print(f"🖥️ Instance ID: {inst['InstanceId']} | State: {inst['State']['Name']}")

    def stop_instance(self, instance_id):
        self.ec2.stop_instances(InstanceIds=[instance_id])
        print(f"🛑 Stopped instance: {instance_id}")

# Example
manager = EC2Manager()
manager.list_instances()
```

💡 **Use Case:**
Reusable EC2 automation class for listing, starting, and stopping servers.

---

## 🐳 10. DevOps Example — Docker Container Manager

```python
import docker

class DockerManager:
    def __init__(self):
        self.client = docker.from_env()

    def list_containers(self):
        for c in self.client.containers.list(all=True):
            print(f"📦 {c.name} | Status: {c.status}")

    def start_container(self, name):
        container = self.client.containers.get(name)
        container.start()
        print(f"🚀 Container {name} started.")

manager = DockerManager()
manager.list_containers()
```

💡 **Use Case:**
OOP-based Docker control for automation pipelines.

---

## 🧩 11. Composition — Combining Multiple Classes

```python
class Logger:
    def log(self, message):
        print(f"[LOG]: {message}")

class Deployment:
    def __init__(self, name):
        self.name = name
        self.logger = Logger()

    def deploy(self):
        self.logger.log(f"Deploying {self.name} app...")

deploy = Deployment("FlaskAPI")
deploy.deploy()
```

💡 **Use Case:**
Combine logging, notifications, and monitoring classes for CI/CD tools.

---

## 🧠 12. Class Variables vs Instance Variables

```python
class Server:
    region = "ap-south-1"  # Class variable

    def __init__(self, name):
        self.name = name  # Instance variable

server1 = Server("WebServer")
server2 = Server("DBServer")

print(server1.region, server2.region)
print(server1.name, server2.name)
```

---

## 🔁 13. Magic Methods (`__str__`, `__len__`, etc.)

```python
class LogFile:
    def __init__(self, name, entries):
        self.name = name
        self.entries = entries

    def __str__(self):
        return f"📄 LogFile: {self.name} ({len(self.entries)} entries)"

logs = LogFile("system.log", ["Start", "Deploy", "Error"])
print(logs)
```

Output:

```
📄 LogFile: system.log (3 entries)
```

---

## ✅ 14. Best Practices

✔️ Use classes to group related operations (e.g., EC2, S3, Jenkins).
✔️ Keep methods **short and single-purpose**.
✔️ Use **inheritance and composition** wisely.
✔️ Prefer **encapsulation** for sensitive data (credentials).
✔️ Write **docstrings** and comments.
✔️ Separate logic into **modules** (e.g., `aws.py`, `docker.py`, `logger.py`).

---

## 🧾 16. Summary

| Concept            | Description                |
| ------------------ | -------------------------- |
| **Class & Object** | Blueprint & instance       |
| **Encapsulation**  | Hide data                  |
| **Inheritance**    | Reuse logic                |
| **Polymorphism**   | One method, many behaviors |
| **Abstraction**    | Hide complexity            |
| **Composition**    | Combine classes            |
| **Magic Methods**  | Customize class behavior   |

---
