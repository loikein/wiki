# rpy2

## References

[rpy2 3.3.1 documentation](https://rpy2.github.io/doc/latest/html/index.html)

## Install with Anaconda/Miniconda

In `environment.yml`:

```yaml
dependencies:
  - r-base
  - r-r.utils
  - rpy2
  # (other r packages)
```

## Basic Use

Imports:

```python
import numpy as np
import rpy2.robjects.packages as rpackages
from rpy2 import robjects
from rpy2.robjects import numpy2ri
```

Import R modules:

```python
base = rpackages.importr("base")
stats = rpackages.importr("stats")
```

Install and load package:

```python
utils = rpackages.importr("utils")
utils.chooseCRANmirror(ind=1)

utils.install_packages("condMVNorm")
condMVNorm = rpackages.importr("condMVNorm")
```

## Python Object to R Object

Begin:

```python
numpy2ri.activate()
```

Make vector:

```python
vec1 = np.array([1.2, 2.5, 3.3])
vec1_r = robjects.FloatVector(vec1)

vec2 = np.array([1, 2, 3])
vec2_r = robjects.IntVector(vec2)
```

Make matrix:

```python
mat = np.arange(1, 10).reshape(3, 3)
mat_r = base.matrix(mat, 3, 3)
```

End:

```python
numpy2ri.deactivate()
```
