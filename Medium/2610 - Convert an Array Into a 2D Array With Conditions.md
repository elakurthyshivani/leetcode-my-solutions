# 2610. Convert an Array Into a 2D Array With Conditions

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions/description/](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions/description/)

### My Solution

```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        counts = {}
        for num in nums:
            if num in counts:
                counts[num] += 1
            else:
                counts[num] = 1
        
        numRows = max(list(counts.values()))
        nums2D = [[] for i in range(numRows)]
        for num, count in counts.items():
            for i in range(count):
                nums2D[i].append(num)
        
        return nums2D
```

Runtime: *54 ms*

### Time and Space Complexities

- Time complexity: $O(n)$ 

- Space complexity: $O(n)$
