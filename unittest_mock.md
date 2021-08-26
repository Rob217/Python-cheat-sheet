# Unittest - mock and patch

This file contains various examples of how to mock and patch different objects/parameters in different ways.

The official documentation can be found [here](https://docs.python.org/3/library/unittest.mock.html).

## Examples

`module.py`:
```python
class Foo:
    foo = 123

    def __init__(self):
        self.att = 123

    @property
    def bar(self):
        return 123

    def func(self):
        return 123
```

`test.py`:
```python
import unittest
from unittest.mock import patch, Mock, PropertyMock
import module


class NewFoo:
    foo = 456


class FooPatchAtt(module.Foo):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.att = 456


class TestFoo(unittest.TestCase):

    def test_foo(self):
        self.assertEqual(module.Foo.foo, 123)
        self.assertEqual(module.Foo().att, 123)
        self.assertEqual(module.Foo().bar, 123)
        self.assertEqual(module.Foo().func(), 123)

    @patch('module.Foo', new=NewFoo)
    def test_patch_class_with_class(self):
        self.assertEqual(module.Foo, NewFoo)
        self.assertEqual(module.Foo.foo, 456)

    @patch('module.Foo')
    def test_patch_class_with_mock(self, mock_foo):
        self.assertEqual(module.Foo, mock_foo)
        module.Foo()
        mock_foo.assert_called()

    @patch('module.Foo.foo', new=456)
    def test_patch_class_attribute(self):
        self.assertEqual(module.Foo.foo, 456)

    @patch('module.Foo', new=FooPatchAtt)
    def test_patch_instance_attribute(self):
        self.assertEqual(module.Foo().att, 456)

    @patch('module.Foo.bar', new_callable=PropertyMock, return_value=456)
    def test_patch_property(self, mock_bar):
        self.assertEqual(module.Foo().bar, 456)

    @patch('module.Foo.func', new=Mock(return_value=456))
    def test_patch_function_with_mock(self):
        self.assertEqual(module.Foo().func(), 456)

    @patch('module.Foo.func', new=lambda *args, **kwargs: 456)
    def test_patch_function_with_func(self):
        self.assertEqual(module.Foo().func(), 456)


if __name__ == "__main__":
    unittest.main()
```

### Note on patching instance attributes
As explained in the documentation section on [autospeccing](https://docs.python.org/3/library/unittest.mock.html#autospeccing), if an attribute is defined solely in the `__init__` function, then autospeccing cannot find it since it only sees attributes defined by the class.

Solutions to this include defining a default value for every attribute in the class scope, creating a new class which can be used for autospeccing, or patching the class with a new class which overwrites the attributes manually (this is what is done in the above example).
