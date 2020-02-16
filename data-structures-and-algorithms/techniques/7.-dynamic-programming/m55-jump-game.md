# M55: Jump Game

## The Problem

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**

```text
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```text
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

## Solution

{% hint style="info" %}
Intuition: Checking from the back, we keep track of the smallest step so far which can go to the last index. From our current index, if the index + its max jump is greater than the smallest step, that means that it can reach the last index. We then update the smallest step, and check back once more.
{% endhint %}

### Solution 1: Iterative + Memoization

```python
class Solution1:
    def canJump(self, nums: List[int]) -> bool:
        N = len(nums)
        dp = [False] * N
        dp[N-1] = True
        leftest = [N-1] * N
        for i in range(N-2, -1, -1):
            if i + nums[i] >= leftest[i + 1]:
                leftest[i] = i
                dp[i] = True
            else:
                leftest[i] = leftest[i+1]
        return dp[0]
```

### Solution 2: Iterative + N Var

Notice that we don't actually need to keep track of all the previous steps, all we need is the smallest step on which we can jump to the final index.

```python
class Solution2:
    def canJump(self, nums: List[int]) -> bool:
        N = len(nums)
        dp = True
        smallest = N-1
        for i in range(N-2, -1, -1):
            if i + nums[i] >= smallest:
                smallest = i
                dp = True
            else:
                dp = False
        return dp
```

### Solution 3: Recursive

Notice now that we don't actually need to test if dp is True or False until the very end. We just need to check successive leftest.

```python
class Solution3:
    def canJump(self, nums: List[int]) -> bool:
        def leftest(i: int) -> int:
            if i == len(nums)-1:
                return i
            leftest_next = leftest(i+1)
            return i if i + nums[i] >= leftest_next else leftest_next
        return leftest(0) == 0 
```

Note: This one is actually the slowest one I tested on Leetcode \(?\) so maybe Iterative is still better.

