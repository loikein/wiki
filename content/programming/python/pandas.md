---
weight: 601
title: "Pandas"
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
    skiprows=1, # if there are pre-data rows
    header=[0,1], # if there are multiple (combined) header rows
    nrows=100, # only read first 100 rows
)
```

Read names of all sheets: \([credit](https://stackoverflow.com/a/17977609)\)

```python
import pandas as pd

xl = pd.ExcelFile(os.path.join("data", "data.xlsx"))
xl.sheet_names
```

Read all sheets: \([credit](https://stackoverflow.com/a/16896091)\)

{{< hint warning >}}
This is significantly slower than the method above. Only use when you actually need every single sheet.
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

### Filter rows conditioning on column value

```python
# only keep rows with certain value for a col
df_subset = df[df["Status Code"]=="A"]
```
