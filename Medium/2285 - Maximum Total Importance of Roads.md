# 2285. Maximum Total Importance of Roads

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/maximum-total-importance-of-roads/description/](https://leetcode.com/problems/maximum-total-importance-of-roads/description/)

## My Solution 1

### Code

```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        degree = [0 for i in range(n)]
        order = list(range(n))
        importance = [0 for i in range(n)]
        totalImportance = 0

        for [u, v] in roads:
            degree[u] += 1
            degree[v] += 1
        order.sort(key = lambda x : degree[x])

        for i in range(len(order)):
            importance[order[i]] = i + 1

        for i in range(len(order)):
            totalImportance += importance[i] * degree[i]
        
        return totalImportance
```

Runtime: *1255 ms*

### Time and Space Complexities

- Time complexity: $O(n ^ 2)$
- Space complexity: $O(n)$

## My Solution 2

### Code

```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        degree = [0 for i in range(n)]
        totalImportance = 0

        for [u, v] in roads:
            degree[u] += 1
            degree[v] += 1
        degree.sort()

        for i in range(len(degree)):
            totalImportance += (i + 1) * degree[i]

        return totalImportance
```

Runtime: *1196 ms*

### Time and Space Complexities

- Time complexity: $O(n ^ 2)$
- Space complexity: $O(n)$
