# E1: Two Sum

{% hint style="info" %}
Problem: [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have _**exactly**_ one solution, and you may not use the _same_ element twice.

**Example:**

```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Solution 1: One-pass with Dict

```python
class Solution:
    def twoSumDict(self, nums: List[int], target: int) -> List[int]:
        seen = {}
        for i, n in enumerate(nums):
            complement = target - n
            if complement in seen:
                return [i, seen[complement]]
            seen[n] = i
```

### Solution 2: Two-pointer

Purpose of this solution: Try to solve without the use of dictionaries. O\(N log N\) time, O\(N\) space. Less optimal than using Dict, but it also gives a soft intro to two-pointer method.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums = list(enumerate(nums))
        nums.sort(key = lambda e: e[1])
        l, r = 0, len(nums) - 1
        while l < r:
            two_sum = nums[l][1] + nums[r][1]
            if two_sum < target:
                l += 1
            elif two_sum > target:
                r -= 1
            else:
                return [nums[l][0], nums[r][0]]
        return None
```

