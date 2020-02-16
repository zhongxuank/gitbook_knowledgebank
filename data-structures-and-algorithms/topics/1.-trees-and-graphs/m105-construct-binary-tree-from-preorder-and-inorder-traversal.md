# M105: Construct Binary Tree from Preorder and Inorder Traversal

{% hint style="info" %}
Problem: [https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/submissions/](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/submissions/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**  
You may assume that duplicates do not exist in the tree.

For example, given

```text
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```text
    3
   / \
  9  20
    /  \
   15   7
```

## Solution

{% hint style="info" %}
Intuition: Recursively slice inorder and preorder lists. First element of Preorder list will always be the root node. Using `index`, we can find the equivalent position `i`of that element in the Inorder list. Note: the first `i` elements in both lists will belong to the main left subtree.
{% endhint %}

{% embed url="https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/discuss/508491/Python-recursive-Solution-very-easy-to-understand-for-beginners." caption="Discussion solution that this is based on." %}

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not inorder:
            return None
        root = TreeNode(preorder[0])
        index = inorder.index(preorder[0])
        root.left = self.buildTree(preorder[1:], inorder[:index])
        root.right = self.buildTree(preorder[1+index:], inorder[index+1:])
        return root
```

