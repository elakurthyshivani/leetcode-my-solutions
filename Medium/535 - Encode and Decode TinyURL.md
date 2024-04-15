# 535. Encode and Decode TinyURL

# 1689. Partitioning Into Minimum Number Of Deci-Binary Numbers

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/encode-and-decode-tinyurl/description/](https://leetcode.com/problems/encode-and-decode-tinyurl/description/)

### My Solution

### Code 1

```python
import random, string
class Codec:
    
    def __init__(self):
        self.long=""
        self.short=""

    def encode(self, longUrl: str) -> str:
        index=''.join(random.choices(string.ascii_letters+\
                                     string.digits, k=6))
        self.long, self.short=longUrl, index
        return "http://tinyyrl.com/"+index
        

    def decode(self, shortUrl: str) -> str:
        return self.long
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(url))
```

Runtime: *41 ms*
