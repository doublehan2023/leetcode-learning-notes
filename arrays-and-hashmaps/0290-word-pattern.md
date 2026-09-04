# 290. Word Pattern

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 290](https://leetcode.com/problems/word-pattern/)

## Approach 1: Forward Mapping and Used Words

Split `s` into words and first verify that their count equals the number of
characters in `pattern`. Map each pattern character to its word. A set of
already-used words enforces the reverse part of the bijection: a new pattern
character cannot claim a word assigned to another character.

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        words = s.split()

        if len(pattern) != len(words):
            return False

        mapping = {}
        used = set()

        for char, word in zip(pattern, words):
            if char in mapping:
                if mapping[char] != word:
                    return False
            else:
                if word in used:
                    return False
                mapping[char] = word
                used.add(word)

        return True
```

## Approach 2: Two-Way Mappings

Maintain both `character -> word` and `word -> character` dictionaries. For
every pair, validate any existing mapping in each direction. Once both checks
pass, writing both entries is safe—even when they repeat the same mapping.

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        words = s.split()

        if len(pattern) != len(words):
            return False

        char_to_word = {}
        word_to_char = {}

        for char, word in zip(pattern, words):
            if char in char_to_word and char_to_word[char] != word:
                return False
            if word in word_to_char and word_to_char[word] != char:
                return False

            char_to_word[char] = word
            word_to_char[word] = char

        return True
```

- Time: `O(n)`, where `n` is the number of words.
- Extra space: `O(n)`.
- Note: Both approaches are optimal. The first uses one dictionary and one set;
  the second makes both directions of the bijection explicit.
