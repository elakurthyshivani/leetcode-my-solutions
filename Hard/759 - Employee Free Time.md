# 759. Employee Free Time

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/employee-free-time/description/](https://leetcode.com/problems/employee-free-time/description/)

## My Solution

### Code

```python
"""
# Definition for an Interval.
class Interval:
    def __init__(self, start: int = None, end: int = None):
        self.start = start
        self.end = end
"""

class Solution:
    def employeeFreeTime(self, schedule: '[[Interval]]') -> '[Interval]':
        def areOverlapping(interval1: Interval, interval2: Interval):
            if interval1.start <= interval2.start <= interval1.end:
                return True
            if interval1.start <= interval2.end <= interval1.end:
                return True
            if interval2.start <= interval1.start <= interval2.end:
                return True
            if interval2.start <= interval1.end <= interval2.end:
                return True
            return False
        
        def getCommonFreeTimes(freeTimes1: list[Interval], freeTimes2: list[Interval]):
            freeTimes = []
            i, j, n, m = 0, 0, len(freeTimes1), len(freeTimes2)
            while i < n and j < m:
                interval1 = freeTimes1[i]
                interval2 = freeTimes2[j]
                if areOverlapping(interval1, interval2):
                    if max(interval1.start, interval2.start) < min(interval1.end, interval2.end):
                        freeTimes.append(Interval(max(interval1.start, interval2.start), min(interval1.end, interval2.end)))
                    if interval1.end > interval2.end:
                        j += 1
                    elif interval1.end < interval2.end:
                        i += 1
                    else:
                        i += 1
                        j += 1
                else:
                    if interval1.end > interval2.end:
                        j += 1
                    elif interval1.end < interval2.end:
                        i += 1
                    else:
                        i += 1
                        j += 1
            return freeTimes

        def getEmployeeFreeTime(schedule: list[Interval]):
            nonlocal minTime, maxTime
            freeTime, n = [], len(schedule)
            for i in range(n + 1):
                if i == 0 and minTime < schedule[i].start:
                    freeTime.append(Interval(minTime, schedule[i].start))
                elif i == n and schedule[i - 1].end < maxTime:
                    freeTime.append(Interval(schedule[i - 1].end, maxTime))
                elif 0 < i < n and schedule[i - 1].end < schedule[i].start:
                    freeTime.append(Interval(schedule[i - 1].end, schedule[i].start))
            return freeTime

        def getMinMaxTime():
            nonlocal schedule
            maxTime, minTime = 0, math.inf
            for empSchedule in schedule:
                for interval in empSchedule:
                    if interval.end > maxTime:
                        maxTime = interval.end
                    if interval.start < minTime:
                        minTime = interval.start
            return (minTime, maxTime)

        minTime, maxTime = getMinMaxTime()
        freeTimes, prevEmpFreeTimes, i = [], [], 0

        for empSchedule in schedule:
            freeTimes = getEmployeeFreeTime(empSchedule)
            if i != 0:
                freeTimes = getCommonFreeTimes(prevEmpFreeTimes, freeTimes)
            prevEmpFreeTimes = freeTimes
            i += 1
        
        return freeTimes
```

Runtime: *267 ms*

### Time and Space Complexities

- Time complexity: $O(n * k)$, where $n$ is number of people and $k$ is the average number of intervals.
- Space complexity: $O(k)$
