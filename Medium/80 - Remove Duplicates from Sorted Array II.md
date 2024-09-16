# 80. Remove Duplicates from Sorted Array II
Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

### Code

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i, j = 0, 0
        currNbr, currCt = nums[0], 1
        for i in range(1, len(nums)):
            if nums[i] == currNbr:
                currCt += 1
                if currCt <= 2:
                    j += 1
            else:
                currCt = 1
                currNbr = nums[i]
                j += 1
            nums[j] = nums[i]
        return j + 1
```

Runtime: *49 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
