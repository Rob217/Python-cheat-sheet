# Unittest - mock and patch

This file contains various examples of how to mock and patch different objects/parameters in different ways.

The official documentation can be found [here](https://docs.python.org/3/library/unittest.mock.html).

## Examples

```python
import unittest
from unittest.mock import patch, Mock, PropertyMock


class Foo:
    foo = 123

    @property
    def bar(self):
        return 123

    def func(self):
        return 123


class NewFoo:
    foo = 456


class TestFoo(unittest.TestCase):

    def test_foo(self):
        self.assertEqual(Foo.foo, 123)
        self.assertEqual(Foo().bar, 123)
        self.assertEqual(Foo().func(), 123)

    @patch('__main__.Foo', new=NewFoo)
    def test_patch_class_with_class(self):
        self.assertEqual(Foo, NewFoo)
        self.assertEqual(Foo.foo, 456)

    @patch('__main__.Foo')
    def test_patch_class_with_mock(self, mock_foo):
        self.assertEqual(Foo, mock_foo)
        Foo()
        mock_foo.assert_called()

    @patch('__main__.Foo.foo', new=456)
    def test_patch_attribute(self):
        self.assertEqual(Foo.foo, 456)

    @patch('__main__.Foo.bar', new_callable=PropertyMock, return_value=456)
    def test_patch_property(self, mock_bar):
        self.assertEqual(Foo().bar, 456)

    @patch('__main__.Foo.func', new=Mock(return_value=456))
    def test_patch_function_with_mock(self):
        self.assertEqual(Foo().func(), 456)

    @patch('__main__.Foo.func', new=lambda *args, **kwargs: 456)
    def test_patch_function_with_func(self):
        self.assertEqual(Foo().func(), 456)


if __name__ == "__main__":
    unittest.main()
```
