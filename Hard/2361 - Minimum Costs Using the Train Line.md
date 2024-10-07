# 2361. Minimum Costs Using the Train Line

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/minimum-costs-using-the-train-line/description/](https://leetcode.com/problems/minimum-costs-using-the-train-line/description/)

## My Solution 1

### Code

```python
class Solution:
    def minimumCosts(self, regular: List[int], express: List[int], expressCost: int) -> List[int]:
        n = len(regular)
        regularCosts = [0] + [math.inf for i in range(n)]
        expressCosts = [expressCost] + [math.inf for i in range(n)]
        
        for i in range(n):
            regularCosts[i + 1] = min(regularCosts[i + 1], regularCosts[i] + regular[i])
            expressCosts[i + 1] = min(expressCosts[i + 1], regularCosts[i + 1] + expressCost, expressCosts[i] + express[i])
            regularCosts[i + 1] = min(expressCosts[i + 1], regularCosts[i + 1])
        
        return regularCosts[1 : ]
```

Runtime: *1002 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
 
## My Solution 2

### Code

```python
class Solution:
    def minimumCosts(self, regular: List[int], express: List[int], expressCost: int) -> List[int]:
        n = len(regular)
        regularCosts = [0] + [math.inf for i in range(n)]
        expressCosts = expressCost
        
        for i in range(n):
            regularCosts[i + 1] = min(regularCosts[i + 1], regularCosts[i] + regular[i])
            expressCosts = min(regularCosts[i + 1] + expressCost, expressCosts + express[i])
            regularCosts[i + 1] = min(expressCosts, regularCosts[i + 1])
        
        return regularCosts[1 : ]
```

Runtime: *939 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
