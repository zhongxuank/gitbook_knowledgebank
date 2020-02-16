# 8. Topological Sort

## What is Topological Sorting?

{% embed url="https://www.geeksforgeeks.org/topological-sorting/" %}

Topological sorting for Directed Acyclic Graphs \(DAGs\) is a linear ordering of vertices such that for every directed edge `(u, v)`, vertex `u` comes before `v` in the ordering. A topological sort of a graph is not possible if the graph is not a DAG.

A quick intuition for topological sort is as follows:

* Initiate a temporary stack.
* Starting with the first vertex, recursively call topological sort for all its adjacent vertices, and then push it to the stack. Note: the vertex is pushed to the stack only after all its adjacent vertices are pushed.
* Once a vertex has completed the topological sort process, we then move onto the next vertex and check if it's been visited. If not, run topological sort on it.
* Once all vertices have been visited, the stack can be emptied and the order in which the elements come out is the ordering of the topological sort.



