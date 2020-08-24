# NumPy
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

#### Save/load data (csv)
If want to read in other programmes and np.ndarray has at most two dimensions, can save as csv:
```python
data = np.array([1, 2, 3, 4])
np.savetxt('data.csv', data, delimiter=',') # save
data = np.loadtxt('data.csv', delimiter=',') # load
```

#### Save/load data (npy)
If np.ndarray has more than two dimensions and will only be loading in Python, use `np.save()`:
```python
data = np.ones([3, 4, 5])
np.save('data.npy', data)
data = np.load('data.npy')
```
