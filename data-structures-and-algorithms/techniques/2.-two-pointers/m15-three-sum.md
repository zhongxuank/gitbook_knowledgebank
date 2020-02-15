# M15: Three Sum

{% hint style="info" %}
Problem: [https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given an array `nums` of _n_ integers, are there elements _a_, _b_, _c_ in `nums` such that _a_ + _b_ + _c_ = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

### Solution

{% hint style="info" %}
Intuition: With a sorted array, we start a pointer going from one end. We then try to find two other numbers in the remaining array with sum equals to the compliment of the original number. We will find the other two numbers using two-sum.
{% endhint %}

```python
class Solution:
    def twoSum(self, target, nums):
        # Assume that nums is already sorted
        res = []
        l, r = 0, len(nums) -1
        while l < r:
            diff = nums[l] + nums[r] - target
            if diff < 0: # sum is less than target
                l += 1
            elif diff > 0: # sum is more than target
                r -= 1
            else:
                res.append([-target, nums[l], nums[r]])
                # skip repeats:
                while l < r and nums[l] == nums[l+1]:
                    l += 1
                while l < r and nums[r] == nums[r-1]:
                    r -= 1
                l += 1
                r -= 1
        return res
    
    def threeSum(self, nums):
        res = []
        nums.sort()
        for i in range(len(nums) - 2):
            if nums[i] > 0:
                break
            if i > 0 and nums[i] == nums[i-1]:
                continue
            target = nums[i]
            res += self.twoSum(-target, nums[i+1:])
        return res
```



