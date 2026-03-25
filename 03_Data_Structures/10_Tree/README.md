
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

A Complete Binary Tree is a binary tree in which:
- All levels are completely filled, except possibly the last level
- The last level is filled from left to right

### Example:

```
      1
     / \
    2   3
   / \  /
  4  5 6
```

### Python Code (Check Complete Binary Tree)
```python
from collections import deque

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def is_complete(root):
    if not root:
        return True
    
    queue = deque([root])
    found_null = False
    
    while queue:
        node = queue.popleft()
        
        if node:
            if found_null:
                return False
            queue.append(node.left)
            queue.append(node.right)
        else:
            found_null = True
    
    return True


# Example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

print(is_complete(root))  # True
```


## 3.5 Perfect Binary Tree

### Definition:

A Perfect Binary Tree is a binary tree in which:
- All internal nodes have exactly 2 children
- All leaf nodes are at the same level
- All levels are completely filled

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

### Python Code (Check Perfect Binary Tree)
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def depth(root):
    d = 0
    while root:
        d += 1
        root = root.left
    return d

def is_perfect(root, d, level=0):
    if root is None:
        return True
    
    # Leaf node
    if root.left is None and root.right is None:
        return d == level + 1
    
    # If one child is missing
    if root.left is None or root.right is None:
        return False
    
    return (is_perfect(root.left, d, level+1) and
            is_perfect(root.right, d, level+1))


# Example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)

d = depth(root)
print(is_perfect(root, d))  # True
```


## 3.6 Balanced Binary Tree

### Definition:

- A Balanced Binary Tree is a binary tree in which the height difference between left and right subtree of every node is at most 1.

### Example:

```
      10
     /  \
    5    15
```

### Python Code (Check Balanced Tree)
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def check_height(root):
    if root is None:
        return 0
    
    left = check_height(root.left)
    if left == -1:
        return -1
    
    right = check_height(root.right)
    if right == -1:
        return -1
    
    if abs(left - right) > 1:
        return -1
    
    return max(left, right) + 1

def is_balanced(root):
    return check_height(root) != -1


# Example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)

print(is_balanced(root))  # True
```


## 3.7 Degenerate (Skewed) Tree

### Definition:

- A Degenerate Tree (also called Skewed Tree) is a binary tree where each node has only one child
- It behaves like a linked list

### Example:

```
1
 \
  2
   \
    3
```

### 
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Create skewed tree (right side)
root = Node(1)
root.right = Node(2)
root.right.right = Node(3)
root.right.right.right = Node(4)

# Traversal (like linked list)
def traverse(node):
    while node:
        print(node.data, end=" ")
        node = node.right   # move only right

traverse(root)
```

### Output:
```
1 2 3 4
```

## 3.8 AVL Tree (Self-Balancing BST)

### Definition:

* A balanced BST
* Maintains balance using **rotations**

- An AVL Tree is a self-balancing Binary Search Tree where the balance factor of every node is −1, 0, or +1

### Balance Factor:

```
BF = Height(left) - Height(right)
```

### Types of Rotations:

* Left Rotation
* Right Rotation
* Left-Right
* Right-Left

### AVL Tree Code (Insertion + Balancing)
```python
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None
        self.height = 1

# Get height
def height(node):
    return node.height if node else 0

# Get balance factor
def get_balance(node):
    return height(node.left) - height(node.right)

# Right rotate
def right_rotate(z):
    y = z.left
    T3 = y.right

    y.right = z
    z.left = T3

    z.height = 1 + max(height(z.left), height(z.right))
    y.height = 1 + max(height(y.left), height(y.right))

    return y

# Left rotate
def left_rotate(z):
    y = z.right
    T2 = y.left

    y.left = z
    z.right = T2

    z.height = 1 + max(height(z.left), height(z.right))
    y.height = 1 + max(height(y.left), height(y.right))

    return y

# Insert
def insert(root, key):
    if not root:
        return Node(key)
    
    if key < root.key:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)

    # Update height
    root.height = 1 + max(height(root.left), height(root.right))

    balance = get_balance(root)

    # LL Case
    if balance > 1 and key < root.left.key:
        return right_rotate(root)

    # RR Case
    if balance < -1 and key > root.right.key:
        return left_rotate(root)

    # LR Case
    if balance > 1 and key > root.left.key:
        root.left = left_rotate(root.left)
        return right_rotate(root)

    # RL Case
    if balance < -1 and key < root.right.key:
        root.right = right_rotate(root.right)
        return left_rotate(root)

    return root


