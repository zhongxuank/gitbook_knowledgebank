# H295: Find Median from Data Stream

{% hint style="info" %}
Problem: [https://leetcode.com/problems/find-median-from-data-stream/](https://leetcode.com/problems/find-median-from-data-stream/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.For example,

`[2,3,4]`, the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum\(int num\) - Add a integer number from the data stream to the data structure.
* double findMedian\(\) - Return the median of all elements so far.

**Example:**

```text
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

**Follow up:**

1. If all integer numbers from the stream are between 0 and 100, how would you optimize it?
2. If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?

### Solution

{% hint style="info" %}
Intuition: Maintain 2 balanced heaps, a Min Heap and a Max Heap. When a new number is added, we add it into the Min Heap if it's above the Median, and to the Max Heap if it's below. Then depending on the parity of the current step, find the Median.
{% endhint %}

#### Details:

* If `num` is being added to an even list:
  * If `num` is greater than median, then push `num` into Max heap `lo`, and replace median with the highest value in `lo` by popping it.
  * Otherwise, push `num` into Min heap `hi`, and replace median with the lowest value in `hi` by popping it.
* If `num` is being added to an odd list:
  * If `num` is greater than median, then push median to `lo`, and `num` to `hi`. Then, replace the median by peeking into both heaps and finding the mean.
  * Otherwise, push median to `hi`, and `num` to `lo`, and replace median by peeking into both heaps and finding the mean.

```python
import heapq

class MinHeap:
    def __init__(self): 
        self.h = []
        
    def push(self, x): 
        heapq.heappush(self.h, x)
        
    def pop(self): 
        return heapq.heappop(self.h)
        
    def peek(self): 
        return self.h[0]
        
        
class MaxHeap:
    def __init__(self): 
        self.h = []
        
    def push(self, x): 
        heapq.heappush(self.h, -x)
    
    def pop(self): 
        return -(heapq.heappop(self.h))
        
    def peek(self): 
        return -self.h[0]
        
        

class MedianFinder:

    def __init__(self):
        self.median = None
        self.hi = MinHeap()
        self.lo = MaxHeap()
        self.len = 0
        

    def addNum(self, num: int) -> None:
        print(num)
        if self.median is None:
            self.median = num
        elif self.len % 2 == 0: # Even case
            if num > self.median:
                self.hi.push(num)
                self.median = self.hi.pop()
            else:
                self.lo.push(num)
                self.median = self.lo.pop()
        else: # Odd case
            if num > self.median:
                self.hi.push(num)
                self.lo.push(self.median)
            else:
                self.lo.push(num)
                self.hi.push(self.median)
            self.median = (self.hi.peek() + self.lo.peek()) / 2
        self.len += 1
        

    def findMedian(self) -> float:
        return self.median
```

