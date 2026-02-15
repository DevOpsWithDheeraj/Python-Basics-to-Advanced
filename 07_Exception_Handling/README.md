# ⚠️ 07_Exception_Handling — Managing Errors Gracefully in Python for DevOps

## 🧠 1. What is an Exception?

**Definition:**  
An **exception** is an error that occurs during program execution, disrupting the normal flow of instructions.

### Example:
```python
print("Starting script...")
x = 10 / 0  # Division by zero error
print("Script completed.")
````

Output:

```
ZeroDivisionError: division by zero
```

💡 Without exception handling, the script **stops immediately**.

---

## 🧩 2. Exception Handling Syntax

```python
try:
    # Code that might cause an error
except ExceptionType:
    # Code to handle that error
```

---

### Example:

```python
try:
    num = int(input("Enter a number: "))
    print(10 / num)
except ZeroDivisionError:
    print("❌ You cannot divide by zero!")
except ValueError:
    print("❌ Please enter a valid number!")
```

---

## ⚙️ 3. Using `else` and `finally` Blocks

```python
try:
    file = open("servers.txt", "r")
except FileNotFoundError:
    print("⚠️ File not found.")
else:
    print("✅ File opened successfully.")
    file.close()
finally:
    print("🔒 Closing script.")
```

💡

* `else` → Executes only when there is **no exception**.
* `finally` → Executes **always**, even if an error occurs (used for cleanup).

---

## 🔧 4. Common Python Exceptions

| Exception           | Description              |
| ------------------- | ------------------------ |
| `FileNotFoundError` | File not found           |
| `ZeroDivisionError` | Division by zero         |
| `ValueError`        | Wrong data type          |
| `KeyError`          | Missing key in dict      |
| `IndexError`        | Invalid list index       |
| `TypeError`         | Operation on wrong type  |
| `ImportError`       | Module not found         |
| `TimeoutError`      | Operation timed out      |
| `PermissionError`   | Insufficient permissions |

---

## 🌐 5. DevOps Example — File Monitoring Script

```python
try:
    with open("system.log", "r") as log:
        print("Log file opened successfully.")
except FileNotFoundError:
    print("❌ Log file not found. Please verify the path.")
finally:
    print("✅ File check complete.")
```

💡 **Use Case:**
Verify log or config file existence before reading it.

---

## 🧩 6. Handling AWS API Errors (Using boto3)

```python
import boto3
from botocore.exceptions import NoCredentialsError, ClientError

try:
    s3 = boto3.client("s3")
    s3.list_buckets()
    print("✅ Connected to AWS S3.")
except NoCredentialsError:
    print("❌ AWS credentials not found.")
except ClientError as e:
    print("⚠️ AWS Client Error:", e)
```

💡 **Use Case:**
Handle credential or permission issues when automating AWS operations.

---

## 🔐 7. Network Error Handling with `requests`

```python
import requests

try:
    response = requests.get("https://jenkins.example.com")
    print("Jenkins Status Code:", response.status_code)
except requests.exceptions.ConnectionError:
    print("❌ Could not connect to Jenkins.")
except requests.exceptions.Timeout:
    print("⏰ Request timed out.")
finally:
    print("🔄 Connection attempt finished.")
```

💡 **Use Case:**
Monitor CI/CD endpoints or trigger pipelines safely.

---

## ⚙️ 8. Handling Subprocess Errors

```python
import subprocess

try:
    result = subprocess.run(["ls", "/invalid_dir"], check=True, text=True, capture_output=True)
    print(result.stdout)
except subprocess.CalledProcessError as e:
    print("❌ Command failed:", e)
```

💡 **Use Case:**
Safely execute Linux commands and handle failed executions in scripts.

---

## 🧩 9. Using `raise` to Trigger Custom Exceptions

```python
import boto3
from botocore.exceptions import ClientError

s3 = boto3.client('s3')

try:
    s3.upload_file('data.txt', 'my-bucket', 'data.txt')
except ClientError as e:
    error_code = e.response['Error']['Code']
    if error_code == 'NoSuchBucket':
        raise Exception("❌ The target S3 bucket does not exist. Check bucket name or region.") from e
    elif error_code == 'AccessDenied':
        raise PermissionError("🚫 Access denied to the S3 bucket. Verify IAM policy.") from e
    else:
        raise        # re-raise unknown AWS errors

```

💡 **Use Case:**
Enforce valid input during automation (e.g., only deploy to allowed environments).

---

## 🧠 10. Creating Custom Exceptions

```python
class DeploymentError(Exception):
    """Custom exception for deployment failures"""
    pass

def deploy(version):
    if version < 1.0:
        raise DeploymentError("Invalid version — deployment aborted.")
    print("✅ Deployment successful!")

try:
    deploy(0.8)
except DeploymentError as e:
    print("🚨 Custom Exception:", e)
```

💡 **Use Case:**
Create project-specific errors like `ServerError`, `APIFailure`, `ConfigMissingError`.

---

## 🔁 11. Retrying Failed Operations (Common in DevOps)

```python
import time

for i in range(3):
    try:
        print("Attempting to connect to server...")
        raise ConnectionError
    except ConnectionError:
        print(f"⚠️ Connection failed. Retrying ({i+1}/3)...")
        time.sleep(2)
    else:
        print("✅ Connected successfully.")
        break
else:
    print("❌ All retries failed.")
```

💡 **Use Case:**
Retry failed SSH, API, or deployment operations.

---

## 📋 12. Logging Exceptions (Instead of Printing)

```python
import logging

logging.basicConfig(filename="error.log", level=logging.ERROR)

try:
    x = 10 / 0
except Exception as e:
    logging.error("Error occurred: %s", e)
    print("⚠️ Error logged to error.log")
```

💡 **Use Case:**
Store all automation errors in log files for debugging.

---

## ✅ 13. Best Practices

✔️ Use **specific exceptions** instead of generic `except:` <br>
✔️ Always log errors instead of ignoring them <br>
✔️ Use `finally` to clean up resources (e.g., close connections) <br>
✔️ Avoid exposing sensitive info in error messages <br>
✔️ Use **retry logic** for network operations <br>
✔️ Create **custom exception classes** for clarity <br>
✔️ Use `raise` for enforcing rules in scripts <br>

---

## 🧾 15. Summary

| Concept            | Description                     |
| ------------------ | ------------------------------- |
| `try/except`       | Handle possible errors          |
| `else`             | Runs if no error occurs         |
| `finally`          | Always executes (cleanup)       |
| `raise`            | Manually trigger exception      |
| `Custom Exception` | Define project-specific errors  |
| `Retry Logic`      | Handle transient network issues |
| `Logging`          | Save errors for debugging       |

---
