---
weight: 301
title: "Writing functions"
---


## `*args` vs `**kwargs`

Refs:

- [python - Use of `*args` and `**kwargs` - Stack Overflow](https://stackoverflow.com/a/3394898/10668706)
- [python - Why can't both args and keyword only arguments be mixed with `*args` and `**kwargs` simultaneously - Stack Overflow](https://stackoverflow.com/a/64447219/10668706)

`*args`: (unstructured: only values)

```python
def add_all(*args):
    """Returns the sum of all values."""
    sum_all = 0
    for num in args:
        sum_all += num

    return sum_all

sum_all(2, 3)                               # 5
sum_all(2, 3, 4, 5, 6)                      # 20
```

`**kwargs`: (structured: names \+ values)

```python
def print_all(**kwargs):
    """Print key-value pairs."""
    for k, v in kwargs.items():
        print(k+" is "+v)

print_all(today="sunday", tomorrow="monday")
# today is sunday
# tomorrow is monday
```

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
