# 2. Add Two Numbers

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/add-two-numbers/description/](https://leetcode.com/problems/add-two-numbers/description/)

## My Solution 1

### Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:

        def getNum(node: Optional[ListNode]):
            curr, i, num = node, 1, 0
            while curr != None:
                num += i * curr.val
                i *= 10
                curr = curr.next
            return num

        def getList(num: int):
            if num == 0:
                return ListNode(0)

            head, prev = None, None
            while num != 0:
                node = ListNode(num % 10)
                if head == None:
                    head = prev = node
                else:
                    prev.next = node
                    prev = node
                num //= 10
            return head

        return getList(getNum(l1) + getNum(l2))
```

Runtime: *70 ms*

### Time and Space Complexities

- Time complexity: $O(n)$, where $n$ is the maximum number of digits in any linked list.
- Space complexity: $O(n)$

## My Solution 2

### Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        def attachNode(node: ListNode):
            nonlocal head, prev
            if head == None:
                head = prev = node
            else:
                prev.next = node
                prev = node

        head, prev, curr1, curr2, carryOn = None, None, l1, l2, 0

        while curr1 != None and curr2 != None:
            node = ListNode((curr1.val + curr2.val + carryOn) % 10)

            if (curr1.val + curr2.val + carryOn) // 10 != 0:
                carryOn = (curr1.val + curr2.val + carryOn) // 10
            else:
                carryOn = 0

            attachNode(node)
            curr1 = curr1.next
            curr2 = curr2.next

        while curr1 != None:
            node = ListNode((curr1.val + carryOn) % 10)

            if (curr1.val + carryOn) // 10 != 0:
                carryOn = (curr1.val + carryOn) // 10
            else:
                carryOn = 0

            attachNode(node)
            curr1 = curr1.next

        while curr2 != None:
            node = ListNode((curr2.val + carryOn) % 10)

            if (curr2.val + carryOn) // 10 != 0:
                carryOn = (curr2.val + carryOn) // 10
            else:
                carryOn = 0

            attachNode(node)
            curr2 = curr2.next

        while carryOn != 0:
            node = ListNode(carryOn % 10)
            if head == None:
                head = prev = node
            else:
                prev.next = node
                prev = node
            carryOn //= 10

        return head
```

Runtime: *51 ms*

### Time and Space Complexities

- Time complexity: $O(n)$, where $n$ is the maximum number of digits in any linked list.
- Space complexity: $O(n)$
