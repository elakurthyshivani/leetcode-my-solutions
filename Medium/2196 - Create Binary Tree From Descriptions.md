# 2196. Create Binary Tree From Descriptions

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/create-binary-tree-from-descriptions/description/](https://leetcode.com/problems/create-binary-tree-from-descriptions/description/)

### My Solution (Using Hash table)

#### Approach

**Step 1**: Create keys in the hash table for every node in the tree.

**Step 2**: Find the root.

**Step 3**: For each `[parent_i, child_i, is_left]`, create the parent node if it has not been created before. Create the child node if it has not been created before. Attach the child node to the left or right of the parent appropriately. Add the created parent and/or child nodes to the hash table.

#### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def createBinaryTree(self, descriptions: List[List[int]]) -> Optional[TreeNode]:
        # All the nodes in the tree.
        # Key of `nodes`: `val` of a node in the binary tree.
        # Value of `nodes`: `TreeNode` object of the node with `val`.
        nodes = {}

        # Root value of the binary tree.
        root = None

        # Iterate through child values, add the value in `nodes`.
        for [_, child, _] in descriptions:
            nodes[child] = None
        
        # Iterate through parent values. 
        # Add the value if it not present in `nodes`. This value is the `root`.
        for[parent, _, _] in descriptions:
            if parent not in nodes:
                root = parent
                nodes[parent] = None
                break
        
        # Create binary tree.
        for [parent, child, isLeft] in descriptions:
            # Create the child node if it has not been created before.
            # Add the child node in `nodes[child]`.
            if nodes[child] is None:
                nodes[child] = TreeNode(child)

            # Create the parent node if it has not been created before.
            # Add the parent node in `nodes[parent]`.
            if nodes[parent] is None:
                nodes[parent] = TreeNode(parent)

            # Add child node to the parent.
            if isLeft:
                nodes[parent].left = nodes[child]
            else:
                nodes[parent].right = nodes[child]

        # Return the root node of the tree.
        return nodes[root]
```

Runtime: *1569 ms*

Link to my Solution: [https://leetcode.com/problems/create-binary-tree-from-descriptions/solutions/4781322/python-memory-beats-86-48-of-users](https://leetcode.com/problems/create-binary-tree-from-descriptions/solutions/4781322/python-memory-beats-86-48-of-users)

#### Time and Space Complexities

- Time complexity: $O((n - 1) * 3) = O(n)$, where $n$ is the number of nodes in the tree 
  - Length of the `descriptions` array is $n-1$.
  - 3 `for` loops iterate over `descriptions`.

- Space complexity: $O(n)$
  - The length of `nodes` dictionary is $n$.

### My Solution (Old: Using Sets and Arrays)

#### Approach

The basic idea of my solution is to first find the number which is going to be the root of the binary tree. Next, I'll find the largest number in the binary tree because I'm using arrays and hashing instead of using dictionaries in this solution. 

<b>Step 1</b>:
To find the root value (say `r`) of the binary tree from the descriptions, I'm creating two sets. One set consists of parent node numbers (set `a`) and the other set consists of child node numbers (set `b`). When I use set difference operation `set a - set b`, I'll obtain the root of the binary tree. If we consider the binary tree has `n` nodes. Consider the example `[[20,15,1],[20,17,0],[50,20,1],[50,80,0],[80,19,1]]` given in the problem statement. The root value is `50`.

<b>Step 2</b>:
To find the largest number in the binary tree (say `m`), I calculated the max value among the parent nodes and the max value among the child nodes. The largest value among these two is the largest number in the binary tree. In the above example, `80` is the max value among the parent nodes (`20, 50, 80`) and `80` is the max value among the child nodes (`15, 17, 20, 80, 19`). `max(80, 80)` is `80`. Since we traversed through the `descriptions`, this process takes $O(n)$ time.

<b>Step 3</b>:
Now, we create the array of size `m` (say `nodes`) to hold all the nodes in the binary tree. If a node has a `val` of `5`, then the reference of this node is stored at `nodes[5]`. The root node will be referenced at index `r`.

<b>Step 4</b>:
Finally, we traverse through each node's `description` in the `descriptions`. For each `description`, we create the parent node if it's not been created before and also create the child node if it's not been created before. We now add the child node to the left or right of the parent appropriately. The time to iterate through the `descriptions` is $O(n)$.

The whole binary tree has been constructed from the `descriptions` where the root of the node is referenced at `nodes[r]`. Finally, just return `nodes[r]`.

#### Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def createBinaryTree(self, descriptions: List[List[int]]) -> Optional[TreeNode]:
        # Steps:
        # 1. Find the root r.
        # 2. Find the largest number.
        # 3. Create an array of 'None's of size r+1.
        # 4. For each description in descriptions, create a node if needed and add it to appropriate index in the array.
        # 5. Return r th index from the array.
        
        # Find the root.
        r=(set([description[0] for description in descriptions])-set([description[1] for description in descriptions])).pop()
        
        # Find the largest number.
        m=max(max(descriptions, key=lambda x:x[1])[1], max(descriptions, key=lambda x:x[0])[0])
        
        # Initialize the array of nodes.
        nodes=[None]*(m+1)
        
        # Iterate through descriptions.
        for description in descriptions:
            parent, child=description[0], description[1]
            if nodes[child]==None:  nodes[child]=TreeNode(child)
            if nodes[parent]==None: nodes[parent]=TreeNode(parent)
            if description[2]==1:   nodes[parent].left=nodes[child]
            else:                   nodes[parent].right=nodes[child]
        
        # Return the root.
        return nodes[r]
```

Runtime: *2352 ms*

Link to my Solution: [https://leetcode.com/problems/create-binary-tree-from-descriptions/solutions/1834926/python3-solution-on-time/](https://leetcode.com/problems/create-binary-tree-from-descriptions/solutions/1834926/python3-solution-on-time/)

#### Time and Space Complexities

- Time complexity: $O(n)$

- Space complexity: $O(n)$
