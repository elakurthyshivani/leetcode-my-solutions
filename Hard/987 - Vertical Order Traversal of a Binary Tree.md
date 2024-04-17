# 987. Vertical Order Traversal of a Binary Tree

### About

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/)

### My Solution

Example: `[1, 2, 3, 4, 6, 5, 7, 8, 9, 10, 11, 12, 14, 13, 15]`

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def verticalTraversal(self, root: Optional[TreeNode]) -> List[List[int]]:
        self.coord=[] # Height, Each element is a dictionary.
        self._verticalTraversal(root, 0, 0)
        # Each index x of coord consists of nodes at x in the binary tree:
		# 0 {0: [1]}
		# 1 {-1: [2], 1: [3]}
		# 2 {-2: [4], 0: [6, 5], 2: [7]}
		# 3 {-3: [8], -1: [12, 10, 9], 1: [14, 13, 11], 3: [15]}

        out, height, outK=[], len(self.coord)-1, 0
        for j in range(-height, height+1):
            out.append([])
            if j%2==1:
                for i in range(height if height%2==1 else height-1, abs(j)-1, -2):
                    if j in self.coord[i]:
                        out[outK].extend(self.coord[i][j])
            else:
                for i in range(height if height%2==0 else height-1, abs(j)-1, -2):
                    if j in self.coord[i]:
                        out[outK].extend(self.coord[i][j])
            if len(out[outK])==0:
                del out[outK]
            else:
                out[outK]=out[outK][::-1]
                outK+=1
				
		# Nodes at position(x, -3): [8]
		# Nodes at position(x, -2): [4]
		# Nodes at position(x, -1): [2, 9, 10, 12]
		# Nodes at position(x, 0): [1, 5, 6]
		# Nodes at position(x, 1): [3, 11, 13, 14]
		# Nodes at position(x, 2): [7]
		# Nodes at position(x, 3): [15]
		
        return out
        
    def _verticalTraversal(self, root, i, j):
        if root==None:
            return
        if i<len(self.coord):
            if j in self.coord[i]:
                for k in range(len(self.coord[i][j])):
                    if self.coord[i][j][k]<root.val:
                        self.coord[i][j].insert(k, root.val)
                        break
                else:
                    self.coord[i][j].append(root.val)
            else:
                self.coord[i][j]=[root.val]
        else:
            self.coord.append({j:[root.val]})
        self._verticalTraversal(root.left, i+1, j-1)
        self._verticalTraversal(root.right, i+1, j+1)
```
Runtime: *37 ms*

Link to my Solution: [https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/solutions/2530113/python-runtime-37-ms-faster-than-9079-memory-usage-142-mb-less-than-7274/](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/solutions/2530113/python-runtime-37-ms-faster-than-9079-memory-usage-142-mb-less-than-7274/)
