# Python

## Snippets

Find the index of minimum in a list: \([credit](https://stackoverflow.com/a/13301022/10668706)\)

```py
val, index = min((val, index) for (index, val) in enumerate(my_list))
```
