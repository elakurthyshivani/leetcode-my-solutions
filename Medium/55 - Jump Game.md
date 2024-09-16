# 55. Jump Game

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/jump-game/description/](https://leetcode.com/problems/jump-game/description/)

## Solution 1

### Code

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        maxIndex = 0
        for i in range(0, len(nums)):
            if i > maxIndex:
                return False
            maxIndex = max(maxIndex, i + nums[i])
        return True
```

Runtime: *376 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$

## Solution 2

### Code

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        output = [False for i in range(n)]
        output[-1] = True
        for i in range(n - 2, -1, -1):
            for j in range(i + 1, min(i + 1 + nums[i], n), 1):
                if output[j]:
                    output[i] = True
                    break
        return output[0]
```

Runtime: *1967 ms*

### Time and Space Complexities

- Time complexity: $O(n^2)$
- Space complexity: $O(n)$
