
# 🌳 1. What is a Tree ?

A **Tree** is a **non-linear data structure** that represents hierarchical relationships.

### Definition:

A tree is a collection of nodes where:

* One node is designated as the **root**
* Every node (except root) has exactly **one parent**
* Nodes can have **zero or more children**



# 🧩 2. Basic Terminology

| Term              | Meaning                                   |
| ----------------- | ----------------------------------------- |
| **Node**          | Basic element containing data             |
| **Root**          | Topmost node                              |
| **Parent**        | Node having children                      |
| **Child**         | Node derived from another node            |
| **Leaf Node**     | Node with no children                     |
| **Internal Node** | Node with at least one child              |
| **Height**        | Longest path from root to leaf            |
| **Depth**         | Distance from root to a node              |
| **Subtree**       | Tree formed by a node and its descendants |



# 🌲 3. Types of Trees

## 3.1 Binary Tree

### Definition:

A tree where each node has **at most 2 children**:
* Left child
* Right child

### Example:

```
      10
     /  \
    5    20
   / \
  2   8
```

### Python Example:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Create nodes
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

# Display (Preorder Traversal)
def preorder(node):
    if node:
        print(node.data, end=" ")
        preorder(node.left)
        preorder(node.right)

preorder(root)
```

### Output:
```
1 2 4 5 3
```


## 3.2 Binary Search Tree (BST)

### Definition:

A Binary Search Tree (BST) is a binary tree where:
- Left subtree → values smaller than root
- Right subtree → values greater than root

### Example:

```
      15
     /  \
    10   20
   / \     \
  8  12     25
```

### Operations:

* Search → O(log n)
* Insert → O(log n)

### Python Example:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Insert into BST
def insert(root, key):
    if root is None:
        return Node(key)
    
    if key < root.data:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)
    
    return root

# Inorder Traversal (Sorted Output)
def inorder(root):
    if root:
        inorder(root.left)
        print(root.data, end=" ")
        inorder(root.right)

# Search in BST
def search(root, key):
    if root is None or root.data == key:
        return root
    
    if key < root.data:
        return search(root.left, key)
    else:
        return search(root.right, key)


# Example
root = None
values = [50, 30, 70, 20, 40, 60, 80]

for v in values:
    root = insert(root, v)

# Print BST (sorted)
inorder(root)

# Search
result = search(root, 40)
print("\nFound" if result else "\nNot Found")
```

### Output:
```
20 30 40 50 60 70 80
Found
```

## 3.3 Full Binary Tree

### Definition:
- A Full Binary Tree is a binary tree in which every node has either 0 or 2 children
- No node has only one child

### Example:

```
      1
     / \
    2   3
       / \
      4   5
```

### Python Code:
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def is_full(root):
    if root is None:
        return True
    
    # If leaf node
    if root.left is None and root.right is None:
        return True
    
    # If both children exist
    if root.left and root.right:
        return is_full(root.left) and is_full(root.right)
    
    return False


# Example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

print(is_full(root))  # True
```

### Output:
```
True
```

## 3.4 Complete Binary Tree

### Definition:

* All levels are filled except possibly last
* Last level filled from **left to right**

### Example:

```
      1
     / \
    2   3
   / \  /
  4  5 6
```



## 3.5 Perfect Binary Tree

### Definition:

* All internal nodes have 2 children
* All leaves are at the same level

### Formula:

Number of nodes = **2^h - 1**

### Example:

```
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```



## 3.6 Balanced Binary Tree

### Definition:

Height difference between left and right subtree ≤ 1

### Example:

```
      10
     /  \
    5    15
```



## 3.7 Degenerate (Skewed) Tree

### Definition:

Tree behaves like a **linked list**

### Example:

```
1
 \
  2
   \
    3
```



## 3.8 AVL Tree (Self-Balancing BST)

### Definition:

* A balanced BST
* Maintains balance using **rotations**

### Balance Factor:

```
BF = Height(left) - Height(right)
```

### Types of Rotations:

* Left Rotation
* Right Rotation
* Left-Right
* Right-Left



## 3.9 Red-Black Tree

### Definition:

A self-balancing BST with color rules:

* Node is either red or black
* Root is always black
* No two consecutive red nodes

Used in:

* Maps
* Sets



## 3.10 Heap (Binary Heap)

### Types:

* **Max Heap** → Parent > Children
* **Min Heap** → Parent < Children

### Example (Max Heap):

```
      50
     /  \
    30   40
   / \
  10 20
```

### Python Example:

```python
import heapq

heap = []
heapq.heappush(heap, 10)
heapq.heappush(heap, 5)
heapq.heappush(heap, 20)

print(heapq.heappop(heap))  # smallest element
```



## 3.11 Trie (Prefix Tree)

### Definition:

Used for storing strings efficiently

### Example Words:

* cat
* car

Structure shares common prefix "ca"

### Python Example:

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False
```



## 3.12 N-ary Tree

### Definition:

Each node can have **more than 2 children**

### Example:

```
        A
      / | \
     B  C  D
        |
        E
```


## 3.13 B-Tree

### Definition:

* Multi-level tree
* Used in databases & file systems
* Stores multiple keys per node



## 3.14 B+ Tree

### Definition:

* All data stored in leaf nodes
* Leaves are linked

Used in:

* Databases
* Indexing systems



# 🔄 4. Tree Traversals

## 4.1 Depth First Traversal (DFS)

### Types:

### 1. Inorder (LNR)

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.data)
        inorder(root.right)
```

### 2. Preorder (NLR)

```python
def preorder(root):
    if root:
        print(root.data)
        preorder(root.left)
        preorder(root.right)
```

### 3. Postorder (LRN)

```python
def postorder(root):
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.data)
```


## 4.2 Breadth First Traversal (Level Order)

```python
from collections import deque

def level_order(root):
    q = deque([root])
    while q:
        node = q.popleft()
        print(node.data)
        if node.left:
            q.append(node.left)
        if node.right:
            q.append(node.right)
```


# ⚡ 5. Time Complexity

| Operation | Average  | Worst |
| --------- | -------- | ----- |
| Search    | O(log n) | O(n)  |
| Insert    | O(log n) | O(n)  |
| Delete    | O(log n) | O(n)  |


# 6. Applications of Trees

* File systems (folders)
* Databases (B-Trees)
* Searching (BST)
* Auto-complete (Trie)
* Networking (routing trees)
* AI (decision trees)

