# 1689. Partitioning Into Minimum Number Of Deci-Binary Numbers

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/description/](https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/description/)

### My Solution

Minimum number of deci-binary numbers needed to they sum up to `n` is the maximum digit present in `n`.

For example, let `n = "82734"`. Solving this backwards, we can start by subtracting `11111` from `n`. This gives us `71623`. Repeating this again, we get `60512`. Now we can continue to subtract using `10111`. This gives us `50401`. `n` becomes `0` when the largest digit in `n` becomes `0`. Therefore, the answer is the max digit in `n`.

### Code 1

```python
class Solution:
    def minPartitions(self, n: str) -> int:
        output = "0"
        for digit in n:
            if digit > output:
                output = digit
        return int(output)
```

Runtime: *67 ms*

### Code 2

```python
class Solution:
    def minPartitions(self, n: str) -> int:
        return int(max(list(str(n))))
```

Runtime: *74 ms*

### Time and Space Complexities

- Time complexity: $O(n)$ 

- Space complexity: $O(1)$
