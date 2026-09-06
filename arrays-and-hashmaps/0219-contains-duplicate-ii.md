# 219. Contains Duplicate II

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 219](https://leetcode.com/problems/contains-duplicate-ii/)

Store each value's most recent index. When a value appears again at index
`i`, compare `i` with its previous index. If their distance is at most `k`, a
valid pair exists. Update the stored index after every iteration so it always
represents the closest previous occurrence.

## Approach 1: Explicit Lookup

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        last_index = {}

        for i in range(len(nums)):
            if nums[i] in last_index:
                prev = last_index[nums[i]]

                if i - prev <= k:
                    return True

            last_index[nums[i]] = i

        return False
```

- Time: `O(n)`.
- Extra space: `O(n)` in the worst case for the stored distinct values.

## Approach 2: `enumerate` and `get`

This equivalent version uses `enumerate` for the current index and value, and
retrieves the previous index with one dictionary lookup. `prev is not None`
is necessary because `0` is a valid index.

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        last_index = {}

        for i, num in enumerate(nums):
            prev = last_index.get(num)

            if prev is not None and i - prev <= k:
                return True

            last_index[num] = i

        return False
```

- Time: `O(n)`.
- Extra space: `O(n)` in the worst case.
