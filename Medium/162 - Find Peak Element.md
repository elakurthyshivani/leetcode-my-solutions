# 162. Find Peak Element

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/find-peak-element/description](https://leetcode.com/problems/find-peak-element/description)

## My Solution

### Code

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        s, e, m = 0, n - 1, 0
        while s <= e:
            m = (s + e) // 2

            if ((m - 1 > -1 and nums[m - 1] < nums[m]) or m == 0) and ((m + 1 < n and nums[m + 1] < nums[m]) or m == n - 1):
                return m
            elif m - 1 > -1 and nums[m - 1] >= nums[m]:
                e = m - 1
            else:
                s = m + 1
        return m
```

Runtime: *51 ms*


### Time and Space Complexities

- Time complexity: $O(log_2 n)$
- Space complexity: $O(1)$
