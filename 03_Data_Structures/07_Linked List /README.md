
# 🔗 Linked List 

## 📌 What is a Linked List?

A **Linked List** is a linear data structure where elements (called **nodes**) are stored **non-contiguously** in memory. 

Each node contains:
1. **Data** → actual value
2. **Pointer/Reference** → address of next node

👉 Unlike arrays, linked lists **do not require contiguous memory**.



## 🧱 Structure of a Node (Python)

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Creating nodes
n1 = Node(10)
n2 = Node(20)
n3 = Node(30)

# Linking nodes
n1.next = n2
n2.next = n3

# Display linked list
temp = n1
while temp:
    print(temp.data, end=" -> ")
    temp = temp.next
print("None")
```

#### Output:
```
10 -> 20 -> 30 -> None
```

## ⚙️ Basic Operations

### 1. Traversal
👉 Traversal means visiting each node one by one from start (head) to end (None).

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Create Linked List: 10 -> 20 -> 30
head = Node(10)
second = Node(20)
third = Node(30)

head.next = second
second.next = third

# Traversal
temp = head
while temp is not None:
    print(temp.data, end=" -> ")
    temp = temp.next
print("None")
```

####  Output
```
10 -> 20 -> 30 -> None
```

### 2. Insertion at Beginning
👉 Insertion at beginning means adding a new node before the current head and updating the head pointer.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Function to insert at beginning
def insert_begin(head, data):
    new_node = Node(data)
    new_node.next = head
    return new_node   # new node becomes new head

# Function to display list
def display(head):
    temp = head
    while temp:
        print(temp.data, end=" -> ")
        temp = temp.next
    print("None")

# Initial Linked List: 20 -> 30
head = Node(20)
head.next = Node(30)

display(head)

# Insert at beginning
head = insert_begin(head, 10)

display(head)
```

#### Output:
```
20 -> 30 -> None
10 -> 20 -> 30 -> None
```

### 3. Insertion at End
👉 Insertion at end means adding a new node at the last position of the linked list.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Function to insert at end
def insert_end(head, data):
    new_node = Node(data)
    
    # If list is empty
    if head is None:
        return new_node
    
    temp = head
    while temp.next:
        temp = temp.next   # traverse to last node
    
    temp.next = new_node  # link last node to new node
    return head

# Function to display list
def display(head):
    temp = head
    while temp:
        print(temp.data, end=" -> ")
        temp = temp.next
    print("None")

# Initial Linked List: 10 -> 20
head = Node(10)
head.next = Node(20)

display(head)

# Insert at end
head = insert_end(head, 30)

display(head)
```

#### Output:
```
10 -> 20 -> None
10 -> 20 -> 30 -> None
```

### 4. Deletion
👉 Deletion means removing a node from the linked list.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Function to delete from beginning
def delete_begin(head):
    if head is None:
        print("List is empty")
        return None
    
    head = head.next   # move head to next node
    return head

# Function to display list
def display(head):
    temp = head
    while temp:
        print(temp.data, end=" -> ")
        temp = temp.next
    print("None")

# Create Linked List: 10 -> 20 -> 30
head = Node(10)
head.next = Node(20)
head.next.next = Node(30)

display(head)

# Delete from beginning
head = delete_begin(head)

display(head)
```

#### Output:
```
10 -> 20 -> 30 -> None
20 -> 30 -> None
```

# 🔥 Types of Linked Lists

## 1. Singly Linked List

👉 A **Singly Linked List** is a collection of nodes where each node contains:
* **Data**
* **Reference (next)** to the next node

### Example Code
```python 
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Create Linked List
head = Node(10)
second = Node(20)
third = Node(30)

# Link nodes
head.next = second
second.next = third

# Traverse (Display)
temp = head
while temp:
    print(temp.data, end=" -> ")
    temp = temp.next
print("None")
```

### Output

```python
10 -> 20 -> 30 -> None
```


## 2. Doubly Linked List (DLL)

👉 A **Doubly Linked List** is a type of linked list where each node contains:
* **Data**
* **Pointer to next node**
* **Pointer to previous node**

### Example Code
```python
class Node:
    def __init__(self, data):
        self.prev = None
        self.data = data
        self.next = None

# Create nodes
head = Node(10)
second = Node(20)
third = Node(30)

# Link nodes
head.next = second
second.prev = head

second.next = third
third.prev = second

# Traverse forward
temp = head
while temp:
    print(temp.data, end=" <-> ")
    temp = temp.next
print("None")
```

### Output:

```python 
10 <-> 20 <-> 30 <-> None
```

### Singly vs Doubly 

| Feature   | Singly LL     | Doubly LL      |
| --------- | ------------- | -------------- |
| Pointers  | 1 (next)      | 2 (prev, next) |
| Traversal | One direction | Two directions |
| Memory    | Less          | More           |


## 3. Circular Linked List

### 📌 Definition:

Last node points back to the **first node**.

### Example:

```
10 -> 20 -> 30 -> (back to 10)
```

### Code Example:

```python
head = Node(10)
second = Node(20)
third = Node(30)

head.next = second
second.next = third
third.next = head  # Circular link
```

### ✔️ Advantages:

* No NULL pointers
* Useful in cyclic processes (e.g., round-robin scheduling)

### ❌ Disadvantages:

* Infinite loops if not handled carefully



## 4. Doubly Circular Linked List

### 📌 Definition:

* Like doubly linked list
* Last node connects to first
* First node connects to last

### Example:

```
10 <-> 20 <-> 30 (circular both sides)
```

### ✔️ Advantages:

* Full two-way circular traversal
* Efficient for navigation systems

### ❌ Disadvantages:

* More complex
* More memory usage



## 5. Self-Referential Linked List (Single Node Loop)

### 📌 Definition:

A node points to **itself**.

### Example:

```
10 -> (points to itself)
```

### Code:

```python
node = Node(10)
node.next = node
```



# ⚡ Time Complexity

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | O(n)            |
| Search    | O(n)            |
| Insertion | O(1)            |
| Deletion  | O(1)            |



# 🧠 Linked List vs Array

| Feature   | Linked List    | Array       |
| --------- | -------------- | ----------- |
| Memory    | Non-contiguous | Contiguous  |
| Size      | Dynamic        | Fixed       |
| Access    | Slow (O(n))    | Fast (O(1)) |
| Insertion | Easy           | Costly      |



# 🚀 Real-Life Applications

* Music Playlist (next/previous songs)
* Undo/Redo operations
* Browser history
* Memory management
* Graph adjacency lists



# 🧾 Final Summary

* Linked Lists store data in **nodes connected via pointers**
* They are **dynamic and flexible**
* Types include:

  * Singly
  * Doubly
  * Circular
  * Doubly Circular
* Best when **frequent insertions/deletions** are needed


