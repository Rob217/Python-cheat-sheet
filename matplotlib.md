# Matplotlib

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

#### Shade between lines
ax.fill_between(x, y1, y2)
