# 426. Convert Binary Search Tree to Sorted Doubly Linked List

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/description/](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/description/)

## My Solution

### Code

```python
# Definition for a binary tree node.
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
"""

class Solution:
    def treeToDoublyList(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if root == None:
            return None
        
        if root.left == None and root.right == None:
            root.left = root.right = root
            return root

        smallestNode, largestNode = None, None

        def traverse(node: Optional[Node]):
            if node == None:
                return

            nonlocal smallestNode, largestNode
            if smallestNode == None or node.val < smallestNode.val:
                smallestNode = node
            if largestNode == None or node.val > largestNode.val:
                largestNode = node

            if node.left == None and node.right == None:
                return

            traverse(node.left)
            traverse(node.right)

            currPrev = node.left
            while currPrev != None and currPrev.right != None:
                currPrev = currPrev.right
            node.left = currPrev
            if currPrev != None:
                currPrev.right = node

            currNext = node.right
            while currNext != None and currNext.left != None:
                currNext = currNext.left
            node.right = currNext
            if currNext != None:
                currNext.left = node

            # print(node.val, node.left.val if node.left != None else None, node.right.val if node.right != None else None)

        traverse(root)

        # print(smallestNode.val if smallestNode != None else None)
        # print(largestNode.val if largestNode != None else None)
        if smallestNode != largestNode and smallestNode != None and largestNode != None:    
            smallestNode.left = largestNode
            largestNode.right = smallestNode
            
        return smallestNode
```

Runtime: *43 ms*


### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$
