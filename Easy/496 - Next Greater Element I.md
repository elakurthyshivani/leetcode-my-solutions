# 496. Next Greater Element I

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/next-greater-element-i/description/](https://leetcode.com/problems/next-greater-element-i/description/)

### My Solution

#### Approach

We need a stack and a hash table (initialize all values to `-1`) to solve this problem in $O(len(nums(2))$. We add values from `nums2` to the stack until we find a value `x` that is greater than the previous element. We pop all the values from the stack that are smaller than `x`. We continue this process until we reach the end of `nums2` and the stack is empty.

#### Code

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        stack, nextt=[nums2[0]], [-1]*(max(nums2)+1)
        for i in range(1, len(nums2)):
            while len(stack)>0 and nums2[i]>stack[-1]:
                nextt[stack.pop()]=nums2[i]
            else:
                stack.append(nums2[i])
        out=[]
        for num in nums1:
            out.append(nextt[num])
        return out
```

Runtime: *48 ms*

Link to my Solution: [https://leetcode.com/problems/next-greater-element-i/solutions/2515779/python-runtime-44-ms-faster-than-9870](https://leetcode.com/problems/next-greater-element-i/solutions/2515779/python-runtime-44-ms-faster-than-9870)

### Time and Space Complexities

- Time complexity: $O(n + m)$, where $n$ is the length of `nums2` and $m$ is the length of `nums1`
  - The first `for` loop iterates $n$ times and the second `for` loop iterates $m$ times.

- Space complexity: $O(n + n + 1) = O(n)$
  - The maximum number of values that `stack` will hold is $n$.
  - The length of `nextt` array is $n + 1$.
