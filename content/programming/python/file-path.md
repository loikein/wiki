---
weight: 400
title: "File System & Path"
---
> The following code has been adapted for use within Jupyter Lab.
> 
> Ref: [python 3.x - `__file__` does not exist in Jupyter Notebook - Stack Overflow](https://stackoverflow.com/questions/39125532/file-does-not-exist-in-jupyter-notebook)
{.book-hint .warning}

## Enumerate Files

The best library I have found for this use case is `glob`.

```python
import glob
```

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

    # find all md and txt files in the sub folder
    for file in [glob.glob(folder + "*.md"), glob.glob(folder + "*.txt")]:
        dict_all_files[folder].append(file)

# pretty print
print(json.dumps(dict_all_files, sort_keys=True, indent=4))
```

## Manipulate files

### Change file name; move file

Refs:

- [python - Recursively rename file extensions - Stack Overflow](https://stackoverflow.com/a/37016368)
- [subdirectory - Browse files and subfolders in Python - Stack Overflow](https://stackoverflow.com/a/5817256)
- [How to rename multiple files recursively using Python?](https://www.tutorialspoint.com/How-to-rename-multiple-files-recursively-using-Python)
- [python - Case insensitive replace - Stack Overflow](https://stackoverflow.com/questions/919056/case-insensitive-replace#comment94426519_919074)

```python
import os
import re

top_dir = "data"

for subdir, dirs, files in os.walk(top_dir):
    for filename in files:
        if filename.lower().find(" extra text") > 0:
            # get the path to your file
            file_path = os.path.join(subdir, filename)
            # create the new name
            new_file_path = re.sub(' extra text', '', file_path, flags=re.IGNORECASE) # create the new name, case insensitive
            # rename your file
            os.rename(file_path, new_file_path)
```

A more elaborated use case:

```python
import os

top_dir = "data"

for subdir, dirs, files in os.walk(top_dir):
    for filename in files:
        if filename.endswith(('.xlsx','.ods')):
            # get the path to your file
            file_path = os.path.join(subdir, filename)
            # get filename and file extension
            file_time, file_ext = filename.split(".")
            # the filename is a date in plain English, change it into ISO
            new_file_time = datetime.datetime.strptime(file_time, '%d %B %Y').strftime('%Y-%m-%d')
            # add back extension
            new_file_name = new_file_time + "." + file_ext
            # apply the new name + move path
            new_file_path = os.path.join(top_dir, new_file_name)
            # rename your file
            os.rename(file_path, new_file_path)
```

### Delete file

Ref: [python - Most pythonic way to delete a file which may not exist - Stack Overflow](https://stackoverflow.com/a/10840586)

```python
import os

try:
    os.remove("test.txt")
except OSError:
    pass
```

### Delete empty folders

Ref: [How to delete only empty folders in Python?](https://www.tutorialspoint.com/how-to-delete-only-empty-folders-in-python)

```python
import os

top_dir = "data"

for dirpath, dirnames, filenames in os.walk(top_dir, topdown=False):
    for dirname in dirnames:
        full_path = os.path.join(dirpath, dirname)
        if not os.listdir(full_path): 
            os.rmdir(full_path)
```
