# 23. Merge k Sorted Lists

### About

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/merge-k-sorted-lists/description/](https://leetcode.com/problems/merge-k-sorted-lists/description/)

### My Solution

```python
import heapq

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class ListNode2(ListNode):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
    
    def __lt__(self, other):
        return self.val < other.val

    def __le__(self, other):
        return self.val <= other.val
    
    def __gt__(self, other):
        return self.val > other.val
    
    def __ge__(self, other):
        return self.val >= other.val

class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        k = len(lists)
        if k == 0:
            return None
        elif k == 1:
            return lists[0]

        output, curr = None, None
        heap = [(head.val, ListNode2(head.val, head.next)) for head in lists if head != None]
        heapq.heapify(heap)

        while len(heap) > 0:
            minNode = heapq.heappop(heap)
            if output == None:
                output = curr = ListNode(minNode[0])
            else:
                curr.next = ListNode(minNode[0])
                curr = curr.next
            if minNode[1].next != None:
                heapq.heappush(heap, (minNode[1].next.val, ListNode2(minNode[1].next.val, minNode[1].next.next)))
        
        return output
```
Runtime: *83 ms*

### Time and Space Complexities

- Time complexity: $O(n(log k))$, where $n$ is the total number of elements in all the sorted arrays.
  - Since we add each the element to the heap once, the time complexity is $O(n)$.
  - The heap will consist of $k$ elements.
  - To build the heap and extract the minimum value from the heap is $O(log k)$.

- Space complexity: $O(k)$
