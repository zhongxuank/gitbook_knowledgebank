# M162: Find Peak Element

{% hint style="info" %}
Problem: [https://leetcode.com/problems/find-peak-element/](https://leetcode.com/problems/find-peak-element/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

A peak element is an element that is greater than its neighbors.

Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `nums[-1] = nums[n] = -∞`.

**Example 1:**

```text
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```text
Input: nums = [1,2,1,3,5,6,4]
Output: 1 or 5 
Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

## Solution

{% hint style="info" %}
Intuition: Imagine the array as a list of mountains and valleys. To find a peak, we look at the spot we are at, and try to gauge the slope \(compare it to the value that comes after it\). We want to search toward the upslope every time, since there must be a peak there.
{% endhint %}

The best solution makes use of a binary search. At each step, we check if the middle node between `l` and `r` to see in what direction the slope is. We then shift the search towards the slope.

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        # binary search
        l, r = 0, len(nums)-1
        while l < r:
            mid = (l + r) // 2
            if nums[mid] > nums[mid + 1]:
                r = mid
            else:
                l = mid + 1
        return l
```

