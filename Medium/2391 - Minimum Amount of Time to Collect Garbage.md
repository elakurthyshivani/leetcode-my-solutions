# 2391. Minimum Amount of Time to Collect Garbage

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage/description/](https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage/description/)

### My Solution

#### Approach
![image](https://github.com/elakurthyshivani/leetcode-my-solutions/assets/95426935/8b517f11-03c9-4169-8f00-4abf3855013f)

#### Code

```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        # `travel` - Cummulative sum
        for i in range(1, len(travel)):
            travel[i] += travel[i - 1]
        
        # Last index for each type of garbage truck
        last = {"G": 0, "P": 0, "M": 0}

        # Time taken in total
        time = 0

        for i in range(len(garbage)):
            # Time taken to pick garbage only
            time += len(garbage[i])
            for g in garbage[i]:
                last[g] = i
        
        # Time taken for a truck to the last location needed
        for index in last.values():
            if index != 0:
                time += travel[index - 1]

        return time
```

Runtime: *735 ms*

#### Time and Space Complexities

- Time complexity: $O(NumberOfGarbageUnits * NumberOfHouses)$

- Space complexity: $O(1)$
