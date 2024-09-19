# 1249. Minimum Remove to Make Valid Parentheses

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description)

## My Solution

One way to solve this problem is to use a stack and push the index everytime `(` is encountered and pop the top everytime `)` is encountered. 
If the stack is empty when a `)` is encountered, then add it to another set, this is an extra parentheses that can be removed from the string. 
After looping through all the characters in the string, if there are any indices in the stack, the parentheses at these indices can also be removed from the string.

### Code

```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack : list[int] = []
        removeAtIndices : set[int] = set()

        for index, character in enumerate(s):
            if character == "(":
                stack.append(index)
            elif character == ")":
                if len(stack) > 0:
                    stack.pop()
                else:
                    removeAtIndices.add(index)
        removeAtIndices.update(stack)

        output = ''
        for index in range(len(s)):
            if index not in removeAtIndices:
                output += s[index]

        return output
```

Runtime: *78 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
