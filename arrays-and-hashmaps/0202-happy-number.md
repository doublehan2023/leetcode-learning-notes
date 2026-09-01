# 202. Happy Number

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 202](https://leetcode.com/problems/happy-number/)

## Approach 1: Track Seen Numbers

Repeatedly replace the current number with the sum of the squares of its
digits. If the sequence reaches `1`, the number is happy. If a full number is
seen again, the sequence has entered a cycle.

```python
class Solution:
    def sumSquares(self, num: int) -> int:
        square = 0

        while num > 0:
            digit = num % 10
            square += digit * digit
            num = num // 10

        return square

    def isHappy(self, n: int) -> bool:
        seen = set()
        target = n

        while target not in seen and target != 1:
            seen.add(target)
            target = self.sumSquares(target)

        return target == 1
```

- Time: `O(k)`, where `k` is the number of generated values before reaching
  `1` or repeating.
- Extra space: `O(k)` for the set of seen values.

## Approach 2: Slow and Fast Pointers

Use Floyd's cycle detection instead of storing prior values. The slow pointer
applies the transformation once per iteration, while the fast pointer applies
it twice. They meet if the sequence is in a cycle; the fast pointer reaches
`1` for a happy number.

```python
class Solution:
    def sumSquares(self, num: int) -> int:
        square = 0

        while num > 0:
            digit = num % 10
            square += digit * digit
            num = num // 10

        return square

    def isHappy(self, n: int) -> bool:
        slow = n
        fast = n

        while True:
            slow = self.sumSquares(slow)
            fast = self.sumSquares(self.sumSquares(fast))

            if fast == 1:
                return True
            if slow == fast:
                return False
```

- Time: `O(k)`.
- Extra space: `O(1)`.
- Tradeoff: saves memory, but the set-based approach is often easier to
  understand and implement.
