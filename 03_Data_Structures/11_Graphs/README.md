
# 🔷 What is a Graph?

A **Graph** is a non-linear data structure used to represent relationships between objects.

* A graph consists of:

  * **Vertices (Nodes)** → Represent entities
  * **Edges (Links)** → Represent connections between nodes

👉 Formally:

```
G = (V, E)
```

* **V** = set of vertices
* **E** = set of edges

# 🔷 Types of Graphs

## 1. Undirected Graph

- An Undirected Graph is a graph in which **edges have no direction**.
- This means the connection between two vertices works both ways.
- If there is an edge between A and B, then: A → B and B → A (both are same)

Example:
```
Vertices = {A, B, C, D}
Edges = {(A, B), (A, C), (B, D)}
```

Python Representation (Adjacency List):

```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A'],
    'D': ['B']
}
```

## 2. Directed Graph (Digraph)

- A Directed Graph (Digraph) is a graph in which edges have a direction.
- Each edge is represented as an ordered pair (u, v)
- This means u → v (from u to v), but v → u is not necessarily true.

Example:

```
Vertices = {A, B, C, D}
Edges = {(A → B), (A → C), (B → D)}
```

Python Representation (Adjacency List):
```python
graph = {
    'A': ['B', 'C'],      # A → B, A → C
    'B': ['D'],           # B → D
    'C': [],          
    'D': []
}
```

## 3. Weighted Graph

👉 A Weighted Graph is a graph in which each edge has an associated value (weight). <br>

➡️ The weight can represent: <br>
- Distance (km)
- Cost (₹)
- Time (minutes)
- Capacity, etc.

Example:
```
Vertices = {A, B, C}
Edges = {(A, B, 5), (A, C, 2), (B, C, 3)}
```

Python Representation (Adjacency List):

```python
graph = {
    'A': [('B', 5), ('C', 2)],
    'B': [('C', 3)],
    'C': []
}
```

## 4. Unweighted Graph

- An Unweighted Graph is a graph in which edges do not have any weight or cost.
- All edges are considered equal
- Each connection has the same importance or distance (usually treated as 1)

Example:
```
Graph:

Vertices = {A, B, C, D}
Edges = {(A, B), (A, C), (B, D)}
```

Python Representation (Adjacency List):
```python
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': [],
    'D': []
}
```

## 5. Cyclic Graph

- A Cyclic Graph is a graph that contains at least one cycle (loop).

- A cycle is a path where you can start from a node and come back to the same node by following edges.

Example:
```
Graph:

Vertices = {A, B, C}
Edges = {(A, B), (B, C), (C, A)}
```
Cycle formed:
```
A → B → C → A
```

Python Representation (Adjacency List):
```
graph = {
    'A': ['B'],
    'B': ['C'],
    'C': ['A']
}
```

## 6. Acyclic Graph

👉 An Acyclic Graph is a graph that does NOT contain any cycle (loop). <br>

➡️ This means you cannot start at a node and come back to the same node by following edges.

👉 Special case:
* **DAG (Directed Acyclic Graph)**

Graph:
```
Vertices = {A, B, C, D}
Edges = {(A → B), (B → C), (C → D)}
```
👉 Path:
```
A → B → C → D
```

Python Representation (Adjacency List):
```python
graph = {
    'A': ['B'],
    'B': ['C'],
    'C': ['D'],
    'D': []
}
```

## 7. Connected Graph

- A Connected Graph is a graph in which there is a path between every pair of vertices. <br>

➡️ This means every node is reachable from any other node.

Example:
Graph:
```
Vertices = {A, B, C, D}
Edges = {(A, B), (B, C), (C, D)}
```
👉 Paths exist:
```
A → B → C → D
B → C
A → C (via B)
✅ All nodes are connected
```

Python Representation (Adjacency List):
```python
graph = {
    'A': ['B'],
    'B': ['A', 'C'],
    'C': ['B', 'D'],
    'D': ['C']
}
```

## 8. Disconnected Graph

A Disconnected Graph is a graph in which not all vertices are reachable from each other. <br>

➡️ This means the graph has two or more separate parts (components) with no connection between them.

Example:
```
Vertices = {A, B, C, D}
Edges = {(A, B), (C, D)}
```
👉 Components:
- Component 1 → A — B
- Component 2 → C — D
- ❌ No path between A and C


Python Representation (Adjacency List):
```
graph = {
    'A': ['B'],
    'B': ['A'],
    'C': ['D'],
    'D': ['C']
}
```
🔹 Explanation
```
A is connected only to B 
C is connected only to D
👉 No connection between (A, B) and (C, D)
```