# Inorder traversal
def inorder(root):
    if root:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)


# Example
root = None
values = [10, 20, 30, 40, 50, 25]

for v in values:
    root = insert(root, v)

inorder(root)
```

### Output:
```
10 20 25 30 40 50
```

## 3.9 Red-Black Tree

### Definition:

A self-balancing BST with color rules:
* Node is either red or black
* Root is always black
* No two consecutive red nodes

- A Red-Black Tree is a self-balancing Binary Search Tree (BST) with extra color property for each node (Red or Black) that ensures the tree remains roughly balanced.

Used in:
* Maps
* Sets

### 
```python
# Install library first
# pip install bintrees

from bintrees import RBTree

# Create Red-Black Tree
rb = RBTree()

# Insert elements
rb.insert(10, "A")
rb.insert(20, "B")
rb.insert(30, "C")
rb.insert(15, "D")
rb.insert(25, "E")

# Inorder Traversal
for key, value in rb.items():
    print(key, value)
```

### Output:
```
10 A
15 D
20 B
25 E
30 C
```


## 3.10 Heap (Binary Heap)

👉 A Binary Heap is a complete binary tree that satisfies the heap property:

Max Heap → Parent node ≥ child nodes
Min Heap → Parent node ≤ child nodes

✅ Complete binary tree → all levels are fully filled except possibly the last, which is filled left to right.

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

# Create empty heap
heap = []

# Insert elements
heapq.heappush(heap, 10)
heapq.heappush(heap, 5)
heapq.heappush(heap, 20)
heapq.heappush(heap, 1)

print("Heap Array:", heap)

# Pop elements (min element first)
while heap:
    print(heapq.heappop(heap), end=" ")
```

### Output:
```
Heap Array: [1, 5, 20, 10]
1 5 10 20
```

## 3.11 Trie (Prefix Tree)

### Definition:

👉 A Trie (pronounced “try”) is a tree-like data structure used to store strings efficiently.

✅ Each node represents a character, and paths from root to leaf represent words.
✅ Useful for autocomplete, spell check, and prefix search.

### Example Words:
* cat
* car

Structure shares common prefix "ca"

### Python Example:

```python
class TrieNode:
    def __init__(self):
        self.children = {}  # dictionary for child nodes
        self.is_end = False # marks end of word

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    # Insert a word
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    # Search for a word
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
    
    # Check if prefix exists
    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True


# Example Usage
trie = Trie()
words = ["apple", "app", "bat", "ball"]
for w in words:
    trie.insert(w)

print(trie.search("app"))       # True
print(trie.search("appl"))      # False
print(trie.starts_with("ba"))   # True
print(trie.starts_with("cat"))  # False
```

### Output:
```
True
False
True
False
```


## 3.12 N-ary Tree

### Definition:

👉 An N-ary Tree is a tree in which each node can have at most N children.

✅ Unlike a binary tree (max 2 children), here a node can have multiple children.

### Example:

```
        A
      / | \
     B  C  D
        |
        E
```

### Python Implementation:
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.children = []  # list of children

# Create Nodes
root = Node(1)
child2 = Node(2)
child3 = Node(3)
child4 = Node(4)

root.children.extend([child2, child3, child4])

child2.children.extend([Node(5), Node(6)])
child4.children.append(Node(7))

# Preorder Traversal
def preorder(node):
    if node:
        print(node.data, end=" ")
        for child in node.children:
            preorder(child)

preorder(root)
```

### Output:
```
1 2 5 6 3 4 7
```


## 3.13 B-Tree

### Definition:

👉 A B-Tree is a self-balancing search tree designed for disk or large memory storage systems.
✅ It maintains sorted data and allows search, insert, delete in O(log n) time.
✅ Each node can have multiple keys and multiple children.

### Python Code (Basic B-Tree Using btrees library)
```python
# Install library first
# pip install BTrees

from BTrees.OOBTree import OOBTree

# Create B-Tree
b_tree = OOBTree()

# Insert keys
b_tree[10] = "A"
b_tree[20] = "B"
b_tree[5] = "C"
b_tree[15] = "D"
b_tree[25] = "E"

# Inorder traversal (sorted order)
for key in b_tree.keys():
    print(key, b_tree[key])
