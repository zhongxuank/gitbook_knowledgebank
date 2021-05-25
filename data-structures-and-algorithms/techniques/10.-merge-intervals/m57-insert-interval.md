# M57: Insert Interval

{% hint style="info" %}
Problem: [https://leetcode.com/problems/insert-interval/](https://leetcode.com/problems/insert-interval/)
{% endhint %}

## The Problem



Given a set of _non-overlapping_ intervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```text
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

**Example 2:**

```text
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

**Example 3:**

```text
Input: intervals = [], newInterval = [5,7]
Output: [[5,7]]
```

**Example 4:**

```text
Input: intervals = [[1,5]], newInterval = [2,3]
Output: [[1,5]]
```

**Example 5:**

```text
Input: intervals = [[1,5]], newInterval = [2,7]
Output: [[1,7]]
```

**Constraints:**

* `0 <= intervals.length <= 104`
* `intervals[i].length == 2`
* `0 <= intervals[i][0] <= intervals[i][1] <= 105`
* `intervals` is sorted by `intervals[i][0]` in **ascending** order.
* `newInterval.length == 2`
* `0 <= newInterval[0] <= newInterval[1] <= 105`

## Solution

### My Solution - Iterating through and checking...

```python
class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[List[int]]
        :type newInterval: List[int]
        :rtype: List[List[int]]
        """
        if intervals == []:
            return [newInterval]
        inserted = False
        res = []
        for low, high in intervals:
            if low <= newInterval[0]:
                if high < newInterval[0]:
                    res.append([low, high])
                else:
                    newInterval[0] = low
                    if high > newInterval[1]:
                        newInterval[1] = high
            elif low <= newInterval[1]:
                if high < newInterval[1]:
                    continue
                newInterval[1] = high
            else:
                if not inserted:
                    res.append(newInterval)
                    inserted = True
                res.append([low, high])
        if not inserted:
            res.append(newInterval)
        return res
```

### Similar Method \(Copied from Jeremy\)

Much more readable.

```python
class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[List[int]]
        :type newInterval: List[int]
        :rtype: List[List[int]]
        """
        def overlap(a, b):
            return not (before(a,b) or after(a,b))
        
        def before(a, b):
            return a[1] < b[0]
        
        def after(a, b):
            return a[0] > b[1]
        
        def merge(a, b):
            return (min(a[0], b[0]), max(a[1], b[1]))
        
        if not intervals:
            return [newInterval]
        
        merged = []
        i = 0
        while i < len(intervals):
            if before(newInterval, intervals[i]):
                break
            if overlap(newInterval, intervals[i]):
                newInterval = merge(newInterval, intervals[i])
            else:
                merged.append(intervals[i])
            i += 1
        merged += [newInterval] + intervals[i:]
        return merged
```

