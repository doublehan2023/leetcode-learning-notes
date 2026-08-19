# 21. Merge Two Sorted Lists

- Category: Linked Lists
- Difficulty: Easy
- Problem: [LeetCode 21](https://leetcode.com/problems/merge-two-sorted-lists/)

## Problem

Merge two sorted linked lists by reusing their nodes, then return the head of
the combined sorted list.

## Your Answer

Use `dummy` as a fixed placeholder and `tail` to track the last node in the
merged list. While both lists have a node, attach the node with the smaller
value and advance its list pointer. When one list is empty, attach the
remaining list.

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        tail = dummy

        # A linked list variable is true when it points to a node
        while list1 and list2:
            if list1.val <= list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next

            tail = tail.next

        tail.next = list1 if list1 else list2

        return dummy.next
```

## Improved / Optimal Answer

Your solution is already optimal: it visits each node once and reuses the
original nodes. There is no algorithmic improvement needed.

One optional readability change is to use a temporary `chosen` variable before
attaching it, but the current version is shorter and clear. Keeping `<=` means
equal values are taken from `list1` first, which is a sensible choice.

## Complexity

- Time: `O(m + n)`
- Extra space: `O(1)`

## Key Takeaway

Use a dummy head to avoid special handling for the first node, and keep a tail
pointer so each chosen node can be appended in constant time.
