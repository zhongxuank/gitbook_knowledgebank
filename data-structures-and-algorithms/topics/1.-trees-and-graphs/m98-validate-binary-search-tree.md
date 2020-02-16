# M98: Validate Binary Search Tree

{% hint style="info" %}
Problem: [https://leetcode.com/problems/validate-binary-search-tree/](https://leetcode.com/problems/validate-binary-search-tree/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```text
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```

**Example 2:**

```text
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

## Solution

We can't just check if `root.left.val < root.val` and `root.right.val > root.val`. We also need to ensure that the maximum value in the left subtree is also less than root, and minimum value of the right subtree is greater than root.

Method: Recursive, returning maximum and minimum.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from math import inf

class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def validRecur(root):
            if root == None:
                return (True, inf, -inf)
            lval, lmin, lmax = validRecur(root.left)
            rval, rmin, rmax = validRecur(root.right)
            if lval and rval and lmax < root.val and rmin > root.val:
                return True, min(lmin, rmin, root.val), max(lmax, rmax, root.val)
            return (False, 0, 0)
        res, _, _ = validRecur(root)
        return res
```

### Solution using inorder traversal

{% hint style="info" %}
Intuition: If the next element in the inorder traversal is smaller than the previous one, then it is not a Binary Search Tree
{% endhint %}

```python
from math import inf

class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        stack, inorder = [], -inf
        
        while stack or root:
            while root:
                # Add all the left subtrees into the stack
                stack.append(root)
                root = root.left
            root = stack.pop()
            if root.val <= inorder:
                return False
            inorder = root.val
            root = root.right
        
        return True
```

