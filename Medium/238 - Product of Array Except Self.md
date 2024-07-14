# 238. Product of Array Except Self

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/product-of-array-except-self/description/](https://leetcode.com/problems/product-of-array-except-self/description/)

### Solution 1

#### Code

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prod, zeroCount = 1, 0
        for num in nums:
            if num != 0:
                prod *= num
            else:
                zeroCount += 1
        
        if zeroCount == len(nums):
            return nums
        elif zeroCount > 1:
            return [0] * len(nums)
        elif zeroCount == 1:
            prods = []
            for num in nums:
                if num != 0:
                    prods.append(0)
                else:
                    prods.append(prod)
            return prods
        else:
            prods = []
            for num in nums:
                prods.append(prod // num)
            return prods
```

Runtime: *255 ms*

Link to my Solution: [https://leetcode.com/problems/product-of-array-except-self/solutions/5477499/python-runtime-beats-93-59/](https://leetcode.com/problems/product-of-array-except-self/solutions/5477499/python-runtime-beats-93-59/)

#### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$

### Solution 2

#### Code

```python
from math import prod
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        output, right=[1], 1
        for i in range(1, len(nums)):
            output.append(output[-1]*nums[i-1])
        for i in range(len(nums)-1, -1, -1):
            output[i]*=right
            right*=nums[i]
        return output
```

Runtime: *234ms*

#### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
