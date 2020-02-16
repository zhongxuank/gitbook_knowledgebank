# E70: Climbing Stairs

{% hint style="info" %}
Problem: [https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/) \[SOLUTION COPIED\]
{% endhint %}

## The Problem

You are climbing a stair case. It takes _n_ steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given _n_ will be a positive integer.

**Example 1:**

```text
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```text
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## Solution

Thought Process:

* Think of base cases. 
  * When there's 1 step, ways = 1
  * When there're 2 steps, ways = 2
* Inductive case: 
  * `ways(n) = ways(n-1) + ways(n-2)`

We will present all 4 DP methods:

* Recursive
* Recursive + Memoization
* Iterative + Memoization
* Iterative + O\(1\) Memory

```python
import functools

class Solution1: # Recursive
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        else: 
            return climbStairs(n-1) + climbStairs(n-2)
            
class Solution2:
    @functools.lru_cache()
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        else: 
            return climbStairs(n-1) + climbStairs(n-2)

class Solution3:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        dp = [None] * (n+1)
        dp[1] = 1
        dp[2] = 2
        for i in range(3, n+1):
            dp[i] = dp[i-1] + dp[i-2]
        return dp[n]

class Solution4:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        prev, prevprev = 2, 1
        for _ in range(3, n+1):
            prev, prevprev = prev + prevprev, prev
        return prev
```



