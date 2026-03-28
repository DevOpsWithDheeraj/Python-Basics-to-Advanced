
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

# Call the function and print result
print(fib(9))
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

print(fib(9))  # Output: 34
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

print(fib(9))  # Output: 34
```


## 🔷 Why DP is Better?

| Approach            | Time Complexity |
| ------------------- | --------------- |
| Recursion           | O(2ⁿ)           |
| Dynamic Programming | O(n)            |

👉 Huge performance improvement 🚀



# 🔷 2. Two Main Approaches of DP

## 🔹 1. Top-Down Approach (Memoization)

Top-Down Approach is a Dynamic Programming technique where a problem is solved by breaking it into smaller subproblems using recursion, and storing the results (memoization) so that each subproblem is solved only once.

### 🔹 Steps in Top-Down Approach (Memoization)

Top-Down DP means: **solve using recursion + store results (memoization)**

1. **Define the Problem Recursively**

   * Express the problem in terms of smaller subproblems
   * Example:

     ```
     fib(n) = fib(n-1) + fib(n-2)
     ```

2. **Create a Storage (Memo Table)**

   * Use a **dictionary / array** to store computed results
   * This avoids recomputation

3. **Check Before Computing**

   * Before solving a subproblem:

     ```
     if n in dp:
         return dp[n]
     ```
   * If already solved → reuse it


4. **Solve Recursively**

   * If not in memory, compute using recursion
   * Break into smaller subproblems


5. **Store the Result (Memoize)**

   * Save the computed value:

     ```
     dp[n] = result
     ```

6. **Return the Result**

   * Return stored or computed value

### 🔷 Example (Fibonacci)

```python
def fib(n, dp={}):
    if n in dp:
        return dp[n]
    
    if n <= 1:
        return n
    
    dp[n] = fib(n-1, dp) + fib(n-2, dp)
    return dp[n]

print(fib(9))  # Output: 34
```

### 🔹 Flow Summary
```
Start with main problem
        ↓
Break into smaller subproblems (recursion)
        ↓
Check if already solved (dp/memo)
        ↓
If not → solve recursively
        ↓
Store result in dp
        ↓
Return result
```

### ✔️ Explanation:

* Without DP → exponential time
* With DP → linear time


## 🔷 2. Bottom-Up Approach (Tabulation)

> Bottom-Up Approach is a Dynamic Programming technique where a problem is solved by starting from the smallest subproblems and building up to the final solution iteratively, storing results in a table (array) to avoid recomputation.

> Bottom-Up Approach = Iteration + Tabulation (solve small → build big)

### 🔹 Steps in Bottom-Up Approach (Tabulation)

Bottom-Up DP means: **solve small subproblems first and build up to the final answer (iteratively)**

### 🔹 Step-by-Step Process

1. **Define the Problem Relation (Recurrence)**

   * Identify how the solution depends on smaller subproblems
   * Example:

     ```
     fib(n) = fib(n-1) + fib(n-2)
     ```

2. **Create a DP Table (Array / List)**

   * Allocate memory to store results of subproblems
   * Example:

     ```python
     dp = [0] * (n + 1)
     ```

3. **Initialize Base Cases**

   * Set initial known values
   * Example:

     ```python
     dp[0] = 0
     dp[1] = 1
     ```
     
4. **Fill the Table Iteratively**

   * Start from smallest subproblem and move upward
   * Example:

     ```python
     for i in range(2, n + 1):
         dp[i] = dp[i-1] + dp[i-2]
     ```

5. **Build Solution Step-by-Step**

   * Each value uses already computed values
   * No recursion involved

6. **Return Final Answer**

   * The required result is stored in:

     ```python
     return dp[n]
     ```

### 🔹 Example (Fibonacci)

```python id="3r7kqg"
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

---

### 🔹 Flow Summary

```text id="0tpcz6"
Start from base cases
        ↓
Initialize dp table
        ↓
Solve small subproblems first
        ↓
Build up to larger problems (iteration)
        ↓
Store results in table
        ↓
Return final answer
```



# 🔷 3. Types of Dynamic Programming Problems

## 🔸 1. Linear DP

**Linear DP** is a type of dynamic programming where:

* The problem is solved **in a linear sequence (1D)**
* Each state depends on **a fixed number of previous states**
* Usually uses a **1D array (dp[])**

👉 In simple words:
> You build the solution step-by-step from **left to right**, using previously computed values.

### 🧠 Example Problem: Climbing Stairs

#### ❓ Problem Statement

You are climbing a staircase with `n` steps.
Each time, you can climb either:

* 1 step
* 2 steps

👉 Find the total number of distinct ways to reach the top.

