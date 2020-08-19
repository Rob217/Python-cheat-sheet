# Python Cheat Sheet

This post is a collection of Python commands and recipes that I have found useful. This is an open post and I will keep updating it with new items.

## Misc Python

#### Timer

```python
import time
get_time = time.perf_counter
t0 = get_time()
### some code ###
t1 = get_time()
print('Time elapsed = {}'.format(t1 - t0))
```

#### Path names
```python
import os
pathname = os.path.join('dir1', 'dir2', 'filename')
# MacOS/Linux: dir1/dir2/filename
# Windows: dir1\dir2\filename
```


## NumPy
```python
import numpy as np
```

#### Modifying ndarray dimensions
Use ```np.tile()``` to add extra dimensions.
Use ```np.moveaxis()``` to exchange dimensions.
```python
>>> A = np.ones([2, 3])
>>> B = np.tile(A, [4, 5, 1, 1])
>>> B.shape()
[4, 5, 2, 3]
>>> C = np.moveaxis(B, [0, 1, 2, 3], [2, 3, 0, 1])
>>> C.shape()
[2, 3, 4, 5]
```


## Matplotlib

#### Nice figures
Loads and uses the functions and style sheets defined in the package [nice-figures](https://github.com/Rob217/nice-figures)
```python
from nice_figures import *

fig_sizes = load_style() # update rcParams, get figure size
cols = load_cols() # load dictionary of custom colours
add_numbering(ax, i=0, loc=(0.8, 0.8)) # add numbers to figure panels
add_border() # add border to figure
```

#### Useful rcParams
Here are some useful rcParams to remember:
```python
import maptlotlib as mpl
mpl.rcParams['figure.dpi'] = 200
```
