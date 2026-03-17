# 🧱 03_Data_Structures — Lists, Tuples, Sets, and Dictionaries

**Data Structure** in Python is a way of **organizing, storing, and managing data efficiently so that it can be accessed and modified easily.**

In simple words, a **data structure** defines how data is **arranged in memory and how operations like insertion, deletion, searching, and updating are performed.**

## Common Data Structures in Python:

| Data Structure | Description                                |
| -------------- | ------------------------------------------ |
| **List**       | Ordered and mutable collection of elements |
| **Tuple**      | Ordered but immutable collection           |
| **Set**        | Unordered collection of unique elements    |
| **Dictionary** | Collection of key–value pairs              |

---

## 📋 1. List — Ordered and Mutable Collection

**Definition:**  
A **list** is an ordered, **mutable (changeable)** collection of items.

**Syntax:**
```python
my_list = [item1, item2, item3]
````

### Example:

```python
tools = ["Docker", "Jenkins", "Ansible", "Kubernetes"]
print(tools)
print(tools[0])     # Access first element
print(tools[-1])    # Access last element
```

### Add / Remove / Modify:

```python
tools.append("Terraform")     # Add item
tools.remove("Jenkins")       # Remove item
tools[1] = "GitLab"           # Modify item
print(tools)
```

### Loop Through a List:

```python
for tool in tools:
    print(f"Setting up {tool}...")
```

💡 **DevOps Use Case:**
Store a list of servers and loop through them for monitoring or deployment.

```python
servers = ["web01", "db01", "cache01"]
for s in servers:
    print(f"Deploying updates on {s}...")
```

---

## 🧱 2. Tuple — Ordered and Immutable Collection

**Definition:**
A **tuple** is an ordered, **immutable (unchangeable)** collection of items.
Used when you want to store fixed data.

**Syntax:**

```python
my_tuple = (item1, item2, item3)
```

### Example:

```python
credentials = ("admin", "p@ssw0rd123")
print(credentials[0])  # Access username
```

### Why Tuples in DevOps?

* Used for **read-only configurations**
* Example: storing **static credentials**, **fixed environment settings**, etc.

```python
aws_regions = ("us-east-1", "us-west-2", "ap-south-1")
for region in aws_regions:
    print(f"Deploying resources to {region}")
```

---

## 🔢 3. Set — Unordered, Unique Collection

**Definition:**
A **set** is an **unordered collection** that does **not allow duplicates**.

**Syntax:**

```python
my_set = {item1, item2, item3}
```

### Example:

```python
tools = {"Docker", "Ansible", "Ansible", "Terraform"}
print(tools)  # Removes duplicates automatically
```

### Set Operations:

```python
devops_tools = {"Docker", "Ansible", "Jenkins"}
cloud_tools = {"AWS", "Terraform", "Docker"}

print(devops_tools.union(cloud_tools))        # Combine sets
print(devops_tools.intersection(cloud_tools)) # Common elements
```

💡 **DevOps Use Case:**
Identify common tools between multiple environments (e.g., staging vs production).

---

## 🔑 4. Dictionary — Key-Value Pairs (Most Used in DevOps)

**Definition:**
A **dictionary** stores data in **key-value** pairs.
It’s **mutable**, **unordered**, and **highly flexible** — ideal for structured data like JSON.

**Syntax:**

```python
my_dict = {"key": "value", "key2": "value2"}
```

### Example:

```python
server = {
    "name": "web01",
    "ip": "192.168.1.10",
    "status": "running"
}

print(server["name"])
print(server.get("status"))
```

### Add / Update / Delete:

```python
server["region"] = "ap-south-1"     # Add
server["status"] = "stopped"        # Update
del server["ip"]                    # Delete
print(server)
```

---

### Loop Through Dictionary:

```python
for key, value in server.items():
    print(f"{key} → {value}")
```

💡 **DevOps Use Case:**
Represent AWS EC2 instance data or configuration file content.

```python
ec2_instance = {
    "InstanceID": "i-0abcd1234ef56789",
    "Type": "t2.micro",
    "State": "running",
    "Region": "ap-south-1"
}

for key, value in ec2_instance.items():
    print(f"{key}: {value}")
```

---

## ⚙️ 5. Nested Data Structures

You can **combine multiple structures** together — useful for real DevOps JSON-like data.

### Example: List of Dictionaries

```python
servers = [
    {"name": "web01", "status": "running"},
    {"name": "db01", "status": "stopped"},
    {"name": "cache01", "status": "running"}
]

for s in servers:
    print(f"{s['name']} → {s['status']}")
```

💡 **Use Case:**
Store and process server inventory, API response, or cluster node data.

---

### Example: Dictionary of Lists

```python
deployments = {
    "production": ["web01", "db01"],
    "staging": ["web02", "db02"]
}

for env, srv_list in deployments.items():
    print(f"{env} servers → {srv_list}")
```

---

## 🧠 6. Conversion Between Data Structures

### Examples:

```python
# List to Set
lst = [1, 2, 2, 3]
print(set(lst))

# Tuple to List
tpl = (1, 2, 3)
print(list(tpl))

# Dict Keys/Values
data = {"tool": "Docker", "env": "Prod"}
print(list(data.keys()))
print(list(data.values()))
```

---

## 🧰 7. DevOps Real-world Examples

### ✅ Example 1: Parse JSON from AWS CLI

```python
import json

aws_output = '{"InstanceId":"i-0123456","State":"running","Type":"t2.micro"}'
instance = json.loads(aws_output)

print(instance["InstanceId"])
print(instance["State"])
```

---

### ✅ Example 2: Server Inventory Report

```python
servers = [
    {"name": "web01", "status": "running"},
    {"name": "db01", "status": "stopped"},
    {"name": "cache01", "status": "running"}
]

running = [s["name"] for s in servers if s["status"] == "running"]
print("Running Servers:", running)
```

---

### ✅ Example 3: Compare Tools Between Teams

```python
team1 = {"Docker", "Jenkins", "Ansible"}
team2 = {"Docker", "Terraform", "GitLab"}

common = team1.intersection(team2)
print("Common Tools:", common)
```

---

## 🧾 8. Summary

| Data Structure | Ordered                        | Mutable | Allows Duplicates   | Example            |
| -------------- | ------------------------------ | ------- | ------------------- | ------------------ |
| **List**       | ✅ Yes                          | ✅ Yes   | ✅ Yes               | `[1, 2, 3]`        |
| **Tuple**      | ✅ Yes                          | ❌ No    | ✅ Yes               | `(1, 2, 3)`        |
| **Set**        | ❌ No                           | ✅ Yes   | ❌ No                | `{1, 2, 3}`        |
| **Dictionary** | ❌ No (3.7+: ordered insertion) | ✅ Yes   | ❌ No duplicate keys | `{"key": "value"}` |

---
