# E141: Linked List Cycle

{% hint style="info" %}
Problem: [https://leetcode.com/problems/linked-list-cycle/](https://leetcode.com/problems/linked-list-cycle/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position \(0-indexed\) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

### Solution

```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        fast = head
        slow = head
        while fast is not None:
            if fast.next is None:
                return False
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True
        return False
```

