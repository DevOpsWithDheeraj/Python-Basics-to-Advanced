
# 📌 1. What is a Queue?

A **Queue** is a linear data structure that follows:

* **FIFO (First In, First Out)** principle
* The element inserted first is removed first.

### Real-Life Example:

* Queue at a ticket counter 🎫
* People stand in line → first person gets served first



# 📌 2. Basic Operations of Queue

| Operation        | Description                        |
| ---------------- | ---------------------------------- |
| **Enqueue**      | Insert element at the rear         |
| **Dequeue**      | Remove element from the front      |
| **Peek / Front** | Get front element without removing |
| **isEmpty**      | Check if queue is empty            |
| **isFull**       | Check if queue is full (for array) |



# 📌 3. Representation of Queue

Queue has two pointers:

* **Front** → points to first element
* **Rear** → points to last element

Example:

```
Front → [10, 20, 30, 40] ← Rear
```



# 📌 4. Implementation of Queue

## 👉 (A) Using List (Python)

```python
queue = []

# Enqueue
queue.append(10)
queue.append(20)
queue.append(30)

# Dequeue
queue.pop(0)

print(queue)
```

⚠️ Problem: `pop(0)` is slow → O(n)



## 👉 (B) Using collections.deque (Best)

```python
from collections import deque

queue = deque()

queue.append(10)
queue.append(20)
queue.append(30)

queue.popleft()

print(queue)
```

✅ Efficient → O(1)



# 📌 5. Types of Queue 



# 🔹 1. Simple Queue (Linear Queue)

### Concept:

* Insert from **rear**
* Delete from **front**

### Example:

```
Enqueue: 10, 20, 30
Queue: [10, 20, 30]

Dequeue → removes 10
Queue: [20, 30]
```

### Python Example:

```python
from collections import deque

q = deque()

q.append(1)
q.append(2)
q.append(3)

q.popleft()

print(q)
```



# 🔹 2. Circular Queue

### Problem in Simple Queue:

Unused space after dequeue

### Solution:

👉 Last position connects to first (circular)

```
[10, 20, 30, _, _]
After dequeue → space wasted ❌

Circular Queue → reuse space ✔
```

### Key Idea:

```
rear = (rear + 1) % size
front = (front + 1) % size
```

### Python Example:

```python
cq = CircularQueue(3)

cq.enqueue(10)
cq.enqueue(20)
cq.enqueue(30)

cq.display()       # 10 20 30

print(cq.dequeue())  # 10

cq.display()       # 20 30

cq.enqueue(40)
cq.display()       # 20 30 40
```



# 🔹 3. Priority Queue

### Concept:

Elements are processed based on **priority**, not order.

👉 Higher priority → served first

### Python Example:

```python
import heapq

pq = []

heapq.heappush(pq, (2, "Low"))
heapq.heappush(pq, (1, "High"))

# Print heap before pop
print("Heap before pop:", pq)

# Pop highest priority element
print("Popped element:", heapq.heappop(pq))

# Print heap after pop
print("Heap after pop:", pq)
```



# 🔹 4. Double Ended Queue (Deque)

### Concept:

Insertion & deletion from **both ends**

| Operation    | Allowed |
| ------------ | ------- |
| Insert Front | ✔       |
| Insert Rear  | ✔       |
| Delete Front | ✔       |
| Delete Rear  | ✔       |

### Python Example:

```python
from collections import deque

dq = deque()

dq.append(10)        # rear
dq.appendleft(20)    # front

dq.pop()             # remove rear
dq.popleft()         # remove front
```



# 🔹 5. Input Restricted Queue

### Concept:

* Insertion allowed only at **one end**
* Deletion allowed at **both ends**

```python
# Queue parameters
size = 5
queue = [None] * size
front = 0
rear = -1
count = 0

# Enqueue (only at rear)
def enqueue(x):
    global rear, count
    if count == size:
        print("Queue Full")
        return
    rear = (rear + 1) % size
    queue[rear] = x
    count += 1

# Dequeue from front
def dequeue_front():
    global front, count
    if count == 0:
        print("Queue Empty")
        return None
    removed = queue[front]
    front = (front + 1) % size
    count -= 1
    return removed

# Dequeue from rear
def dequeue_rear():
    global rear, count
    if count == 0:
        print("Queue Empty")
        return None
    removed = queue[rear]
    rear = (rear - 1 + size) % size
    count -= 1
    return removed

# Display queue
def display():
    if count == 0:
        print("Queue Empty")
        return
    i = front
    for _ in range(count):
        print(queue[i], end=" ")
        i = (i + 1) % size
    print()

# -----------------------------
# Example usage
enqueue(10)
enqueue(20)
enqueue(30)
display()               # 10 20 30

print(dequeue_front())  # 10
display()               # 20 30

print(dequeue_rear())   # 30
display()               # 20

enqueue(40)
display()               # 20 40
```

# 🔹 6. Output Restricted Queue

### Concept:

* Deletion allowed only at **one end**
* Insertion allowed at **both ends**

```python
# Queue parameters
size = 5
queue = [None] * size
front = 0
rear = -1
count = 0

# Enqueue at rear
def enqueue_rear(x):
    global rear, count
    if count == size:
        print("Queue Full")
        return
    rear = (rear + 1) % size
    queue[rear] = x
    count += 1

# Enqueue at front
def enqueue_front(x):
    global front, count
    if count == size:
        print("Queue Full")
        return
    front = (front - 1 + size) % size
    queue[front] = x
    count += 1

# Dequeue (only from front)
def dequeue():
    global front, count
    if count == 0:
        print("Queue Empty")
        return None
    removed = queue[front]
    front = (front + 1) % size
    count -= 1
    return removed

# Display queue
def display():
    if count == 0:
        print("Queue Empty")
        return
    i = front
    for _ in range(count):
        print(queue[i], end=" ")
        i = (i + 1) % size
    print()

# -----------------------------
# Example Usage
enqueue_rear(10)
enqueue_rear(20)
enqueue_front(5)
display()           # 5 10 20

print(dequeue())    # 5
display()           # 10 20

enqueue_front(2)
enqueue_rear(30)
display()           # 2 10 20 30
```

# 📌 6. Time Complexity

| Operation | Complexity |
| --------- | ---------- |
| Enqueue   | O(1)       |
| Dequeue   | O(1)       |
| Peek      | O(1)       |



# 📌 7. Applications of Queue

👉 Very important for interviews & teaching:

1. **CPU Scheduling**
2. **Breadth First Search (BFS)**
3. **Printer Queue**
4. **Call Center System**
5. **Task Scheduling (OS)**
6. **Handling Requests in Web Servers**



# 📌 8. Queue vs Stack

| Feature   | Queue | Stack |
| --------- | ----- | ----- |
| Principle | FIFO  | LIFO  |
| Insert    | Rear  | Top   |
| Delete    | Front | Top   |



# 🎯 Final Summary

* Queue follows **FIFO**
* Key operations: **enqueue, dequeue**
* Best implementation in Python → `deque`
* Types:
  * Simple Queue
  * Circular Queue
  * Priority Queue
  * Deque
  * Restricted Queues