## 9. Complete Graph

👉 A Complete Graph is a graph in which every pair of distinct vertices is connected by an edge. <br>

➡️ This means each node is directly connected to every other node.

🔹 Example
```
Vertices = {A, B, C}
Edges = {(A, B), (A, C), (B, C)}
```
👉 Every node is connected to every other node

Python Representation (Adjacency List):
```
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'C'],
    'C': ['A', 'B']
}
```

🔹 Explanation
```
A ↔ B, A ↔ C
B ↔ C
```
👉 No missing edges → Complete Graph

## 10. Bipartite Graph

A Bipartite Graph is a graph in which vertices can be divided into two disjoint sets such that:
- No two vertices within the same set are connected
- All edges connect one set to the other set only

Sets:
- U = {A, B}
- V = {1, 2}

Edges:
(A, 1), (A, 2), (B, 1)

👉 No edge between A–B or 1–2

Python Representation (Adjacency List):
```
graph = {
    'A': ['1', '2'],
    'B': ['1'],
    '1': ['A', 'B'],
    '2': ['A']
}
```


# 🔷 Graph Representation

## 🔹 1. Adjacency List (Most Used)

- An **Adjacency List** is a way to represent a graph where **each vertex stores a list of its neighboring vertices**.

- Instead of storing all possible edges (like matrix), we store **only existing connections**.

- For every node, keep a **list of nodes it is connected to**

Example format:
```
A → B, C
B → A, D
```

## Example

### Graph:
```
Vertices = {A, B, C, D}
Edges = {(A, B), (A, C), (B, D)}
```

###  Adjacency List Representation
```
A → B, C
B → A, D
C → A
D → B
```

## Python Example
```python id="adj_list_code"
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A'],
    'D': ['B']
}

# Print adjacency list
for node in graph:
    print(node, "->", graph[node])
```

## Output
```text id="adj_list_output"
A -> ['B', 'C']
B -> ['A', 'D']
C -> ['A']
D -> ['B']
```

## Explanation
* **A → B, C** → A is connected to B and C
* **B → A, D** → B is connected to A and D
* Only **existing edges are stored**

## Advantages
* Saves **memory** (efficient for sparse graphs)
* Easy to **traverse neighbors**
* Flexible and widely used

## Disadvantages
* Checking if edge exists → may take **O(n)**
* Slightly complex compared to matrix

## Time Complexity
| Operation      | Complexity |
| -------------- | ---------- |
| Add edge       | O(1)       |
| Remove edge    | O(n)       |
| Check edge     | O(n)       |
| Traverse graph | O(V + E)   |


## 🔹 2. Adjacency Matrix

- An **Adjacency Matrix** is a way to represent a graph using a **2D matrix (rows × columns)**.

- If there is an edge between two vertices, we store **1 (or weight)**, otherwise **0**.

- For a graph with **n vertices**, we create an **n × n matrix**

* **matrix[i][j] = 1** → edge exists
* **matrix[i][j] = 0** → no edge

## Example
### Graph:
```
Vertices = {A, B, C, D}
Edges = {(A, B), (A, C), (B, D)}
```

### Adjacency Matrix
|   | A | B | C | D |
| - | - | - | - | - |
| A | 0 | 1 | 1 | 0 |
| B | 1 | 0 | 0 | 1 |
| C | 1 | 0 | 0 | 0 |
| D | 0 | 1 | 0 | 0 |

## Python Example
```python id="adj_matrix_code"
# A, B, C, D mapped to 0,1,2,3

matrix = [
    [0, 1, 1, 0],  # A
    [1, 0, 0, 1],  # B
    [1, 0, 0, 0],  # C
    [0, 1, 0, 0]   # D
]

# Print matrix
for row in matrix:
    print(row)
```

## Output
```text id="adj_matrix_output"
[0, 1, 1, 0]
[1, 0, 0, 1]
[1, 0, 0, 0]
[0, 1, 0, 0]
```
## Explanation
* A → B, C → so row A has 1 at B and C
* B → A, D → row B has 1 at A and D
* Matrix is **symmetric** (undirected graph)

## 🔹 For Weighted Graph

👉 Instead of 1, we store **weights**

Example:
```python
matrix = [
    [0, 5, 2],
    [5, 0, 3],
    [2, 3, 0]
]
```

## Advantages
* Easy to **check edge existence → O(1)**
* Simple representation
* Good for **dense graphs**

## Disadvantages
* Uses more **memory → O(V²)**
* Not efficient for sparse graphs

