
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

## 1. Breadth-First Search (BFS)

* Level-by-level traversal
* Uses **Queue**

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            queue.extend(graph[node])
```


## 2. Depth-First Search (DFS)

* Goes deep first
* Uses **Stack / Recursion**

```python
def dfs(graph, node, visited=set()):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
```


# 🔷 Important Graph Algorithms

## 1. Dijkstra’s Algorithm

* Finds **shortest path**
* Works for weighted graphs


## 2. Floyd-Warshall

* All-pairs shortest path


## 3. Prim’s Algorithm

* Minimum Spanning Tree (MST)


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

