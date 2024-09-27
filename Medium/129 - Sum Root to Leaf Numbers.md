# 129. Sum Root to Leaf Numbers

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/sum-root-to-leaf-numbers/description](https://leetcode.com/problems/sum-root-to-leaf-numbers/description)

## My Solution

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        sumNums = 0
        
        def traverse(curr: Optional[TreeNode], num: str):
            if curr == None:
                return
            
            if curr.left == None and curr.right == None:
                nonlocal sumNums
                sumNums += int(f"{num}{curr.val}")
                return
            
            traverse(curr.left, f"{num}{curr.val}")
            traverse(curr.right, f"{num}{curr.val}")
        
        traverse(root, "")
        return sumNums
```

Runtime: *38 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(h)$, $h$ is the height of the binary tree.
