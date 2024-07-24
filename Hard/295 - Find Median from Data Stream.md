# 295. Find Median from Data Stream

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/find-median-from-data-stream/description/](https://leetcode.com/problems/find-median-from-data-stream/description/)

### My Solution

```python
class MedianFinder:

    def __init__(self):
        self.arr=[]        

    def addNum(self, num: int) -> None:
        for i in range(len(self.arr)):
            if self.arr[i]>num:
                self.arr.insert(i, num)
                break
        else:
            self.arr.append(num)
        # print(self.arr)

    def findMedian(self) -> float:
        n=len(self.arr)
        if n%2==0:
           return (self.arr[n//2]+self.arr[n//2-1])/2
        else:
            return self.arr[n//2]


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```
Runtime: *7785 ms*

Link to my Solution: [https://leetcode.com/problems/find-median-from-data-stream/solutions/5038533/python-memory-beats-100-00-of-users/](https://leetcode.com/problems/find-median-from-data-stream/solutions/5038533/python-memory-beats-100-00-of-users/)
