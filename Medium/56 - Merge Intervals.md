# 156. Merge Intervals

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/merge-intervals/description/](https://leetcode.com/problems/merge-intervals/description/)

### My Solution

Sort the intervals by start time and check if two consecutive intervals overlap by checking the end time of the first interval with the start time of the second interval. If they overlap, then update the first interval with the maximum value of the end time of these 2 intervals and continue the process. If two consecutive intervals do not overlap, process to the next set of consecutive intervals.

#### Code

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key = lambda x : x[0])
        i, n = 1, len(intervals)
        while i < n:
            if intervals[i - 1][1] >= intervals[i][0]:
                intervals[i - 1][1] = intervals[i][1] if intervals[i][1] > intervals[i - 1][1] else intervals[i - 1][1]
                intervals.pop(i)
                n -= 1
            else:
                i += 1
        return intervals
```

Runtime: *127 ms*

#### Time and Space Complexities

- Time complexity: $O(n(log n))$
- Space complexity: $O(1)$