## Time Complexity
| Operation  | Complexity |
| ---------- | ---------- |
| Add edge   | O(1)       |
| Check edge | O(1)       |
| Traverse   | O(V²)      |



# 🔷 Graph Traversal Algorithms

## 🔹 1. Breadth-First Search (BFS)

- **Breadth-First Search (BFS)** is a graph traversal algorithm that visits nodes **level by level** starting from a source node.

- It explores all **neighbors first**, then moves to the next level.


##  Key Idea

👉 Uses a **Queue (FIFO)**

* Visit node
* Add its neighbors to queue
* Repeat until queue is empty


## Algorithm Steps
1. Start from a **source node**
2. Mark it as **visited**
3. Add it to **queue**
4. While queue is not empty:

   * Remove node from queue
   * Visit it
   * Add all **unvisited neighbors** to queue

## Python Example
```python id="bfs_graph"
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            
            for neighbor in graph[node]:
                if neighbor not in visited:
                    queue.append(neighbor)

# Example graph
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': [],
    'F': []
}

bfs(graph, 'A')
```

## Output
```text id="bfs_graph_output"
A B C D E F
```

## Key Points
* Uses **Queue (FIFO)**
* Traverses **level by level**
* Guarantees **shortest path** in unweighted graph

## Applications
* Shortest path (unweighted graph)
* Network broadcasting
* Web crawling
* Social networks

## 🔹 Time Complexity

| Case | Complexity |
| ---- | ---------- |
| BFS  | O(V + E)   |

(V = vertices, E = edges)



## 🔹2. Depth-First Search (DFS)

* **Depth-First Search (DFS)** is a graph traversal algorithm that explores **as deep as possible along a branch before backtracking**.

* It goes **node → neighbor → neighbor’s neighbor** until no further path, then comes back.


## Key Idea
👉 Uses a **Stack (LIFO)**
* Can be implemented using **recursion** (implicit stack)
* Or using an **explicit stack**

## Algorithm Steps
1. Start from a **source node**
2. Mark it as **visited**
3. Visit the node
4. Recursively visit all **unvisited neighbors**
5. Backtrack when no neighbor is left


## Python Example (Recursive DFS)
```python id="dfs_graph"
def dfs(graph, node, visited=set()):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)

# Example graph
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': [],
    'F': []
}

dfs(graph, 'A')
```

## Output
```text id="dfs_graph_output"
A B D E C F
```

## Key Points
* Uses **Stack (LIFO)**
* Goes **deep first**, then backtracks
* Does **not guarantee shortest path**

## Applications
* Path finding
* Cycle detection
* Topological sorting
* Solving puzzles (maze, Sudoku)


## Time Complexity

| Case | Complexity |
| ---- | ---------- |
| DFS  | O(V + E)   |

(V = vertices, E = edges)


# 🔷 Important Graph Algorithms

## 1. Dijkstra’s Algorithm (Shortest Path Algorithm)

**Definition:**
* Dijkstra’s Algorithm is used to find the **shortest path from a source vertex to all other vertices** in a **weighted graph** (with **non-negative weights**).


### 🔷 Key Idea
It works by:
* Picking the **closest unvisited node**
* Updating distances of its neighbors
* Repeating until all nodes are visited


### 🔷 Steps of the Algorithm
1. Assign:
   * Distance = **0** to source node
   * Distance = **∞ (infinity)** to all other nodes
2. Mark all nodes as **unvisited**
3. Select the node with the **smallest distance**
4. Update distances of its adjacent nodes:
   ```
   new_distance = current_distance + edge_weight
   ```
5. If new distance is smaller → update it
6. Mark the node as **visited**
7. Repeat until all nodes are visited


### 🔷 Example
Consider this graph:
```
Vertices: A, B, C, D

Edges:
A → B = 1
A → C = 4
B → C = 2
B → D = 5
C → D = 1
```

### 🔷 Step-by-Step Execution

#### Initial State:

```
Distance:
A = 0
B = ∞
C = ∞
D = ∞
```

#### Step 1: Visit A

* Update neighbors:

  * B = 0 + 1 = 1
  * C = 0 + 4 = 4

```
A = 0, B = 1, C = 4, D = ∞
```

#### Step 2: Visit B (smallest = 1)

* Update neighbors:

  * C = min(4, 1 + 2 = 3) → 3
  * D = 1 + 5 = 6

```
A = 0, B = 1, C = 3, D = 6
```

#### Step 3: Visit C (smallest = 3)

* Update neighbor:

  * D = min(6, 3 + 1 = 4) → 4

```
A = 0, B = 1, C = 3, D = 4
```

#### Step 4: Visit D

