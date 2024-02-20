---
weight: 601
title: "Pandas"
description: "Real problems and real solutions."
---
## Most important notes

`axis: {0 or ‘index’ (rows), 1 or ‘columns’}, default 0`

## \(Maybe\) Useful resources

- [Cookbook — pandas 2.1.0 documentation](https://pandas.pydata.org/docs/user_guide/cookbook.html)

## Import Data

### Dict/JSON

Doc: [pandas.DataFrame.from_dict — pandas 1.3.5 documentation](https://pandas.pydata.org/pandas-docs/version/1.3/reference/api/pandas.DataFrame.from_dict.html)

For dict like `{"id1": data1, "id2": data2, ...}`:

```python
df = pd.DataFrame.from_dict(
    data_dict,
    orient='index',
    columns=["data"],   # otherwise very troublesome to rename later
)
df.index = df.index.set_names(["ID"])
```

For dict like: `{"row1": [...], "row2": [...], ...}`, and JSON files:

```python
df = pd.DataFrame.from_dict(
    data_json
).transpose()
```


### Excel

Doc: [pandas.read_excel — pandas 2.0.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html)

> Extra dependency: `openpyxl`
{.book-hint .info}

Read sheet:

```python
import pandas as pd

df = pd.read_excel(
    os.path.join("data", "data.xlsx"),  # read ./data/data.xlsx
    sheet_name="Sheet 1",
    skiprows=1,                         # if there are pre-data rows
    header=[0,1],                       # if there are multiple (combined) header rows
    nrows=100,                          # only read first x rows
    usecols=["ID", "Rating", "Date"],   # only import certain columns
    index_col="Location ID",            # set index as soon as import
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

> This is significantly slower than the `pd.ExcelFile` method above. Only use when you actually need every single sheet.
{.book-hint .warning}

```python
import pandas as pd

dfs = pd.read_excel(file_name, sheet_name=None)
dfs.keys() # similar result as xl.sheet_names
```

#### Custom `usecol` function for fuzzy column names

See [Python #Match case \(Switch\)](/programming/python/#match-case-switch)

### CSV/TSV

#### Pandas

Doc: [pandas.read_csv — pandas 2.0.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html)

```python
import pandas as pd

names_list = ["col 1", "col 2", "col 3"]

df = pd.read_csv(
    os.path.join("data", "data.csv"), # read ./data/data.csv
    # sep='\t',                       # if tsv
    # quotechar="'",                  # if see extra quotation marks after import
    header=None,
    index_col=[0, 1],                 # can use names if given
    names=names_list,
    usecols=[0, 1, 2, 3],             # can use names if given
    dtype={"Phone number": "str"},    # read columns as type
    nrows=100,                        # only read first 100 rows
)
```

#### CSV module

See [Python #CSV](/programming/python/#csv).

### ODS

#### `pandas-ods-reader`

> Extra dependency: [`pandas-ods-reader`](https://github.com/iuvbio/pandas_ods_reader/tree/master), [`ezodf`](https://github.com/T0ha/ezodf), and `lxml`
{.book-hint .info}

> The newest code on GitHub supports `skiprows`, but not `nrows`. However, the pip version does not support `skiprows` yet. To get it, download and use the development version of the package.
{.book-hint .warning}

This is by far the fastest method, if you know the sheet name.

```python
import pandas as pd
from pandas_ods_reader import read_ods

df = read_ods(
    os.path.join("data", "data.ods"),   # read ./data/data.ods
    sheet=2,                            # get 2nd sheet (1 based), default 1
    # or
    sheet="sheet 1",                    # get sheet by name
    skiprows=1,                         # only works if you have the development version
    columns=["ID", "Rating", "Date"]    # this is NOT usecols!! it renames the columns, and truncates the sheet if list is shorter than # of columns
)

# Simulate usecols callable
usecols = pd.array([usecols_fn(col) for col in df.columns], dtype="boolean")
df = df.loc[:, usecols]
```

#### `pd.read_excel`

> Extra dependency: [`odfpy`](https://github.com/eea/odfpy)
{.book-hint .info}

> Since `odfpy` does not have row selection method when loading files,
`nrows` option happens after the whole file is loaded into memory, unlike when dealing with other types of tables. This causes long loading time when the file is huge. See [pandas-dev/pandas Issue #53185](https://github.com/pandas-dev/pandas/issues/53185).
{.book-hint .warning}

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

### Stata dta

#### `pd.read_stata`

Convert \(all\) categorical to strings \(objects\):

> This will use up significantly more memory compared to the second method below.
{.book-hint .warning}

```python
import pandas as pd

data_path = os.path.join("data", "data.dta")

df = pd.read_stata(
    data_path,
    convert_categoricals=False,
)

with pd.io.stata.StataReader(data_path) as sr:
    value_labels = sr.value_labels()

for col in df:
    if col in value_labels:
        df[col].replace(value_labels[col], inplace=True)
```

#### `pd.io.stata.StataReader`

When getting `ValueError: Value labels for column col_x are not unique. These cannot be converted to pandas categoricals. The repeated labels are: Not applicable`, I found this alternative way of doing the import by excessive digging into the \(not documented any more\) methods.

It may be easier if you have access to Stata and can do the cleaning up in Stata first. See: [python - Stata to Pandas: even if there are repeated Value Labels? - Stack Overflow](https://stackoverflow.com/a/46038793/10668706)

More detailed explanation: [python - Loading STATA file: Categorial values must be unique - Stack Overflow](https://stackoverflow.com/a/77236478/10668706)

Docs:

- [IO tools (text, CSV, HDF5, …) — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/user_guide/io.html)
- [pandas.read_stata — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.read_stata.html#pandas-read-stata)

**Step 1**: read the Stata file with the io reader.

```python
import pandas as pd

df_reader = pd.io.stata.StataReader(
    os.path.join("data", "data.dta"),
)
```

**Step 2**: Verify the repeated labels.

```python
print(df_reader.value_labels()["col_x"])

# {...
#  -1: 'Not applicable',
#  ...
#  6: 'Not applicable'}
```

**Step 3**: Replace the repeated value with something else.

```python
df_reader.value_labels()["col_x"][6] = "Not applicable (1)"
```

**Step 4**: Read the file from reader.

```python
df = df_reader.read()
```

Done!

Since [it is said in code that](https://github.com/pandas-dev/pandas/blob/v2.1.1/pandas/io/stata.py#L1121) `Using StataReader as a context manager is the only supported method`, this is the context manager version:

```python
import pandas as pd

data_path = os.path.join("data", "data.dta")

with pd.io.stata.StataReader(path) as sr:
    value_labels = sr.value_labels()
    # print(value_labels["col_x"])
    # ...
    value_labels["col_x"][6] = "Not applicable (1)"
    # ...
    df = sr.read()
```


## Export DataFrame

### As Excel/ODS file

> Extra dependency: `openpyxl` or `odfpy`
{.book-hint .info}

```python
df.to_excel(os.path.join("data", "data.xlsx"))
df.to_excel(os.path.join("data", "data.ods"))

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


## Debugging

### Import

If get `UnicodeDecodeError: 'utf-8' codec can't decode byte 0x92 in position xx: invalid start byte`, try: \([credit](https://stackoverflow.com/a/46000253)\)

```python {hl_lines="3"}
df = pd.read_csv(
    os.path.join("data", "data.csv"), # read ./data/data.csv
    encoding="cp1252",
)
```


### Calculation

If get `TypeError: unhashable type: 'numpy.ndarray'`, it means one \(or more\) of the cells contain list value \(instead of single value\).

Get a subset of all rows containing list-value cells:

```python
df_subset = df[df["Average"].apply(lambda x: isinstance(x, np.ndarray))]
```

### Index

If get `ValueError: Index contains duplicate entries, cannot reshape`, it means there are duplicate indices sets (rows where all indices are identical).

First [check the rows contain same data](/programming/python/pandas/#list-rows-with-duplicated-values-of-indices), then [drop rows with duplicate indices](/programming/python/pandas/#drop-things).

---

`PerformanceWarning: DataFrame is highly fragmented` could happen after a concat, when no index is present in all sub-dfs, but somehow there are still repeated indices. Try the following:

```python
df = df.reset_index()
df = df.drop(["index"], axis=1)
```


## Observe things

### Calculate bivariate correlation coefficients and p-values matrix

Ref: [python - pandas columns correlation with statistical significance - Stack Overflow](https://stackoverflow.com/a/55166951/10668706)

```python
import numpy as np
import pandas as pd
from scipy.stats import pearsonr

# Correlation coefficients: (same)
corr = df.corr() 
corr = df.corr(method=lambda x, y: pearsonr(x, y)[0]) 

# p-values:
p_val = df.corr(method=lambda x, y: pearsonr(x, y)[1]) - np.eye(len(df.columns))
# p_val = p_val.round(decimals=4)
```

### Calculate mode by any level of MultiIndex

Ref: [python - GroupBy pandas DataFrame and select most common value - Stack Overflow](https://stackoverflow.com/questions/15222754/groupby-pandas-dataframe-and-select-most-common-value)

> So far I haven't found any way to get this mode df [merge/join/concat/etc](https://pandas.pydata.org/docs/user_guide/merging.html) with the original df, except first pivot the original df.
{.book-hint .warning}

> `mode` could return a list of values. Make sure to check the type of your modes before proceeding to other tasks.
{.book-hint .warning}

```python
# mode of each ID
df.groupby(["ID"]).agg(lambda x: x.mode())

# mode of each ID x each date
df.groupby(["ID","Date"]).agg(lambda x: x.mode())
```

### Calculate sum of all columns or rows

```python
# sum of all rows, by column
df.sum(axis=0)

# sum of all columns, by row
df.sum(axis=1)
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
#      ... 
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

### Find the n-th largest and smallest number

Ref: [python - How to extract the n-th maximum/minimum value in a column of a DataFrame in pandas? - Stack Overflow](https://stackoverflow.com/a/48026477/10668706)

```python
# full list of largest n and smallest n
df["col"].nlargest(3)
df["col"].nsmallest(3)

# only the single point
df["col"].nlargest(3).iloc[[-1]]
df["col"].nsmallest(3).iloc[[-1]]
```

### List all columns

Ref: [python - How to show all columns' names on a large pandas dataframe? - Stack Overflow](https://stackoverflow.com/a/49189503/10668706)

For huge databases, best to refer to its data manual.

```python
# Cut off after 1,000 columns
print(df.columns.tolist())

# Shows everything, slow:
with pd.option_context("display.max_columns", None):
    print(df.head())
```

### List all unique values of a column

Ref: [python - print the unique values in every column in a pandas dataframe - Stack Overflow](https://stackoverflow.com/a/27241331/10668706)

```python
print(df["Status Code"].unique())
```

To sort the unique values, use: \(`dropna` in case there is NaN\)

```python
sorted(df["Status Code"].dropna().unique())
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

### List rows with NaN in certain columns

Ref: [python - How to check if any value is NaN in a Pandas DataFrame - Stack Overflow](https://stackoverflow.com/a/47377251/10668706)

```python
df[df["Bad column"].isnull()]
```


## Select columns \(filter\)

### By name

```python
# must use double brackets
df_subset = pd.DataFrame(df[['col1']])
df_subset = pd.DataFrame(df[['col1', 'col2', ...]])
```

### By name with RegEx

Credit: [python - How to select columns from dataframe by regex - Stack Overflow](https://stackoverflow.com/a/30808571/10668706)

```python
rating_cols = df.filter(regex=("rating_*")).columns

# then when need to use
df[rating_cols]                     # returns a small df
df[rating_cols]["rating_2021_1"]    # returns a series
```

### By column type

Doc: [pandas.DataFrame.select_dtypes — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.select_dtypes.html)

```python
# See type of all columns
df.dtypes

# Only get columns of float type
df_subset = df.select_dtypes("float")
```

## Select rows \(filter\)

### By index

Doc: [pandas.DataFrame.loc — pandas 2.1.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html)

```python
df.loc["A0001"]
```

### By column value

With boolean indexing:

```python
# only keep rows with certain value for a col
df_subset = df[df["Status Code"]=="A"]

# only keep rows without certain value for a col
df_subset = df[df["Status Code"]!="B"]

# only keep rows with a certain starting
# https://stackoverflow.com/a/17958424/10668706
df_subset = df[df["Name"].str.startswith("One d", na=False)]

# especially, for nan values:
df_subset = df[df["Status Code"].isna()]
df_subset = df[df["Status Code"].notna()]
```

With query:

> When the value of some cells are lists, pandas will raise `ValueError: The truth value of an array with more than one element is ambiguous. Use a.any() or a.all()`. In that case, try this method instead:
> 
> Credit: [python - How do I select rows from a DataFrame based on column values? - Stack Overflow](https://stackoverflow.com/a/46165056/10668706)
{.book-hint .warning}

Also see: [Calculate average of columns with many filters (conditions)](#calculate-average-of-columns-with-many-filters-conditions)

```python
# only keep rows with certain value for a col
# https://stackoverflow.com/a/50697599
df_subset = df.query('`Status Code` == "A"')

# only keep rows with certain value for a col
df_subset = df.query('`Status Code` != "B"')

# no backticks for single word columns
df_subset = df.query('Date != 2015')

# multiple conditions
df_subset = df.query('Date != 2015 & `Status Code` == "A"')
```

Also see: \(not tested\)

- [python - Pandas filter data frame rows by function - Stack Overflow](https://stackoverflow.com/a/75839871)
- [python - Pandas filtering not working - Stack Overflow](https://stackoverflow.com/a/47420094)

### By column value from another DataFrame

Ref: [python - pandas - filter dataframe by another dataframe by row elements - Stack Overflow](https://stackoverflow.com/a/33282617)

The core idea is to get a list of index (from another DataFrame), and use the index list to filter the original DataFrame.

This extra column is not within the original DataFrame, the only thing they need to have in common is the index.

With boolean indexing:

```python
i_q_0_258 = df_q_sum[(df_q_sum['q'] < 258) & (df_q_sum['q'] >0)].index

# old way of subsetting
df_q_0_258  = df[df.index.isin(i_q_0_258)]
# new way of subsetting
df_q_0_258 = df.loc[i_q_0_258]

len(df_q_0_258)
# 41
```

With query:

```python
i_q_0_258 = df_q_sum.query('q < 258 & q > 0').index

# old way of subsetting
df_q_0_258  = df[df.index.isin(i_q_0_258)]
# new way of subsetting
df_q_0_258 = df.loc[i_q_0_258]

len(df_q_0_258)
# 41
```

### By cell type in column

Credit: [python - Select row from a DataFrame based on the type of the object(i.e. str) - Stack Overflow](https://stackoverflow.com/a/39277211/10668706)

```python
# only keep rows with certain types of value
df_subset = df[df["Rating"].apply(lambda x: isinstance(x, float))]

# or the opposite
df_subset = df[df["Rating"].apply(lambda x: not isinstance(x, float))]
```

### Select \(mask\) triangle of DataFrame

[python - Melt the Upper Triangular Matrix of a Pandas Dataframe - Stack Overflow](https://stackoverflow.com/a/40391559/10668706)

```python
corr = df.corr()

# k=1 for dropping diagonal, k=0 for keeping it
keep = np.triu(corr, k=1).astype('bool').reshape(corr.size)
# or for tril, k=-1 for dropping diagonal, k=0 for keeping it
keep = np.tril(corr, k=-1).astype('bool').reshape(corr.size)

corr_flat = corr.stack()[keep].reset_index()
corr_flat.columns = ["x1","x2","Coef"]
```

After this, can do a `sns.kdeplot(data=corr_flat,x="Coef")` to see the kernel density of all the coefficients.


## Groupby

Doc: [pandas.DataFrame.groupby — pandas 2.1.1 documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)

### Calculate average of columns with many filters \(conditions\)

```python
import pandas as pd

# Condition: A=Yes or B=Yes
# For and conditions, use &
df_subset = hse_micro.query('A == "Yes" | B == "Yes"')

# For every possible combination of C and D,
# get average of AGE and YEAR
df_subset.groupby([["C", "D"]])[["AGE", "YEAR"]].mean()
```

### Groupby column names \(custom `groupby` function\)

Use case: get average columns across multiple columns with similar names.

Ref: [python - Automatically grouping multiple columns with similar names in a pandas data frame - Stack Overflow](https://stackoverflow.com/a/31929037)

**Step 0**: Consider list of groups

```python
groups = ["AAA", "BBB", ...]
len(groups)
# 18
```

**Step 1**: Write groupby function

```python
def groupby_fn(col):
    groups = ["AAA", "BBB", ...]

    col_group = col.replace("Rating_", "").split("0")[0]

    if col_group in groups:
        return col_group    # Mark col as col_group
    else:
        return "Others"     # Mark col as Others
```

**Step 2**: Get columns to group by \(optional\)

```python
cols = df.filter(regex=("Rating_*")).columns
```

**Step 3**: Groupby

```python
df_grouped = df.groupby(groupby_fn, axis=1).mean()

# Or if used Step 2:
df_grouped = df[cols].groupby(groupby_fn, axis=1).mean()

# Check no col was marked as Others, otherwise check groupby function
len(df_grouped.columns)
# 18
```

Done!


## Column-level operations

### Convert number to range categories

Use case: one column of various numbers => one column of ranges in words.

#### Method 1: empty column

Ref: [python - How to add an empty column to a dataframe? - Stack Overflow](https://stackoverflow.com/a/16327135)

```python
df["q_groups"] = ""

# Note: this used to be: df[(df["q_sum"]>=434)]["q_groups"]
# But newer versions of pandas will raise warning
df.loc[(df["q_sum"]>=434), "q_groups"] = "Q>=434"
df.loc[(df["q_sum"]>=289) & (df["q_sum"]<434), "q_groups"] = "289<=Q<434"
df.loc[(df["q_sum"]>=258) & (df["q_sum"]<289), "q_groups"] = "258<=Q<289"
df.loc[(df["q_sum"]<258), "q_groups"] = "Q<258"
```

#### Method 2: boolean columns

**Step 1**: get range booleans \([credit](https://stackoverflow.com/a/26830867/10668706)\)

The new column names here will be the name of ranges.

```python
df["Q>=434"] = (df["q_sum"] >= 434)
df["289<=Q<434"] = (df["q_sum"] >= 289) & (df["q_sum"] < 434)
df["258<=Q<289"] = (df["q_sum"] >= 258) & (df["q_sum"] < 289)
df["Q<258"] = (df["q_sum"] < 258)
```

**Step 2**: make backup df (skip if no other columns are boolean)

```python
q_groups = df.copy(deep=True)
q_groups = df.drop(["q_sum", ...], axis=1) # drop all other columns
```

**Step 3**: make one column \([credit](https://stackoverflow.com/a/46754885/10668706)\)

```python
q_groups_col = q_groups.eq(True).dot(q_groups.columns + ',').str.rstrip(',')
```

**Step 4**: merge back

```python
df["q_groups"] = q_groups_col
```

Done!

### Convert type of columns

Inspect column types:

```python
df.info()
```

To numeric:

```python
# float
df["Rating"] = df["Rating"].astype('float')

# auto
df["Rating"] = pd.to_numeric(df["Rating"])
```

To string:

```python
df = df.astype("string")

df = df.astype({"col1": "string", "col2": "float", ... })  # need quotes
df = df.astype(dict(col1="string", col2="float", ...))     # no quotes
```

To category:

```python
from pandas.api.types import CategoricalDtype

rate_type = CategoricalDtype(
    categories=["No rating", "Bad", "Good", "Outstanding"],
    ordered=True,
)

df["Rating"] = df["Rating"].astype(rate_type)
```

With inline functions:

```python
# datetime to string
df["Date"] = [ cell.strftime("%Y") for cell in df["Date"] ]


df["Location ODS Code"] = [str(val) for val in df["Location ODS Code"]]
df["Service / Population Group"] = [str(val) for val in df["Service / Population Group"]]
df["Domain"] = [str(val) for val in df["Domain"]]
```

### Combine multiple columns

Refs: 

- [python - Combine two columns of text in pandas dataframe - Stack Overflow](https://stackoverflow.com/a/36911306/10668706)
- [python - pandas combine two strings ignore nan values - Stack Overflow](https://stackoverflow.com/a/33158556/10668706)

```python
data["Address"] = data["Address Line 1"].fillna("")

for col in ["Address Line 2", "Address Line 3", "Address Line 4", "Address Line 5", "Postcode"]:
    data["Address"] = data["Address"].astype(str) + " " + data[col].fillna("").astype(str)
```

### Fill NA with certain values

Ref: [python - Pandas dataframe fillna() only some columns in place - Stack Overflow](https://stackoverflow.com/a/38134049/10668706)

```python
df[["a", "B"]] = df[["a", "B"]].fillna(value="Something")
```

### Get column-wise delta \(difference\)

Docs:

- [pandas.DataFrame.diff — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.diff.html)
- [pandas.DataFrame.pct_change — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.pct_change.html)

```python
# numerical changes
df_diff = df.diff(axis=1)             # first column empty
df_diff = df.diff(periods=2, axis=1)  # first two columns empty

# percentage change
df_diff_pct = df.pct_change(axis=1)             # first column empty
df_diff_pct = df.pct_change(periods=2, axis=1)  # first two columns empty
```

<!-- ### Normalise a column

Refs: 

- [python - How to normalize a numpy array to a unit vector - Stack Overflow](https://stackoverflow.com/a/51512965/10668706)
- [python - Normalize columns of a dataframe - Stack Overflow](https://stackoverflow.com/a/57067342/10668706)

> If `np.linalg.norm(df["col"])` returns `nan`, check if there are `nan` values in the column. \([Ref](https://github.com/JustGlowing/minisom/issues/51#issuecomment-557906393)\)
{.book-hint .info}

```python
df_new = df[~df["Score"].isna()]
x = df_new["Score"]
df_new["Score_norm"] = x/np.linalg.norm(x)
``` -->

### Reorder columns

Ref: [python - How to change the order of DataFrame columns? - Stack Overflow](https://stackoverflow.com/a/13148611/10668706)

```python
# Take the last column to first
cols = df.columns.tolist()
cols = cols[-1:] + cols[:-1]
df = df[cols]
```


## Index-level operations

Unset indices:

```python
# return all indices back to normal columns
df = df.reset_index()

# return only selected indices
df = df.reset_index(level=["Status", "Level", ...])
```

Set new indices:

```python
df = df.set_index(["ID", ...])
```


## DataFrame-level operations

### Combine two DataFrames

Docs: 

- [Merge, join, concatenate and compare — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/user_guide/merging.html)
- [pandas.DataFrame.merge — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html)
- [pandas.concat — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.concat.html)
- [pandas.DataFrame.join — pandas 2.1.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.join.html)

#### Concat \(same columns\)

\(Stack\):

```python
df_AB = pd.concat([df_A, df_B])
```

Make all column names upper case or lower case: \([credit](https://stackoverflow.com/a/18305185)\) \(also see: [lower case for cell values](https://stackoverflow.com/questions/29761915/case-insensitive-pandas-dataframe-merge)\)

```python
# should also work on pd.merge, not tested

df_AB = pd.concat(
    [df_A.rename(columns=str.lower),
    df_B.rename(columns=str.lower)]
)

df_AB = pd.concat(
    [df_A.rename(columns=str.upper),
    df_B.rename(columns=str.upper)]
)
```

#### Join  \(same indices\)

> Always use index to join. Do not use `on="Data col"` when performing join, pandas will raise `ValueError: You are trying to merge on object and int64 columns. If you wish to proceed you should use pd.concat`.  
> If you do not want to modify the original df, use `df_AB = df_A.set_index("col").join(df_B.set_index("col"))`.
{.book-hint .info}

> You can join single-indexed DataFrame with MultiIndex DataFrame using this commend, but it must be approached very carefully. When the single shared index has different values, aka, `outer` does not equal `inner`, the join function returns an error.
> 
> Possible methods:
> 
> 1. Make the MultiIndex DataFrame single-indexed first. First use commands like `df_multi_index.index.set_names` and `df_multi_index.reset_index(level=[<all non-shared indices>])`.
> 2. Avoid `how="outer"`. If the MultiIndex DataFrame is left, use `how="left"` and `on="<shared_single_index>"`.
{.book-hint .warning}

With two parts:

```python
df_AB = df_A.join(
    df_B,                       # Or [df_B, df_C, ...]
    how="outer",                # Keep all different index values
    lsuffix="A", rsuffix="B",   # if get ValueError: columns overlap 
)
```

If want to select only one column of the left df, will return `AttributeError: 'Series' object has no attribute 'join'`. In this case, do:

```python {hl_lines="1"}
df_AB = df_A[["Rating"]].join(
    df_B,
    how="inner",
)
```

With a single list of DataFrames: \(index is `ID`\) \([credit](https://stackoverflow.com/a/38089112)\)

```python
df = reduce(lambda x, y: pd.merge(x, y, on="ID"), df_list)
```


### Drop things

Rows with duplicate indices:

Doc: [Duplicate Labels — pandas 2.1.0 documentation](https://pandas.pydata.org/docs/user_guide/duplicates.html)

Credit: [python - Remove pandas rows with duplicate indices - Stack Overflow](https://stackoverflow.com/questions/13035764/remove-pandas-rows-with-duplicate-indices)

```python
df.index.is_unique
# False

# Look at content of all duplicated index
df[df.index.duplicated()]

# Drop all rows with duplicated index but the first instance
df = df[~df.index.duplicated(keep='first')]
```

Columns:

```python
df = df.drop(["drop", ...], axis=1)
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

Refer to [index debugging](#index) when in trouble.

Result:

```text
            CODE  A-1        A-2          ...
            LEVEL B-1    B-2 B-1   B-3    ...
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


### Loop over rows

Ref: [python - How to iterate over rows in a DataFrame in Pandas - Stack Overflow](https://stackoverflow.com/a/16476974/10668706)

Docs:

- [pandas.DataFrame.iterrows — pandas 2.1.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.iterrows.html)
- [pandas.Series.items — pandas 2.1.0 documentation](https://pandas.pydata.org/docs/reference/api/pandas.Series.items.html)

> `row["new_col"]` does not work within the loops.
> 
> Doc:
> 
> > You should **never modify** something you are iterating over. This is not guaranteed to work in all cases. Depending on the data types, the iterator returns a copy and not a view, and writing to it will have no effect.
{.book-hint .danger}

```python
for ind, row in qof_perc.iterrows():
    print("\033[1m" + "ind:" + "\033[0m" + "\n")
    print(ind)              # A0001
    
    print("\n" + "\033[1m" + "row:" + "\033[0m" + "\n")
    print(row)              # pd.series
    
    # print(row["column1"])   # value of df.loc["A0001"]["column1"]
    
    print("\n" + "\033[1m" + "cells:" + "\033[0m" + "\n")
    for cell in row.items():
        print(cell[0])      # column name
        print(cell[1])      # cell value

    break
```

### Loop over list of DataFrames

Ref: [python - Pandas Loop through list of Data Frames and Change Index - Stack Overflow](https://stackoverflow.com/a/44631098/10668706)

Things would fail or stop operating after first iteration if use `for df in list`. Write instead:

```python
for i, df in enumerate(df_list):
    # ...
```

### Rename things

Index columns:

```python
df.index = df.index.set_names(["ID"])
```

Normal columns:

```python
df = df.rename(columns={"A": "a", "B": "c"})

# or (no quotation marks)
df = df.rename(columns=dict(A="a", B="c"))
```

By column index \(for `None` columns that are otherwise helpless\): \([ref](https://stackoverflow.com/a/41096634/10668706)\)

```python
df.columns.values[0] = "Safe"
```

Batch rename columns:

```python
# with string operation
df = df.rename(columns=lambda x: x.replace("_FINAL", ""))
df = df.rename(columns=lambda x: x+"_PERC")

# with regex
# https://stackoverflow.com/a/26500249/10668706
import re

df = df.rename(columns=lambda x: re.sub(" $", "", x))
```

Custom regex rename function: \(inspired by [ref](https://stackoverflow.com/a/75089993), also see [Python #Match case \(Switch\)](/programming/python/#match-case-switch)\)

```python
import re

class RegexEqual(str):
    def __eq__(self, pattern):
        return bool(re.match(pattern, self))

def rename_fn(col):
    match RegexEqual(col):
        case "[A-z\s]*Date":
            return "Date"
        case "Previous Rating": # Checks something more specific
            return "Previous"
        case "[A-z\s]*Rating":  # Then a fuzzy check
            return "Rating"
    return col                  # otherwise could get None columns
```

### Find \& replace in all cells

Credit: [python - How to replace a value in pandas, with NaN? - Stack Overflow](https://stackoverflow.com/a/29251086/10668706)

```python
df["rating"] = df["rating"].replace("No ratings", np.NaN)
```

Using dictionary: \([credit](https://stackoverflow.com/a/49259581/10668706)\)

```python
replace = {"No ratings": np.NaN}

df["rating"].map(replace)
# Or (slower, but also works in a loop)
df["rating"].replace(replace, inplace=True)
```

### Sort things

Rows by values in columns:

```python
df = df.sort_values(["ID","level"])
```

Rows by index values:

```python
df = df.sort_index()
```

Columns by column names: ([credit](https://stackoverflow.com/a/11067072/10668706))

```python
df = df.reindex(sorted(df.columns), axis=1)
```
