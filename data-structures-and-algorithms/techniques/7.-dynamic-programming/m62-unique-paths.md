# M62: Unique Paths

{% hint style="info" %}
Problem: [https://leetcode.com/problems/unique-paths/](https://leetcode.com/problems/unique-paths/) \[SOLUTION PARTIALLY COPIED\]
{% endhint %}

## The Problem

A robot is located at the top-left corner of a _m_ x _n_ grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

How many possible unique paths are there?

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)  
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** _m_ and _n_ will be at most 100.

**Example 1:**

```text
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```text
Input: m = 7, n = 3
Output: 28
```

## Solution

{% hint style="info" %}
Idea: The number of unique paths in a `m * n` board is just the number of paths in a `m-1 * n` board + the number of paths in a `m * n-1` board.
{% endhint %}

I'll try and implement various DP approaches to this problem.

### Solution 1: Recursive

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        if m == 0 or n == 0:
            return 0
        if m == 1 and n == 1:
            return 1
        return self.uniquePaths(m - 1, n) + self.uniquePaths(m, n-1)
```

Very pretty, but it causes a stack overflow. Bad!

### Solution 2: Recursive + Memoization

```python
import functools

class Solution:
    @functools.lru_cache()
    def uniquePaths(self, m: int, n: int) -> int:
        if m == 0 or n == 0:
            return 0
        if m == 1 and n == 1:
            return 1
        return self.uniquePaths(m - 1, n) + self.uniquePaths(m, n-1)
```

Works! But seems a little slow. Can we do better?

### Solution 3: Iterative + Grid Memoization

```python
class Solution3:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0 for _ in range(m+1)] for _ in range(n+1)]
        dp[1][1] = 1
        for i in range(1, n+1):
            for j in range(1, m+1):
                dp[i][j] += int(dp[i-1][j]) + int(dp[i][j-1])
        return dp[n][m]
```

As with all iterative steps, we need to ask if we need to keep all of the past data. For this case, we don't - we only need to keep the last row.

### Solution 4: Iterative + N Val

```python
class Solution4:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [0 for _ in range(m+1)]
        dp[1] = 1
        for _ in range(1, n+1):
            for i in range(1, m+1):
                dp[i] += dp[i-1]
        return dp[m]
```



