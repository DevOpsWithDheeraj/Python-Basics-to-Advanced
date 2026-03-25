
# 🔍 What is Searching?
- Searching is the process of locating a target element (key) within a data structure and returning its position (index) or confirming its absence.



## Types of Searching

Searching techniques can be broadly classified into:

1. **Linear Search (Sequential Search)**
2. **Binary Search**
3. **Hashing (Direct Access Search)**
4. **Tree-Based Searching (BST, AVL, etc.)**
5. **Graph Searching (DFS, BFS)**



## 1️⃣ Linear Search (Sequential Search)
- Linear Search checks each element one by one until the desired element is found or the list ends.

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
- Binary Search works by repeatedly dividing a **sorted array** into halves.

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
- Hashing uses a **hash function** to map keys directly to indices.

### 🧠 Idea:

Instead of searching, we compute the index using a function.

### 🧠 Example:

```python
data = {
    "name": "Dheeraj",
    "role": "DevOps",
    "city": "Bangalore"
}

key = input("Enter key to search: ")

if key in data:
    print("Value:", data[key])
else:
    print("Key not found")
```

### ⏱ Time Complexity:

* Average: O(1)
* Worst Case: O(n) (due to collisions)

### ⚠️ Concepts:

* Hash Function
* Collision Handling (Chaining, Open Addressing)

## 🔹 Collision Resolution (Chaining)

👉 **Collision** happens when **two keys map to the same index** in a hash table. <br>
👉 One simple way to handle it is **Chaining** (store multiple values at same index using a list).


### Example Code (Chaining)

```python id="hash_chaining"
# Hash function
def hash_func(key, size):
    return key % size

# Create hash table (list of empty lists)
size = 5
hash_table = [[] for _ in range(size)]

# Insert function
def insert(key):
    index = hash_func(key, size)
    hash_table[index].append(key)

# Search function
def search(key):
    index = hash_func(key, size)
    if key in hash_table[index]:
        return True
    return False

# Insert elements (collision will happen)
insert(10)   # 10 % 5 = 0
insert(15)   # 15 % 5 = 0  → collision with 10
insert(20)   # 20 % 5 = 0  → collision again

# Display hash table
print(hash_table)

# Search
print("Search 15:", search(15))
```

### 🔥 Output
```python id="hash_chain_output"
[[10, 15, 20], [], [], [], []]
Search 15: True
```

### 🔹 Explanation
* All keys **10, 15, 20 → index 0**
* Instead of overwriting, we **store them in a list**
* This list is called a **chain**


## 🔹 Collision Resolution (Linear Probing)

👉 Another way to handle collision is **Linear Probing (Open Addressing)** <br>
👉 If a slot is full, we **check the next available slot**

### Example Code (Linear Probing)

```python id="hash_linear_probing"
size = 5
hash_table = [None] * size

# Hash function
def hash_func(key):
    return key % size

# Insert using linear probing
def insert(key):
    index = hash_func(key)

    # Find next empty slot
    while hash_table[index] is not None:
        index = (index + 1) % size

    hash_table[index] = key

# Search using linear probing
def search(key):
    index = hash_func(key)
    start = index

    while hash_table[index] is not None:
        if hash_table[index] == key:
            return True
        index = (index + 1) % size
        if index == start:
            break
    return False

# Insert elements (collision happens)
insert(10)   # 10 % 5 = 0
insert(15)   # 15 % 5 = 0 → collision → move to next index
insert(20)   # 20 % 5 = 0 → collision → move further

# Display hash table
print(hash_table)

# Search
print("Search 15:", search(15))
```

### 🔥 Output

```python id="hash_linear_output"
[10, 15, 20, None, None]
Search 15: True
```

### 🔹 Explanation
* `10 → index 0`
* `15 → index 0 (collision) → placed at index 1`
* `20 → index 0 (collision) → index 1 full → placed at index 2`


## 4️⃣ Tree-Based Searching

👉 Tree Searching is the process of finding a specific node or value in a tree data structure by traversing its nodes in a systematic way.

## 🌳 Binary Search Tree (BST)
👉 In a Binary Search Tree (BST):
- Left subtree → values smaller than root
- Right subtree → values greater than root

### 🔁 Searching Process:

1. Start at root
2. Compare target with root
3. Move left or right accordingly

### 🧠 Example:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Insert function to build BST
def insert(root, key):
    if root is None:
        return Node(key)
    if key < root.data:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)
    return root

# Search function
def search(root, key):
    if root is None:
        return "Not Found"
    
    if root.data == key:
        return "Found"
    
    elif key < root.data:
        return search(root.left, key)
    else:
        return search(root.right, key)

# Create BST
root = None
for value in [50, 30, 70, 20, 40, 60, 80]:
    root = insert(root, value)

# Search key
print(search(root, 60))
```
### Output:
```
Found
```

### 🔹 Step-by-Step Search (Key = 60)
- Start at root → 50
- 60 > 50 → go right
- Move to 70
- 60 < 70 → go left
- Move to 60 → ✅ Found

  
### ⏱ Time Complexity:

* Average: O(log n)
* Worst: O(n) (skewed tree)



## 🌳 Balanced Trees (AVL, Red-Black)

### 📖 Definition:

Self-balancing trees maintain height to ensure efficient search.

### ⏱ Time Complexity:

* Always: O(log n)


## 5️⃣ Graph Searching

👉 Graph Searching is the process of visiting or exploring all the vertices (nodes) of a graph in a systematic way to find a particular node or to traverse the entire graph.

## 🔎 Breadth-First Search (BFS)
- Breadth-First Search (BFS) is a graph/tree searching algorithm that visits nodes level by level, starting from a source node and exploring all its neighbors before moving to the next level.

### 🧠 Example:
```python
from collections import deque

# Graph representation
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': [],
    'F': []
}

# BFS function
def bfs(start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            
            # Add neighbors to queue
            for neighbor in graph[node]:
                if neighbor not in visited:
                    queue.append(neighbor)

# Run BFS
bfs('A')
```
### Output:
```
A B C D E F
```
### 🔹 How it works
- Start from A
- Visit neighbors → B, C
- Then next level → D, E, F
- 

## 🔎 Depth-First Search (DFS)

- Depth-First Search (DFS) is a graph/tree searching algorithm that explores nodes as deep as possible first, and then backtracks to explore other paths.

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


