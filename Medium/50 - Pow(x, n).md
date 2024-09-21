# 50. Pow(x, n)

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/powx-n/description/](https://leetcode.com/problems/powx-n/description/)

## My Solution 1

### Code

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if x == 0 or x == 1:
            return x
        if n == 0:
            return 1
        if n == 1:
            return x
        if n == -1:
            return 1 / x

        if n % 2 == 0:
            return self.myPow(x * x, n // 2)
        else:
            return x * self.myPow(x * x, n // 2)
```

Runtime: *38 ms*

### Time and Space Complexities

- Time complexity: $O(log(n))$
- Space complexity: $O(1)$

## My Solution 2

### Code

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if x == 0 or x == 1:
            return x
        if n == 0:
            return 1
        if n == 1:
            return x
        if n == -1:
            return 1 / x

        powers = {1 : x, -1: 1 / x}

        def _pow(x: float, n: int):
            if n in powers:
                return powers[n]
            y = _pow(x, n // 2)
            z = _pow(x, n // 2) if n % 2 == 0 else _pow(x, n // 2 + 1)
            if n not in powers:
                powers[n] = y * z
            return powers[n]
        
        return _pow(x, n)
```

Runtime: *37 ms*

### Time and Space Complexities

- Time complexity: $O(log(n))$
- Space complexity: $O(log(n))$