```

### Output:
```
5 C
10 A
15 D
20 B
25 E
```

## 3.14 B+ Tree

### Definition:

👉 A B+ Tree is an extension of B-Tree where:
- All keys are stored in leaf nodes.
- Internal nodes only store keys for indexing/searching.
- Leaf nodes are linked for sequential access.
✅ Widely used in databases, file systems, and indexing because range queries are efficient.

Used in:
* Databases
* Indexing systems

### Python Code (Simulation)
```python
# Simple B+ Tree simulation (basic)

class BPlusNode:
    def __init__(self, leaf=False):
        self.leaf = leaf
        self.keys = []
        self.children = []

# Create root leaf node
root = BPlusNode(leaf=True)
root.keys = [5, 10, 15, 20, 25]

# Function to search in B+ tree
def search(root, key):
    if root.leaf:
        if key in root.keys:
            return True
        return False
    # Internal node traversal (simplified)
    for i, k in enumerate(root.keys):
        if key < k:
            return search(root.children[i], key)
    return search(root.children[-1], key)

# Test search
print(search(root, 15))  # True
print(search(root, 12))  # False
```


# 🔄 4. Tree Traversals

👉 Tree traversal is the process of visiting all nodes in a tree in a specific order.

✅ Traversals are mainly of two types:
- Depth-First Traversal (DFS)
- Breadth-First Traversal (BFS)

## 4.1 Depth First Traversal (DFS)
👉 Depth First Traversal (DFS) is a tree or graph traversal technique where we explore as far as possible along each branch before backtracking.
✅ DFS uses stack (can be recursion or explicit stack) to remember nodes.

### Types:
### 1. Inorder (LNR)
👉 Inorder Traversal is a type of Depth-First Traversal (DFS) where we visit nodes in the order:
L → N → R 
- L = Left subtree
- N = Node (root)
- R = Right subtree
✅ In a Binary Search Tree (BST), Inorder traversal gives nodes in sorted order.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Sample BST:
#       4
#      / \
#     2   6
#    / \ / \
#   1  3 5  7

root = Node(4)
root.left = Node(2)
root.right = Node(6)
root.left.left = Node(1)
root.left.right = Node(3)
root.right.left = Node(5)
root.right.right = Node(7)

# Inorder Traversal (LNR)
def inorder(node):
    if node:
        inorder(node.left)
        print(node.data, end=" ")
        inorder(node.right)

print("Inorder Traversal: ", end="")
inorder(root)
```

### Output:
```
Inorder Traversal: 1 2 3 4 5 6 7
```

### 2. Preorder (NLR)
👉 Preorder Traversal is a type of Depth-First Traversal (DFS) where nodes are visited in the order:

N → L → R

- N = Node (root)
- L = Left subtree
- R = Right subtree

✅ Useful for copying a tree, creating prefix expressions, or saving tree structure.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Sample tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

# Preorder Traversal (NLR)
def preorder(node):
    if node:
        print(node.data, end=" ")
        preorder(node.left)
        preorder(node.right)

print("Preorder Traversal: ", end="")
preorder(root)
```

### Output:
```
Preorder Traversal: 1 2 4 5 3
```

### 3. Postorder (LRN)
👉 Postorder Traversal is a type of Depth-First Traversal (DFS) where nodes are visited in the order:

L → R → N

- L = Left subtree
- R = Right subtree
- N = Node (root)

✅ Useful for deleting a tree, evaluating postfix expressions, or freeing memory.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Sample tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

# Postorder Traversal (LRN)
def postorder(node):
    if node:
        postorder(node.left)
        postorder(node.right)
        print(node.data, end=" ")

print("Postorder Traversal: ", end="")
postorder(root)
```

### Output:
```
Postorder Traversal: 4 5 2 3 1
```

## 4.2 Breadth First Traversal (Level Order)

👉 Breadth-First Traversal (BFS) visits nodes level by level, starting from the root, going left to right at each level.
✅ Also called Level Order Traversal.
✅ Uses a queue to keep track of nodes.

```python
from collections import deque

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Sample tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

# Level Order Traversal (BFS)
def level_order(root):
    if not root:
        return
    queue = deque([root])
    while queue:
        node = queue.popleft()
        print(node.data, end=" ")
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

print("Level Order Traversal: ", end="")
level_order(root)
```

### Output:
```
Level Order Traversal: 1 2 3 4 5
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

