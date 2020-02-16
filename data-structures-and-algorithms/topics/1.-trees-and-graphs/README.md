# 1. Trees and Graphs

## Graph Representation

There are a few ways to represent graphs \(manually\) as a data structure.

### 1. Edge List

One of the most basic ways that a graph can be represented is as a list of edges. These edges are often represented as tuples, and depending on use case, can be either undirected \(order doesn't matter\) or directed \(order matters, a tuple `(u, v)` represents an edge going from `u` to `v`\).

```python
Graph = [(0,1), (1,2), (0,3), (1,3)]
```

### 2. Dictionary

A convenient way to represent a graph would be with a dictionary. This dictionary will have all vertices as keys, whose value would be all its adjacent vertices, stored as a set or a list. This allows for quick traversal, and it also has some nice features, like having an easy way to get the degree of a vertex.

```python
Graph = {0: {1, 3},
         1: {0, 2, 3},
         2: {1},
         3: {0, 1}}
```

### 3. Adjacency Matrix

This representation is used a lot in mathematics, and for use when doing message passing with graphs. For a graph on `n` vertices, the adjacency matrix will be a `n * n` sparse matrix, where the `[i, j]` element is 1 if the edge `(v[i], v[j])` exists. Else, it is a 0.

```python
Graph = [[0,1,0,1],
         [1,0,1,1],
         [0,1,0,0],
         [1,1,0,0]]
```

### 4. Incidence Matrix

The incidence matrix of a graph is another representation. For a graph on `n` vertices and `m` edges, the graph is a `n * m` matrix where each row represents a vertex and each column represents an edge. If the vertex is in the edge, the corresponding value is 1, otherwise it is 0. Each column should only have 2 '1's.

```python
Graph = [[1,0,1,0],
         [1,1,0,1],
         [0,1,0,0],
         [0,0,1,1]]
```

