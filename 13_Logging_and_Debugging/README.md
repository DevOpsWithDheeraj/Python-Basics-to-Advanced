# 🧩 13_Logging_and_Debugging

In DevOps automation, **logging and debugging** are essential for identifying issues, tracking execution, and ensuring reliability in scripts and systems.
Python provides a robust **logging module** and built-in debugging tools like **pdb** to help developers monitor and fix issues efficiently.

---

## 🔹 1. Python Logging Module

### 📘 Definition:

The **logging module** in Python is used to record messages that describe the flow of a program, including information, warnings, and errors.

It allows:

* Tracking **events and errors** in automation scripts
* Writing logs to **console or file**
* Setting different **log levels** for better filtering

---

### 🧩 Example 1: Basic Logging Example

```python
import logging

# Configure basic logging
logging.basicConfig(level=logging.INFO)

logging.debug("This is a debug message")
logging.info("Script started successfully")
logging.warning("Low disk space warning")
logging.error("File not found!")
logging.critical("Server down! Immediate attention needed!")
```

🟢 Output:

```
INFO:root:Script started successfully
WARNING:root:Low disk space warning
ERROR:root:File not found!
CRITICAL:root:Server down! Immediate attention needed!
```

✅ *Use Case:* Log automation progress (e.g., file backup, deployment steps).

---

## 🔹 2. Logging Levels and Configuration

### 📘 Definition:

Logging levels help define the **severity** of log messages.
Python provides the following levels (from lowest to highest severity):

| Level    | Description                                           |
| -------- | ----------------------------------------------------- |
| DEBUG    | Detailed information, useful for debugging            |
| INFO     | General information about normal operations           |
| WARNING  | Something unexpected happened, but program still runs |
| ERROR    | Serious issue; some function failed                   |
| CRITICAL | Very serious error; may cause system failure          |

---

### 🧩 Example 2: Custom Logging Configuration

```python
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S'
)

logging.debug("Debugging the script execution")
logging.info("Deployment script initiated")
logging.warning("Memory usage high")
logging.error("Build failed due to missing dependency")
logging.critical("Critical failure in pipeline execution")
```

🟢 Output (formatted):

```
2025-11-02 22:00:01 - DEBUG - Debugging the script execution
2025-11-02 22:00:02 - INFO - Deployment script initiated
2025-11-02 22:00:03 - WARNING - Memory usage high
2025-11-02 22:00:04 - ERROR - Build failed due to missing dependency
2025-11-02 22:00:05 - CRITICAL - Critical failure in pipeline execution
```

✅ *Use Case:* Helps in Jenkins or CI/CD jobs for detailed run logs.

---

## 🔹 3. Writing Logs to Files

### 📘 Definition:

You can store logs in files for **long-term tracking, analysis, or debugging**.
This is useful for DevOps pipelines, cron jobs, and background services.

---

### 🧩 Example 3: Writing Logs to File

```python
import logging

logging.basicConfig(
    filename='automation.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

logging.info("Script started")
logging.warning("API response delayed")
logging.error("Failed to connect to database")
```

🟢 File: `automation.log`

```
2025-11-02 22:05:01 - INFO - Script started
2025-11-02 22:05:02 - WARNING - API response delayed
2025-11-02 22:05:03 - ERROR - Failed to connect to database
```

✅ *Use Case:* Maintain automation or monitoring logs in `/var/log/devops_scripts.log`.

---

## 🔹 4. Debugging with **pdb** (Python Debugger)

### 📘 Definition:

`pdb` is the **Python Debugger**, a built-in tool that helps you **pause code execution**, inspect variables, and step through lines interactively.

It is invaluable when troubleshooting complex automation logic.

---

### 🧩 Example 4: Using pdb for Debugging

```python
import pdb

def divide(a, b):
    pdb.set_trace()  # Pauses execution here
    return a / b

result = divide(10, 0)
print(result)
```

When you run this, Python enters **debug mode** in the terminal:

```
(Pdb) p a
10
(Pdb) p b
0
(Pdb) c
ZeroDivisionError: division by zero
```

✅ *Common pdb Commands:*

| Command   | Description          |
| --------- | -------------------- |
| `n`       | Next line            |
| `s`       | Step into function   |
| `c`       | Continue execution   |
| `p <var>` | Print variable value |
| `q`       | Quit debugger        |

✅ *Use Case:* Debug automation errors like failed file transfers or API calls.

---

## 🔹 5. Debugging with IDE Debuggers

### 📘 Definition:

Modern IDEs (like **VS Code**, **PyCharm**, or **IDLE**) come with **graphical debuggers** that allow:

* Setting **breakpoints**
* Viewing **variable values in real-time**
* Stepping through code visually

✅ *Use Case:* Debug Jenkins scripts or AWS automation functions before deployment.

---

## 🧾 Summary

| Concept        | Description                         | DevOps Use Case                |
| -------------- | ----------------------------------- | ------------------------------ |
| Logging module | Built-in library for event tracking | Monitor automation scripts     |
| Log levels     | Define severity                     | Filter logs in CI/CD           |
| File logging   | Write logs to files                 | Persist job logs               |
| pdb            | Command-line debugger               | Debug runtime errors           |
| IDE Debugger   | Visual debugging                    | Test Python automation locally |

---

## 💡 DevOps Real-Life Use Cases

* Record execution of **infrastructure provisioning scripts**.
* Debug failed **AWS automation (boto3)** or **API integrations**.
* Maintain **deployment logs** for auditing and compliance.
* Detect and resolve **cron job or CI/CD failures**.

---
