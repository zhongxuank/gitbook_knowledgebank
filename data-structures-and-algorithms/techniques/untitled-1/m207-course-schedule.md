# M207: Course Schedule

{% hint style="info" %}
Problem: [https://leetcode.com/problems/course-schedule/](https://leetcode.com/problems/course-schedule/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

There are a total of n courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

### Solution

{% hint style="info" %}
Intuition: If a course is part of a cycle of pre-requisites, then we know that it is impossible to finish all the courses. 
{% endhint %}

* When checking for whether a course is part of a cycle, we can trace its prerequisites, keeping track of whether we've visited them \(with a `-1`\). Once we land on a recently traversed node, we know that we have a cycle.
* Once we have checked that a course itself is not part of a cycle, then we can mark it as safe \(with a `1`\). This is to reduce the amount of work that needs to be done, and prevents the time complexity from hitting O\(V!\). 

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        preReqs = [[] for _ in range(numCourses)]
        visited = [0 for _ in range(numCourses)]
        for c, p in prerequisites:
            preReqs[c].append(p)
            
        def partOfCycle(c):
            if visited[c] == -1:
                return True
            if visited[c] == 1:
                return False
            visited[c] = -1
            for p in preReqs[c]:
                if partOfCycle(p):
                    return True
            visited[c] = 1
            return False
    
        for c in range(numCourses):
            if partOfCycle(c):
                return False
        return True
```

