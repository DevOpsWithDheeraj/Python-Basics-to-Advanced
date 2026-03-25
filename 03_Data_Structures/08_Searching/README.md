
# 🔍 What is Searching?

**Definition:**
Searching is the process of locating a target element (key) within a data structure and returning its position (index) or confirming its absence.



## Types of Searching

Searching techniques can be broadly classified into:

1. **Linear Search (Sequential Search)**
2. **Binary Search**
3. **Hashing (Direct Access Search)**
4. **Tree-Based Searching (BST, AVL, etc.)**
5. **Graph Searching (DFS, BFS)**



## 1️⃣ Linear Search (Sequential Search)

### 📖 Definition:

Linear Search checks each element one by one until the desired element is found or the list ends.

### ✅ When to Use:

* Unsorted data
* Small datasets

### 🔁 Algorithm:

1. Start from the first element
2. Compare each element with the target
3. If found → return index
4. If not found → return -1

### 🧠 Example:

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

arr = [10, 20, 30, 40, 50]
print(linear_search(arr, 30))  # Output: 2
```

### ⏱ Time Complexity:

* Best Case: O(1)
* Worst Case: O(n)



## 2️⃣ Binary Search

### 📖 Definition:

Binary Search works by repeatedly dividing a **sorted array** into halves.

### ⚠️ Requirement:

* Array must be **sorted**

### 🔁 Algorithm:

1. Find middle element
2. If target == middle → found
3. If target < middle → search left half
4. If target > middle → search right half

### 🧠 Example:

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
            
    return -1

arr = [10, 20, 30, 40, 50]
print(binary_search(arr, 40))  # Output: 3
```

### ⏱ Time Complexity:

* Best Case: O(1)
* Worst Case: O(log n)



## 3️⃣ Hashing (Direct Access Search)

### 📖 Definition:

Hashing uses a **hash function** to map keys directly to indices.

### 🧠 Idea:

Instead of searching, we compute the index using a function.

### 🧠 Example:

```python
hash_table = {}

# Insert
hash_table["apple"] = 10
hash_table["banana"] = 20

# Search
print(hash_table["apple"])  # Output: 10
```

### ⏱ Time Complexity:

* Average: O(1)
* Worst Case: O(n) (due to collisions)

### ⚠️ Concepts:

* Hash Function
* Collision Handling (Chaining, Open Addressing)



## 4️⃣ Tree-Based Searching

## 🌳 Binary Search Tree (BST)

### 📖 Definition:

A tree where:

* Left child < Root
* Right child > Root

### 🔁 Searching Process:

1. Start at root
2. Compare target with root
3. Move left or right accordingly

### 🧠 Example:

```python
class Node:
    def __init__(self, value):
        self.left = None
        self.right = None
        self.value = value

def search(root, key):
    if root is None or root.value == key:
        return root
    
    if key < root.value:
        return search(root.left, key)
    else:
        return search(root.right, key)
```

### ⏱ Time Complexity:

* Average: O(log n)
* Worst: O(n) (skewed tree)



## 🌳 Balanced Trees (AVL, Red-Black)

### 📖 Definition:

Self-balancing trees maintain height to ensure efficient search.

### ⏱ Time Complexity:

* Always: O(log n)



## 5️⃣ Graph Searching

## 🔎 Breadth-First Search (BFS)

### 📖 Definition:

Explores level by level using a queue.

### 🧠 Example:

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node)
            visited.add(node)
            queue.extend(graph[node])
```



## 🔎 Depth-First Search (DFS)

### 📖 Definition:

Explores as deep as possible before backtracking.

### 🧠 Example:

```python
def dfs(graph, node, visited=set()):
    if node not in visited:
        print(node)
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
```



# 🔄 Comparison Table

| Method        | Data Requirement | Time Complexity | Use Case          |
| ------------- | ---------------- | --------------- | ----------------- |
| Linear Search | Unsorted         | O(n)            | Small data        |
| Binary Search | Sorted           | O(log n)        | Large sorted data |
| Hashing       | Any              | O(1) avg        | Fast lookup       |
| BST           | Structured       | O(log n) avg    | Dynamic data      |
| BFS / DFS     | Graph            | O(V + E)        | Network traversal |



# 🚀 Key Takeaways

* **Linear Search** → simplest but slow
* **Binary Search** → fast but needs sorted data
* **Hashing** → fastest lookup
* **Trees** → good for dynamic ordered data
* **Graphs (BFS/DFS)** → used in complex relationships


