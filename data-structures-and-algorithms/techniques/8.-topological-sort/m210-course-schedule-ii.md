# M210: Course Schedule II

{% hint style="info" %}
Problem: [https://leetcode.com/problems/course-schedule-ii/](https://leetcode.com/problems/course-schedule-ii/) 
{% endhint %}

## The Problem

There are a total of _n_ courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**

```text
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```

**Example 2:**

```text
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

## Solution

Topological sort is all that needs to be done. If it is valid \(i.e. it is a DAG\), then the order of the stack produced by the topological sort is the order in which we should take the classes as it guarantees that all prerequisite courses \(heads of edges\) are taken prior to the course that requires them \(tails of edges\).

To keep track of whether or not the graph is valid, we take note of which vertices we are currently traversing in the recursive call. If during a single chain of recursive calls, we visit a vertex that was part of the recursive call, then we know that a cycle exists, and it is not a DAG.

Notes on the solution:

1. We first convert the graph from an edge list to a dictionary for ease of use. This is done using the `defaultdict` function in the `collections` library. 
2. We also initialize a memo to keep track of which vertices have been visited. 
3. Lastly, we initialize the stack.
4. We define a topological function.
5. First, the function checks if we have visited the vertex in the current recursive call, which is indicated by a `-1` value in the memo. If it does, it raises an Exception.
6. We then check if we have visited before in a previous recursive call. If it has, we end the current recursive call.
7. We then set the current course to `-1` in the memo to indicate that it was traversed in the current call.
8. For each course that the current course is a prerequisite for, we call topological sort onto it.
9. Once all the sorting is done, we set the current course to `1` in the memo, to indicate that it has already been visited. We also append it into the stack.
10. For each course, we then try to run topological sort on it. If it raises an exception, this means that the graph is not a DAG, and thus we return an empty list. 

```python
from collections import defaultdict

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        prGraph = defaultdict(list) #[1]
        for u, v in prerequisites:
            prGraph[u].append(v)
        memo = [0 for _ in range(numCourses)] #[2]
        stk = [] #[3]
        def topSort(c): #[4]
            if memo[c] == -1: #[5]
                raise Exception("Cycle Found")
            if memo[c] == 1: #[6]
                return
            memo[c] = -1 #[7]
            for v in prGraph[c]: #[8]
                topSort(v)
            memo[c] = 1 #[9]
            stk.append(c)
        
        for c in range(numCourses): #[10]
            try:
                topSort(c)
            except:
                return []
        return stk
```

