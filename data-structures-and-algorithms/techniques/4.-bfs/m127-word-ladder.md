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
Intuition: Build a graph on words that only differ by 1 letter, and then use BFS rooted on beginWord to search for endWord, which will give us a list of the shortest possible length.
{% endhint %}

* O\(n \* k\) to construct a graph, with N words and K letters
* O\(n\) or O\(n^2\) to do BFS. Worse case would be a complete graph, and to check all possibilities.

