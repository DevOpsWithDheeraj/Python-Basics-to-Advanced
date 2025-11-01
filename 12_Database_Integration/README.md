# 🗄️ 12_Database_Integration

In DevOps, automation scripts often need to **store, fetch, and manage data** such as build logs, monitoring metrics, or deployment information.
Python provides easy ways to integrate with various databases like **MySQL, PostgreSQL, and SQLite** to perform **CRUD operations** (Create, Read, Update, Delete).

---

## 🔹 1. Connecting to Databases (MySQL, PostgreSQL, SQLite)

### 📘 Definition:

Python connects to databases using libraries like:

* **MySQL** → `mysql.connector`
* **PostgreSQL** → `psycopg2`
* **SQLite** → `sqlite3` (comes pre-installed with Python)

These libraries help execute SQL queries and manage data from within Python scripts — perfect for automation, logging, or analytics.

---

### 🧩 Example 1: Connecting to **SQLite Database**

SQLite is **lightweight** and ideal for small automation projects or local data storage.

```python
import sqlite3

# Connect to database (creates if not exists)
conn = sqlite3.connect("devops_data.db")

# Create a cursor to execute SQL commands
cursor = conn.cursor()

# Create a table
cursor.execute('''CREATE TABLE IF NOT EXISTS builds (
                    id INTEGER PRIMARY KEY,
                    project_name TEXT,
                    status TEXT,
                    build_time TEXT)''')

print("Database and table created successfully!")

conn.close()
```

✅ *Use Case:* Store Jenkins build data or automation logs locally.

---

### 🧩 Example 2: Connecting to **MySQL Database**

```python
import mysql.connector

# Connect to MySQL
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="devops_db"
)

cursor = conn.cursor()
print("Connected to MySQL Database successfully!")
conn.close()
```

✅ *Use Case:* Automate storing deployment metadata in a MySQL database.

---

### 🧩 Example 3: Connecting to **PostgreSQL Database**

```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    database="devops_db",
    user="postgres",
    password="password"
)

cursor = conn.cursor()
print("Connected to PostgreSQL successfully!")
conn.close()
```

✅ *Use Case:* Store monitoring metrics or CI/CD job results.

---

## 🔹 2. Executing CRUD Operations

CRUD = **Create, Read, Update, Delete** — the four fundamental database operations.

Let’s perform these using **SQLite** as an example (same concept works for MySQL/PostgreSQL).

---

### 🧱 Create (Insert Data)

```python
import sqlite3

conn = sqlite3.connect("devops_data.db")
cursor = conn.cursor()

# Insert data into the table
cursor.execute("INSERT INTO builds (project_name, status, build_time) VALUES (?, ?, ?)",
               ("WebApp", "Success", "2025-11-02 22:00"))

conn.commit()
print("Record inserted successfully!")
conn.close()
```

---

### 📖 Read (Fetch Data)

```python
conn = sqlite3.connect("devops_data.db")
cursor = conn.cursor()

cursor.execute("SELECT * FROM builds")
rows = cursor.fetchall()

for row in rows:
    print(row)

conn.close()
```

✅ *Use Case:* Generate a report of the last 10 builds.

---

### ✏️ Update (Modify Data)

```python
conn = sqlite3.connect("devops_data.db")
cursor = conn.cursor()

cursor.execute("UPDATE builds SET status = 'Failed' WHERE id = 1")

conn.commit()
print("Record updated successfully!")
conn.close()
```

✅ *Use Case:* Update build status after rerun.

---

### ❌ Delete (Remove Data)

```python
conn = sqlite3.connect("devops_data.db")
cursor = conn.cursor()

cursor.execute("DELETE FROM builds WHERE id = 1")
conn.commit()

print("Record deleted successfully!")
conn.close()
```

✅ *Use Case:* Delete old logs or completed job records.

---

## 🔹 3. Reading Data for Reporting or Automation

You can use database data to **generate reports**, **trigger alerts**, or **feed CI/CD dashboards**.

**Example:** Fetch failed builds and print report.

```python
import sqlite3

conn = sqlite3.connect("devops_data.db")
cursor = conn.cursor()

cursor.execute("SELECT project_name, status FROM builds WHERE status='Failed'")
failed_builds = cursor.fetchall()

if failed_builds:
    print("🚨 Failed Builds Report:")
    for build in failed_builds:
        print(f"Project: {build[0]} | Status: {build[1]}")
else:
    print("✅ All builds passed successfully!")

conn.close()
```

✅ *Automation Idea:* Use this in Jenkins post-build script to notify failures via email or Slack.

---

## 🧾 Summary

| Database   | Library         | Use Case                                    |
| ---------- | --------------- | ------------------------------------------- |
| SQLite     | sqlite3         | Local storage for automation logs           |
| MySQL      | mysql.connector | Centralized DevOps data management          |
| PostgreSQL | psycopg2        | Storing CI/CD pipeline results or analytics |

---

## 💡 DevOps Real-Life Use Cases

* Store **deployment history** or build logs for auditing.
* Automate **report generation** from CI/CD pipelines.
* Manage **infrastructure inventory** data (servers, clusters).
* Track **test results** or **error logs** from automation scripts.

---
