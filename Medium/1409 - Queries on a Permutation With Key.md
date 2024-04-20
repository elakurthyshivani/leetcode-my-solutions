# 1409. Queries on a Permutation With Key

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/queries-on-a-permutation-with-key/description/](https://leetcode.com/problems/queries-on-a-permutation-with-key/description/)

### My Solution

```python
class Solution:
    def processQueries(self, queries: List[int], m: int) -> List[int]:
        arr = [i for i in range(1, m + 1)]
        output = []
        for query in queries:
            index = arr.index(query)
            output.append(index)
            arr.insert(0, arr.pop(index))
        return output
```

Runtime: *44 ms*

Link to my Solution: [https://leetcode.com/problems/queries-on-a-permutation-with-key/solutions/5051501/python-runtime-beats-95-01-of-users-memory-beats-94-72-of-users/](https://leetcode.com/problems/queries-on-a-permutation-with-key/solutions/5051501/python-runtime-beats-95-01-of-users-memory-beats-94-72-of-users/)

### Time and Space Complexities

- Time complexity: $O(mn)$

- Space complexity: $O(n)$
