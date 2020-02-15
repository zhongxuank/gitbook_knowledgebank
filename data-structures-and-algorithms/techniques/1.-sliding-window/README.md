# 1. Sliding Window

### Generic Approach \(for substring problems\)

Adapted from [https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-%27substring%27-problems](https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-%27substring%27-problems)

```python
from math import inf
from collections import Counter

class Solution:
    def findSubstring(self, s: str, t: str) -> str: # s input, t substr
        l = r = 0 # two pointers, l = head, r = tail
        counts = Counter(t) # used to check validity of substring
        num_t = len(t) #length of the substring
        head, length = 0, inf #storing the best result
        
        while r < len(s): 
            if s[r] in counts:
                if counts[s[r]] > 0:
                    # Modify counter here
            r += 1 
            while num_t == ?: # check counter condition here 
                # If finding MINIMUM, check and update here
                if s[l] in counts: 
                    # Modify counter here
                l += 1 
            # If finding MAXIMUM, check and update here
        return head, length # or result derived from this
```



