# 1043. Partition Array for Maximum Sum

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/partition-array-for-maximum-sum/description/](https://leetcode.com/problems/partition-array-for-maximum-sum/description/)

### Solution

```python
class Solution:
    def maxSumAfterPartitioning(self, arr: List[int], k: int) -> int:
        n = len(arr)
        if n == 1:
            return arr[0]
        
        dp = [0 for i in range(n)]
        for i in range(n - 1, -1, -1):
            maxInSubArray = 0
            maxSum = 0
            for j in range(i, min(n, i + k)):
                maxInSubArray = max(maxInSubArray, arr[j])
                maxSum = max(maxSum, maxInSubArray * (j - i + 1) + (dp[j + 1] if j + 1 < n else 0))
            dp[i] = maxSum
        return dp[0]
```

Runtime: *273 ms*

Link to my Solution: [https://leetcode.com/problems/partition-array-for-maximum-sum/solutions/5525200/python-beats-81-53-of-users/](https://leetcode.com/problems/partition-array-for-maximum-sum/solutions/5525200/python-beats-81-53-of-users/)

### Time and Space Complexities

- Time complexity: $O(nk)$
- Space complexity: $O(n)$
