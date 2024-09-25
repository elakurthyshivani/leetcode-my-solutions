# 236. Lowest Common Ancestor of a Binary Tree

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

### My Solution

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        pVisited, qVisited, lcaUpdated, lca = False, False, False, root

        def traverse(curr: 'TreeNode'):
            if curr == None:
                return False
            
            lRes = traverse(curr.left)
            rRes = traverse(curr.right)

            nonlocal lcaUpdated, lca
            if lcaUpdated == False:
                if lRes and rRes:
                    lca = curr
                    lcaUpdated = True
                if (lRes or rRes) and (curr.val == p.val or curr.val == q.val):
                    lca = curr
                    lcaUpdated = True
                if curr.val == p.val or curr.val == q.val:
                    return True
            
            return lRes or rRes
            
        traverse(root)
        return lca
```

Runtime: *42 ms*

Link to my solution: [https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solutions/5833850/python-runtime-beats-92-40-of-users/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solutions/5833850/python-runtime-beats-92-40-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
