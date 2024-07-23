# 103. Binary Tree Zigzag Level Order Traversal

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/)

### My Solution

One way to solve this problem is to traverse through the tree by updating the level and saving the node values in an `output` list of lists. Later, the alternative lists in this `output` can be reversed.

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        output = []
        self.traversal(root, 0, output)
        for i in range(1, len(output), 2):
            output[i] = output[i][ : : -1]
        return output

    def traversal(self, root: Optional[TreeNode], depth: int, output: List[List[int]]) -> None:
        if root == None:
            return
        
        if depth == len(output):
            output.append([root.val])
        else:
            output[depth].append(root.val)

        self.traversal(root.left, depth + 1, output)
        self.traversal(root.right, depth + 1, output)
```

Runtime: *38 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
