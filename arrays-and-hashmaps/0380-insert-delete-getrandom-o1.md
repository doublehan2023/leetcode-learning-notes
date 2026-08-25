# 380. Insert Delete GetRandom O(1)

- Category: Arrays & Hash Maps
- Difficulty: Medium
- Problem: [LeetCode 380](https://leetcode.com/problems/insert-delete-getrandom-o1/)

## Problem

Design a set supporting insertion, deletion, and returning a uniformly random
element, all in average `O(1)` time.

## Your Answer: Array + Hash Map

```python
import random


class RandomizedSet:
    def __init__(self):
        self.lst = []
        self.map = {}

    def insert(self, val: int) -> bool:
        if val in self.map:
            return False

        self.lst.append(val)
        self.map[val] = len(self.lst) - 1
        return True

    def remove(self, val: int) -> bool:
        if val not in self.map:
            return False

        idx = self.map[val]
        self.lst[idx] = self.lst[-1]
        self.map[self.lst[-1]] = idx
        self.lst.pop()
        del self.map[val]
        return True

    def getRandom(self) -> int:
        return random.choice(self.lst)
```

### Idea

Store values in a list so `random.choice` can select each index with equal
probability. Store each value's current list index in a hash map for average
`O(1)` existence checks and lookups.

To remove a value without shifting later list elements, overwrite its position
with the final value, update that moved value's index in the map, then pop the
last list position. List order is not important.

- Time: `O(1)` average per operation
- Extra space: `O(n)`

## Python Hash Map Basics

Python's hash map is a `dict`. These operations are average `O(1)`:

```python
positions = {}

# Add a key-value pair, or overwrite the value for an existing key.
positions[10] = 0

# Look up a value when the key is known to exist.
index = positions[10]

# Check whether a key exists.
if 10 in positions:
    pass

# Safely read a key with a fallback value when it may be absent.
index = positions.get(10, -1)

# Delete a key that is known to exist.
del positions[10]

# Safely remove a key that may be absent; returns the removed value or None.
index = positions.pop(10, None)
```

## Key Takeaway

When order does not matter, deleting an array element can be made `O(1)` by
swapping it with the last element and popping. A value-to-index map supplies
the index needed for that swap.
