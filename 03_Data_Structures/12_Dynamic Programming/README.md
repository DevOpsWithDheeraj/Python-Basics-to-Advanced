
# 🔷 1. What is Dynamic Programming (DP)?

**Definition:** <br>
Dynamic Programming is an algorithmic technique used to solve problems by **breaking them into smaller overlapping subproblems**, solving each subproblem **only once**, and **storing the result** to avoid repeated computation.


## 🔷 Key Idea

👉 “**Don’t repeat work — store and reuse results**”

Dynamic Programming is mainly used when: 

### ✅ 1. Overlapping Subproblems
* Same subproblem occurs multiple times <br>
👉 Example: Fibonacci

### ✅ 2. Optimal Substructure
* Optimal solution can be built from optimal solutions of subproblems <br>
👉 Example: Shortest path



## 🔷 Two Approaches in DP

1. **Top-Down (Memoization)**

   * Use recursion + cache (dictionary/array)
2. **Bottom-Up (Tabulation)**

   * Build solution iteratively using a table


## 🔷 Example: Fibonacci Number

👉 Problem: Find nth Fibonacci number
Formula:

```
F(n) = F(n-1) + F(n-2)
```


## 🔷 Normal Recursion (Inefficient)

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

❌ Time Complexity: **O(2ⁿ)** (very slow due to repeated calls)


## 🔷 Dynamic Programming Solution

### ✅ Top-Down (Memoization)

```python
def fib(n, dp={}):
    if n in dp:
        return dp[n]
    
    if n <= 1:
        return n
    
    dp[n] = fib(n-1, dp) + fib(n-2, dp)
    return dp[n]

print(fib(6))  # Output: 8
```


### ✅ Bottom-Up (Tabulation)

```python
def fib(n):
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

print(fib(6))  # Output: 8
```


## 🔷 Why DP is Better?

| Approach            | Time Complexity |
| ------------------- | --------------- |
| Recursion           | O(2ⁿ)           |
| Dynamic Programming | O(n)            |

👉 Huge performance improvement 🚀



# 🔷 2. Two Main Approaches of DP

## 🔹 1. Top-Down Approach (Memoization)

* Uses **recursion**
* Stores results in a cache (dictionary/array)
* Avoids recomputation

## 📌 Example: Fibonacci (Memoization)

```python
def fib(n, dp={}):
    if n in dp:
        return dp[n]
    if n <= 1:
        return n
    dp[n] = fib(n-1, dp) + fib(n-2, dp)
    return dp[n]

print(fib(6))  # Output: 8
```

### ✔️ Explanation:

* Without DP → exponential time
* With DP → linear time

---

## 🔹 2. Bottom-Up Approach (Tabulation)

* Uses **iteration**
* Builds solution from smallest subproblems

### 📌 Example: Fibonacci (Tabulation)

```python
def fib(n):
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

print(fib(6))  # Output: 8
```


# 🔷 3. Types of Dynamic Programming Problems

## 🔸 1. Linear DP

Problems where state depends on previous states in a sequence

### 📌 Example: Fibonacci, Climbing Stairs

```python
def climb_stairs(n):
    if n <= 2:
        return n
    
    dp = [0]*(n+1)
    dp[1], dp[2] = 1, 2
    
    for i in range(3, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```


## 🔸 2. Grid-Based DP

Used in matrix/grid traversal problems

### 📌 Example: Unique Paths

```python
def unique_paths(m, n):
    dp = [[1]*n for _ in range(m)]
    
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    
    return dp[m-1][n-1]
```

## 🔸 3. Knapsack DP

Used in optimization problems

### 📌 Example: 0/1 Knapsack

```python
def knapsack(W, wt, val, n):
    dp = [[0]*(W+1) for _ in range(n+1)]
    
    for i in range(1, n+1):
        for w in range(1, W+1):
            if wt[i-1] <= w:
                dp[i][w] = max(val[i-1] + dp[i-1][w-wt[i-1]], dp[i-1][w])
            else:
                dp[i][w] = dp[i-1][w]
    
    return dp[n][W]
```

## 🔸 4. Longest Common Subsequence (LCS)

Used in string comparison

### 📌 Example:

```python
def lcs(X, Y):
    m, n = len(X), len(Y)
    dp = [[0]*(n+1) for _ in range(m+1)]
    
    for i in range(1, m+1):
        for j in range(1, n+1):
            if X[i-1] == Y[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]
```

## 🔸 5. Subset / Partition DP

### 📌 Example: Subset Sum

```python
def subset_sum(arr, target):
    n = len(arr)
    dp = [[False]*(target+1) for _ in range(n+1)]
    
    for i in range(n+1):
        dp[i][0] = True
    
    for i in range(1, n+1):
        for j in range(1, target+1):
            if arr[i-1] <= j:
                dp[i][j] = dp[i-1][j-arr[i-1]] or dp[i-1][j]
            else:
                dp[i][j] = dp[i-1][j]
    
    return dp[n][target]
```

## 🔸 6. DP on Trees

Used in tree structures (DFS + DP)

👉 Example: Maximum path sum in a tree


## 🔸 7. DP with Bitmasking

Used when dealing with subsets

👉 Example: Traveling Salesman Problem (TSP)


## 🔸 8. Digit DP

Used in number problems with constraints

👉 Example: Count numbers with certain digit properties


# 🔷 5. Time & Space Complexity

| Approach    | Time Complexity | Space Complexity |
| ----------- | --------------- | ---------------- |
| Recursion   | Exponential     | High             |
| Memoization | O(n)            | O(n)             |
| Tabulation  | O(n)            | O(n)             |


# 🔷 6. Key Terms in DP

* **State** → Representation of subproblem
* **Transition** → Relation between states
* **Base Case** → Smallest problem
* **Memoization** → Storing results
* **Tabulation** → Iterative table filling


# 🔷 7. How to Solve DP Problems

1. Identify if DP is applicable
2. Define the **state**
3. Write the **recurrence relation**
4. Choose Top-down or Bottom-up
5. Optimize space (if possible)


# 🔷 9. Real-Life Applications

* Shortest path algorithms
* Stock market profit problems
* Text editing (spell check, diff tools)
* Game strategies
* Resource allocation

