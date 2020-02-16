# E100: Same Tree

{% hint style="info" %}
Problem: [https://leetcode.com/problems/same-tree/](https://leetcode.com/problems/same-tree/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Example 1:**

```text
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```

**Example 2:**

```text
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```

**Example 3:**

```text
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

## Solutions

The solution is a recursive one, and involves a Depth First Search. There are 2 ways this can be one - purely recursive or with a stack.

### Solution 1: Pure Recursion

```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if not p or not q:
            return False
        return p.val == q.val and \
            self.isSameTree(p.left, q.left) and \
            self.isSameTree(p.right, q.right)
```

### Solution 2: Stack

```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        stk = [(p, q)]
        while stk:
            p, q = stk.pop()
            if p is None and q is None:
                continue
            elif p is None or q is None:
                return False
            else:
                if p.val != q.val:
                    return False
                else:
                    stk += [(p.right, q.right), (p.left, q.left)]
        return True
```

