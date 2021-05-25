# M127: Word Ladder

{% hint style="info" %}
Problem: [https://leetcode.com/problems/word-ladder/](https://leetcode.com/problems/word-ladder/) \[SOLUTION COPIED\]
{% endhint %}

### The Problem

Given two words \(_beginWord_ and _endWord_\), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord_ to _endWord_, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that _beginWord_ is _not_ a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume _beginWord_ and _endWord_ are non-empty and are not the same.

### Solution

{% hint style="info" %}
hIntuition: Traverse word list by searching for words that defer from current word by 1 letter. Using a BFS guarantees that the shortest path will be reported first. Generate a dictionary of letters in each position in a given word list to speed up the search through all possible words.
{% endhint %}

```python
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        idxs = collections.defaultdict(set)
        words = set(wordList)
        
        if endWord not in words:
            return 0
        # Store all possible letters in each position
        for word in words:
            for i, c in enumerate(word):
                idxs[i].add(c)
        
        # BFS
        q = collections.deque()
        q.append((beginWord, 1))
        
        seen = set()
        seen.add(beginWord)
        
        while q:
            w, s = q.popleft()
            if w == endWord:
                return s
            for i in range(len(w)):
                for c in idxs[i]:
                    new_word = w[:i] + c + w[i+1:]
                    if new_word in words and new_word not in seen:
                        q.append((new_word, s+1))
                        seen.add(new_word)
        return 0
```

