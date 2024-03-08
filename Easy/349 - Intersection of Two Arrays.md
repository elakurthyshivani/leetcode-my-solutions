# 349. Intersection of Two Arrays

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/intersection-of-two-arrays/description/](https://leetcode.com/problems/intersection-of-two-arrays/description/)

### My Solution (Using Hash Table)

#### Code

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # Intersection of nums1 and nums2 the arrays
        result = []

        # Will be True at index `i` if `i` is present in nums1
        isPresent = [False for i in range(max(max(nums1), max(nums2)) + 1)]

        for num in nums1:
            isPresent[num] = True
        
        for num in nums2:
            # If a `num` from nums2 has `isPresent` True at index `num`, that means this `num`
            # is also present in nums1
            if isPresent[num]:
                # Add this `num` to `result`
                result.append(num)
                # Mark False in `isPresent` at index `num`
                # If there are any more `num`s in `nums2`, we don't want to add it to the `result`
                # array more than once.
                isPresent[num] = False

        return result
```

Runtime: *35 ms*

Link to my Solution: [https://leetcode.com/problems/intersection-of-two-arrays/solutions/4843862/python-runtime-beats-98-76-of-users-memory-beats-91-74-of-users/](https://leetcode.com/problems/intersection-of-two-arrays/solutions/4843862/python-runtime-beats-98-76-of-users-memory-beats-91-74-of-users/)

#### Time and Space Complexities

- Time complexity: $O(n + m)$, where $n$ is the length of `nums1` and $m$ is the length of `nums2`
  - The first `for` loop iterates $n$ times and the second `for` loop iterates $m$ times.

- Space complexity: $O(k) , where $k$ is maximum value from both `nums1` and `nums2`.

### Another Solution (Using Sets)

#### Code

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return set(nums1) & set(nums2) # Convert `nums1` and `nums2` into sets and perform intersection between them
```

Runtime: *44ms*
