
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

- An Undirected Graph is a graph in which edges have no direction.
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

* Edges have **direction**

Example:

```
A → B → C
```

Python:

```python
graph = {
    'A': ['B'],
    'B': ['C'],
    'C': []
}
```


## 3. Weighted Graph

* Each edge has a **weight (cost/distance)**

Example:

```
A --(5)--> B
```

Python:

```python
graph = {
    'A': [('B', 5)],
    'B': []
}
```

## 4. Unweighted Graph

* All edges have equal weight


## 5. Cyclic Graph

* Contains at least one **cycle**

Example:

```
A → B → C → A
```

## 6. Acyclic Graph

* No cycles present

👉 Special case:

* **DAG (Directed Acyclic Graph)**


## 7. Connected Graph

* Every node is reachable from any other node



## 8. Disconnected Graph

* Some nodes are not connected



## 9. Complete Graph

* Every node is connected to every other node



## 10. Bipartite Graph

* Nodes divided into 2 sets
* Edges only between sets (not within)



# 🔷 Graph Representation

## 1. Adjacency Matrix

* 2D array
* `matrix[i][j] = 1` if edge exists

Example:

```python
graph = [
 [0, 1, 0],
 [1, 0, 1],
 [0, 1, 0]
]
```

### Pros:

* Fast edge lookup: O(1)

### Cons:

* Space complexity: O(V²)



## 2. Adjacency List (Most Used)

* Dictionary or list of lists

```python
graph = {
    'A': ['B', 'C'],
    'B': ['A'],
    'C': ['A']
}
```

### Pros:

* Space efficient: O(V + E)



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

