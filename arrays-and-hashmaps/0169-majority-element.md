# 169. Majority Element

- Category: Arrays & Hash Maps
- Difficulty: Easy
- Problem: [LeetCode 169](https://leetcode.com/problems/majority-element/)

## Problem

Given an integer array `nums`, return the majority element: the element that
appears more than `floor(n / 2)` times. A majority element is guaranteed to
exist.

## Your Naive Answer

Track each number's frequency in a hash map. Return a number as soon as its
frequency exceeds `n // 2`.

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        counter = {}
        threshold = len(nums) // 2

        for num in nums:
            counter[num] = counter.get(num, 0) + 1

            if counter[num] > threshold:
                return num
```

- Time: `O(n)`
- Extra space: `O(n)`

## Improved / Optimal Answer: Boyer-Moore Voting

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        candidate = 0
        count = 0

        for num in nums:
            if count == 0:
                candidate = num

            if num == candidate:
                count += 1
            else:
                count -= 1

        return candidate
```

### Mechanism

Treat matching occurrences of the current `candidate` as votes. A different
number cancels one vote. Whenever `count` reaches zero, every occurrence in
that stretch has been paired and cancelled, so the current number becomes the
new candidate.

The majority element appears more than half the time, so all of its
occurrences cannot be cancelled by other values. It must be the final
candidate.

- Time: `O(n)`
- Extra space: `O(1)`

## Key Takeaway

The hash-map solution is already linear time. Boyer-Moore preserves `O(n)`
time while optimizing the extra space from `O(n)` to `O(1)`. This is a voting
or cancellation algorithm, not a two-pointer algorithm.
