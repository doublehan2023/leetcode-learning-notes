# 134. Gas Station

- Category: Greedy
- Difficulty: Medium
- Problem: [LeetCode 134](https://leetcode.com/problems/gas-station/)
- Status: Needs review

## Your Answer

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        net = 0
        tank = 0
        start = 0

        for i in range(len(gas)):
            net += gas[i] - cost[i]
            tank += gas[i] - cost[i]

            if tank < 0:
                tank = 0
                start = i + 1

        return -1 if net < 0 else start
```

## Why This Is Greedy

For each station, `gas[i] - cost[i]` is its net contribution to the tank.
Maintain two running values during a single scan:

- `net` is the contribution across the entire circuit. If it is negative, the
  total available gas cannot pay the total travel cost, so no answer exists.
- `tank` is the contribution from the current candidate `start` through the
  current station. If it becomes negative at `i`, the current start and every
  station up through `i` can be discarded. The next possible candidate is
  `i + 1`, and the local tank resets to `0`.

The reset is safe because the tank did not become negative before this first
failure within the current segment. Any later starting station in that segment
would have even less accumulated gas available by the time it reaches `i`.

For `gas = [1, 2, 3, 4, 5]` and `cost = [3, 4, 5, 1, 2]`, the net values are
`[-2, -2, -2, 3, 3]`. The scan discards starts `0`, `1`, and `2`, then keeps
start `3`. The total net contribution is `0`, so starting at `3` completes
the circuit.

## Complexity

- Time: `O(n)`.
- Extra space: `O(1)`.

## Key Takeaway

Reset based on a negative running `tank`, not simply a negative individual
station contribution. A station can have a negative net value while the car
still has enough fuel to continue. A final `net >= 0` means a complete circuit
exists; the problem guarantees that this valid starting index is unique.
