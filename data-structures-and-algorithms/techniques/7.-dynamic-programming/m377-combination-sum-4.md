# M377: Combination Sum 4

{% hint style="info" %}
Problem: [https://leetcode.com/problems/combination-sum-iv/](https://leetcode.com/problems/combination-sum-iv/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

**Example:**

```text
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```

**Follow up:**  
What if negative numbers are allowed in the given array?  
How does it change the problem?  
What limitation we need to add to the question to allow negative numbers?

## Solution

{% hint style="info" %}
Solution recurses on the target value. For `dp(i)` = the number of ways to get i from nums, we have that `dp(i) = sum{dp(i-n) where i < n, and 1 where i ==n}`
{% endhint %}

Note: Recursive solutions cause a stack overflow with this problem, due to the sheer amount of recursive step this generates. The subproblem overlap is huge in this problem, thus an iterative solution with memoization is the best way forward.

```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        if target < 1:
            return 0
        dp = [0] * target + 1
        for i in range(1, target + 1):
            for n in nums:
                dp[i] += dp[i - n] if i <= n else 0
        return dp[target]
```

