# M3: Longest substring without repeating characters

{% hint style="info" %}
Problem: [https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given a string, return the length of the longest substring without repeating characters.

### Solution

Sliding window with counter

{% hint style="info" %}
Shift 'r' while keeping count of each character seen along the way. Once a repeat is found, shift 'l' while removing counts from the characters removed in the moving process, and stop once the repeat is removed. Continuously track the length of substring, keeping the max.
{% endhint %}

```python
from collections import Counter

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l, r, max_l, d = 0, 0, 0, Counter()
        while r < len(s):
            d[s[r]] += 1
            while d[s[r]] > 1:
                d[s[l]] -= 1
                l += 1
            r += 1
            max_l = max(max_l, r-l)
        return max_l
```



