# 2888. Reshape Data: Concatenate

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/reshape-data-concatenate/description/](https://leetcode.com/problems/reshape-data-concatenate/description/)

### My Solution

```python
class Solution:
import pandas as pd

def concatenateTables(df1: pd.DataFrame, df2: pd.DataFrame) -> pd.DataFrame:
    return pd.concat([df1, df2])
```

Runtime: *787 ms*
