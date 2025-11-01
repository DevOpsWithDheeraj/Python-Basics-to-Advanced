# 🚀 14_Testing_and_CI_CD

In DevOps, **testing and continuous integration (CI/CD)** are essential to ensure code quality, prevent regressions, and maintain reliable automation pipelines.
Python provides a powerful testing ecosystem, with tools for **unit testing, mocking, code formatting, and CI/CD integration**.

---

## 🔹 1. Unit Testing with `unittest` and `pytest`

### 📘 Definition:

* **Unit testing** verifies that individual components (functions, modules) work as expected.
* **unittest** is Python’s built-in testing framework.
* **pytest** is a more powerful, user-friendly alternative widely used in DevOps projects.

---

### 🧩 Example 1: Using `unittest`

```python
import unittest

def add(a, b):
    return a + b

class TestMathOperations(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)

if __name__ == '__main__':
    unittest.main()
```

🟢 Output:

```
..
----------------------------------------------------------------------
Ran 2 tests in 0.001s
OK
```

✅ *Use Case:* Validate automation functions before integrating into Jenkins or GitLab pipelines.

---

### 🧩 Example 2: Using `pytest`

```python
def add(a, b):
    return a + b

def test_add():
    assert add(5, 3) == 8
    assert add(-2, 2) == 0
```

Run the test:

```bash
pytest test_math.py
```

🟢 Output:

```
collected 1 item
test_math.py .                                                   [100%]
```

✅ *Use Case:* Run fast, simple tests in CI/CD for AWS or Docker automation scripts.

---

## 🔹 2. Mocking and Fixtures

### 📘 Definition:

* **Mocking** replaces real dependencies (e.g., API calls, DB connections) with fake ones for safe testing.
* **Fixtures** provide reusable test setup/teardown resources (e.g., test data, temporary files).

---

### 🧩 Example 3: Mocking with `unittest.mock`

```python
from unittest.mock import patch

def get_user_data():
    import requests
    response = requests.get("https://api.example.com/users/1")
    return response.json()

@patch("requests.get")
def test_get_user_data(mock_get):
    mock_get.return_value.json.return_value = {"name": "Dheeraj", "role": "DevOps Engineer"}
    result = get_user_data()
    assert result["name"] == "Dheeraj"
```

✅ *Use Case:* Test automation scripts without hitting live APIs or AWS services.

---

### 🧩 Example 4: Using `pytest` Fixtures

```python
import pytest

@pytest.fixture
def sample_data():
    return {"project": "DevOps Automation", "status": "success"}

def test_sample_data(sample_data):
    assert sample_data["status"] == "success"
```

✅ *Use Case:* Reuse setup data in multiple test cases (e.g., test Jenkins or Docker APIs).

---

## 🔹 3. Integrating Python Tests in CI/CD Pipelines (Jenkins / GitLab)

### 📘 Definition:

DevOps teams use CI/CD tools like **Jenkins** and **GitLab CI** to automate testing whenever code is committed or deployed.

You can integrate Python tests to ensure **code reliability before deployment**.

---

### 🧩 Example 5: Jenkins Pipeline Integration

**Jenkinsfile:**

```groovy
pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'pip install pytest'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest --junitxml=report.xml'
            }
        }
    }
    post {
        always {
            junit 'report.xml'
        }
    }
}
```

✅ *Use Case:* Automatically run tests for Python scripts during deployment or after every code change.

---

### 🧩 Example 6: GitLab CI Integration

**.gitlab-ci.yml:**

```yaml
stages:
  - test

test_python:
  image: python:3.10
  stage: test
  script:
    - pip install pytest
    - pytest --maxfail=1 --disable-warnings -q
```

✅ *Use Case:* Validate Python automation scripts before merging branches.

---

## 🔹 4. Code Quality with `flake8`, `black`, and `mypy`

### 📘 Definition:

To maintain clean, consistent, and bug-free code, Python uses **linting** and **formatting** tools.

| Tool       | Purpose                                      |
| ---------- | -------------------------------------------- |
| **flake8** | Checks for syntax errors and PEP8 violations |
| **black**  | Automatically formats Python code            |
| **mypy**   | Performs static type checking                |

---

### 🧩 Example 7: Using `flake8`

```bash
pip install flake8
flake8 my_script.py
```

🟢 Output:

```
my_script.py:10:5: E303 too many blank lines (2)
```

✅ *Use Case:* Enforce consistent coding standards in DevOps scripts.

---

### 🧩 Example 8: Using `black`

```bash
pip install black
black my_script.py
```

🟢 Output:

```
reformatted my_script.py
All done! ✨ 🍰 ✨
```

✅ *Use Case:* Automatically format scripts before deployment (add to pre-commit hooks).

---

### 🧩 Example 9: Using `mypy` (Type Checking)

```python
def greet(name: str) -> str:
    return "Hello, " + name

greet(123)  # ❌ Type mismatch
```

Run:

```bash
mypy script.py
```

🟢 Output:

```
script.py:4: error: Argument 1 to "greet" has incompatible type "int"; expected "str"
```

✅ *Use Case:* Prevent type-related errors in automation pipelines.

---

## 🧾 Summary

| Topic        | Tool                  | Description               | DevOps Use Case                   |
| ------------ | --------------------- | ------------------------- | --------------------------------- |
| Unit Testing | unittest / pytest     | Test individual functions | Validate automation logic         |
| Mocking      | unittest.mock         | Replace APIs/DBs          | Safe test environments            |
| Fixtures     | pytest                | Setup reusable data       | Simplify complex tests            |
| CI/CD        | Jenkins / GitLab      | Automate testing          | Ensure code quality before deploy |
| Code Quality | flake8 / black / mypy | Lint, format, type check  | Maintain consistent standards     |

---

## 💡 DevOps Real-Life Use Cases

* Automatically run **unit tests** before pushing code to production.
* Integrate **pytest reports** in Jenkins dashboard.
* Ensure **code formatting & typing** before Terraform or Ansible automation runs.
* Detect **API or deployment script failures** early through CI/CD validation.

---
