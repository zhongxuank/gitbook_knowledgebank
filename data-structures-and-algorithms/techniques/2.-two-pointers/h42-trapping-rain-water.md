# H42: Trapping Rain Water

{% hint style="info" %}
Problem: [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given _n_ non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

### Solution

{% hint style="info" %}
Notice that in this issue, the only case where we have a height sticking out of a water level is if it's the maximum height. For all other parts of the map, we can find the height of the water above each point by traversing from each end towards the tallest height, and deducting by the maximum height that was viewed by the pointer along the way.
{% endhint %}

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        l, r = 0, len(height)-1
        vol = l_max = r_max = 0
        while l < r:
            l_max = max(height[l], l_max)
            r_max = max(height[r], r_max)
            if l_max < r_max:
                vol += l_max - height[l]
                l += 1
            else:
                vol += r_max - height[r]
                r -= 1
        return vol
```

