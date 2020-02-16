# M152: Maximum Product Subarray

## The Problem

Given an integer array `nums`, find the contiguous subarray within an array \(containing at least one number\) which has the largest product.

**Example 1:**

```text
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```text
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

## Solution

Note: this defers from regular Maximum subarray problem \(which can be solved with a sliding window\) because a small negative number could turn big if multiplied by another negative number. Thus, we have to keep track of the smallest and biggest numbers as we iterate down the list.

* Base Case: when at `nums[0]`, we have that `big = small = maximum = 0`.
* Inductive Case: given `big`, `small`, and `maximum` at step `i-1`, and for `n = nums[i]`, we set `big = max(n, n*big, n*small)` and `small = min(n, n*small, n*big)`. We then set `maximum = big` if `big > maximum`.

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if nums == []:
            return 0
        big = small = maximum = nums[0]
        for n in nums[1:]:
            big, small = max(n, n*big, n*small), min(n, n*big, n*small)
            if maximum < big:
                maximum = big
        return maximum
```

