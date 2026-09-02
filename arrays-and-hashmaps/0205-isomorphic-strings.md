# 205. Isomorphic Strings

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 205](https://leetcode.com/problems/isomorphic-strings/)

## Approach: Forward Mapping and Used Targets

Track each character mapping from `s` to `t`. When a character from `s` has
already been seen, it must map to the same character in `t`. For a new source
character, ensure its target character has not already been claimed by a
different source character.

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        mapping = {}
        used = set()

        for char_s, char_t in zip(s, t):
            if char_s in mapping:
                if mapping[char_s] != char_t:
                    return False
            else:
                if char_t in used:
                    return False
                mapping[char_s] = char_t
                used.add(char_t)

        return True
```

- Time: `O(n)`.
- Extra space: `O(n)` in the general case.
- Note: If the character set is guaranteed to be fixed and small, arrays can
  reduce the extra space to `O(1)`, but the hash map and set are more flexible.
