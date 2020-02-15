# M200: Number of Islands

{% hint style="info" %}
Problem: [https://leetcode.com/problems/number-of-islands/](https://leetcode.com/problems/number-of-islands/) \[SOLUTION PARTIALLY COPIED\]
{% endhint %}

### The Problem

Given a 2d grid map of `'1'`s \(land\) and `'0'`s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```text
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```text
Input:
11000
11000
00100
00011

Output: 3
```

### Solution

{% hint style="info" %}
Intuition: Traverse each node in the grid. Once on land, start to do a DFS to visit all connected land masses. Mark each of those land masses as visited when passing. Next time, if it has already been visited, we skip it. Count the number of times a DFS is started.
{% endhint %}

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0
        H, W = len(grid), len(grid[0])
        
        def dfs(i, j):
            if not (0 <= i < H and 0 <= j < W):
                return
            if grid[i][j] == '1':
                grid[i][j] = '0'
                for x, y in [(i + 1, j), (i - 1, j), (i, j + 1), (i, j - 1)]:
                    dfs(x, y)
        
        islands = 0
        for i in range(H):
            for j in range(W):
                if grid[i][j] == '1':
                    dfs(i,j)
                    islands += 1
        return islands
```

