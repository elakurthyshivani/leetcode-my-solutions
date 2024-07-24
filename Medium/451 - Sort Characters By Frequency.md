# 451. Sort Characters By Frequency

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/sort-characters-by-frequency/](https://leetcode.com/problems/sort-characters-by-frequency/)

### Solution

```python
class Solution:
    def frequencySort(self, s: str) -> str:
        counts = self.getCountsTuple(s)
        counts.sort(key = lambda x : x[0], reverse = True)
        # print(counts)
        return self.countsTupleToString(counts)

    def getCountsTuple(self, s: str) -> list[tuple[int, int]]:
        counts = {}
        for character in s:
            if character in counts:
                counts[character] += 1
            else:
                counts[character] = 1
        countsTuple = []
        for character, count in counts.items():
            countsTuple.append((count, character))
        return countsTuple

    def countsTupleToString(self, countsTuple : list[tuple[int, int]]):
        output = ""
        for (count, character) in countsTuple:
            output += (count * character)
        return output
```

Runtime: *58 ms*

### Time and Space Complexities

- Time complexity: $O(n(log n))$
- Space complexity: $O(n)$
