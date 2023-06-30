---
bookCollapseSection: true
title: "Python"
---

## Dictionary

Get head of a dictionary: \([credit](https://stackoverflow.com/a/28704691)\)

```python
from itertools import islice

dict(islice(my_dict.items(), 0, 5))
```


## List

Find the index of minimum in a list: \([credit](https://stackoverflow.com/a/13301022/10668706)\)

```python
val, index = min((val, index) for (index, val) in enumerate(my_list))
```

Write a list to file: \([credit](https://pynative.com/python-write-list-to-file/)\)

```python
import os

my_list = ["A", "B", "C"]

# open file in write mode
with open(os.path.join("data", "log.txt"), 'w') as f:
    for item in my_list:
        # write each item on a new line
        f.write("%s\n" % item)

print("Done.")
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

## Pretty print

### JSON

Pretty print: \([credit](https://stackoverflow.com/a/12944035)\)

```python
import json

print(json.dumps(json.loads(json_data), indent=4))

# if get TypeError: the JSON object must be str, bytes or bytearray, not dict
# then use:
print(json.dumps(json_data, indent=4))
```

Split a big JSON file into smaller files: \([credit](https://plainenglish.io/blog/split-big-json-file-into-small-splits)\)

```python
import os
import json
from itertools import islice


def split_json(
    data_path,
    file_name,
    size_split=1000,
):
    """Split a big JSON file into chunks.
    file_name : exclude ".json"
    """
    with open(os.path.join(data_path, file_name + ".json"), "r") as f:
        whole_file = json.load(f)

    split = len(whole_file) // size_split

    for i in range(split + 1):
        with open(os.path.join(data_path, file_name + "_"+ str(split+1) + "_" + str(i+1) + ".json"), 'w') as f:
            json.dump(dict(islice(whole_file.items(), i*size_split, (i+1)*size_split)), f)
    return
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
