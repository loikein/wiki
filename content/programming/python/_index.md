---
bookCollapseSection: true
title: "Python"
---

# Python snippets

## List

Find the index of minimum in a list: \([credit](https://stackoverflow.com/a/13301022/10668706)\)

```python
val, index = min((val, index) for (index, val) in enumerate(my_list))
```

## Benchmarking

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

## Pickle

```python
import os
import pickle

pickle_path = os.path.join("data", "data.pickle") # path: ./data/data.pickle

# create pickle
with open(pickle_path, "wb") as f:
    pickle.dump(df, f)

# use pickle
if os.path.isfile(pickle_path):
    with open(pickle_path, "rb") as f:
        df = pickle.load(f)
else:
    print("Pickle not found. Please create one first.")
```

## Try except

```python
try:
    assert(len(list) == 5)
except AssertionError:
    print("Error: List length is wrong.")
except:
    print("Error: Unknown error.")
```
