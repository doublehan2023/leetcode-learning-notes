# 28. Find the Index of the First Occurrence in a String

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

## Approach 1: Compare a Slice at Every Valid Start

Check every position where `needle` can still fit inside `haystack`. Return the
first index whose substring equals `needle`.

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i:i + len(needle)] == needle:
                return i

        return -1
```

- Time: `O((h - n + 1) * n)`, commonly written as `O(h * n)`.
- Extra space: `O(n)` in Python, because each slice makes a new string of up
  to `n` characters.
- Strength: short, readable, and easy to verify.

## Approach 2: Compare Characters Without Slicing

At each valid starting index, compare the two strings one character at a time.
If every character in `needle` matches, return that starting index.

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(len(haystack) - len(needle) + 1):
            j = 0

            while j < len(needle) and haystack[i + j] == needle[j]:
                j += 1

            if j == len(needle):
                return i

        return -1
```

- Time: `O((h - n + 1) * n)`, commonly written as `O(h * n)`.
- Extra space: `O(1)`.
- Strength: avoids allocating substring copies.
- Tradeoff: more verbose and easier to make an indexing mistake.

## Comparison

| Approach | Time | Extra space in Python | Tradeoff |
| --- | --- | --- | --- |
| Slice and compare | `O(h * n)` | `O(n)` | Most concise, but allocates temporary substrings |
| Character-by-character | `O(h * n)` | `O(1)` | More code, but avoids slice allocation |

`h` is the length of `haystack` and `n` is the length of `needle`.

For this problem, the slice version is usually the best default because it is
very readable. Prefer the character-by-character version when you specifically
want constant auxiliary space or need to demonstrate the underlying search.
