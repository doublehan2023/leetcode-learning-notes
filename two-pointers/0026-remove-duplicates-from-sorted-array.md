# 26. Remove Duplicates from Sorted Array

- Category: Two Pointers
- Difficulty: Easy
- Problem: [LeetCode 26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

## Python Solution

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        
        k = 0
        for i in range(1, len(nums)):
            if nums[k] != nums[i]:
                k += 1
                nums[k] = nums[i]
            
        return k+1
```
