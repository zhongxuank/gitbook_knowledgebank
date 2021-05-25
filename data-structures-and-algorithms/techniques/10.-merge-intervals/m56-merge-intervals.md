# M56: Merge Intervals

{% hint style="info" %}
Problem: [https://leetcode.com/problems/merge-intervals/](https://leetcode.com/problems/merge-intervals/)
{% endhint %}

## The Problem

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

```text
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```text
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**Note:**

1. The intervals may be fully overlapped by another.

## The Solution

### Brute Force:

Compare all intervals. NOT IMPLEMENTING BC ... why.

### Sort first!

Sorting first allows us to assume an increasing order of the start of intervals, allowing us to only require one traversal of the list, rather than comparing all.

```python
class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: List[List[int]]
        """
        if intervals == []:
            return []
        intervals.sort(key=lambda x:x[0])
        low, high = intervals[0]
        merged = []
        for interval in intervals[1:]:
            if interval[0] <= high:
                if interval[1] > high:
                    high = interval[1]
                else:
                    continue
            else:
                merged.append([low, high])
                low = interval[0]
                high = interval[1]
        merged.append([low, high])
        return merged
```

