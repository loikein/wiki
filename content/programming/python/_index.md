# Python

## Snippets

Find the index of minimum in a list: \([credit](https://stackoverflow.com/a/13301022/10668706)\)

```python
val, index = min((val, index) for (index, val) in enumerate(my_list))
```

Benchmarking:

more readings: [performance - How to measure elapsed time in Python? - Stack Overflow](https://stackoverflow.com/questions/7370801/how-to-measure-elapsed-time-in-python)

```python
import time

# use round() if only the first digit is necessary
start = time.time()

# ...

end = time.time()
elapsed = end - start
print(elapsed)
```
