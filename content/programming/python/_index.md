---
bookCollapseSection: true
title: "Python"
---
## \(Maybe\) Useful resources

- [Gallery of Jupyter Books - Executable Books](https://executablebooks.org/en/latest/gallery/)
- [The Hitchhiker’s Guide to Python](https://docs.python-guide.org/)
- [nkmk/python-snippets](https://github.com/nkmk/python-snippets)
- [satwikkansal/wtfpython](https://github.com/satwikkansal/wtfpython)
- [Python Tutorials – Data to Fish](https://datatofish.com/python-tutorials/)
- [Intermediate Python — Python Tips 0.1 documentation](https://book.pythontips.com/en/latest/index.html#)
    + Repository: [yasoob/intermediatePython](https://github.com/yasoob/intermediatePython)
- [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
    + Repository: [jakevdp/PythonDataScienceHandbook](https://github.com/jakevdp/PythonDataScienceHandbook)
- [Python - CopyProgramming](https://copyprogramming.com/t/python)
- [Coding for Economists](https://aeturrell.github.io/coding-for-economists/intro.html)
    + Repository: [aeturrell/coding-for-economists](https://github.com/aeturrell/coding-for-economists)
- [Python Cookbook 3rd Edition 中文版](https://python3-cookbook.readthedocs.io/zh-cn/latest/index.html)
    + Repo: [yidao620c/python3-cookbook](https://github.com/yidao620c/python3-cookbook)
- [R you ready for Python?](https://shiny.abdn.ac.uk/Stats/R_Python_tutorial/index.html) \(R/Python integration\)
- [nkmk note](https://note.nkmk.me/en/) \(in English & Japanese\)
- [Python Plotting for Exploratory Analysis](https://pythonplot.com/) \(compares code of the same graphs produced by Pandas/Matplotlib/Seaborn/plotnine/plotly/Altair/ggplot2\)
    - Repository: [tdhopper/pythonplot.com](https://github.com/tdhopper/pythonplot.com)
- [Plotly Open Source Graphing Libraries](https://plotly.com/graphing-libraries/)
- [Data Science for Energy System Modelling](https://fneum.github.io/data-science-for-esm/intro.html)


## File handling

### CSV

> This section focuses on the Python module `csv`. For the package `pandas`, see [Pandas](/programming/python/pandas/).
{.book-hint .info}

Docs: [csv — CSV File Reading and Writing — Python 3.11.4 documentation](https://docs.python.org/3/library/csv.html)

Import as list: \([Ref](https://stackoverflow.com/a/24662707/10668706)\)

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

### JSON

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

### Dictionary

#### Append

```python
new_dict = {}
new_dict.update({"name": number})
```

#### Head

Get head of a dictionary: \([credit](https://stackoverflow.com/a/28704691)\)

```python
from itertools import islice

dict(islice(my_dict.items(), 0, 5))
```

#### Loop

```python
# key only
for key in my_dict:
    print(key)

# value only
for value in my_dict.values():
    print(value)

# key-value
for key, value in my_dict.items():
  print(key, value)
```

#### Search

Keys:

```python
if key in my_dict:
    # ...
```

### List

Doc: [5. Data Structures — Python 3.12.2 documentation](https://docs.python.org/3/tutorial/datastructures.html)

#### Find index of

Find the index of minimum in a list: \([credit](https://stackoverflow.com/a/13301022/10668706)\)

```python
val, index = min((val, index) for (index, val) in enumerate(my_list))
```

#### Find n-th element

```python
# first
my_list[0]

# last
my_list[-1]

# middle
# https://stackoverflow.com/questions/38130895/find-middle-of-a-list#comment105177234_38131003
my_list[int(len(my_list)//2)]
```

#### Export to file

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

#### Sort

```python
my_list = ["B", "C", "D"]
my_list.sort()
print(my_list)
# ['B', 'C', 'D']
```

### Pickle

See [Writing functions #Dark magic](/programming/python/writing-functions/#dark-magic) for the wrapper function version.

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

### String

#### Add leading zeros

Ref: [python - Best way to format integer as string with leading zeros? - Stack Overflow](https://stackoverflow.com/a/733478)

```python
year = [2015]
month = list(range(1, 13))

for y in year:
    for m in month:
        print(str(y) + "_" + str(m).zfill(2))
```

This gives the exact same output as below, but exposes year and month variables to tinker with: \([ref](https://stackoverflow.com/a/59755426)\)

```python
import pandas as pd

pr = pd.period_range(start='2015-01',end='2015-12', freq='M')
for period in pr:
    print(period)
```


## Print

Refs:

- [7. Input and Output — Python 3.12.2 documentation](https://docs.python.org/3/tutorial/inputoutput.html)
- [A Guide to the Newer Python String Format Techniques – Real Python](https://realpython.com/python-formatted-output/)

### Bold

Ref: [How can I print bold text in Python? - Stack Overflow](https://stackoverflow.com/a/11784589/10668706)

```python
print("\033[1m" + "hello world" + "\033[0m")
```

### Table

Ref: [python - Printing Lists as Tabular Data - Stack Overflow](https://stackoverflow.com/a/26937531/10668706)

TBA.

### JSON/Dictionary

Pretty print: \([credit](https://stackoverflow.com/a/12944035)\)

> `json.dumps()` does not work if there are keys with type `int32`.
{.book-hint .warning}

```python
import json

print(json.dumps(json.loads(json_data), indent=4))

# if get TypeError: the JSON object must be str, bytes or bytearray, not dict
# then use:
print(json.dumps(json_data, indent=4))
```


## Statements

### Loop

Parallel iteration:

> `zip` only goes through the shortest list given.
{.book-hint .warning}

```python
lower = [a, b, c]
upper = [A, B, C]

for l, u in zip(lower, upper):
    print(f"{l} = {u}")
```

Cartesian product of lists:

```python
import itertools

year = [2015]
month = list(range(1, 13))

for period in itertools.product(year, month):
    print(period)
```

### Match case \(Switch\)

> This is [new feature in Python 3.10](https://docs.python.org/3/whatsnew/3.10.html).
{.book-hint .info}

Regex match I use to import some badly headered datasets: \([ref](https://stackoverflow.com/a/75089993)\)

```python
import re

class RegexEqual(str):
    def __eq__(self, pattern):
        return bool(re.match(pattern, self))

def usecols_fn(col):
    match RegexEqual(col):
        case "ID":
            return True
        case "[A-z\s]*Date":
            return True
        case "[A-z\s]*Rating":
            return True
    return False

df = pd.read_excel(
    "data.xlsx",
    sheet_name="Sheet 1",
    usecols=usecols_fn,
    index_col="ID",
)
```


## Useful tricks

### Docstring/Help

Like R's `?` function.

```python
help(np.log)

# If it is a method, need something that the method can run from:
help(df.reset_index)
```

### `functools.partial`

Ref: [python - How does functools partial do what it does? - Stack Overflow](https://stackoverflow.com/a/15331841/10668706)

### `lambda` functions


### List attributes

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

### Ternary conditional operator

Ref: [Does Python have a ternary conditional operator? - Stack Overflow](https://stackoverflow.com/a/394814)
