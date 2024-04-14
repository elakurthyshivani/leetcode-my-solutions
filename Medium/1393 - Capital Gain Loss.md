# 1393. Capital Gain/Loss

Difficulty: **Medium**

Link to Problem Statement: [https://leetcode.com/problems/capital-gainloss/description/](https://leetcode.com/problems/capital-gainloss/description/)

### My Solution

```python
import pandas as pd

def capital_gainloss(stocks: pd.DataFrame) -> pd.DataFrame:
    stocks.loc[stocks[stocks.operation == "Buy"].index.to_list(), "price"] = - stocks[stocks.operation == "Buy"].price
    output = stocks[["stock_name", "price"]].groupby(by="stock_name").sum().reset_index()
    output.columns = ["stock_name", "capital_gain_loss"]
    return output
```

Runtime: *845 ms*
