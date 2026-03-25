
# 📌 What is DSA?

**Data Structures and Algorithms (DSA)** is a fundamental concept in computer science that helps in organizing, storing, and processing data efficiently.

* **Data Structure** → Way to store and organize data
* **Algorithm** → Step-by-step procedure to solve a problem

👉 Together, DSA helps in writing **optimized, scalable, and efficient code**

# 🧱 Data Structures (Using Python)

## 1. Array (List in Python)

**Definition:** A collection of elements stored in contiguous memory locations.

```python
arr = [1, 2, 3, 4]
print(arr[0])  # Access
```

* Ordered, mutable
* Index-based access
* Time Complexity:

  * Access → O(1)
  * Insert/Delete → O(n)


## 2. Stack

**Definition:** Linear data structure following **LIFO (Last In First Out)**.

```python
stack = []
stack.append(10)  # Push
stack.pop()       # Pop
```

* Operations:

  * Push
  * Pop
  * Peek



## 3. Queue

**Definition:** Linear data structure following **FIFO (First In First Out)**.

```python
from collections import deque

queue = deque()
queue.append(10)     # Enqueue
queue.popleft()      # Dequeue
```



## 4. Linked List

**Definition:** Collection of nodes where each node contains data and a pointer to the next node.

* Types:

  * Singly Linked List
  * Doubly Linked List
  * Circular Linked List



## 5. Set

**Definition:** Unordered collection of unique elements.

```python
s = {1, 2, 3}
s.add(4)
```


## 6. Dictionary (HashMap)

**Definition:** Collection of key-value pairs.

```python
d = {"name": "Dheeraj", "age": 25}
print(d["name"])
```

* Fast lookup → O(1)


## 7. Tree

**Definition:** Hierarchical data structure with nodes connected by edges.

* Types:

  * Binary Tree
  * Binary Search Tree (BST)
  * AVL Tree



## 8. Graph

**Definition:** Collection of nodes (vertices) and edges.

* Types:

  * Directed
  * Undirected
  * Weighted



# ⚙️ Algorithms

## 📌 What is an Algorithm?

A **finite set of instructions** used to solve a problem.



## 🔹 Types of Algorithms

### 1. Searching Algorithms

* Linear Search → O(n)
* Binary Search → O(log n)



### 2. Sorting Algorithms

* Bubble Sort
* Selection Sort
* Insertion Sort
* Merge Sort
* Quick Sort



### 3. Recursion

**Definition:** A function calling itself.

```python
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n-1)
```



### 4. Backtracking

Used to solve problems by trying all possibilities.

* Example: N-Queens, Sudoku



### 5. Greedy Algorithm

Chooses the best option at each step.

* Example: Coin Change



### 6. Dynamic Programming (DP)

**Definition:** Optimized recursion using stored results.

* Example: Fibonacci



# ⏱️ Time & Space Complexity

## 📌 Time Complexity

Measures how fast an algorithm runs.

* O(1) → Constant
* O(log n) → Logarithmic
* O(n) → Linear
* O(n²) → Quadratic



## 📌 Space Complexity

Measures how much memory is used.



# 🎯 Real-Life Applications of DSA

* Navigation (Google Maps → Graphs)
* Social Media (Friends → Graphs)
* Undo feature (Stack)
* Job scheduling (Queue)
* Databases (Trees)



# ✅ Conclusion

DSA is the **backbone of programming**.
Learning it using Python makes it **simpler, faster, and more practical**.

---
