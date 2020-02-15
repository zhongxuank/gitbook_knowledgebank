# 4. BFS

## General Method

Use `deque` from Python's `collections` library to build a Queue. Start with `deque([root, 1])` while keeping track of the visited nodes \(in a set\). Then, use `queue.popleft()` to pop the next node in visit order, and appending nodes that you want to add to visit order in to queue.

