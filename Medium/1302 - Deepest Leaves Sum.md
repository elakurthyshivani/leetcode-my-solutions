# 1302. Deepest Leaves Sum

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/deepest-leaves-sum/description/](https://leetcode.com/problems/deepest-leaves-sum/description/)

### My Solution

One way to solve this problem is to traverse through the tree by updating the height and saving the maximum height seen and the sum of the nodes at this height in a variable.

### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deepestLeavesSum(self, root: Optional[TreeNode]) -> int:
        def traverse(curr, height, sums):
            if curr == None:
                return
            if height in sums:
                sums[height] += curr.val
            else:        
                maxHeight = list(sums.keys())[0]
                if height > maxHeight:
                    sums.pop(maxHeight)
                    sums[height] = curr.val
            traverse(curr.left, height + 1, sums)
            traverse(curr.right, height + 1, sums)
        
        sums = {1: 0}
        traverse(root, 1, sums)
        return list(sums.values())[0]
```

Runtime: *130 ms*

Link to my Solution: [https://leetcode.com/problems/deepest-leaves-sum/solutions/5032317/python-memory-beats-98-27-of-users/](https://leetcode.com/problems/deepest-leaves-sum/solutions/5032317/python-memory-beats-98-27-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
