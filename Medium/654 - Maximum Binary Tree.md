# 654. Maximum Binary Tree

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/maximum-binary-tree/description/](https://leetcode.com/problems/maximum-binary-tree/description/)

### My Solution 1 (Using Monotonically decreasing stack)

#### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        if nums == None or len(nums) == 0:
            return None

        # Monotonically decreasing stack
        mdStack = []
        
        # Previous node
        prev = None

        for num in nums:
            # Create a node for curr num
            curr = TreeNode(num)

            # If curr node value is greater than the one in the top of the stack, 
            # pop until the stack is empty or a node greater than curr occurs.
            while len(mdStack) > 0 and mdStack[-1].val < num:
                prev = mdStack.pop()
            
            # If there are nodes in the stack and the top of the stack node is greater
            # than the curr node, then add curr node to the top the stack node's right.
            # Note that as we traverse through `nums`, the index increases.
            if len(mdStack) > 0:
                mdStack[-1].right = curr
            
            # In the above while loop, we set prev value when the top of the stack value
            # is less than curr node. Now this needs to be added to the left of the curr
            # node.
            curr.left = prev

            # Add the curr node to the stack
            mdStack.append(curr)
            
            # Reset prev
            prev = None

        return mdStack[0]
```

Runtime: *112 ms*

Link to my Solution: [https://leetcode.com/problems/maximum-binary-tree/solutions/5038519/python-runtime-beats-98-15-of-users/](https://leetcode.com/problems/maximum-binary-tree/solutions/5038519/python-runtime-beats-98-15-of-users/)

#### Time and Space Complexities

- Time complexity: $O(n)$

- Space complexity: $O(n)$

### My Solution 2

#### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        # `nums` is empty
        if len(nums) == 0:
            return None
        
        # `nums` consist of only 1 element, create a node for it
        elif len(nums) == 1:
            return TreeNode(nums[0])

        # Find the max num and create a node for it
        maxNum = max(nums)
        root = TreeNode(maxNum)

        # Recursively continue this process for the remaining nums to the left of max num
        root.left = self.constructMaximumBinaryTree(nums[ : nums.index(maxNum)])
        # Recursively continue this process for the remaining nums to the right of max num
        root.right = self.constructMaximumBinaryTree(nums[nums.index(maxNum) + 1 : ])

        return root
```

Runtime: *136 ms*

#### Time and Space Complexities

- Time complexity: $O(n^2)$

- Space complexity: $O(n)$

### My Solution 3

#### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        # Head of new tree
        root = None

        # Insert into binary tree function
        def insert(curr, num):
            if curr == None:
                return TreeNode(num)
            
            nonlocal indices
            if indices[num] < indices[curr.val]:
                curr.left = insert(curr.left, num)
            else:
                curr.right = insert(curr.right, num)
            return curr

        # Convert nums into a dictionary in num: index form
        indices = dict(zip(nums, range(len(nums))))

        # Sort nums in descending order
        nums.sort(reverse = True)

        for num in nums:
            # Add into binary tree
            root = insert(root, num)

        return root
```

Runtime: *171 ms*

#### Time and Space Complexities

- Time complexity: $O(n^2)$

- Space complexity: $O(n)$
