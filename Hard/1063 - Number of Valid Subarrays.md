# 1063. Number of Valid Subarrays

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/number-of-valid-subarrays/description/](https://leetcode.com/problems/number-of-valid-subarrays/description/)

## My Solution 1

### Code

```python
class Solution:
    def validSubarrays(self, nums: List[int]) -> int:
        count, n = 0, len(nums)
        for i in range(n):
            count += 1
            for j in range(i + 1, n):
                if nums[i] <= nums[j]:
                    count += 1
                else:
                    break
        return count
```

Runtime: *3019 ms*

### Time and Space Complexities

- Time complexity: $O(n^2)$
- Space complexity: $O(1)$
 
## My Solution 2

Using monotonic stack.

### Code

```python
class Solution:
    def validSubarrays(self, nums: List[int]) -> int:
        monotonicStack, count, n = [], 0, len(nums)
        for i in range(n):
            # print(i, monotonicStack)
            while len(monotonicStack) > 0 and nums[i] < monotonicStack[-1][0]:
                _, index = monotonicStack.pop()
                count += (i - index)
            monotonicStack.append((nums[i], i))
        # print(count, monotonicStack)
        while len(monotonicStack) > 0:
            _, i = monotonicStack.pop()
            count += (n - i)
        return count
```

Runtime: *359 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
