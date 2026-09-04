# 242. Valid Anagram

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 242](https://leetcode.com/problems/valid-anagram/)

## Approach: Fixed-Size Frequency Array

Because the input contains lowercase English letters, use a list of 26 counts.
Count every letter in `s`, then consume the matching count while walking through
`t`. If a letter's count is already zero, `t` contains that letter too many
times and cannot be an anagram.

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        freq = [0] * 26

        for char in s:
            freq[ord(char) - ord("a")] += 1

        for char in t:
            index = ord(char) - ord("a")
            if freq[index] <= 0:
                return False
            freq[index] -= 1

        return True
```

- Time: `O(n)`.
- Extra space: `O(1)`, since the frequency list always contains 26 entries.
- Note: This uses the lowercase-English-letter constraint. For arbitrary
  characters, use a dictionary of character counts instead.
