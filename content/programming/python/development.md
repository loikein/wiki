---
weight: 301
title: "Development"
---

## Error handling

### Try except

Refs:

- [8. Errors and Exceptions — Python 3.12.2 documentation](https://docs.python.org/3/tutorial/errors.html)
- [exception - What is the intended use of the optional "else" clause of the "try" statement in Python? - Stack Overflow](https://stackoverflow.com/questions/855759/)

```python
try:
    assert(len(list) == 5)
except AssertionError:
    print("Error: List length is wrong.")
except Exception as e:
    print(e)
```

### `assert`

Ref: [python - What's the difference between raise, try, and assert? - Stack Overflow](https://stackoverflow.com/a/40183030)

```python
assert(isinstance("hello", str))
```


## Function input

### `*args` vs `**kwargs`

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
    for key, value in kwargs.items():
        print(key+" is "+value)

print_all(today="sunday", tomorrow="monday")
# today is sunday
# tomorrow is monday
```

## Function return

### Return nothing

Ref: [python - return, return None, and no return at all? - Stack Overflow](https://stackoverflow.com/a/15300671)


## Useful tricks

### Benchmarking

Ref: [performance - How to measure elapsed time in Python? - Stack Overflow](https://stackoverflow.com/questions/7370801/how-to-measure-elapsed-time-in-python)

```python
import time

# use round() if only the first digit is necessary
start = time.time()

# (some heavy load operations)

end = time.time()
elapsed = end - start
print(elapsed)
```


## Dark magic

> Proceed at your own risk. You have been warned.
{.book-hint .danger}

### Get variable name of user input

Function:

```python
import os
import pickle
from varname import argname

def make_pickle(
    variable,
    *args,
):
    """Save user_input as a file with the same name."""
    file_name = argname("variable") + ".pickle"
    file_path = "."
    for path in args:
        file_path = os.path.join(file_path, path)
    file_path = os.path.join(file_path, file_name)
    with open(file_path, "wb") as f:
        pickle.dump(variable, f)
    return

make_pickle(df_1, "data", "pt1", ...)
# result: /data/pt1/.../df_1.pickle
```

### Make variable name out of string

Credit: [Convert String to Variable Name in Python - PythonForBeginners.com](https://www.pythonforbeginners.com/basics/convert-string-to-variable-name-in-python)

> This will not work as an imported function.
{.book-hint .warning}

```python
import os
import pickle

def use_pickle(
    name,
    *args,
):
    """Use user_input pickle."""
    file_name = name + ".pickle"
    file_path = "."
    for path in args:
        file_path = os.path.join(file_path, path)
    file_path = os.path.join(file_path, file_name)
    if os.path.isfile(file_path):
        with open(file_path, "rb") as f:
            global_vars = globals()
            global_vars.__setitem__(name, pickle.load(f))
    else:
        raise FileNotFoundError("Pickle not found. Please create one first.")
    return

use_pickle("df_1", "data", "pt1", ...)
# result: df_1 (type: dataframe)
```
