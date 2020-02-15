# M11: Container with Most Water

{% hint style="info" %}
Problem: [https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate \(i, ai\). n vertical lines are drawn such that the two endpoints of line i is at \(i, ai\) and \(i, 0\). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and n is at least 2.

### Solution

{% hint style="info" %}
Intuition: Start with two pointers on opposite ends. Initialize our maximum value at this point. Notice that shifting the taller of the 2 lines will not increase the area, but shifting the shorter one might. The current value is the maximum value of any container with the shorter end.
{% endhint %}

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        maxArea = 0
        l, r = 0, len(height) - 1
        
        while l < r:
            minHeight = min(height[l], height[r])
            width = r-l
            area = minHeight * width
            maxArea = max(area, maxArea)
            if height[l] > height[r]:
                r -= 1
            else:
                l += 1
        return maxArea
```



