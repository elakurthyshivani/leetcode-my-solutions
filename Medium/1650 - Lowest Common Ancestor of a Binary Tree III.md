# 1650. Lowest Common Ancestor of a Binary Tree III

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/description/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/description/)

## My Solution 1

### Code

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
"""

class Solution:
    def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
        depthP, depthQ = 0, 0

        def depthOfANode(node: 'Node', depth: int):
            if node == None:
                return
            
            nonlocal depthP, depthQ

            if node.val == p.val:
                depthP = depth

            if node.val == q.val:
                depthQ = depth

            depthOfANode(node.left, depth + 1)
            depthOfANode(node.right, depth + 1)


        def getRootOfNode(node: 'Node'):
            if node.parent == None:
                return node
            
            return getRootOfNode(node.parent)


        root = getRootOfNode(p)
        depthOfANode(root, 0)
        
        while depthP != depthQ:
            if depthP > depthQ:
                depthP -= 1
                p = p.parent
            else:
                depthQ -= 1
                q = q.parent
        
        while p != q:
            p = p.parent
            q = q.parent

        return p
```

Runtime: *54 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$

## My Solution 2

### Code

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
"""

class Solution:
    def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
        pCurr, qCurr = p, q
        while pCurr != qCurr:
            pCurr = pCurr.parent if pCurr.parent != None else q
            qCurr = qCurr.parent if qCurr.parent != None else p
        return pCurr
```

Runtime: *50 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
