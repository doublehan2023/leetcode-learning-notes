# 14. Longest Common Prefix

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 14](https://leetcode.com/problems/longest-common-prefix/)

## Approach 1: Shrink a Candidate Prefix

Start with the first word as the candidate prefix. For each remaining word,
remove characters from the end of the candidate until the word starts with it.

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        prefix = strs[0]

        for word in strs:
            while not word.startswith(prefix):
                prefix = prefix[:-1]
                if not prefix:
                    return ""

        return prefix
```

- Time: `O(n * m)`
- Extra space: `O(1)`
- Strength: intuitive and concise.
- Tradeoff: repeated `startswith` calls and string slices create some extra
  work in practice.

## Approach 2: Compare Characters by Column

Use the first word as a reference. At each character index, check whether every
other word has the same character. Return as soon as a word ends or a mismatch
appears.

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        for i, char in enumerate(strs[0]):
            for word in strs[1:]:
                if i == len(word) or word[i] != char:
                    return strs[0][:i]

        return strs[0]
```

- Time: `O(n * m)`
- Extra space: `O(1)`
- Strength: directly stops at the first mismatching character; generally the
  cleanest choice for this problem.

## Approach 3: Sort, Then Compare the Extremes

After lexicographic sorting, only the first and last words need comparison:
any prefix shared by both is shared by every word between them.

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        strs.sort()

        first = strs[0]
        last = strs[-1]
        i = 0

        while i < len(first) and i < len(last) and first[i] == last[i]:
            i += 1

        return first[:i]
```

- Time: `O(n log n * m)` in the usual string-comparison analysis.
- Extra space: implementation-dependent for Python's sort.
- Tradeoff: mutates `strs` and performs unnecessary sorting, so it is not an
  optimization for a single prefix lookup.

## Comparison

| Approach | Time | Mutates input? | Best use |
| --- | --- | --- | --- |
| Shrink candidate prefix | `O(n * m)` | No | Simple, readable baseline |
| Compare by column | `O(n * m)` | No | Preferred solution |
| Sort and compare extremes | `O(n log n * m)` | Yes | When data is already sorted or sorting is needed for another reason |

`n` is the number of strings and `m` is the length of the relevant prefix (at
most the shortest string's length).
