# 317. Shortest Distance from All Buildings

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/shortest-distance-from-all-buildings/description/](https://leetcode.com/problems/shortest-distance-from-all-buildings/description/)

## My Solution 1

### Code

```python
class Solution:
    def shortestDistance(self, grid: List[List[int]]) -> int:
        n, m = len(grid), len(grid[0])

        def getBuildings():
            nonlocal n, m
            buildings = []
            for i in range(n):
                for j in range(m):
                    if grid[i][j] == 1:
                        buildings.append((i, j))
            return buildings

        def markCellAsVisited(i : int, j : int, distance : int, cells : list):
            nonlocal currEmptyVal, distances
            if grid[i][j] == currEmptyVal:
                grid[i][j] -= 1
                distances[i][j] += distance
                cells.append((i, j, distance))
            elif grid[i][j] > currEmptyVal:
                grid[i][j] = currEmptyVal - 1
                distances[i][j] += math.inf

        def visitNeighboringCells(i : int, j : int, distance : int):
            nonlocal currEmptyVal, distances, n, m
            cells = []
            if i - 1 >= 0 and grid[i - 1][j] < 1:
                markCellAsVisited(i - 1, j, distance, cells)
            if i + 1 < n and grid[i + 1][j] < 1:
                markCellAsVisited(i + 1, j, distance, cells)
            if j - 1 >= 0 and grid[i][j - 1] < 1:
                markCellAsVisited(i, j - 1, distance, cells)
            if j + 1 < m and grid[i][j + 1] < 1:
                markCellAsVisited(i, j + 1, distance, cells)
            return cells
        
        def getShortestTotalTravel():
            nonlocal distances, n, m, currEmptyVal
            shortest = math.inf
            for i in range(n):
                for j in range(m):
                    if distances[i][j] != 0 and grid[i][j] == currEmptyVal and distances[i][j] < shortest:
                        shortest = distances[i][j]
            return shortest

        buildings = getBuildings()
        distances = [[0 for j in range(m)] for i in range(n)]
        b, currEmptyVal = len(buildings), 0

        for building in buildings:
            stack = visitNeighboringCells(building[0], building[1], 1)
            if len(stack) == 0:
                return -1
            while len(stack) > 0:
                currCell = stack.pop(0)
                stack.extend(visitNeighboringCells(currCell[0], currCell[1], currCell[2] + 1))
            currEmptyVal -= 1
        
        shortest = getShortestTotalTravel()
        return shortest if shortest != math.inf else -1
```

Runtime: *1833 ms*

Link to my Solution: [https://leetcode.com/problems/shortest-distance-from-all-buildings/solutions/5879461/python-memory-beats-89-84-of-users-runtime-beats-76-93-of-users/](https://leetcode.com/problems/shortest-distance-from-all-buildings/solutions/5879461/python-memory-beats-89-84-of-users-runtime-beats-76-93-of-users/)

### Time and Space Complexities

- Time complexity: $O(n^2 * m^2)$, where $n$ is the number of rows and $m$ is the number of columns.
  - Time complexity for `getBuildings()` and `getShortestTotalTravel()` is $O(nm)$.
  - The number of buildings could be anywhere between $0$ to $n * m$ (all cells in the grid could be buildings). So the `for` loop iterating the buildings takes $n * m$ time.
  - Using BFS, the neighboring cells are visited inside the `buildings` for loop. Visiting these cells take $n * m$ time.
  - Total time complexity = $O(nm) + O(n * m * n * m) + O(nm)$ = $O(n^2 * m^2)$
- Space complexity: $O(nm)$
  - The number of buildings could be anywhere between $0$ to $n * m$ (all cells in the grid could be buildings). The space required for `buildings` is $O(nm)$.
  - The `distances` takes $O(nm)$ space.
  - The `stack` would hold at most $(nm) cells.
 
## My Solution 2

Without using the `buildings` list.

### Code

```python
class Solution:
    def shortestDistance(self, grid: List[List[int]]) -> int:
        n, m = len(grid), len(grid[0])

        def markCellAsVisited(i : int, j : int, distance : int, cells : list):
            nonlocal currEmptyVal, distances
            if grid[i][j] == currEmptyVal:
                grid[i][j] -= 1
                distances[i][j] += distance
                cells.append((i, j, distance))
            elif grid[i][j] > currEmptyVal:
                grid[i][j] = currEmptyVal - 1
                distances[i][j] += math.inf

        def visitNeighboringCells(i : int, j : int, distance : int):
            nonlocal currEmptyVal, distances, n, m
            cells = []
            if i - 1 >= 0 and grid[i - 1][j] < 1:
                markCellAsVisited(i - 1, j, distance, cells)
            if i + 1 < n and grid[i + 1][j] < 1:
                markCellAsVisited(i + 1, j, distance, cells)
            if j - 1 >= 0 and grid[i][j - 1] < 1:
                markCellAsVisited(i, j - 1, distance, cells)
            if j + 1 < m and grid[i][j + 1] < 1:
                markCellAsVisited(i, j + 1, distance, cells)
            return cells
        
        def getShortestTotalTravel():
            nonlocal distances, n, m, currEmptyVal
            shortest = math.inf
            for i in range(n):
                for j in range(m):
                    if distances[i][j] != 0 and grid[i][j] == currEmptyVal and distances[i][j] < shortest:
                        shortest = distances[i][j]
            return shortest

        distances = [[0 for j in range(m)] for i in range(n)]
        currEmptyVal = 0

        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    stack = visitNeighboringCells(i, j, 1)
                    if len(stack) == 0:
                        return -1
                    while len(stack) > 0:
                        currCell = stack.pop(0)
                        stack.extend(visitNeighboringCells(currCell[0], currCell[1], currCell[2] + 1))
                    currEmptyVal -= 1
        
        shortest = getShortestTotalTravel()
        return shortest if shortest != math.inf else -1
```

Runtime: *1831 ms*

### Time and Space Complexities

- Time complexity: $O(n^2 * m^2)$
- Space complexity: $O(nm)$
