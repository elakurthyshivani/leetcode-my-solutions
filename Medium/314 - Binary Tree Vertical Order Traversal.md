# 314. Binary Tree Vertical Order Traversal

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/](https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/)

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
    def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if root == None:
            return None

        startIndex, endIndex, maxDepth = 0, 0, 0
        tree = {}

        def traverse(node: Optional[TreeNode], depth: int, index: int):
            if node == None:
                return
            
            nonlocal tree, startIndex, endIndex, maxDepth

            if index in tree:
                if depth in tree[index]:
                    tree[index][depth].append(node.val)
                else:
                    tree[index][depth] = [node.val]
            else:
                tree[index] = {depth: [node.val]}

            if index < startIndex:
                startIndex = index
            if index > endIndex:
                endIndex = index
            if depth > maxDepth:
                maxDepth = depth

            traverse(node.left, depth + 1, index - 1)
            traverse(node.right, depth + 1, index + 1)

        traverse(root, 0, 0)

        output = []
        for i in range(startIndex, endIndex + 1):
            row = []
            for j in range(maxDepth + 1):
                if j in tree[i]:
                    row.extend(tree[i][j])
            output.append(row)
        return output
```

Runtime: *31 ms*

Link to my solution: [https://leetcode.com/problems/binary-tree-vertical-order-traversal/solutions/5878918/python-beats-90-92-of-users/](https://leetcode.com/problems/binary-tree-vertical-order-traversal/solutions/5878918/python-beats-90-92-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
