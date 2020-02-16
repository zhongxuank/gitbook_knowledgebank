# E198: House Robber

{% hint style="info" %}
Problem: [https://leetcode.com/problems/house-robber/](https://leetcode.com/problems/house-robber/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```text
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```text
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

## Solution

{% hint style="info" %}
Recursive relation: Define dp\(i\) = maximum amount of money that can be robbed from houses 0 - i, we have that

```python
dp(i) = max(nums[i] + dp(i - 2), dp(i-1))
```
{% endhint %}

* Robbing house i only depends on the maximum value that we could have possibly gotten had we robbed house i-1. In any case, we should still try to know what the maximum possible value was had we robbed house i-1 or house i-2.
* In the case where dp\(i - 1\) does not include house i-1, then we should definitely rob house\(i\), which will be the case since dp\(i - 2\) == dp\(i - 1\).

Here, for practice, I will be coding all 4 types of solutions:

### Solution 1: Recursive

```python
class Solution1:
    def rob(self, nums: List[int]) -> int:
        if nums == []:
            return 0
        if len(nums) <= 2:
            return max(nums)
        return max(nums[-1] + self.rob(nums[:-2]), self.rob(nums[:-1]))
        
```

### Solution 2: Recursive + Memo

```python
import functools

class Solution2:
    def rob(self, nums: List[int]) -> int:            
        if nums == []:
            return 0
        @functools.lru_cache()
        def dp(n):
            if n <= 2:
                return max(nums[:n])
            return max(nums[n-1] + dp(n-2), dp(n-1))
        return dp(len(nums))
```

### Solution 3: Iterative + Memo

```python
class Solution3:
    def rob(self, nums: List[int]) -> int:
        if nums == []:
            return 0
        n = len(nums)
        if n <= 2:
            return(max(nums))
        dp = [None] * (n + 1)
        dp[1] = nums[0]
        dp[2] = max(nums[:2])
        for i in range(3, n+1):
            dp[i] = max(nums[i-1] + dp[i-2], dp[i-1])
        return dp[n] 
    
```

### Solution 4: Iterative + N vars

```python
class Solution4:
    def rob(self, nums: List[int]) -> int:
        if nums == []: 
            return 0
        prev1, prev2 = 0,0
        for i in range(len(nums)):
            prev1, prev2 = max(nums[i] + prev2, prev1), prev1
        return prev1
```

