
# 🔹 1. Time Complexity

### ✅ Definition

Time Complexity measures **how the running time of an algorithm grows** as the input size (`n`) increases.

👉 It does **NOT** measure actual time (seconds), but the **number of operations**.

---

### ✅ Common Time Complexities

| Complexity | Name        | Example                 |
| ---------- | ----------- | ----------------------- |
| O(1)       | Constant    | Accessing array element |
| O(log n)   | Logarithmic | Binary Search           |
| O(n)       | Linear      | Traversing array        |
| O(n log n) | Linear Log  | Merge Sort              |
| O(n²)      | Quadratic   | Nested loops            |
| O(2ⁿ)      | Exponential | Recursive Fibonacci     |

---

### ✅ Example 1: Constant Time — O(1)

```python
def get_first(arr):
    return arr[0]
```

👉 Only one operation → **O(1)**

---

### ✅ Example 2: Linear Time — O(n)

```python
def print_all(arr):
    for i in arr:
        print(i)
```

👉 Runs `n` times → **O(n)**

---

### ✅ Example 3: Quadratic Time — O(n²)

```python
def pairs(arr):
    for i in arr:
        for j in arr:
            print(i, j)
```

👉 Runs `n × n = n²` → **O(n²)**

---

### ✅ Example 4: Logarithmic Time — O(log n)

```python
def binary_search(arr, target):
    left, right = 0, len(arr)-1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
```

👉 Input halves every step → **O(log n)**

---

# 🔹 2. Space Complexity

### ✅ Definition

Space Complexity measures **how much memory an algorithm uses** as input size increases.

---

### ✅ Types of Space

1. **Auxiliary Space** → Extra memory used
2. **Input Space** → Memory used by input

---

### ✅ Example 1: Constant Space — O(1)

```python
def sum(a, b):
    return a + b
```

👉 Uses fixed variables → **O(1)**

---

### ✅ Example 2: Linear Space — O(n)

```python
def copy(arr):
    new_arr = []
    for i in arr:
        new_arr.append(i)
    return new_arr
```

👉 New array of size `n` → **O(n)**

---

### ✅ Example 3: Quadratic Space — O(n²)

```python
def create_matrix(n):
    matrix = []
    for i in range(n):
        row = []
        for j in range(n):
            row.append(0)
        matrix.append(row)
    return matrix
```

👉 Explanation:

* You are creating a 2D matrix (list of lists)
* Total elements = n × n = n²
* Memory grows with square of input size

✅ Space Complexity = O(n²)

---

# 🔹 3. Asymptotic Notations

These are mathematical tools to describe **growth rate of algorithms**.

---

## 🔸 3.1 Big-O Notation (O)

### ✅ Definition

Represents the **upper bound (worst-case)** time complexity.

👉 "Maximum time an algorithm can take"

---

### ✅ Example

```python
for i in range(n):
    print(i)
```

👉 Worst case operations = `n` → **O(n)**

---

## 🔸 3.2 Big-Omega Notation (Ω)

### ✅ Definition

Represents the **lower bound (best-case)** time complexity.

👉 "Minimum time required"

---

### ✅ Example

Linear Search:

* Best case → element found at first position
  👉 **Ω(1)**

---

## 🔸 3.3 Big-Theta Notation (Θ)

### ✅ Definition

Represents the **tight bound (average case)**

👉 When upper and lower bounds are same

---

### ✅ Example

```python
for i in range(n):
    print(i)
```

👉 Always runs `n` times
👉 **Θ(n)**

---

# 🔹 4. Key Rules for Calculating Complexity

---

### ✅ Rule 1: Ignore Constants

```python
O(2n + 3) → O(n)
```

---

### ✅ Rule 2: Focus on Highest Term

```python
O(n² + n) → O(n²)
```

---

### ✅ Rule 3: Nested Loops Multiply

```python
for i in range(n):
    for j in range(n):
```

👉 O(n × n) = **O(n²)**

---

### ✅ Rule 4: Separate Loops Add

```python
for i in range(n):
    print(i)

for j in range(n):
    print(j)
```

👉 O(n + n) = **O(n)**

---

# 🔹 5. Time vs Space Tradeoff

Sometimes:

* Faster algorithms use **more memory**
* Memory-efficient algorithms take **more time**

👉 Example:

* Merge Sort → Fast but uses extra space
* Bubble Sort → Less space but slower

---

# 🔹 6. Summary

* **Time Complexity** → How fast algorithm runs
* **Space Complexity** → How much memory it uses
* **Big-O** → Worst case
* **Big-Ω** → Best case
* **Big-Θ** → Average case

---

# 🔹 7. Quick Comparison Table

| Concept          | Meaning               |
| ---------------- | --------------------- |
| Time Complexity  | Execution time growth |
| Space Complexity | Memory usage growth   |
| Big-O            | Worst case            |
| Big-Ω            | Best case             |
| Big-Θ            | Average case          |

---
