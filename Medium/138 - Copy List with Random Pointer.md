# 138. Copy List with Random Pointer

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/copy-list-with-random-pointer/description](https://leetcode.com/problems/copy-list-with-random-pointer/description)

## My Solution 1

### Code

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        orig, copy, newHead = {}, [], None

        prev, curr, i = None, head, 0
        while curr != None:
            orig[curr] = i
            newCurr = Node(curr.val)
            copy.append(newCurr)
            if prev == None:
                prev = newHead = newCurr
            else:
                prev.next = newCurr
                prev = newCurr
            i += 1
            curr = curr.next


        
        curr, newCurr, i = head, newHead, 0
        while curr != None:
            rand = curr.random
            if rand != None:
                newCurr.random = copy[orig[rand]]
            i += 1
            curr = curr.next
            newCurr = newCurr.next

        return newHead
```

Runtime: *45 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(n)$

## My Solution 2

### Code
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if head == None:
            return None
            
        curr = head
        while curr != None:
            cNext = curr.next
            curr.next = Node(curr.val)
            curr.next.next = cNext
            curr = curr.next.next
        
        curr = head
        while curr != None:
            newCurr = curr.next
            cNext = newCurr.next
            if cNext:
                newCurr.next = cNext.next
            cRand = curr.random
            print(curr.val, curr.random.val if curr.random else None)
            if cRand:
                newCurr.random = cRand.next
            curr = cNext

        return head.next
```

Runtime: *41 ms*

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
