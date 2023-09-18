---
bookCollapseSection: true
title: "Python"
---
## \(Maybe\) Useful resources

- [Gallery of Jupyter Books - Executable Books](https://executablebooks.org/en/latest/gallery/)
- [The Hitchhiker’s Guide to Python](https://docs.python-guide.org/)
- [nkmk/python-snippets](https://github.com/nkmk/python-snippets)
- [satwikkansal/wtfpython](https://github.com/satwikkansal/wtfpython)


## Dictionary

### Append

```python
new_dict = {}
new_dict.update({"name": number})
```


### Head

Get head of a dictionary: \([credit](https://stackoverflow.com/a/28704691)\)

```python
from itertools import islice

dict(islice(my_dict.items(), 0, 5))
```



## Help

Like R's `?` function.

```python
help(np.log)

# If it is a method, need something that the method can run from:
help(df.reset_index)
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

## CSV

> This section focuses on the Python module `csv`. For the package `pandas`, see [Pandas](/programming/python/pandas/).
{.book-hint .info}

Docs: [csv — CSV File Reading and Writing — Python 3.11.4 documentation](https://docs.python.org/3/library/csv.html)

### Import as list

Ref: [Python import csv to list - Stack Overflow](https://stackoverflow.com/a/24662707/10668706)

```python
import csv

with open("data.csv", newline="") as f:
    reader = csv.reader(f)
    data = list(reader)

print(data)
# [
#   ["first", "row"], ["second", "row"], …
# ]
```

## JSON

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

Merge said smaller files into one file: \([my answer](https://stackoverflow.com/a/76203282/10668706)\)

```python
json_all = dict()
split = 4         # this is the 1-based actual number of splits

for i in range(1, split+1):
    with open(os.path.join("data_folder", "data_file_" + str(split) + "_" + str(i) + ".json"), 'r') as f:
        json_i = json.load(f)
        json_all.update(json_i)
```

## Objects

List all attributes \(\& methods\) of an object: \([credit](https://stackoverflow.com/a/48522820/10668706)\)

```python
for attr in dir(object_a):
    if not attr.startswith('_'):
        print(attr)
```

List all methods of an object: \([credit](https://stackoverflow.com/a/34452/10668706)\)

```python
for method in dir(object_a):
    if callable(getattr(object_a, method)) and (not method.startswith('_')):
        print(method)
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

## Print

### Bold

Ref: [How can I print bold text in Python? - Stack Overflow](https://stackoverflow.com/a/11784589/10668706)

```python
print("\033[1m" + "hello world" + "\033[0m")
```


## Pretty print

### Table

Ref: [python - Printing Lists as Tabular Data - Stack Overflow](https://stackoverflow.com/a/26937531/10668706)

TBA.


### JSON

Pretty print: \([credit](https://stackoverflow.com/a/12944035)\)

```python
import json

print(json.dumps(json.loads(json_data), indent=4))

# if get TypeError: the JSON object must be str, bytes or bytearray, not dict
# then use:
print(json.dumps(json_data, indent=4))
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
