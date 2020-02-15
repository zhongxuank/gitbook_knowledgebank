# M199: Binary Tree Right-side View

{% hint style="info" %}
Problem: [https://leetcode.com/problems/binary-tree-right-side-view/submissions/](https://leetcode.com/problems/binary-tree-right-side-view/submissions/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given a binary tree, imagine yourself standing on the _right_ side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```text
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

### Solution

Depth-First Search, keeping track of the depths of each level. Use a stack for convenience. Left-side first, and replace the node that is viewed as we go to each depth level.

```python
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        stack = [(root, 0)]
        res = []
        while stack:
            node, depth = stack.pop()
            if len(res) < depth + 1:
                res.append(node.val)
            else:
                res[depth] = node.val
            if node.right:
                stack.append((node.right, depth + 1))
            if node.left:
                stack.append((node.left, depth + 1))
        return res
```

