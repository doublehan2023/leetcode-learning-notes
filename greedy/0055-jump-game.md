# 55. Jump Game

- Category: Greedy
- Difficulty: Medium
- Problem: [LeetCode 55](https://leetcode.com/problems/jump-game/)

## Problem

Starting at index `0`, each value in `nums` gives the maximum number of
positions you may jump forward. Return whether it is possible to reach the
last index.

A jump length is a maximum, not an exact requirement. If a value is larger
than the remaining array, you can choose a shorter jump that lands on the last
index.

## Your Answer

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        last_index = len(nums) - 1
        farthest = 0

        for i in range(len(nums)):
            if i > farthest:
                return False

            farthest = max(farthest, i + nums[i])

            if farthest >= last_index:
                return True

        return True
```

## Why This Is Greedy

Instead of choosing and exploring every possible jump path, keep one piece of
state: the farthest index reachable from any position seen so far.

- If `i > farthest`, index `i` cannot be reached, so no later index can be
  reached either.
- Otherwise, standing at `i` can extend the reachable range to `i + nums[i]`.
- Once `farthest >= last_index`, the last index is reachable.

For `[2, 3, 1, 1, 4]`, index `0` reaches through index `2`; index `1` then
extends that range through index `4`, so the answer is `True`.

For `[3, 2, 1, 0, 4]`, the farthest reachable index remains `3`. Index `4`
is unreachable, so the answer is `False`.

## Complexity

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

When each reachable position can expand a shared forward boundary, track that
boundary rather than branching into every possible path.
