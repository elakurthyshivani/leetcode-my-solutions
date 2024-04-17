# 2181. Merge Nodes in Between Zeros

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/merge-nodes-in-between-zeros/description/](https://leetcode.com/problems/merge-nodes-in-between-zeros/description/)

### My Solution 

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        output = None
        curr, curr2 = head, None
        while curr != None:
            if curr.val == 0 and curr.next != None:
                if output == None:
                    output = curr2 = ListNode(0)
                else:
                    curr2.next = ListNode(0)
                    curr2 = curr2.next
            else:
                curr2.val += curr.val
            curr = curr.next
        print(curr2)
        return output
```

Runtime: *1006 ms*

#### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
