# 13. Roman to Integer

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 13](https://leetcode.com/problems/roman-to-integer/)

## Your Answer

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        values = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }

        total = 0
        for i in range(len(s)):
            if i < len(s)-1 and values[s[i]]<values[s[i+1]]:
                total -= values[s[i]]
            else:
                total += values[s[i]]
        return total
```

### Idea

Store each Roman symbol and its value in a hash map. Scan the string from left
to right: subtract a value when it is smaller than the symbol immediately to
its right; otherwise, add it.

- Time: `O(n)`
- Extra space: `O(1)`
