---
weight: 301
title: "Writing functions"
---
# Writing Python functions


## `*args` vs `**kwargs`


## Get variable name of user input

Function:

```python
from varname import argname

def make_pickle(
    user_input
):
    """Save user_input as a file with the same name."""
    file_name = argname("user_input") + ".pickle"
    with open(file_name, "wb") as f:
        pickle.dump(file_name, f)
    return

make_pickle(df_1)
# result: df_1.pickle
```
