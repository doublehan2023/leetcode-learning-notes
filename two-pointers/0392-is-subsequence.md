# 392. Is Subsequence

- Category: Two Pointers
- Difficulty: Easy
- Problem: [LeetCode 392](https://leetcode.com/problems/is-subsequence/)

## Problem

Return `True` when the characters of `s` appear in `t` in the same relative
order. Characters in `t` may be skipped.

For example, `"ace"` is a subsequence of `"abcde"`, but `"aec"` is not:
although all three characters occur in `t`, `e` appears after `c`.

## Answer

Scan `t` from left to right while `i` tracks the next character needed from
`s`. Advance `i` only when the current character matches. If every character
in `s` is matched, `s` is a subsequence.

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        if len(s) > len(t):
            return False

        i = 0
        for char in t:
            if i < len(s) and s[i] == char:
                i += 1

        return i == len(s)
```

- Time: `O(len(t))`
- Extra space: `O(1)`

## Key Takeaway

Checking only whether every character in `s` exists somewhere in `t` is not
enough: their order must also match. The LeetCode memory percentile may vary
because it includes Python runtime and test-harness overhead; this algorithm
still has optimal `O(1)` auxiliary space.
