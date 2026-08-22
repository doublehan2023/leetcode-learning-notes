# 45. Jump Game II

- Category: Greedy
- Difficulty: Medium
- Problem: [LeetCode 45](https://leetcode.com/problems/jump-game-ii/)
- Status: Needs review

## Problem

Starting at index `0`, each value in `nums` gives the maximum number of
positions you may jump forward. Return the minimum number of jumps needed to
reach the last index. The problem guarantees that the last index is reachable.

## Your Answer

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        jumps = 0
        farthest = 0
        current_end = 0

        for i in range(len(nums) - 1):
            farthest = max(farthest, i + nums[i])

            if i == current_end:
                jumps += 1
                current_end = farthest

        return jumps
```

## Why This Is Greedy

Each range from the previous boundary through `current_end` represents all
positions reachable using the current number of jumps. While scanning that
range, `farthest` tracks the best endpoint available with one additional jump.

When the scan reaches `current_end`, every option using the current number of
jumps has been considered. Commit to the next jump by incrementing `jumps` and
setting `current_end` to `farthest`.

For `[2, 3, 1, 1, 4]`:

```text
After 1 jump: indices 1 through 2 are reachable.
After scanning that range: index 4 is reachable in 2 jumps.
```

The loop stops before the last index. Once that index is reached, no additional
jump is needed; processing it would add one extra jump. This also makes a
single-element array return `0`.

## Complexity

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

Treat all positions reachable with the same number of jumps as one range.
Increase the jump count only after scanning the entire current range.
