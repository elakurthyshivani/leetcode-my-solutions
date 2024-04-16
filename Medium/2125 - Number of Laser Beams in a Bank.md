# 2125. Number of Laser Beams in a Bank

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/number-of-laser-beams-in-a-bank/description/](https://leetcode.com/problems/number-of-laser-beams-in-a-bank/description/)

### My Solution 1

#### Code

```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        counts = []
        for row in bank:
            rowCount = row.count("1")
            if rowCount > 0:
                counts.append(rowCount)
        if len(counts) < 2:
            return 0
        totalLasers = 0
        for i in range(1, len(counts)):
            totalLasers += counts[i] * counts[i - 1]
        return totalLasers
```

Runtime: *94 ms*

#### Time and Space Complexities

- Time complexity: $O(mn)$
- Space complexity: $O(m)$

### My Solution 2

```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        totalLasers = 0
        previousRowCount = 0
        for row in bank:
            rowCount = row.count("1")
            if rowCount > 0:
                totalLasers += rowCount * previousRowCount
                previousRowCount = rowCount
        return totalLasers
```

Runtime: *87 ms*

Link to my Solution: [https://leetcode.com/problems/number-of-laser-beams-in-a-bank/solutions/5032372/python-runtime-87-ms/](https://leetcode.com/problems/number-of-laser-beams-in-a-bank/solutions/5032372/python-runtime-87-ms/)

### Time and Space Complexities

- Time complexity: $O(mn)$
- Space complexity: $O(1)$
