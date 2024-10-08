# 2136. Earliest Possible Day of Full Bloom

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/earliest-possible-day-of-full-bloom/description/](https://leetcode.com/problems/earliest-possible-day-of-full-bloom/description/)

## My Solution

### Code

```python
class Solution:
    def earliestFullBloom(self, plantTime: List[int], growTime: List[int]) -> int:
        plantTime = list(enumerate(plantTime))
        plantTime.sort(key = lambda x: growTime[x[0]], reverse = True)
        for i in range(1, len(plantTime)):
            plantTime[i] = (plantTime[i][0], plantTime[i][1] + plantTime[i - 1][1])
        earliestBloom = 0
        for index, days in plantTime:
            earliestBloom = max(earliestBloom, days + growTime[index])
        return earliestBloom
```

Runtime: *1354 ms*

### Time and Space Complexities

- Time complexity: $O(n log(n)$
- Space complexity: $O(n)$
