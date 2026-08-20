# 189. Rotate Array

- Category: Two Pointers
- Difficulty: Medium
- Problem: [LeetCode 189](https://leetcode.com/problems/rotate-array/)

## Problem

Rotate `nums` to the right by `k` steps, modifying the original array in place.

## Initial Answer

Move the last `k` elements to the front, followed by the remaining elements.
Reduce `k` first so rotations larger than the array length are handled.

```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k %= len(nums)  # Handle k larger than len(nums).
        nums[:] = nums[-k:] + nums[:-k]
```

`nums[:] = ...` replaces the contents of the original list, satisfying the
in-place requirement. The expression on the right creates a temporary list.

## Improved / Optimal Answer

Reverse the entire array, then reverse its first `k` elements and the
remaining elements. Reversing swaps values with a left and right pointer, so
the solution does not need another list.

```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k %= len(nums)

        def reverse(left: int, right: int) -> None:
            while left < right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1

        reverse(0, len(nums) - 1)
        reverse(0, k - 1)
        reverse(k, len(nums) - 1)
```

## Complexity

### Initial Answer

- Time: `O(n)`
- Extra space: `O(n)`

### Improved / Optimal Answer

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

For an in-place rotation with constant extra space, use three reversals and
two pointers.
