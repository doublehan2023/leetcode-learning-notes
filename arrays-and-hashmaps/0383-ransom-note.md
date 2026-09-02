# 383. Ransom Note

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 383](https://leetcode.com/problems/ransom-note/)

## Approach 1: Frequency Hash Map

Count the letters available in `magazine`. Then spend one count for every
letter required by `ransomNote`. A negative count means the magazine does not
contain enough of that letter.

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        counts = {}

        for char in magazine:
            counts[char] = counts.get(char, 0) + 1

        for char in ransomNote:
            counts[char] = counts.get(char, 0) - 1

            if counts[char] < 0:
                return False

        return True
```

- Time: `O(m + n)`, where `m` and `n` are the lengths of `magazine` and
  `ransomNote`.
- Extra space: `O(k)`, where `k` is the number of distinct letters.

## Approach 2: Fixed-Size Frequency Array

Because the problem contains lowercase English letters, replace the hash map
with an array of 26 counters. This keeps the same linear runtime while using
constant extra space.

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        if len(ransomNote) > len(magazine):
            return False

        counts = [0] * 26

        for char in magazine:
            counts[ord(char) - ord("a")] += 1

        for char in ransomNote:
            index = ord(char) - ord("a")
            counts[index] -= 1

            if counts[index] < 0:
                return False

        return True
```

- Time: `O(m + n)`.
- Extra space: `O(1)` because the array always contains 26 counters.
- Tradeoff: this uses less memory, while the hash map is more flexible and
  works naturally when the character set is not limited to lowercase letters.
