# M213: House Robber II

{% hint style="info" %}
Problem: [https://leetcode.com/problems/house-robber-ii/](https://leetcode.com/problems/house-robber-ii/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```text
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```

**Example 2:**

```text
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

## Solution

Very similar to the solution to E198: House Robber. Only difference is that we now consider 2 cases. We either rob the first house \(which means we can't rob the last house\), or we don't rob the first house. These two cases are equivalent to finding the maximum amount if we robbed houses 1 to n-1, or the maximum amount if we robbed houses 2 to n. Thus, we just need to consider both cases, and find the maximum.

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        def rob_row(nums):
            now = prev = 0
            for n in nums:
                now, prev = max(n + prev, now), now
            return now
        if len(nums) == 0:
            return 0
        if len(nums) == 1:
            return nums[0]
        return max(rob_row(nums[1:]), rob_row(nums[:-1]))
```

