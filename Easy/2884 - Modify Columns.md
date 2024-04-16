# 2884. Modify Columns

Difficulty: **Easy**

Link to Problem Statement: [https://leetcode.com/problems/modify-columns/description/](https://leetcode.com/problems/modify-columns/description/)

### My Solution

```python
import pandas as pd

def modifySalaryColumn(employees: pd.DataFrame) -> pd.DataFrame:
    employees.salary = employees.salary * 2
    return employees
```

Runtime: *575 ms*
