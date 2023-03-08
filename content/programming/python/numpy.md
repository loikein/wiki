---
weight: 600
title: "Numpy"
---

# Numpy

## Array

Make array of five 0's:

```python
import numpy as np

y = np.tile(0, 5)
y

# array([0, 0, 0, 0, 0])
```

## Matrix

Make array of 1 \~ 100:

```python
import numpy as np

sigma = np.arange(1, 101).reshape(10, 10)
sigma

# array([[  1,   2,   3,   4,   5,   6,   7,   8,   9,  10],
#        [ 11,  12,  13,  14,  15,  16,  17,  18,  19,  20],
#        [ 21,  22,  23,  24,  25,  26,  27,  28,  29,  30],
#        [ 31,  32,  33,  34,  35,  36,  37,  38,  39,  40],
#        [ 41,  42,  43,  44,  45,  46,  47,  48,  49,  50],
#        [ 51,  52,  53,  54,  55,  56,  57,  58,  59,  60],
#        [ 61,  62,  63,  64,  65,  66,  67,  68,  69,  70],
#        [ 71,  72,  73,  74,  75,  76,  77,  78,  79,  80],
#        [ 81,  82,  83,  84,  85,  86,  87,  88,  89,  90],
#        [ 91,  92,  93,  94,  95,  96,  97,  98,  99, 100]])
```

Make array out of arbitrary numbers: \([taken from here](https://www.math.utah.edu/~zwick/Classes/Fall2012_2270/Lectures/Lecture33_with_Examples.pdf), a positive definite matrix\)

```python
import numpy as np

sigma = np.reshape((2, -1, 0, -1, 2, -1, 0, -1, 2), (3, 3))
sigma

# array([[ 2, -1,  0],
#        [-1,  2, -1],
#        [ 0, -1,  2]])
```

Make diagonal matrix: \([credit](https://stackoverflow.com/a/52989703/10668706)\)

```python
sigma = np.diagflat([-1] * 3)
sigma

# array([[-1,  0,  0],
#        [ 0, -1,  0],
#        [ 0,  0, -1]])
```

