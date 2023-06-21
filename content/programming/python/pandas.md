---
weight: 601
title: "Pandas"
description: "Real problems and real solutions."
---

# Pandas

## Import Data

### Excel

Doc: [pandas.read_excel — pandas 2.0.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html)

{{< hint info >}}
Needs to have `openpyxl` in the environment.
{{< /hint >}}

Read sheet:

```python
import pandas as pd

df = pd.read_excel(
    os.path.join("data", "data.xlsx"), # read ./data/data.xlsx
    sheet_name="Sheet 1",
    skiprows=1,   # if there are pre-data rows
    header=[0,1], # if there are multiple (combined) header rows
    nrows=100,    # only read first 100 rows
)
```

Read names of all sheets: \([credit](https://stackoverflow.com/a/17977609)\)

```python
import pandas as pd

xl = pd.ExcelFile(os.path.join("data", "data.xlsx"))
xl.sheet_names           # list of sheet names

df = xl.parse("Sheet 1") # if need sheets
```

Read all sheets: \([credit](https://stackoverflow.com/a/16896091)\)

{{< hint warning >}}
This is significantly slower than the `pd.ExcelFile` method above. Only use when you actually need every single sheet.
{{< /hint >}}

```python
import pandas as pd

dfs = pd.read_excel(file_name, sheet_name=None)
dfs.keys() # similar result as xl.sheet_names
```

### CSV

Doc: [pandas.read_csv — pandas 2.0.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html)

```python
import pandas as pd

names_list = ["col 1", "col 2", "col 3"]

df = pd.read_csv(
    os.path.join("data", "data.csv"), # read ./data/data.csv
    header=None,
    names=names_list,
    dtype={"Phone number": "str"},    # read columns as type
)
```

### ODS

#### `pandas-ods-reader`

{{< hint info >}}
Needs to have [`pandas-ods-reader`](https://github.com/iuvbio/pandas_ods_reader/tree/master), `ezodf`, and `lxml` in the environment.
{{< /hint >}}

{{< hint warning >}}
Supports `skiprows`, but not `nrows`.
{{< /hint >}}

```python
import pandas as pd
from pandas_ods_reader import read_ods

df = read_ods(
    os.path.join("data", "data.ods"), # read ./data/data.ods
    2,                                # get 2nd sheet (1 based), default 1
    # or
    "sheet 1",                        # get sheet by name
)
```

#### `pd.read_excel`

{{< hint info >}}
Needs to have `odfpy` in the environment.
{{< /hint >}}

{{< hint warning >}}
Since `odfpy` does not have row selection method when loading files,
`nrows` option happens after the whole file is loaded into memory, unlike when dealing with other types of tables. This causes long loading time when the file is huge. See [pandas-dev/pandas Issue #53185](https://github.com/pandas-dev/pandas/issues/53185).
{{< /hint >}}

Slightly faster \(and more robust\) method:

```python
import pandas as pd

ods = pd.ExcelFile(os.path.join("data", "data.ods"))
ods.sheet_names   # get all sheet names

df = ods.parse("sheet 1")
```

Documented method:

```python
import pandas as pd

df = pd.read_excel(
    os.path.join("data", "data.ods"), # read ./data/data.ods
)
```

### Debugging

If get `UnicodeDecodeError: 'utf-8' codec can't decode byte 0x92 in position xx: invalid start byte`, try: \([credit](https://stackoverflow.com/a/46000253)\)

```python
df = pd.read_csv(
    os.path.join("data", "data.csv"), # read ./data/data.csv
    encoding="cp1252",
)
```

## Observe things

### Calculate mode by any level of MultiIndex

Ref: [python - GroupBy pandas DataFrame and select most common value - Stack Overflow](https://stackoverflow.com/questions/15222754/groupby-pandas-dataframe-and-select-most-common-value)

{{< hint warning >}}
So far I haven't found any way to get this mode df [merge/join/concat/etc](https://pandas.pydata.org/docs/user_guide/merging.html) with the original df, except first pivot the original df.
{{< /hint >}}

```python
# mode of each ID
df.groupby(["ID"]).agg(lambda x: x.mode())

# mode of each ID x each date
df.groupby(["ID","Date"]).agg(lambda x: x.mode())
```

### Count length of levels of MultiIndex

Ref: [python - Hierarhical Multi-index counts in Pandas - Stack Overflow](https://stackoverflow.com/a/51405700/10668706) 

```python
df.groupby(level=["ID"]).size()
df.groupby(level=["ID","Date"]).size()

# example output:
# ID
# 01    240
# 02    240
# 03    240
# 04    240
# 05    240
#      ... 
# 55    211
# 56    211
# 57    211
# 59    211
# 60    211
# Length: 60, dtype: int64
```

### Display full width of a DataFrame

Ref:

- [python - How can I display full (non-truncated) dataframe information in HTML when converting from Pandas dataframe to HTML? - Stack Overflow ](https://stackoverflow.com/a/64155503/10668706)
- [Python, Pandas : write content of DataFrame into text File - Stack Overflow](https://stackoverflow.com/a/58070237/10668706)

```python
# method 1
with pd.option_context('display.max_colwidth', None):
  display(df)

# method 2
print(df.to_string())
```

### List all unique values of a column

Ref: [python - print the unique values in every column in a pandas dataframe - Stack Overflow](https://stackoverflow.com/a/27241331/10668706)

```python
print(df["Status Code"].unique())
```

### List rows with duplicated values of a column

Ref: [How do I get a list of all the duplicate items using pandas in python? - Stack Overflow](https://stackoverflow.com/a/41786821/10668706)

```python
df[df.duplicated(["ID"], keep=False)].sort_values("ID")
```

### List rows with duplicated values of indices

```python
df[df.index.duplicated(keep='first')]
```


## Select things

### Select columns with RegEx

Credit: [python - How to select columns from dataframe by regex - Stack Overflow](https://stackoverflow.com/a/30808571/10668706)

```python
rating_cols = df.filter(regex=("rating_*")).columns

# then when need to use
df[rating_cols]                     # returns a small df
df[rating_cols]["rating_2021_1"]    # returns a series
```


## Column-level operations

### Combine multiple columns

Refs: 

- [python - Combine two columns of text in pandas dataframe - Stack Overflow](https://stackoverflow.com/a/36911306/10668706)
- [python - pandas combine two strings ignore nan values - Stack Overflow](https://stackoverflow.com/a/33158556/10668706)

```python
data["Address"] = data["Address Line 1"].fillna("")

for col in ["Address Line 2", "Address Line 3", "Address Line 4", "Address Line 5", "Postcode"]:
    data["Address"] = data["Address"].astype(str) + " " + data[col].fillna("").astype(str)
```

## Index-level operations

Unset indices:

```python
# return all indices to normal columns
df = df.reset_index()

# return only selected indices
df = df.reset_index(level=["Status", "Level"])
```

Rename index:

```python
df.index = df.index.set_names(["ID", "Address"])
```

## DataFrame-level operations

### Combine two DataFrames

With same columns (stack):

```python
df_AB = pd.concat([df_A, df_B])
```

With same indices (join):

{{< hint warning >}}
It is said by some people online that you can join single-indexed DataFrame with MultiIndex DataFrame using this commend, which is not correct (at least not stable). When the single shared index has different values, aka, `outer` does not equal `inner`, the join returns an error.

To avoid this, first use commands like `df_multi_index.index.set_names` and `df_multi_index.reset_index(level=[<all non-shared indices>])` to make the MultiIndex DataFrame single-indexed first, then perform the join.
{{< /hint >}}

```python
df_AB = df_A.join(
    df_B,
    how="outer",    # Keep all different index values
)
```

### Drop rows with duplicate indices

Credit: [python - Remove pandas rows with duplicate indices - Stack Overflow](https://stackoverflow.com/questions/13035764/remove-pandas-rows-with-duplicate-indices)

```python
df = df[~df.index.duplicated(keep='first')]
```

### Filter rows conditioning on column value

```python
# only keep rows with certain value for a col
df_subset = df[df["Status Code"]=="A"]

# only keep rows without certain value for a col
df_subset = df[df["Status Code"]!="B"]
```

### Long to wide

Reverse of [pandas.wide_to_long — pandas 2.0.2 documentation](https://pandas.pydata.org/docs/reference/api/pandas.wide_to_long.html).

For example, say you have a very long MultiIndex DataFrame like this (asterisk means index column):

```text
                       VALUE
ID      CODE   LEVEL               
*A0001* *A-1*  *B-1*   96.0
               *B-2*   5.0
        *A-2*  *B-1*   18.0
               *B-2*   18.0
               *B-3*   1.0
        *A-3*  ...
...
```

But want you really want is one ID per row, with everything in the row.

**Step 1:**

```python
df_unstack = df.stack().unstack(level=['CODE', 'LEVEL']) 
```

Which has almost identical effects as (but this one returns only one index)

```python
df_unstack = pd.pivot(
    df.reset_index(),
    index="ID",
    columns=["CODE", "LEVEL"],
    values="VALUE",
)
```

{{< hint info >}}
If get `ValueError: Index contains duplicate entries, cannot reshape`, it means that there are duplicate indices sets (rows where all indices are identical).

In that case, first [check the rows contain same data](/programming/python/pandas/#list-rows-with-duplicated-values-of-indices), then do [#Drop rows with duplicate indices](/programming/python/pandas/#drop-rows-with-duplicate-indices). Now the pivot should work just fine.
{{< /hint >}}

Result:

```text
            CODE  A-1        A-2          ...
            LEVEL B-1    B-2 B-1   B-2    ...
ID      (unnamed)
*A0001* *VALUE*    96.0  5.0  18.0  18.0 
*A0002* *VALUE*   505.0  5.0 182.0 191.0 
*A0003* *VALUE*   275.0  5.0 156.0 159.0 
*A0004* *VALUE*   245.0  5.0  72.0  72.0 
*A0005* *VALUE*   377.0  5.0 196.0 196.0 
```

**Step 2:**

```python
df_unstack.columns = ['_'.join(col) for col in df_unstack.columns]
```

{{< details "If want to do this to index" >}}
This code also works for index:

```python
df.index = ['_'.join(ind) for ind in df.index]
```

But need to make sure all values in the indices are strings. If not, try first convert:

```python
df = df.reset_index()

df["Level"] = [str(val) for val in df["Level"]]
# or if values are timestamps
df["Date"] = [val.strftime("%Y-%m-%d") for val in df["Date"]]
```
{{< /details >}}

Result:

```text
                  A-1_B-1 A-1_B-2 A-2_B-1 ...
ID      (unnamed)
*A0001* *VALUE*    96.0   5.0      18.0
*A0002* *VALUE*   505.0   5.0     182.0
*A0003* *VALUE*   275.0   5.0     156.0
*A0004* *VALUE*   245.0   5.0      72.0
*A0005* *VALUE*   377.0   5.0     196.0
```

**Step 3:**

If you have used `pd.pivot`, skip this step.

```python
df_unstack.index = df_unstack.index.set_names(["ID", "drop"])   # give the second index a name
df_unstack = df_unstack.reset_index(level=["drop"])             # un-index
df_unstack = df_unstack.drop("drop",axis=1)                     # remove
```

Result:

```text
      A-1_B-1 A-1_B-2 A-2_B-1 ...
ID
A0001  96.0   5.0      18.0
A0002 505.0   5.0     182.0
A0003 275.0   5.0     156.0
A0004 245.0   5.0      72.0
A0005 377.0   5.0     196.0
```

Done!

### Rename things

Index column:

```python
df.index = df.index.set_names(["ID"])
```

Normal column:

```python
df = df.rename(columns={"A": "a", "B": "c"})
```

### Replace cells by value

Credit: [python - How to replace a value in pandas, with NaN? - Stack Overflow](https://stackoverflow.com/a/29251086/10668706)

```python
df["rating"] = df["rating"].replace("No ratings", np.NaN)
```

### Sort things

Rows by values in columns:

```python
df = df.sort_values(["ID","level"])
```

Columns by column names: ([credit](https://stackoverflow.com/a/11067072/10668706))

```python
df = df.reindex(sorted(df.columns), axis=1)
```


## Export DataFrame

### As Excel file

```python
df.to_excel(os.path.join("data", "data.xlsx"))
# or if the df is too big
df.iloc[:1000, :1000].to_excel(os.path.join("data", "data.xlsx"))
```

### As plain text file

Ref: [Python, Pandas : write content of DataFrame into text File - Stack Overflow](https://stackoverflow.com/questions/31247198/python-pandas-write-content-of-dataframe-into-text-file)

```python
# method 1
df.to_csv(os.path.join("data", "data.txt"))

# method 2
with open(os.path.join("data", "data.txt"), "w") as f:
    f.write(df.to_string())
```
