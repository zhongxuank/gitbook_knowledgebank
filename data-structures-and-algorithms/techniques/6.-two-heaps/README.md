# 6. Two Heaps

## What is a Heap?

Links: [https://towardsdatascience.com/data-structure-heap-23d4c78a6962](https://towardsdatascience.com/data-structure-heap-23d4c78a6962), [https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/](https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/)

A Heap is a data-structure often used as an implementation of a Priority Queue. Heaps often come in 2 forms - Max Heaps and Min Heaps. Heaps are represented often as binary trees, with the property that for a Max \(Min\) Heap, the parent node will always have a larger \(smaller\) value than its two children. This means that we can always find the max \(min\) in constant time, and pop it out in O\(log N\) time.

Heaps often come with the following methods \(I will be using a min heap for simplicity\)

* `min_heapify` which makes some nodes and its descendant nodes meet the heap property \(O\(log N\) time worse case
* `build_min_heap` which runs `min_heapify` on the whole tree to build on an arbitrary array
* `find_min` which just returns the value of the root
* `remove_min` which pops the value of the root, then replaces it with last value of the array, and runs `min_heapify` to get back a min heap



