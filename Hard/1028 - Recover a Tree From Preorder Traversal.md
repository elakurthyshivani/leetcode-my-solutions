# 1028. Recover a Tree From Preorder Traversal

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/recover-a-tree-from-preorder-traversal/description/](https://leetcode.com/problems/recover-a-tree-from-preorder-traversal/description/)

## My Solution - Backtracking

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def recoverFromPreorder(self, traversal: str) -> Optional[TreeNode]:

        def traverse(node : Optional[TreeNode], depth : int):
            nonlocal traversal
            n = len(traversal)

            if n == 0:
                return

            i = 0
            while traversal[i].isdigit() is False:
                i += 1

            j, val = i, ''
            while j < n and traversal[j].isdigit():
                val += traversal[j]
                j += 1
            val = int(val)
            # print(i, val)

            if depth + 1 == i:
                traversal = traversal[j : ]
                # print(traversal)
                if node.left == None:
                    node.left = TreeNode(val)
                    traverse(node.left, depth + 1)
                else:
                    node.right = TreeNode(val)
                    traverse(node.right, depth + 1)
                traverse(node, depth)
            elif depth >= i:
                # print("Backtrack -", traversal)
                return

        i, n = 0, len(traversal)
        while i < n and traversal[i].isdigit():
            i += 1
        root, traversal = TreeNode(int(traversal[ : i])), traversal[i : ]
        traverse(root, 0)
        return root
```

Runtime: *73 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(h)$, where $h$ is the depth of the tree
