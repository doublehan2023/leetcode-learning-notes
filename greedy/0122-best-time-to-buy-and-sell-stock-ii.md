# 122. Best Time to Buy and Sell Stock II

- Category: Greedy
- Difficulty: Medium
- Problem: [LeetCode 122](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

## Problem

Given daily stock prices, find the greatest profit possible when any number of
transactions is allowed, while holding at most one share at a time.

## Your Answer

Each positive change from one day to the next is profit worth taking. A price
drop is skipped, because we do not want to hold through it.

```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        profit = 0

        for i in range(1, len(prices)):
            if prices[i] > prices[i - 1]:
                profit += prices[i] - prices[i - 1]

        return profit
```

For example, `[1, 5, 3, 6]` earns the gains from `1 → 5` and `3 → 6`, while
skipping the `5 → 3` loss.

## Why This Is Greedy

Taking every positive adjacent gain is always safe: a longer upward run has
the same total profit whether it is one transaction or several consecutive
ones. For example, `1 → 2 → 4 → 7` earns `(2 - 1) + (4 - 2) + (7 - 4)`, which
equals `7 - 1`.

## Comparison with #121: Best Time to Buy and Sell Stock

| | #121 | #122 |
|---|---|---|
| Allowed transactions | At most one | Any number |
| Goal | Find one best buy/sell pair | Capture every upward movement |
| Key state | Lowest price seen so far | Positive change from yesterday |
| Example `[1, 5, 3, 6]` | Buy at `1`, sell at `6`: profit `5` | `1 → 5` plus `3 → 6`: profit `7` |

In #121, selling at `5` would use up the only transaction, so you must compare
that choice against waiting to sell at `6`. In #122, selling at `5` and buying
again at `3` is allowed, so each separate rise can be collected.

## Complexity

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

When unlimited non-overlapping transactions are allowed, sum every positive
day-to-day price increase.
