# 1. Two Sum

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 1](https://leetcode.com/problems/two-sum/)

## Naive Approach: Check Every Pair

For each number, check every number after it. If the pair adds up to `target`,
return their indices. Starting the inner loop at `i + 1` avoids using the same
element twice and avoids checking the same pair in reverse order.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(0, len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return i, j
```

- Time: `O(n^2)`
- Extra space: `O(1)`
- Strength: direct and easy to reason about.
- Tradeoff: it may examine nearly every pair, so it becomes slow for large
  inputs.

## Hash Map Approach: Look Up the Needed Complement

Store each previously seen number and its index. For the current number,
calculate the complement needed to reach `target`; if it is already in the
map, return the earlier index and the current index.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}

        for i in range(len(nums)):
            needed = target - nums[i]

            if needed in seen:
                return [seen[needed], i]

            seen[nums[i]] = i
```

- Time: `O(n)` on average.
- Extra space: `O(n)`.
- Key detail: check `needed` before adding the current number so one element
  cannot be used twice.