No updates needed.

### 🔷 Final Shortest Distances from A

| Vertex | Distance |
| ------ | -------- |
| A      | 0        |
| B      | 1        |
| C      | 3        |
| D      | 4        |

### 🔷 Shortest Paths

* A → B = 1
* A → B → C = 3
* A → B → C → D = 4

### 🔷 Time Complexity
* Using simple array: **O(V²)**
* Using priority queue (min-heap): **O((V + E) log V)**


### 🔷 Important Notes
* Works **only for non-negative weights**
* Used in:
  * Google Maps / GPS navigation
  * Network routing
  * Shortest path problems

### 🔷 Python Code (Using heapq)
```python
import heapq

def dijkstra(graph, start):
    # Initialize distances
    distances = {node: float('inf') for node in graph}
    distances[start] = 0

    # Priority queue (min-heap)
    pq = [(0, start)]  # (distance, node)

    while pq:
        current_distance, current_node = heapq.heappop(pq)

        # Skip if we already found a better path
        if current_distance > distances[current_node]:
            continue

        # Check neighbors
        for neighbor, weight in graph[current_node]:
            distance = current_distance + weight

            # Relaxation step
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))

    return distances


# Example graph (Adjacency List)
graph = {
    'A': [('B', 1), ('C', 4)],
    'B': [('C', 2), ('D', 5)],
    'C': [('D', 1)],
    'D': []
}

# Run Dijkstra
result = dijkstra(graph, 'A')

# Print result
for node, dist in result.items():
    print(f"Distance from A to {node} is {dist}")
```

### 🔷 Output
```
Distance from A to A is 0
Distance from A to B is 1
Distance from A to C is 3
Distance from A to D is 4
```


## 2. BellmanFord Algorithm

**Definition:**
* Bellman–Ford is a shortest path algorithm that finds the **minimum distance from a source vertex to all other vertices**, even when the graph has **negative edge weights**.


### 🔷 Why Bellman–Ford?

* ✅ Works with **negative weights**
* ✅ Can **detect negative weight cycles**
* ❌ Slower than Dijkstra


### 🔷 Core Idea

Instead of greedily picking the nearest node, it:

* **Relaxes all edges repeatedly (V − 1 times)**
* Ensures shortest paths are found step by step


### 🔷 Algorithm Steps

1. Initialize:

   * Distance[source] = 0
   * All others = ∞
2. Repeat **V − 1 times**:

   * For every edge (u → v, weight):

     ```
     if dist[u] + weight < dist[v]:
         dist[v] = dist[u] + weight
     ```
3. Check for **negative cycle**:

   * If still possible to relax → cycle exists


### 🔷 Example

```id="y5x7gk"
Vertices: A, B, C, D

Edges:
A → B = 1
A → C = 4
B → C = -2
B → D = 5
C → D = 1
```


### 🔷 Step-by-Step Idea

* After 1st iteration → distances start improving
* After V−1 iterations → shortest paths finalized
* Final result from A:

  ```
  A = 0
  B = 1
  C = -1
  D = 0
  ```


### 🔷 Python Code

```python id="3pq1wb"
def bellman_ford(graph, vertices, start):
    # Step 1: Initialize distances
    dist = {v: float('inf') for v in vertices}
    dist[start] = 0

    # Step 2: Relax edges V-1 times
    for _ in range(len(vertices) - 1):
        for u, v, weight in graph:
            if dist[u] != float('inf') and dist[u] + weight < dist[v]:
                dist[v] = dist[u] + weight

    # Step 3: Detect negative cycle
    for u, v, weight in graph:
        if dist[u] != float('inf') and dist[u] + weight < dist[v]:
            print("Graph contains a negative weight cycle")
            return None

    return dist


# Example edges (Edge List)
graph = [
    ('A', 'B', 1),
    ('A', 'C', 4),
    ('B', 'C', -2),
    ('B', 'D', 5),
    ('C', 'D', 1)
]

vertices = ['A', 'B', 'C', 'D']

# Run algorithm
result = bellman_ford(graph, vertices, 'A')

# Print result
if result:
    for node, distance in result.items():
        print(f"Distance from A to {node} is {distance}")
```


### 🔷 Output

```id="b5b3p6"
Distance from A to A is 0
Distance from A to B is 1
Distance from A to C is -1
Distance from A to D is 0
```


### 🔷 Time Complexity

* **O(V × E)**
  (V = vertices, E = edges)


### 🔷 Dijkstra vs Bellman–Ford

