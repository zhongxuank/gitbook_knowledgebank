# M79: Word Search

{% hint style="info" %}
Problem: [https://leetcode.com/problems/word-search/](https://leetcode.com/problems/word-search/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```text
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

### Solution: Recursive DFS

We can traverse the board by doing a DFS, traversing to a node's adjacent neighbors. The issue is with keeping track of where we have already visited - a simple solution to this would be to replace the current board element with a filler tile \(like `#`\)  before making the traversal, and then adding back before returning the result.

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not board: # If given an empty board
            return False
        h = len(board)
        w = len(board[0])
        
        def dfs(board, i, j, word):
            # Check termination condition
            if len(word) == 0:
                return True
            # Check boundary / false termination condition
            if not (0 <= i < h) or not (0 <= j < w) or word[0] != board[i][j]:
                return False
            tmp = board[i][j]
            board[i][j] = "#"
            res = dfs(board, i+1, j, word[1:]) or dfs(board, i-1, j, word[1:]) or 
                  dfs(board, i, j-1, word[1:]) or dfs(board, i, j+1, word[1:])
            board[i][j] = tmp
            return res
        
        for i in range(h):
            for j in range(w):
                if dfs(board, i, j, word):
                    return True
        return False
```

