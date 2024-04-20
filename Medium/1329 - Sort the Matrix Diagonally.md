# 1329. Sort the Matrix Diagonally

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/sort-the-matrix-diagonally/description/](https://leetcode.com/problems/sort-the-matrix-diagonally/description/)

### My Solution

```python
class Solution:
    def diagonalSort(self, mat: List[List[int]]) -> List[List[int]]:
        n, m = len(mat), len(mat[0])
        start = [(i, 0) for i in range(n)] + [(0, j) for j in range(m)]
        for si, sj in start:
            diag, i, j = [], si, sj
            while i < n and j < m:
                diag.append(mat[i][j])
                i += 1
                j += 1
            diag.sort()
            i, j = si, sj
            while i < n and j < m:
                mat[i][j] = diag.pop(0)
                i += 1
                j += 1
        return mat
```

Runtime: *66 ms*

Link to my Solution: [https://leetcode.com/problems/sort-the-matrix-diagonally/solutions/5051537/python-runtime-beats-85-42-of-users-memory-beats-84-68-of-users/](https://leetcode.com/problems/sort-the-matrix-diagonally/solutions/5051537/python-runtime-beats-85-42-of-users-memory-beats-84-68-of-users/)

### Time and Space Complexities

- Time complexity: $O(nm)$

- Space complexity: $O(n + m)$