### 🔍 Understanding the Logic

Let:

* `dp[i]` = number of ways to reach step `i`

Then:

* To reach step `i`, you can come from:

  * Step `i-1` (1 step jump)
  * Step `i-2` (2 step jump)

So,

👉 **Recurrence Relation:**

```
dp[i] = dp[i-1] + dp[i-2]
```

### ⚙️ Base Cases

* `dp[0] = 1` → 1 way (stay at ground)
* `dp[1] = 1` → only 1 step possible

### 💻 Code Climbing Stairs (Bottom-Up Linear DP)

```python
def climb_stairs(n):
    if n <= 1:
        return 1

    dp = [0] * (n + 1)
    
    dp[0] = 1
    dp[1] = 1

    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]

print(climb_stairs(5))  # Output: 8
```

### 🔄 Step-by-Step Example (n = 5)

| Step (i) | dp[i] | Explanation |
| -------- | ----- | ----------- |
| 0        | 1     | Base case   |
| 1        | 1     | Base case   |
| 2        | 2     | (1+1)       |
| 3        | 3     | (2+1)       |
| 4        | 5     | (3+2)       |
| 5        | 8     | (5+3)       |

### ⚡ Optimized Version (Space Optimization)

Since we only need last two values:

```python
def climb_stairs(n):
    if n <= 1:
        return 1

    prev2 = 1  # dp[0]
    prev1 = 1  # dp[1]

    for i in range(2, n + 1):
        curr = prev1 + prev2
        prev2 = prev1
        prev1 = curr

    return prev1

print(climb_stairs(5))  # Output: 8
```

### 📌 Key Takeaways

* Linear DP uses **1D progression**
* Each state depends on **previous states**
* Climbing stairs is similar to **Fibonacci sequence**
* Time Complexity: **O(n)**
* Space Complexity:

  * Normal DP: **O(n)**
  * Optimized: **O(1)**


## 🔸 2. Grid-Based DP

* **Grid-Based DP** is used when a problem is represented as a **2D grid (matrix)** and you need to compute values by moving across cells.

* You solve each cell using results from **neighboring cells** (like top, left, or diagonal).


### 🧠 Core Idea

Let:

* `dp[i][j]` = answer for cell `(i, j)`

Then:

* Each cell depends on previously computed cells like:

  * Top → `(i-1, j)`
  * Left → `(i, j-1)`
  * Diagonal → `(i-1, j-1)` (in some problems)

### 🔑 General Pattern

```python
for i in range(rows):
    for j in range(cols):
        dp[i][j] = function_of_neighbors(...)
```

### 🧩 Example 1: Unique Paths

#### ❓ Problem

Move from top-left to bottom-right in a grid.
Allowed moves: ➡️ Right, ⬇️ Down


#### 🔍 Recurrence

```
dp[i][j] = dp[i-1][j] + dp[i][j-1]
```

#### 💻 Code

```python
def unique_paths(m, n):
    dp = [[1]*n for _ in range(m)]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]

print(unique_paths(3, 3))  # 6
```

#### 📊 DP Table (3×3)

```
1  1  1
1  2  3
1  3  6
```

### 🧩 Example 2: Minimum Path Sum

#### ❓ Problem

Each cell has a cost. Find minimum cost path.


#### 🔍 Recurrence

```
dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
```


#### 💻 Code

```python
def min_path_sum(grid):
    m, n = len(grid), len(grid[0])

    dp = [[0]*n for _ in range(m)]
    dp[0][0] = grid[0][0]

    # First row
    for j in range(1, n):
        dp[0][j] = dp[0][j-1] + grid[0][j]

    # First column
    for i in range(1, m):
        dp[i][0] = dp[i-1][0] + grid[i][0]

    # Fill rest
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])

    return dp[m-1][n-1]
```

### ⚡ Space Optimization (1D DP)

```python
def unique_paths(m, n):
    dp = [1]*n

    for i in range(1, m):
        for j in range(1, n):
            dp[j] = dp[j] + dp[j-1]

    return dp[-1]
```

### 🎯 Common Grid DP Patterns

| Pattern        | Movement | Example            |
| -------------- | -------- | ------------------ |
| Right + Down   | → ↓      | Unique Paths       |
| Min/Max Path   | → ↓      | Min Path Sum       |
| Diagonal       | ↘️       | LCS, Edit Distance |
| All Directions | ↑ ↓ ← →  | DP + BFS problems  |

### 📌 Key Takeaways

* Grid DP uses **2D DP array**
* Each state depends on **neighboring cells**
* Time Complexity: **O(m × n)**
* Often optimized to **O(n) space**
* Very common in **interviews & coding rounds**


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

