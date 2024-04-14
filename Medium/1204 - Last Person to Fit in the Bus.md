# 1204. Last Person to Fit in the Bus

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/last-person-to-fit-in-the-bus/description/](https://leetcode.com/problems/last-person-to-fit-in-the-bus/description/)

### My Solution 1

```python
import pandas as pd

def last_passenger(queue: pd.DataFrame) -> pd.DataFrame:
    cummulativeWeights = 0
    lastPerson = ""
    def boardBus(person):
        nonlocal cummulativeWeights, lastPerson
        cummulativeWeights += person.weight
        if cummulativeWeights <= 1000:
            lastPerson = person.person_name
    queue.sort_values("turn", inplace = True)
    queue.apply(boardBus, axis = 1)
    return pd.DataFrame({"person_name": [lastPerson]})
```

Runtime: *785 ms*

### My Solution 2

```python
import pandas as pd

def last_passenger(queue: pd.DataFrame) -> pd.DataFrame:
    queue.sort_values("turn", inplace = True)
    queue["cummulativeWeight"] = queue.weight.cumsum()
    return queue[queue.cummulativeWeight <= 1000][["person_name"]].tail(1)
```

Runtime: *693 ms*
