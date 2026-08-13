# 88. Merge Sorted Array

- Category: Two Pointers
- Difficulty: Easy
- Problem: [LeetCode 88](https://leetcode.com/problems/merge-sorted-array/)

## Problem

`nums1` has length `m + n`: its first `m` elements are sorted values and its
last `n` positions are empty. Merge the `n` sorted values in `nums2` into
`nums1` in non-decreasing order.

## Your Answer

Merge from right to left so writing into `nums1` never overwrites a value that
still needs to be compared.

- `i = m - 1`: last valid value in `nums1`
- `j = n - 1`: last value in `nums2`
- `k = m + n - 1`: last position in `nums1`

```python
class Solution:
    def merge(self, nums1: list[int], m: int,
              nums2: list[int], n: int) -> None:
        i = m - 1
        j = n - 1
        k = m + n - 1

        while j >= 0:
            if i >= 0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1

            k -= 1
```

## Improved / Optimal Answer

This is already the optimal approach. Start at the end because `nums1` has
empty space there. At each step, place the larger remaining value at `k`.

The loop only needs `while j >= 0`:

- If `nums2` is exhausted, the remaining values in `nums1` are already in the
  correct positions.
- If `nums1` is exhausted (`i < 0`), copy the remaining values from `nums2`.
- This naturally handles `m = 0` and `n = 0`; no separate edge-case code is
  needed.

## Complexity

- Time: `O(m + n)`
- Extra space: `O(1)`

## Key Takeaway

When an array has unused space at the end, fill it backwards to avoid
overwriting values you have not processed yet.
