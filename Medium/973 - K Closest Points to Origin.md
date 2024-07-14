# 1973. K Closest Points to Origin

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/k-closest-points-to-origin/description/](https://leetcode.com/problems/k-closest-points-to-origin/description/)

### My Solution 1

```python
import math

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        points.sort(key = lambda point : math.sqrt(point[0] * point[0] + point[1] * point[1]))
        return points[:k]
```

Runtime: *567 ms*

### My Solution 2

```python
import math

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        self.mergeSort(points, 0, len(points) - 1)
        return points[ : k]

    def mergeSort(self, points : List[List[int]], s : int, e : int) -> None:
        if s >= e:
            return;

        m = (s + e) // 2

        self.mergeSort(points, s, m)
        self.mergeSort(points, m + 1, e)
        self.merge(points, s, m, e)
    
    def merge(self, points : List[List[int]], s : int, m : int, e : int) -> None:
        i, j, k, temp = s, m + 1, s, points[:]

        while i <= m and j <= e:
            if math.sqrt(temp[i][0] * temp[i][0] + temp[i][1] * temp[i][1]) < math.sqrt(temp[j][0] * temp[j][0] + temp[j][1] * temp[j][1]):
                points[k] = temp[i]
                i += 1
            else:
                points[k] = temp[j]
                j += 1
            k += 1
        
        while i <= m:
            points[k] = temp[i]
            i += 1
            k += 1
        
        while j <= e:
            points[k] = temp [j]
            j += 1
            k += 1
```

Runtime: *3015 ms*
