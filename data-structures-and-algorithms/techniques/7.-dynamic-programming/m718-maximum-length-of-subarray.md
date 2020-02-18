# M718: Maximum Length of Subarray

{% hint style="info" %}
Problem: [https://leetcode.com/problems/maximum-length-of-repeated-subarray/](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)
{% endhint %}

## The Problem

Given two integer arrays `A` and `B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**

```text
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

## Solution

This solution involves dynamic programming and honestly some crazy brain magic.

{% hint style="info" %}
Intuition: For any matching subarray of length `k`, there are also matching subarrays of length `k-1`, `k-2`, etc. Thus, all that is needed is to sequentially check pairs of entries to see if they match. If they do match, we then store that information in a memo by taking the memo entry of `i+1, j+1` i.e. the amount stored \(0 if not matched, &gt; 0 if previously matched\), and adding 1 to it. This keeps a running tally of the maximum matching subarray found so far. Then, just take a max to solve it.
{% endhint %}

```python
class Solution:
    def findLength(self, A: List[int], B: List[int]) -> int:
        m = len(A)
        n = len(B)
        memo = [[0 for _ in range(m + 1)] for _ in range(n + 1)]
        for i in range(m - 1, -1, -1):
            for j in range(n -1, -1, -1):
                if A[i] == B[j]:
                    memo[j][i] = memo[j+1][i+1] + 1
        return max([max(row) for row in memo])
```

