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
pytest
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
