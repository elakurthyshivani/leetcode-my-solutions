# 1630. Arithmetic Subarrays

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/arithmetic-subarrays/](https://leetcode.com/problems/arithmetic-subarrays/)

### My Solution

```python
class Solution:
    def checkArithmeticSubarrays(self, nums: List[int], l: List[int], r: List[int]) -> List[bool]:
        output = []
        for i in range(len(l)):
            arr = nums[l[i]: r[i] + 1]
            if len(arr) <= 2:
                output.append(True)
                continue
            arr.sort()
            diff = arr[1] - arr[0]
            for j in range(2, len(arr)):
                if arr[j] - arr[j - 1] != diff:
                    output.append(False)
                    break
            else:
                output.append(True)
        return output
```

Runtime: *147 ms*
