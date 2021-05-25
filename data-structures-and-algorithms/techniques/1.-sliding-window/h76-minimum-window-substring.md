# H76: Minimum Window Substring

{% hint style="info" %}
Problem: [https://leetcode.com/problems/minimum-window-substring/](https://leetcode.com/problems/minimum-window-substring/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O\(n\).

**Example:**

```text
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

* If there is no such window in S that covers all characters in T, return the empty string `""`.
* If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

### Solution

{% hint style="info" %}
* The key idea is to shift `r` until we get a valid window, and then try to shorten the window by shifting `l` until our window is invalid, then continue shifting `r` again to get another valid window
* Use a **counter** to keep track of the elements that we need to account for, **decrementing** them when they are **added** to a window
* To account for extra counts, decrement the counters **past 0** 
* Do the opposite when shrinking windows: when an element leaves the window, increase the count, and check if we needed them or if we had extra to spare
{% endhint %}

#### Full Description:

1. Set `l` and `r` to `0`.
2. Represent the elements in `t` with a `Counter()`, using the built in class.
3. When the total count reaches 0, it indicates that we have found all the elements in `t`. So that we don't have to repeatedly sum, we keep track of the number of elements accounted for using `num_t`.
4. We also keep track of the length and start point of the minimum-length valid window so far.
5. The terminating condition for shifting `r` is `r < len(s)`.
6. If the current element `e` is an element we still need, then we indicate that we have found it by decrementing `num_t`.
7. Regardless of whether we needed `e`, we still decrease `e`'s count in the counter. The negative count accounts for the extra `e`s we find along the way.
8. In this specific implementation, the counter is only manipulated if `e` is in `t`, but this method would still work even if it wasn't in `t`, as the counter returns a 0 if a non-existing key is inserted. This is done so that the code is clearer, and to reduce the size of `count`.
9. We shift `r` down by 1 at this point. We can use `r` for length calculations due to zero-indexing.
10. After shifting `r`, we will check if we have achieved a valid window \(`num_t == 0`\). If we have, then we begin shifting `l` until we get an invalid window.
11. If we have achieved a new minimum length, save its length and starting point.
12. We then do the opposite of \[6\] and \[7\] - check if the element that `l` is pointing to is an element we need. If it is, we increase the count. If the count goes above 0, this means that we had no more spares, and thus we increase `num_t`.
13. We shift `l` down by 1.
14. In the final step, we check if we never found any valid windows. If we didn't we return an empty string `""`. Else, we return the string by indexing based on starting point and length.

```python
from math import inf
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        l = r = 0 #[1]
        counts = Counter(t) #[2]
        num_t = len(t) #[3]
        head, min_length = 0, inf #[4]
        
        while r < len(s): #[5]
            if s[r] in counts:
                if counts[s[r]] > 0: #[6]
                    num_t -= 1
                counts[s[r]] -= 1 #[7]. [8]
            r += 1 #[9]
            while num_t == 0: #[10]
                if r - l < min_length: #[11]
                    min_length = r-l
                    head = l
                if s[l] in counts: #[12]
                    counts[s[l]] += 1
                    if counts[s[l]] > 0:
                        num_t += 1
                l += 1 #[13]
        return '' if min_length == inf else s[head : head + min_length] #[14]
```