| Feature                  | Dijkstra      | Bellman–Ford        |
| ------------------------ | ------------- | ------------------- |
| Negative weights         | ❌ Not allowed | ✅ Allowed           |
| Negative cycle detection | ❌             | ✅                   |
| Time complexity          | Faster        | Slower              |
| Approach                 | Greedy        | Dynamic Programming |

### 🔷 When to Use?

* Use **Dijkstra** → when all weights are positive
* Use **Bellman–Ford** → when:

  * Negative edges exist
  * Need to detect negative cycles



## 3. Prim’s Algorithm (Minimum Spanning Tree)

**Definition:**
Prim’s Algorithm is used to find a **Minimum Spanning Tree (MST)** of a **connected, weighted, undirected graph**.

👉 **Minimum Spanning Tree:** A subset of edges that:
* Connects all vertices
* Has **no cycles**
* Has **minimum total weight**


### 🔷 Key Idea

* Start from any vertex
* At each step, pick the **minimum weight edge** that connects:

  * A **visited node** → an **unvisited node**


### 🔷 Steps of the Algorithm

1. Start from any node (say A)
2. Mark it as **visited**
3. Add all its edges to a **priority queue (min-heap)**
4. Pick the **smallest edge**
5. If it connects to an unvisited node:

   * Add it to MST
   * Mark node visited
6. Repeat until all vertices are included


### 🔷 Example

```id="3r5r0u"
Vertices: A, B, C, D

Edges:
A — B = 2
A — C = 3
B — C = 1
B — D = 4
C — D = 5
```


### 🔷 Step-by-Step Execution

#### Step 1: Start from A

* Edges: (A-B=2), (A-C=3)

👉 Pick smallest → **A-B (2)**


#### Step 2: Visited = {A, B}

* New edges: (B-C=1), (B-D=4), (A-C=3)

👉 Pick smallest → **B-C (1)**


#### Step 3: Visited = {A, B, C}

* New edges: (C-D=5), (B-D=4)

👉 Pick smallest → **B-D (4)**


### 🔷 Final MST

Edges in MST:

```
A — B = 2
B — C = 1
B — D = 4
```

👉 **Total Weight = 7**


### 🔷 Python Code (Using Min-Heap)

```python id="5b2o0p"
import heapq

def prim(graph, start):
    visited = set()
    min_heap = [(0, start)]  # (weight, node)
    mst_cost = 0

    while min_heap:
        weight, node = heapq.heappop(min_heap)

        if node in visited:
            continue

        visited.add(node)
        mst_cost += weight

        for neighbor, edge_weight in graph[node]:
            if neighbor not in visited:
                heapq.heappush(min_heap, (edge_weight, neighbor))

    return mst_cost


# Graph (Adjacency List)
graph = {
    'A': [('B', 2), ('C', 3)],
    'B': [('A', 2), ('C', 1), ('D', 4)],
    'C': [('A', 3), ('B', 1), ('D', 5)],
    'D': [('B', 4), ('C', 5)]
}

# Run Prim's Algorithm
cost = prim(graph, 'A')
print("Minimum Cost of MST:", cost)
```


### 🔷 Output

```id="a5nn82"
Minimum Cost of MST: 7
```


### 🔷 Time Complexity

* Using Min-Heap: **O(E log V)**
* Using simple array: **O(V²)**
  

### 🔷 Important Notes

* Works only for **undirected graphs**
* Graph must be **connected**
* Gives **Minimum Spanning Tree**, not shortest path

### 🔷 Prim’s vs Kruskal’s

| Feature        | Prim’s       | Kruskal’s     |
| -------------- | ------------ | ------------- |
| Approach       | Node-based   | Edge-based    |
| Data Structure | Min-Heap     | Disjoint Set  |
| Best for       | Dense graphs | Sparse graphs |


## 4. Kruskal’s Algorithm

* MST using greedy approach


## 5. Topological Sorting

* Used in DAGs
* Ordering of tasks


# 🔷 Applications of Graphs

* GPS Navigation
* Social Networks
* Recommendation Systems
* Network Routing
* Dependency Resolution (like package managers)


# 🔷 Time & Space Complexity

| Operation              | Complexity |
| ---------------------- | ---------- |
| Add Vertex             | O(1)       |
| Add Edge               | O(1)       |
| BFS / DFS              | O(V + E)   |
| Adjacency Matrix Space | O(V²)      |
| Adjacency List Space   | O(V + E)   |


# 🔥 Quick Summary

* Graph = Nodes + Edges
* Can be **directed/undirected, weighted/unweighted**
* Represented using **matrix or list**
* Traversed using **BFS & DFS**
* Used in **real-world network problems**

