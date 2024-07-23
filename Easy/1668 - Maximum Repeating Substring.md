# 1668. Maximum Repeating Substring

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/maximum-repeating-substring/description/](https://leetcode.com/problems/maximum-repeating-substring/description/)

### My Solution (Sliding Window)

#### Code

```python
class Solution:
    def maxRepeating(self, sequence: str, word: str) -> int:
        seqLength, wordLength = len(sequence), len(word)
        if wordLength == seqLength:
            return 1 if sequence == word else 0
        
        i, j, maxRepetitions = 0, 0, 0
        while i < seqLength:
            j, k, repetitions = 0, 0, 0
            while i + j < seqLength and sequence[i + j] == word[k]:
                j += 1
                k += 1
                if k == wordLength:
                    k = 0
                    repetitions += 1
            if maxRepetitions < repetitions:
                maxRepetitions = repetitions
            i = i + 1
        
        return maxRepetitions
```

Runtime: *44 ms*

#### Time and Space Complexities

- Time complexity: $O(nm)$, where $n$ is the length of `sequence` and $m$ is the length of `word`
  - The first `for` loop iterates $n$ times and the second `for` loop iterates a finite no. of $m$ times.

- Space complexity: $O(1)$.

### Another Solution

#### Code

```python
class Solution:
    def maxRepeating(self, sequence: str, word: str) -> int:
        count = 0
        while word * count in sequence:
            count += 1
        return count - 1
```

Runtime: *35 ms*
