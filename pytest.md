# Testing with pytest

Some of the following examples are taken or adapted from [here](https://realpython.com/pytest-python-testing/).

## Basic usage

test.py:
```python
def add(a, b):
    return a + b

def test_add():
    assert add(3, 4) == 7
```
Then run 
```Shell
pytest # run all discovered tests
pytest test.py # run specific test
pytest test_dir/ # run all tests within directory
```

## Catch expected exceptions
```python
import pytest

def add_positive_numbers(a, b):
    if (a < 0) or (b < 0):
        raise ValueError('Inputs should not be negative')
    return a + b

def test_negative_input():
    with pytest.raises(ValueError, match='Inputs should not be negative'):
        add_positive_numbers(2, -1)
```
The match is unnecessary if just want to catch any ValueError.

## Test if approximately equal
See [documentation](https://docs.pytest.org/en/latest/reference.html#pytest-approx)
```python
>>> 1 + 1e-8 == pytest.approx(1)
True
>>> 1 + 1e-8 == approx(1, abs=1e-12) # set absolute tolerance (default = 1e-12)
False
>>> 1 + 1e-8 == approx(1, rel=1e-6, abs=1e-12) # set relative and absolute tolerance (default = 1e-6, 1e-12)
True
```

## Compare numpy arrays

```python
import numpy as np
np.testing.assert_array_equal(arr_a, arr_b)
```

## Fixtures

Use fixtures to save, e.g., underlying test data that will be used in multiple tests:
```python
import pytest

@pytest.fixture
def example_data():
    return (3, 4)

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def test_add(example_data):
    a, b = example_data
    assert add(a, b) == 7

def test_subtract(example_data):
    a, b = example_data
    assert subtract(a, b) == -1
```
If fixtures are going to be used in multiple test files, you can put them into a `conftest.py` file which `pytest` will automatically find and load (without needing to manually import anything).

## Marks
Use marks to select certain tests to run or not run (like keywords).

First you need to register custom marks in either a `pytest.ini` file:
```python
[pytest]
markers = 
    slow: marks tests as slow (deselect with '-m "not slow"')
    subtract
```
or as a `pytest_configure` hook in the test file (see [documenation](https://docs.pytest.org/en/stable/mark.html)).
Then inside the python file:
```python
import pytest

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

@pytest.mark.slow
def test_add_slow():
    for i in range(10000):
        assert add(5, i) == 5 + i

@pytest.mark.slow
@pytest.mark.subtract
def test_subtract_slow():
    for i in range(10000):
        assert subtract(5, i) == 5 - i

@pytest.mark.subtract
def test_substract():
    assert subtract(6, 2) == 4
```
In the Shell:
```Shell
pytest --markers # get list of available markers
pytest -m 'slow' # just tests marked as 'slow'
pytest -m 'not slow' # everything except tests marked as 'slow'
```

## Parametrization: repeat test for multiple inputs

Make a list of inputs for a given parameter:
```python
import pytest

def is_positive(a):
    if a > 0:
        return True
    else:
        return False

@pytest.mark.parametrize("positive_tests", [
    2,
    1e5,
    5.3,
])
def test_is_positive(positive_tests):
    assert is_positive(positive_tests)
```

Or for multiple input parameters:
```python
import pytest

def add(a, b):
    return a + b

@pytest.mark.parametrize("a,b,output", [
    (3, 4, 7),
    (-2, 3, 1),
    (3.4, 2.1, 5.5),
])
def test_add(a, b, output):
    assert add(a, b) == output
```

To reuse paramaters, need to define them separately, e.g.,
```python
import pytest

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

test_data = [(3, 4), (-2, 3), (3.4, 2.1)]

@pytest.mark.parametrize("a,b", test_data)
def test_add(a, b):
    assert add(a, b) == a + b

@pytest.mark.parametrize("a,b", test_data)
def test_subtract(a, b):
    assert subtract(a, b) == a - b
```

## Finding slowest tests

Find 3 slowest tests:
```Shell
pytest --durations=3
```

## Randomize test order

Tests ideally should be stand alone and not depend on each other. To test whether this is the case, use [`pytest-randomly`](https://github.com/pytest-dev/pytest-randomly)

## Coverage

To check how much of the python scripts are being tested, use the [`coverage`](https://coverage.readthedocs.io/en/coverage-5.2.1/) package.
