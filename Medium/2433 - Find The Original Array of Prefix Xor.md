# 2433. Find The Original Array of Prefix Xor

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/find-the-original-array-of-prefix-xor/description/](https://leetcode.com/problems/find-the-original-array-of-prefix-xor/description/)

### My Solution

Let the original array be `originalArray = [5,7,2,3,2]`. In order to generate the prefix XOR array `pref`, we perform XOR using the formula `pref[i] = arr[0] ^ arr[1] ^ ... ^ arr[i]`.
So, `pref` will be
```
pref[0] = 5
pref[1] = 5 ^ 7 = 2
pref[2] = 5 ^ 7 ^ 2 = 0
pref[3] = 5 ^ 7 ^ 2 ^ 3 = 3
pref[4] = 5 ^ 7 ^ 2 ^ 3 ^ 2 = 1
```
In order to solve this problem we just have to work backwards. We have `pref = [5, 2, 0, 3, 1]`. To calculate `originalArray`, we just have to perform `originalArray[i] = pref[i] ^ pref[i - 1]`.
For example, to calculate `originalArray[3]`
```
pref[3] ^ pref[2]
= (originalArray[0] ^ originalArray[1] ^ originalArray[2] ^ originalArray[3]) ^ (originalArray[0] ^ originalArray[1] ^ originalArray[2])
= originalArray[3] (Note: x ^ x = 0)
```

### Code

```python
class Solution:
    def findArray(self, pref: List[int]) -> List[int]:
        originalArray = [pref[0]]
        for i in range(1, len(pref)):
                originalArray.append(pref[i] ^ pref[i - 1])
        return originalArray
```

Runtime: *544 ms*

Link to my Solution: [https://leetcode.com/problems/find-the-original-array-of-prefix-xor/solutions/5023613/python-runtime-beats-95-55-of-users/](https://leetcode.com/problems/find-the-original-array-of-prefix-xor/solutions/5023613/python-runtime-beats-95-55-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$
- Space complexity: $O(1)$
