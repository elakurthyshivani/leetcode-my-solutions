# 726. Number of Atoms

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/number-of-atoms/description/](https://leetcode.com/problems/number-of-atoms/description/)

### My Solution

```python
class Solution:
    def countOfAtoms(self, formula: str) -> str:
        # If the formula length is 1, just return it.
        if len(formula)==1:
            return formula
        
        # Create an empty stack.
        stack, i=[], 0

        while i<len(formula):
            # If we find an upper case letter.
            if formula[i].isupper():
                element=formula[i]
                j=i+1
                # If the element symbol not yet finished (lower case letters).
                while j<len(formula) and formula[j].islower():
                    element+=formula[j]
                    j+=1
                # Get the number.
                num=''
                while j<len(formula) and formula[j].isdigit():
                    num+=formula[j]
                    j+=1
                # If no number is mentioned, it is 1.
                num=1 if num=='' else int(num)

                # If top of the stack is a dictionary, add this element to it.
                if len(stack)>0 and type(stack[-1])==type({}):
                    if element in stack[-1]:
                        stack[-1][element]+=num
                    else:
                        stack[-1][element]=num
                # Or else, create a new one.
                else:
                    stack.append({element: num})
                # Update i.
                i=j

            # If we find an open bracket.
            elif formula[i]=='(':
                # Add this to the stack.
                stack.append('(')
                i+=1
            
            elif formula[i]==')':
                j=i+1
                # Get the number.
                num=''
                while j<len(formula) and formula[j].isdigit():
                    num+=formula[j]
                    j+=1
                # If no number is mentioned, it is 1.
                num=1 if num=='' else int(num)
                # Get the top of the stack.
                top=stack.pop(-1)
                # Multiply by num.
                for k in top:
                    top[k]*=num
                
                # If top of the stack is (. Since the formula is valid, this is always true.
                if len(stack)>0 and stack[-1]=='(':
                    # Remove this from the stack.
                    stack.pop(-1)
                    # Check if the stack is empty or the top is not a dictionary.
                    if len(stack)==0 or type(stack[-1])!=type({}):
                        # Add this dictionary to the stack.
                        stack.append(top)
                    else:
                        # Merge this dictionary with the top dictionary of the stack.
                        main=stack[-1]
                        for i in top:
                            if i in main:
                                main[i]+=top[i]
                            else:
                                main[i]=top[i]
                i=j       

        # Stack now consists of only 1 element. Convert it into output.
        output=''
        for i in sorted(stack[-1].keys()):
            if stack[-1][i]>1:
                output+=f"{i}{stack[-1][i]}"
            else:
                output+=i
        # Return output
        return output
```
Runtime: *34 ms*

Link to my Solution: [https://leetcode.com/problems/number-of-atoms/solutions/3838571/python-runtime-34ms-beats-9702-of-users](https://leetcode.com/problems/number-of-atoms/solutions/3838571/python-runtime-34ms-beats-9702-of-users)

### Time and Space Complexities

- Time complexity: $O(n*26) = O(n)$

- Space complexity: $O(n)$
