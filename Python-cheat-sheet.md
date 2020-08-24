# Python Cheat Sheet

This post is a collection of Python commands and recipes that I have found useful. This is an open post and I will keep updating it with new items.

# Table of contents
1. [Misc Python](#MiscPython)
2. [Virtual Environments](#VirtualEnvironments)
3. [NumPy](#NumPy)
4. [Matplotlib](#Matplotlib)

## Misc Python <a name="MiscPython"></a>

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

#### Executing in terminal
To run ```script.py``` you can use the following terminal command:
```bash
python script.py
```
However, if you want to run it as an executable file without calling the ```python``` command, just add the following text to the head of ```script.py```:
```python
#!/usr/bin/env python
# coding: utf-8
```
Then you can run the script using
```bash
./script.py
```

#### Packages
Useful resources:
- https://packaging.python.org/tutorials/packaging-projects/
- https://kiwidamien.github.io/making-a-python-package.html
- https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56

Load package from inside directory:
```bash
python -m pip install .
```

Reload package (e.g., if made edits):
```bash
python -m pip install --upgrade --force-reinstall ..
```

## Virtual environments <a name="VirtualEnvironments"></a>
Useful resources:
- https://packaging.python.org/tutorials/installing-packages/
- https://www.youtube.com/watch?v=N5vscPTWKOk

Steps for creating and using a virtual environment:
1. Create a directory in which your virtual environment is going to be stored, e.g., ```test_env_dir```
```bash
> mkdir test_env_dir
> cd test_env_dir
```
2. Inside that directory, create a new virtual environment using the ```virtualenv``` package
```bash
> python -m virtualenv test_env
```
3. Activate this new environment
```bash
> test_env/Scripts/activate
```
4. Notice now that `[test_env]` is at the start of the command line indicating you are in the new environment and can load and install Python packages as required.
```bash
(test_env) >
```
5. To exit the virtual environment type:
```bash
(test_env) > deactivate
```


## NumPy <a name="NumPy"></a>
```python
import numpy as np
```

#### Modifying ndarray dimensions
Use ```np.tile()``` to add extra dimensions.
Use ```np.moveaxis()``` to exchange dimensions.
```python
>>> A = np.ones([2, 3])
>>> B = np.tile(A, [4, 5, 1, 1])
>>> B.shape
(4, 5, 2, 3)
>>> C = np.moveaxis(B, [0, 1, 2, 3], [2, 3, 0, 1])
>>> C.shape
(2, 3, 4, 5)
```

#### Slicing ndarrays without losing dimensions
The following index slice loses a dimension from the ndarray:
```python
>>> a = np.ones([5, 4, 1])
>>> b = a[:, 0, :]
>>> b.shape
(4, 1)
```
To keep the same dimension structure, use this instead:
```python
>>> c = a[:, [0], :]
>>> c.shape
(4, 1, 1)
```
This might occur if assigning one array to another with a variable dimension size which may be 1.

#### Random numbers
See https://numpy.org/doc/stable/reference/random/index.html?highlight=random#module-numpy.random for updated methods
```python
from numpy.random import default_rng
rng = default_rng(5)
vals = rng.standard_normal(10) # standard deviation with shape (10,)
vals = rng.random((10, 2, 4)) # uniform distribution with shape (10, 2, 4)
```
`default_rng(n)` initialized the seed using the integer n, ensuring reproducability. If left blank, will initialize with random seed.

## Matplotlib <a name="Matplotlib"></a>

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
```

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
mpl.rcParams['figure.dpi'] = 200
```

#### Colorbars
```python
c_bar = plt.colorbar()
c_bar.set_label('colorbar label')
```

#### Get and set object attributes (e.g., color, ...)
Use ```plt.getp(object_handle)``` and ```plt.setp(object_handle)``` (see [here](https://matplotlib.org/3.1.0/gallery/misc/set_and_get.html))
```python
>>> line, = ax.plot(x, y, color='r')
>>> plt.getp(line) # lists all available attributes
agg_filter = None
alpha = None
animated = False
...
>>> plt.getp(line, 'color') # get color attribute
'r'
>>> plt.setp(line, color='b', linewidth=2) # set color and linewidth
>>> line.get_color() # sometime specific functions exist for getting specific attributes
'b'
```

#### Figure title with subplots
E.g., https://matplotlib.org/gallery/images_contours_and_fields/image_nonuniform.html#sphx-glr-gallery-images-contours-and-fields-image-nonuniform-py
```python
fig, axs = plt.sublots(2, 2, constrained_layout=True)
fig.suptitle('Figure title')
```
Note that it is important to set ```constrained_layout=True``` otherwise title may overlap with subplots.

#### Stacking order of plots
Use ```zorder``` to control which lines appear on top of which, with ```zorder < 0``` appearing behind ```zorder > 0```, e.g.,
```python
ax.plot(x, y, zorder = 10) # appears in front
ax.plot(x, y, zorder = -5) # appears behind
```
