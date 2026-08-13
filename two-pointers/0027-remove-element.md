# 27. Remove Element

- Category: Two Pointers
- Difficulty: Easy
- Problem: [LeetCode 27](https://leetcode.com/problems/remove-element/)

## Problem

Given an integer array `nums` and an integer `val`, remove every occurrence of
`val` in-place. Return the number of elements that remain. The first `k`
elements of `nums` must be the elements that do not equal `val`; their order
does not need to be preserved.

## Idea

Use a write pointer `k` to mark where the next kept value belongs. Scan through
the array once. When the current value is not `val`, copy it to `nums[k]` and
move `k` forward. Values equal to `val` are skipped.

## Python Solution

```python
class Solution:
    def removeElement(self, nums: list[int], val: int) -> int:
        k = 0

        for num in nums:
            if num != val:
                nums[k] = num
                k += 1

        return k
```

## Complexity

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

When removing values in-place, use a separate write pointer instead of deleting
elements while iterating.
