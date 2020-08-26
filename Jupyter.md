# Jupyter lab/notebooks

#### Inline figures
```Jupyter Notebook
%matplotlib inline
```

#### Timer
```Jupyter Notebook
%timeit some_function()
```

#### PEP8 code style checking
To check code against the [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/#blank-lines) can use the [`pycodestyle`](https://pypi.org/project/pycodestyle/) or [`flake8`](https://pypi.org/project/flake8/) modules (see links for installation).

1. Install pycodestyle_magic
```Shell
pip install flake8 pycodestyle_magic
```
2. Inside notebook cell (see [pycodestyle_magic notes](https://github.com/mattijn/pycodestyle_magic)):
```Jupyter Notebook
%load_ext pycodestyle_magic
%pycodestyle_on
%pycodestyle_off
```
