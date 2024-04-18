# 2482. Difference Between Ones and Zeros in Row and Column

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column/description/](https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column/description/)

### My Solution

```python
class Solution:
    def onesMinusZeros(self, grid: List[List[int]]) -> List[List[int]]:
        n, m = len(grid), len(grid[0])
        output = [row[:] for row in grid]
        # Rows:
        # Count 0's and 1's for each row
        for i in range(n):
            count0, count1 = 0, 0
            for j in range(m):
                if grid[i][j] == 0:
                    count0 += 1
                else:
                    count1 += 1
            # Update all the columns in each row with the number of 0's and 1's
            # in respective row
            for j in range(m):
                output[i][j] = count1 - count0
        
        # Columns:
        # Count 0's and 1's for each column
        for j in range(m):
            count0, count1 = 0, 0
            for i in range(n):
                if grid[i][j] == 0:
                    count0 += 1
                else:
                    count1 += 1
            # Update all the rows in each row with the number of 0's and 1's
            # in the respective column
            for i in range(n):
                output[i][j] += (count1 - count0)
        
        return output
```

Runtime: *1237 ms*

Link to my Solution: [https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column/solutions/5042283/python-memory-beats-74-28-of-users/](https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column/solutions/5042283/python-memory-beats-74-28-of-users/)

### Time and Space Complexities

- Time complexity: $O(nm)$
- Space complexity: $O(nm)$
