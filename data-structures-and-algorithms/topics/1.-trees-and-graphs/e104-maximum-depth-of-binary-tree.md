# E104: Maximum Depth of Binary Tree

{% hint style="info" %}
Problem: [https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
{% endhint %}

## The Problem

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

## Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        stk = [(root, 1)]
        maximum = 0
        while stk:
            v, d = stk.pop()
            if v == None:
                continue
            if d > maximum:
                maximum = d
            stk += [(v.left, d+1), (v.right, d+1)]
        return maximum            
```

