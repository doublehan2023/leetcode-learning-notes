# 58. Length of Last Word

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 58](https://leetcode.com/problems/length-of-last-word/)

## Your Answer

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        i = len(s) - 1

        while s[i] == ' ':
            i -= 1
        
        length = 0
        while i >= 0 and s[i] != ' ':
            length += 1
            i -= 1
        
        return length
```

### Idea

Start at the end of the string. First skip trailing spaces, then count
non-space characters until reaching the preceding space or the start of the
string.

- Time: `O(n)`
- Extra space: `O(1)`
