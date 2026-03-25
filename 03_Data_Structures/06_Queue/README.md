
# 📌 1. What is a Queue?

A **Queue** is a linear data structure that follows:

👉 **FIFO (First In, First Out)** principle
The element inserted first is removed first.

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



# 📌 5. Types of Queue (Very Important)



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
class CircularQueue:
    def __init__(self, size):
        self.queue = [None]*size
        self.size = size
        self.front = -1
        self.rear = -1

    def enqueue(self, data):
        if (self.rear + 1) % self.size == self.front:
            print("Queue Full")
        elif self.front == -1:
            self.front = self.rear = 0
            self.queue[self.rear] = data
        else:
            self.rear = (self.rear + 1) % self.size
            self.queue[self.rear] = data

    def dequeue(self):
        if self.front == -1:
            print("Queue Empty")
        elif self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.size
```



# 🔹 3. Priority Queue

### Concept:

Elements are processed based on **priority**, not order.

👉 Higher priority → served first

### Example:

```
Insert: (10, priority 2), (20, priority 1)

Output:
20 (higher priority)
10
```

### Python Example:

```python
import heapq

pq = []

heapq.heappush(pq, (2, "Low"))
heapq.heappush(pq, (1, "High"))

print(heapq.heappop(pq))  # (1, "High")
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



# 🔹 6. Output Restricted Queue

### Concept:

* Deletion allowed only at **one end**
* Insertion allowed at **both ends**



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


