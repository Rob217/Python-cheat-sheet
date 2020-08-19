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

#### pathnames
```python
import os
pathname = os.path.join('dir1', 'dir2', 'filename')
# MacOS/Linux: dir1/dir2/filename
# Windows: dir1\dir2\filename
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
