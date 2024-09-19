# 17. Letter Combinations of a Phone Number

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

## My Solution 1 (Total Iterative)

### Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if len(digits) == 0:
            return []
        
        ALPHABETS = {
            "2": ["a", "b", "c"],
            "3": ["d", "e", "f"],
            "4": ["g", "h", "i"],
            "5": ["j", "k", "l"],
            "6": ["m", "n", "o"],
            "7": ["p", "q", "r", "s"],
            "8": ["t", "u", "v"],
            "9": ["w", "x", "y", "z"]
        }
        prev = [""]
        curr = []
        for digit in digits:
            for prevCharacter in prev:
                for character in ALPHABETS[digit]:
                    curr.append(prevCharacter + character)
            prev = curr
            curr = []
        
        return prev
```

Runtime: *37 ms*


### Time and Space Complexities

- Time complexity: $O(4^n * n)$
- Space complexity: $O(4^n)$

## My Solution 2 (Backtracking)

### Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if len(digits) == 0:
            return []
        
        ALPHABETS = {
            "2": ["a", "b", "c"],
            "3": ["d", "e", "f"],
            "4": ["g", "h", "i"],
            "5": ["j", "k", "l"],
            "6": ["m", "n", "o"],
            "7": ["p", "q", "r", "s"],
            "8": ["t", "u", "v"],
            "9": ["w", "x", "y", "z"]
        }
        output = []

        def backtrack(index : int, character : str):
            if len(digits) == index:
                output.append(character)
                return
            
            for alphabet in ALPHABETS[digits[index]]:
                backtrack(index + 1, character + alphabet)

        backtrack(0, "")

        return output
```

Runtime: *27 ms*

*Link to my solution*: [https://leetcode.com/problems/letter-combinations-of-a-phone-number/solutions/5806502/python-backtrack-runtime-beats-93-95/](https://leetcode.com/problems/letter-combinations-of-a-phone-number/solutions/5806502/python-backtrack-runtime-beats-93-95/)

### Time and Space Complexities

- Time complexity: $O(4^n * n)$
- Space complexity: $O(n)$
