# M139: Word Break





## Solutions

### Solution 1: Recursive

```python
class Solution1:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if wordDict == []:
            return False
        if s == "":
            return True
        possible = False
        for word in wordDict:
            if s.startswith(word):
                if self.wordBreak(s[len(word):], wordDict):
                    possible = True
        return possible
```

Stack overflow \):

### Solution 2: Iterative + Memoization

{% hint style="info" %}
Intuition: Begin from position 0 and check iteratively. At position i, if `s[:i]` ends with a word, then we check if `i-w` could be segmented. We then store that truth value at `i`. Keep going until we've reached the final position, and check.
{% endhint %}

```python
class Solution2:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if wordDict == []:
            return False
        n = len(s)
        dp = [False for _ in range(n+1)]
        dp[0] = True
        for i in range(1, n+1):
            for word in wordDict:
                if s[:i].endswith(word) and dp[i-len(word)] == True:
                    dp[i] = True
        return dp[n]
```

