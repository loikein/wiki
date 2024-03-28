---
weight: 301
title: "Performance"
---
I rarely stop to think about performance, but my computer is getting very old and slow for the things I want to do very quickly, so here we go \(again\).

<!-- ## \(Maybe\) Useful resources

- [Python Performance Tuning: 20 Simple Tips - Stackify](https://stackify.com/20-simple-python-performance-tuning-tips/)
- ~~[PythonSpeed/PerformanceTips - Python Wiki](https://wiki.python.org/moin/PythonSpeed/PerformanceTips)~~ -->


## Parallel: `joblib`

Doc: [joblib.Parallel — joblib 1.4.dev0 documentation](https://joblib.readthedocs.io/en/latest/generated/joblib.Parallel.html)

Explanation of `n_jobs`:

> The maximum number of concurrently running jobs, such as the number of Python worker processes when `backend="multiprocessing"` or the size of the thread-pool when `backend="threading"`. If `-1` all CPUs are used. If `1` is given, no parallel computing code is used at all, and the behavior amounts to a simple python for loop. \[…\] Thus for `n_jobs = -2`, all CPUs but one are used. `None` is a marker for ‘unset’ that will be interpreted as `n_jobs=1` unless the call is performed under a `parallel_config()` context manager that sets another value for `n_jobs`.

### Single loop

Ref: [parallel processing - How do I parallelize a simple Python loop? - Stack Overflow](https://stackoverflow.com/a/50926231/10668706)

```python
from joblib import Parallel, delayed

def func(i):
    return i * i
    
results = Parallel(n_jobs=2)(delayed(process)(i) for i in range(10))
print(results)  # prints [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### Multiple looping items

Ref: [parallel processing - Parallelize these nested for loops in python - Stack Overflow](https://stackoverflow.com/a/41270442/10668706)

Implementing [geographical distance calculation](/programming/python/geo-plots/#distance) between all combinations of a list of locations.

Performance gain: It took 3 seconds to run the outside loop once. The Parallel job finished under 2 minutes for `len(places_df.index)=1000` with `n_jobs=3`.

```python
import numpy as np
import pandas as pd
from joblib import Parallel, delayed
from itertools import product

def distance(i, j):
    # This is a loop-turned function just for the parallelisation,
    # not a real practical function.
    list_all = []
    globe = cgeo.Geodesic()

    # for i in range(len(places_df.index)):
    lon_home = places_df.iloc[i]["longitude"]
    lat_home = places_df.iloc[i]["latitude"]
    # list_row = []

    # for j in range(len(places_df.index)):
    lon_aim = places_df.iloc[j]["longitude"]
    lat_aim = places_df.iloc[j]["latitude"]

    list_all.append(
        (globe.inverse([lon_home, lat_home], [lon_aim, lat_aim]).T[0]/1000)[0]
    )
    # list_all.append(list_row)
    return list_all

results = Parallel(n_jobs=-1)(delayed(distance)(i, j) for i, j in product(range(len(places_df.index)), range(len(places_df.index))))
len(results)
# 1000000

distance_matrix = pd.DataFrame(
    np.reshape(results, (len(places_df.index), len(places_df.index))),
    index=places_df.index,
    columns=places_df.index,
)
```


## JIT: `numba.jit`

Doc: [Compiling Python code with @jit — Numba 0+untagged.2155.g9ce83ef.dirty documentation](https://numba.readthedocs.io/en/stable/user/jit.html)

Gist: add `@jit(nopython=True)` decorator before function definitions. I recall that that some functions cannot be used in `nopython` mode, but cannot remember exactly which ones.
