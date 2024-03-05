# 1750. Minimum Length of String After Deleting Similar Ends

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/description/](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/description/)

### My Solution

Using **Sliding window** concept and **two pointers**

### Code

```python
class Solution:
    def minimumLength(self, s: str) -> int:
        n = len(s)

        # If the string `s` contains only 1 character, then there cannot be both a prefix and a suffix,
        # so the length of the remaining string would be 1
        if n == 1:
            return 1

        prefix, suffix = 0, n - 1

        # Loop until `prefix` and `suffix` pointers overlap
        # In each loop, 1 prefix and suffix will be deleted
        while prefix < suffix:

            # Starting with the leftmost character in the prefix, checking if it matches the rightmost
            # character in the suffix
            if s[prefix] == s[suffix]:

                # Loop until the rightmost character in the prefix is reached
                while s[prefix] == s[suffix] and prefix < suffix:
                    prefix += 1
                # If the whole string is processed, then there are no characters remaining in the string
                # after deleting the prefix and suffix, so the length of the remaining string would be 0
                if prefix == suffix:
                    return 0

                # Loop until the leftmost character in the suffix is reached
                while s[prefix - 1] == s[suffix] and prefix - 1 < suffix:
                    suffix -= 1

            # If the leftmost character in the prefix does not match with the rightmost character in the
            # suffix, break from the loop
            else:
                break

        # Return the length of the remaining string
        return suffix - prefix + 1
```

Runtime: *64 ms*

Link to my Solution: [https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/solutions/4829613/python-memory-beats-92-00-of-users/](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/solutions/4829613/python-memory-beats-92-00-of-users/)

### Time and Space Complexities

- Time complexity: $O(n)$ 
  - Despite the inner loops, each character in the string is only traversed once.

- Space complexity: $O(1)$
