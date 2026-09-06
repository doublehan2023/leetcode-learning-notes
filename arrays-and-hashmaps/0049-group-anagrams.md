# 49. Group Anagrams

- Category: Arrays & Hash Maps
- Difficulty: Medium
- Problem: [LeetCode 49](https://leetcode.com/problems/group-anagrams/)

Anagrams contain the same letters with the same frequencies. For every word,
build a 26-item frequency list, convert it to a tuple so it can be used as a
dictionary key, and append the word to that key's group.

## Approach 1: Letter-Frequency Tuple

```python
from collections import defaultdict
from typing import List


class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)

        for word in strs:
            counts = [0] * 26

            for char in word:
                counts[ord(char) - ord("a")] += 1

            key = tuple(counts)
            groups[key].append(word)

        return list(groups.values())
```

- Time: `O(n * m)`, where `n` is the number of words and `m` is their
  average length.
- Extra space: `O(n * m)` for the returned groups and dictionary keys.
- Why a tuple: lists are mutable and cannot be dictionary keys; a tuple is
  immutable and preserves all 26 character counts.

## Concepts Clarified

### Tuple as a Dictionary Key

A tuple is an immutable sequence. Build counts in a mutable list, then convert
that list with `tuple(counts)` before using it as a dictionary key. Anagrams
produce identical count tuples, so they map to the same group.

```python
counts = [0] * 26
# Count the letters in one word.
key = tuple(counts)
```

The check must use `ord(char)`, with parentheses, because `ord` is a function.
Square brackets such as `ord[char]` try to index into the function and raise a
`TypeError`.

### `defaultdict(list)`

`defaultdict(list)` behaves like a dictionary, but automatically creates an
empty list for a missing key. This makes grouping concise:

```python
groups = defaultdict(list)
groups[key].append(word)
```

On the first occurrence of `key`, the empty list is created before `word` is
appended. Later anagrams reuse that same list. Finally,
`list(groups.values())` returns all of the groups.

### Mapping a Letter to Its Count Slot

`ord` returns a character's numeric Unicode value. For lowercase English
letters, `ord(char) - ord("a")` maps `"a"` through `"z"` to indices `0`
through `25`, respectively.

## Alternative: Sorted-Word Key

Sorting each word also creates a shared key for anagrams, but it takes
`O(m log m)` per word. The frequency-tuple approach is faster for the
lowercase English-letter constraint.
