# M209: Minimum Size Subarray Sum

{% hint style="info" %}
Problem: [https://leetcode.com/problems/minimum-size-subarray-sum/](https://leetcode.com/problems/minimum-size-subarray-sum/)
{% endhint %}

## The Problem

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```text
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

## Solution

I will be providing 2 possible solutions.

### Solution 1: Sliding Window / Two Pointers

{% hint style="info" %}
Intuition: Start `l` and `r` on 0. Increment `r` and add element to cumulative sum. Once the sum exceeds s, note down the length if its better than the best so far. Then, start to increment `l` until the sum no longer exceeds s. Repeat until you've reached the last possible `r` and return the best possible answer.
{% endhint %}

```python
from math import inf

class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = 0
        n = len(nums)
        cumsum = 0
        ans = inf
        for i in range(n):
            cumsum += nums[i]
            while cumsum >= s:
                ans = min(ans, i - l + 1)
                cumsum -= nums[l]
                l += 1
        return 0 if ans == inf else ans
```

Time Complexity: O\(n\) 

* each pointer traverses the array at most once. 

### Solution 2: Binary Search + Presum array

{% hint style="info" %}
Start by generating a presum array. Iterate through it, skipping all the values less than `s`. Then, for each remaining value in the presum array, we want to find the index of the first presum that is more than `s - presum[i]`. We can do this with a Binary search. Once we find it, we update the answer if it's smaller than the current one.
{% endhint %}

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        n = len(nums)
        ans = n + 1
        presum = [0 for _ in range(n + 1)]
        for i in range(1, n+1):
            presum[i] = presum[i-1] + nums[i-1]
        for i in range(1, n+1):
            if presum[i] < s:
                continue
            to_find = presum[i] - s
            l, r = 0, i
            while l < r:
                m = (l+r)//2
                if presum[m] <= to_find:
                    l = m + 1
                else:
                    r = m
            ans = min(ans, i - l + 1)
        return 0 if ans == n + 1 else ans
```

Time Complexity: O\(n log n\)

* We traverse the presum array once. At each state, Binary Search takes O\(log n\) to find the target value.

