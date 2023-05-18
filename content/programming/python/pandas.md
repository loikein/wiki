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

{{< hint info >}}
Needs to have `odfpy` in the environment.
{{< /hint >}}

{{< hint warning >}}
Since `odfpy` does not have row selection method when loading files,
`nrows` option happens after the whole file is loaded into memory, unlike when dealing with other types of tables. This causes long loading time when the file is huge. See [pandas-dev/pandas Issue #53185](https://github.com/pandas-dev/pandas/issues/53185).
{{< /hint >}}

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


## DataFrame-level operations

### Rename indices

```python
df.index = df.index.set_names(["ID"])
```

### Filter rows conditioning on column value

```python
# only keep rows with certain value for a col
df_subset = df[df["Status Code"]=="A"]
```


## Export DataFrame

### As Excel file

```python
df.head(1000).to_excel(os.path.join("data", "data.xlsx"))
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
