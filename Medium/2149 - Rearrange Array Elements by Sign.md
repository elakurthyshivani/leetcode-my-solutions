# 2149. Rearrange Array Elements by Sign

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/rearrange-array-elements-by-sign/description/](https://leetcode.com/problems/rearrange-array-elements-by-sign/description/)

### My Solution

```python
class Solution:
    def rearrangeArray(self, nums: List[int]) -> List[int]:
        n = len(nums)
        output = [0] * n
        i, j = 0, 1
        for num in nums:
            if num > 0:
                output[i] = num
                i += 2
            else:
                output[j] = num
                j += 2
        return output
```

Runtime: *958 ms*

Link to my Solution: [https://leetcode.com/problems/rearrange-array-elements-by-sign/solutions/5051476/python-runtime-beats-99-40-of-users/](https://leetcode.com/problems/rearrange-array-elements-by-sign/solutions/5051476/python-runtime-beats-99-40-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$ 

- Space complexity: $O(1)$
