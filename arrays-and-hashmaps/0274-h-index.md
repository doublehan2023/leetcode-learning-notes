# 274. H-Index

- Category: Arrays & Hash Maps
- Difficulty: Medium
- Problem: [LeetCode 274](https://leetcode.com/problems/h-index/)

## Problem

Given `citations`, where each value is the citation count of one paper,
return the largest `h` such that at least `h` papers have at least `h`
citations.

## Your Initial Answer: Test Every h

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        h = len(citations)

        while h >= 0:
            count = 0
            for citation in citations:
                if citation >= h:
                    count += 1

            if count >= h:
                return h

            h -= 1
```

### Idea

Try possible h-index values from the number of papers down to zero. For each
candidate `h`, count papers with at least `h` citations. The first valid
candidate is the maximum because the scan is descending.

- Time: `O(n^2)`
- Extra space: `O(1)`

## Improved Answer: Citation Buckets

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        n = len(citations)
        buckets = [0] * (n + 1)

        for citation in citations:
            if citation < n:
                buckets[citation] += 1
            else:
                buckets[n] += 1

        papers = 0
        for h in range(n, -1, -1):
            papers += buckets[h]
            if papers >= h:
                return h
```

### Idea

The h-index cannot exceed the number of papers, `n`, so every citation count
greater than or equal to `n` can be grouped in bucket `n`. Each bucket stores
how many papers have that citation count. Scan from `n` down to zero while
accumulating papers in the visited buckets; these are the papers with at
least the current `h` citations. The first `h` where `papers >= h` is the
answer.

- Time: `O(n)`
- Extra space: `O(n)`

## Key Takeaway: Frequency Buckets

When a value has a useful bounded range, an array can act as a set of
frequency buckets: index `i` records the number of occurrences of value `i`.
Here, citation counts greater than `n` are capped at `n` because no h-index
can exceed the total number of papers. A reverse cumulative scan then turns
the exact-count buckets into counts of papers with at least each threshold.

### Example

For `citations = [3, 0, 6, 1, 5]`, `n = 5`. The frequency buckets are:

```text
index (citations):  0  1  2  3  4  5+
papers:             1  1  0  1  0  2
```

The `5+` bucket contains both `5` and `6`. Scanning backward gives 2 papers
with at least 5 citations, 2 with at least 4, and 3 with at least 3. Since 3
papers have at least 3 citations, the h-index is `3`.
