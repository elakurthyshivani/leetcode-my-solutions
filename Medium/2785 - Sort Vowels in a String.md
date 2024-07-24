# 2785. Sort Vowels in a String

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/sort-vowels-in-a-string/description/](https://leetcode.com/problems/sort-vowels-in-a-string/description/)

### My Solution

Grab the vowels in the same order into a separate list. Sort this list. Traverse the string and replace the vowel with the vowels from the sorted list in the same order.

#### Code

```python
class Solution:
    def sortVowels(self, s: str) -> str:
        vowels = []
        for character in s:
            if character in "aeiouAEIOU":
                vowels.append(character)
        
        n = len(vowels)
        if n == 0:
            return s
        else:
            vowels.sort()
            i, output = 0, []
            for character in s:
                if character in "aeiouAEIOU":
                    output.append(vowels[i])
                    i += 1
                else:
                    output.append(character)
            return "".join(output)
```

Runtime: *103 ms*

#### Time and Space Complexities

- Time complexity: $O(n(log n))$
- Space complexity: $O(n)$
