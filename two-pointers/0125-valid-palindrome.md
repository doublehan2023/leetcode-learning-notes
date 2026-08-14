# 125. Valid Palindrome

- Category: Two Pointers
- Difficulty: Easy
- Problem: [LeetCode 125](https://leetcode.com/problems/valid-palindrome/)

## Problem

Return whether a string is a palindrome after ignoring non-alphanumeric
characters and letter case.

## Your Answer

First build a lowercase string containing only alphanumeric characters. Then
compare its characters from both ends with two pointers.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        cleaned = ""
        for char in s:
            if char.isalnum():
                cleaned += char.lower()

        left = 0
        right = len(cleaned) - 1

        while left < right:
            if cleaned[left] != cleaned[right]:
                return False

            left += 1
            right -= 1

        return True
```

- Time: `O(n)`
- Extra space: `O(n)` for `cleaned`

## Improved / Optimal Answer

Keep the two pointers in the original string. Before comparing, move each
pointer past non-alphanumeric characters. This avoids constructing a separate
string.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        left = 0
        right = len(s) - 1

        while left < right:
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1

            if s[left].lower() != s[right].lower():
                return False

            left += 1
            right -= 1

        return True
```

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

Two pointers can filter a string in place: skip irrelevant characters before
each comparison instead of creating a cleaned copy first.
