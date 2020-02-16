# M63: Unique Paths II

{% hint style="info" %}
Problem: [https://leetcode.com/problems/unique-paths-ii/submissions/](https://leetcode.com/problems/unique-paths-ii/submissions/)
{% endhint %}

## The Problem

A robot is located at the top-left corner of a _m_ x _n_ grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** _m_ and _n_ will be at most 100.

**Example 1:**

```text
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

## Solutions

Before we begin, important to do some simple sanity checks

* Is there an obstacle in the starting grid? If yes, then numPaths = 0
* Is there an obstacle in the finishing grid? If yes, then numPaths = 0

### Solution 1: Recursive + Memoization

```python
import functools

class Solution1:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        R = len(obstacleGrid)
        C = len(obstacleGrid[0])
        @functools.lru_cache()
        def pathsAt(r,c):
            if r == R + 1 or c == C + 1:
                return 0
            if r == R and c == C and obstacleGrid[R-1][C-1] != 1:
                return 1
            elif r == R and c == C:
                return 0
            paths = 0
            if not (r == R or obstacleGrid[r][c-1] == 1):
                paths += pathsAt(r+1, c)
            if not (c == C or obstacleGrid[r-1][c] == 1):
                paths += pathsAt(r, c+1)
            return paths
        return pathsAt(1, 1) if obstacleGrid[0][0] == 0 else 0
```

### Solution 2: Iterative + Grid Memoization

{% hint style="info" %}
Intuition: Working backwards from the finishing line, we can iteratively generate potential paths by heading left and up towards the starting line. If we reach a grid which has an obstacle, we can account for it by leaving the number of possible paths from that spot as 0. In subsequent steps, this will effectively represent that there are no paths to the finishing line if you were to head into a grid with an obstacle on it.
{% endhint %}

We create an oversized memoization so that we can account for the cases on the edge of the grid easily. If there is an obstacle on the current position, we just leave the number of paths as 0.

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        R = len(obstacleGrid)
        C = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1:
            return 0
        if obstacleGrid[R-1][C-1] == 1:
            return 0
        dp = [[0 for _ in range(C+1)] for _ in range(R+1)]
        dp[R-1][C-1] = 1
        for r in range(R-1, -1, -1):
            for c in range(C-1, -1, -1):
                if obstacleGrid[r][c] == 1:
                    continue
                dp[r][c] += dp[r][c+1] + dp[r+1][c]
        return dp[0][0]
```



