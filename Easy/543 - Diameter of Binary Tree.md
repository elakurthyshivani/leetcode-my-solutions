# 543. Diameter of Binary Tree

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/diameter-of-binary-tree/description/](https://leetcode.com/problems/diameter-of-binary-tree/description/)

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
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        diameter = 0

        def traverse(curr : Optional[TreeNode]):
            if curr == None:
                return 0
            
            x = traverse(curr.left)
            y = traverse(curr.right)

            nonlocal diameter
            diameter = max(diameter, x + y)

            return max(x, y) + 1

        traverse(root)
        return diameter
```

Runtime: *41 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
