# M236: Lowest Common Ancestor of Binary Tree

{% hint style="info" %}
Problem: [https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants \(where we allow **a node to be a descendant of itself**\).”

Given the following binary tree:  root = \[3,5,1,6,2,0,8,null,null,7,4\]

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

**Example 1:**

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

## Solution

{% hint style="info" %}
Intuition: Recursively check the nodes, DFS. Returns true if left, right or current value is equals to either P or Q. Only if current node is the LCA will it return true for  2 or more of left, right or current.
{% endhint %}

```python
class Solution:
    def __init__(self):
        self.ans = None
        
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        def auxFn(current):
            if not current:
                return False
            left = auxFn(current.left)
            right = auxFn(current.right)
            
            mid = current == p or current == q
            
            if mid + left + right >= 2:
                self.ans = current
            
            return mid or left or right
        
        auxFn(root)
        return self.ans
```

