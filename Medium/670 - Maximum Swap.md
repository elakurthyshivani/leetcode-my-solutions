# 670. Maximum Swap

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/maximum-swap/description](https://leetcode.com/problems/maximum-swap/description)

## My Solution 1

### Code

```python
class Solution:
    def maximumSwap(self, num: int) -> int:
        s = str(num)
        for i in range(len(s)):
            m = i
            for j in range(i + 1, len(s)):
                if s[j] >= s[m]:
                    m = j
            if m != i and s[m] != s[i]:
                s = s[ : i] + s[m] + s[i + 1 : m] + s[i] + s[m + 1: ]
                return int(s)
        return int(s)
```

Runtime: *32 ms*

### Time and Space Complexities

- Time complexity: $O(n^2)$
- Space complexity: $O(1)$

## My Solution 2

### Code

```python
class Solution:
    def maximumSwap(self, num: int) -> int:
        s = str(num) 
        lastIndex = {int(s[i]): i for i in range(len(s))}
        for i in range(len(s)):
            for j in range(9, int(s[i]), -1):
                if j in lastIndex and lastIndex[j] > i:
                    return int(s[ : i] + s[lastIndex[j]] + s[i + 1 : lastIndex[j]] + s[i] + s[lastIndex[j] + 1 : ])
        return num
```

Runtime: *38 ms*

### Time and Space Complexities

- Time complexity: $O(n * 10)$ = $O(n)$
- Space complexity: $O(n)$
