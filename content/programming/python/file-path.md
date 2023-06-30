---
weight: 400
title: "File System & Path"
---

The best library I have found to handle file path is `glob`.

```python
import glob
```

## Enumerate Files

List all second level subfolders:

```python
list_sub = []

for folder in glob.glob("**/**/"):
    list_sub.append(folder)
```

List all subfolders recursively: \([credit](https://stackoverflow.com/a/57025016)\)

```python
list_sub_r = []

for folder in glob.glob("**/", recursive=True):
    list_sub_r.append(folder)
```

List all .md files in each subfolder, recursively:

```python
dict_all_files = {}

# for each folder
for folder in glob.glob("**/", recursive=True):
    dict_all_files[folder] = []

    # find all md files in the sub folder
    for file in glob.glob(folder + "*.md"):
        dict_all_files[folder].append(file)

# pretty print
print(json.dumps(dict_all_files, sort_keys=True, indent=4))
```
