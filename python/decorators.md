# Decorators in python

### Higher Order Functions

A Higher-order function (HOF) in mathematics and computer science, is a function which does at least one of the following -

1. Takes one or more functions as arguments
2. Returns a function as a result

Decorators, in python, provide a simple syntax for calling higher-order functions. A decorator is a function which takes another function and extends the behavior of the latter without explicitly modifying it.


Python allows introspection i.e. the ability of an object to know about its own attribute at runtime.

```python
>>> print
<built-in function print>

>>> print.__name__
'print'

>>> help(print)
Help on built-in function print in module builtins:

print(...)
    <full help message>
```
After being decorated, the **introspection** get confusing

```python
def func_name(func):
  def wrapper_func_name():
    return func
  return wrapper_func_name


@func_name
def say_hello():
  print("hello")

def say_simple_hello():
  print("hello")

print(say_hello.__name__)  # prints: wrapper_func_name (this is confusing)
print(say_simple_hello.__name__)  # prints: say_simple_hello
```
To fix this, we can use `functiontools` wraps method which preserves the identity of the underlying function

```python
def func_name(func):
  @wraps(func)
  def wrapper_func_name():
    return func

  return wrapper_func_name

print(say_hello.__name__)  # prints: say_hello
print(say_simple_hello.__name__)  # prints: say_simple_hello
```

The `@functools.wraps` decorator uses the function `functools.update_wrapper()` to update special attributes like `__name__` and `__doc__` that are used in the introspection.