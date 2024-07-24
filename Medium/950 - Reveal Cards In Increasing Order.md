# 950. Reveal Cards In Increasing Order

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/reveal-cards-in-increasing-order/description/](https://leetcode.com/problems/reveal-cards-in-increasing-order/description/)

### My Solution

Initially sort the deck. In a queue, push all the indices of the output array in increasing order. Pop from the queue one index at a time and continue until the queue is empty. When the first index is popped, pop the first card from the deck and add it to the output list at the popped index. Now push the second index popped from the queue back to the end of the queue. Continue this process until the queue is empty.

#### Code (Using Quick Sort)

```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        n = len(deck)
        self.quickSort(deck, 0, n - 1, False)
        output = [0 for i in range(n)]
        queue = [i for i in range(n)]
        i, skip = 0, False
        while queue != []:
            if skip == False:
                output[queue.pop(0)] = deck[i]
                i += 1
                skip = True
            else:
                queue.append(queue.pop(0))
                skip = False
        return output
        
    def quickSort(self, arr: list[int] | list[str], start : int, end : int, reverse : bool = False) -> None:
        if start >= end:
            return
        partitionIndex = self.partition(arr, start, end)
        self.quickSort(arr, start, partitionIndex - 1, reverse)
        self.quickSort(arr, partitionIndex + 1, end, reverse)

    def partition(self, arr: list[int] | list[str], start : int, end : int, reverse : bool = False) -> int:
        partitionIndex = end
        i, j = 0, 0
        while i < end and j < end:
            if (reverse == False and arr[j] <= arr[partitionIndex]) or (reverse and arr[j] >= arr[partitionIndex]):
                arr[i], arr[j] = arr[j], arr[i]
                i += 1
            j += 1
        arr[i], arr[partitionIndex] = arr[partitionIndex], arr[i]
        return i
```

Runtime: *220 ms*

#### Solution 2 - Code

```python
class Solution:
    def deckRevealedIncreasing(self, deck: List[int]) -> List[int]:
        n = len(deck)
        deck.sort()
        output = [0 for i in range(n)]
        queue = [i for i in range(n)]
        i, skip = 0, False
        while queue != []:
            if skip == False:
                output[queue.pop(0)] = deck[i]
                i += 1
                skip = True
            else:
                queue.append(queue.pop(0))
                skip = False
        return output
```

Runtime: *55 ms*

#### Time and Space Complexities

- Time complexity: $O(n(log n))$
- Space complexity: $O(n)$
