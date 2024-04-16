# 6. Zigzag Conversion

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/zigzag-conversion/description/](https://leetcode.com/problems/zigzag-conversion/description/)

### My Solution

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        if numRows == len(s):
            return s
        rows = [[] for i in range(numRows)]
        i, increment = 0, True
        for char in s:
            if i == numRows:
                increment = False
                i -= 2
            elif i == -1:
                increment = True
                i += 2

            if increment:
                rows[i].append(char)
                i += 1
            else:
                rows[i].append(char)
                i -= 1
        return "".join(["".join(row) for row in rows])
```

Runtime: *55 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
