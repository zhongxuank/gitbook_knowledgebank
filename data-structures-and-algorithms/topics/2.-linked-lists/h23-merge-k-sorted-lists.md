# H23: Merge k Sorted Lists

{% hint style="info" %}
Problem: [https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)
{% endhint %}

## The Problem

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

```text
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

**Example 2:**

```text
Input: lists = []
Output: []
```

**Example 3:**

```text
Input: lists = [[]]
Output: []
```

## Solutions

### Solution Type 1: Brute Force

Extract all the values out of the Linked Lists by traversing them, sort, and then recreate the linked lists.

**Run Time:** `O(N log(N))`

### Solution Type 2: Compare One at a Time, with Priority Queue

We compare the heads of all the linked list, adding them to a Priority Queue such that we can always get the lowest value node out at `O(1)` time. 

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
from Queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = point = ListNode(0)
        q = PriorityQueue()
        # Add initial nodes into priority queue, by val
        for l in lists:
            if l:
                q.put((l.val, l))
        while not q.empty():
            # get from queue i.e. lowest val
            val, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            # if not empty, put next value into queue
            if node:
                q.put((node.val, node))
        return head.next
```

### Solution Type 3: Merge 2 at a time w. Divide and Conquer

Using Merge 2 Lists, Merge lists 2 at a time, going pairwise and repeating until only 1 left. This method is faster than mergine each list into a master list as it only requires `Log(k)` runs of Merge 2 Lists, rather than `k` runs.

```python
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        amount = len(lists)
        interval = 1 # This determines the intervals in which we combine
        while interval < amount:
            for i in range(0, amount - interval, interval * 2):
                lists[i] = self.merge2Lists(lists[i],
                                           lists[i+interval])
            interval *= 2
        return lists[0] if amount > 0 else None
        
    def merge2Lists(self, l1, l2):
        head = point = ListNode(0)
        while l1 and l2:
            if l1.val <= l2.val:
                point.next = l1
                l1 = l1.next
            else:
                point.next = l2
                l2 = l2.next
            point = point.next
        if not l1:
            point.next = l2
        else:
            point.next = l1
        return head.next
```

