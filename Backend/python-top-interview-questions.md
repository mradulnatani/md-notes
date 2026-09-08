Absolutely. Below is a **Top 100 Python interview questions with answers**, written for interview preparation rather than textbook theory. I’ll keep the answers concise enough to remember, but detailed enough to explain them in an interview.

# Python Top 100 Interview Questions & Answers

## 1. Python Fundamentals

### 1. What is Python?

Python is a **high-level, general-purpose, dynamically typed programming language**. It supports multiple programming paradigms, including procedural, object-oriented, and functional programming.

Its major advantages are readability, a large standard library, portability, and a huge ecosystem of third-party packages.

---

### 2. What are the main features of Python?

Important features include:

* Easy and readable syntax
* Dynamically typed
* Interpreted/bytecode-executed
* Object-oriented
* Cross-platform
* Automatic memory management
* Large standard library
* Supports functional and procedural programming
* Large third-party ecosystem

---

### 3. Why is Python called an interpreted language?

Python source code is generally compiled into **bytecode**, which is then executed by the Python virtual machine.

For example:

```python
x = 10
print(x)
```

The `.py` source is converted into bytecode, typically represented in `__pycache__`, and executed by the Python runtime.

So saying "Python is interpreted" is a simplification; CPython actually performs **compilation to bytecode followed by interpretation/execution**.

---

### 4. Is Python dynamically typed or statically typed?

Python is **dynamically typed**.

You don't have to explicitly declare the type of a variable.

```python
x = 10
x = "hello"
```

The same variable name can refer to objects of different types during execution.

Python is also **strongly typed**, meaning it generally doesn't perform arbitrary implicit conversions between incompatible types.

---

### 5. What is duck typing?

Duck typing means Python determines whether an object is suitable based on **what operations it supports**, rather than its explicit type.

```python
class Dog:
    def speak(self):
        print("Bark")

class Person:
    def speak(self):
        print("Hello")

def make_speak(obj):
    obj.speak()
```

Both objects can be passed to `make_speak()` because both provide `speak()`.

The idea is:

> If it behaves like a duck, Python can treat it like a duck.

---

### 6. What is the difference between Python 2 and Python 3?

Python 3 is the modern version and Python 2 is obsolete.

Some differences:

```python
# Python 3
print("Hello")
```

Python 3 also has:

* Unicode strings by default
* Better exception handling
* Improved standard library
* `range()` behaves as a lazy sequence
* Different division behavior

Python 2 reached **end-of-life in 2020**.

---

### 7. What are Python's built-in data types?

Common built-in types include:

```text
int
float
complex
bool
str
list
tuple
set
frozenset
dict
bytes
bytearray
NoneType
```

Example:

```python
x = 10
name = "Mradul"
numbers = [1, 2, 3]
user = {"name": "Mradul"}
```

---

### 8. What is the difference between mutable and immutable objects?

A **mutable object can be modified after creation**.

Examples:

```python
list
dict
set
```

An **immutable object cannot be modified after creation**.

Examples:

```python
int
float
str
tuple
frozenset
```

Example:

```python
x = "hello"
x = x + " world"
```

The original string wasn't modified. A new string was created.

---

### 9. Which Python data types are mutable?

The most important mutable built-in types are:

```text
list
dict
set
bytearray
```

Example:

```python
numbers = [1, 2, 3]
numbers.append(4)
```

The same list object has been modified.

---

### 10. Which Python data types are immutable?

Common immutable types include:

```text
int
float
bool
str
tuple
frozenset
bytes
complex
```

---

### 11. What is type casting?

Type casting means converting an object from one type to another.

```python
x = "100"

y = int(x)
z = float(x)
```

Here:

```text
"100" → int → 100
"100" → float → 100.0
```

---

### 12. What is the difference between `is` and `==`?

`==` compares **values**.

`is` compares **object identity**.

```python
a = [1, 2]
b = [1, 2]

print(a == b)   # True
print(a is b)   # False
```

Both lists contain the same values but are different objects.

Use `is` particularly when checking for `None`:

```python
if value is None:
    ...
```

---

### 13. What is `None` in Python?

`None` represents the absence of a value.

Its type is:

```python
type(None)
```

which gives:

```text
<class 'NoneType'>
```

Example:

```python
result = None
```

It is commonly used when a function doesn't return a meaningful value.

---

### 14. What are truthy and falsy values?

Python allows objects to be evaluated as Boolean values.

Falsy examples include:

```python
False
None
0
0.0
""
[]
{}
set()
()
```

Most other objects are truthy.

Example:

```python
if []:
    print("True")
else:
    print("False")
```

Output:

```text
False
```

---

### 15. What is variable scope?

Scope determines where a variable can be accessed.

Python primarily follows:

```text
Local
Enclosing
Global
Built-in
```

This is called the **LEGB rule**.

---

### 16. Explain local, global and nonlocal variables.

```python
x = 10       # global

def func():
    y = 20   # local
```

`global` allows modification of a global variable:

```python
x = 10

def func():
    global x
    x = 20
```

`nonlocal` allows modification of a variable from an enclosing function:

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20
```

---

### 17. What is the LEGB rule?

Python searches for variables in this order:

**L → E → G → B**

```text
Local
Enclosing
Global
Built-in
```

For example, when Python encounters:

```python
print(x)
```

it searches these scopes in that order.

---

### 18. What is garbage collection?

Garbage collection is the process of automatically reclaiming memory occupied by objects that are no longer reachable.

Python primarily uses **reference counting**, supplemented by a cyclic garbage collector.

---

### 19. What is reference counting?

Every Python object maintains a count of references pointing to it.

```python
x = [1, 2, 3]
y = x
```

Now both `x` and `y` reference the same object.

When an object's reference count reaches zero, CPython can generally reclaim it immediately.

---

### 20. What is the GIL?

The **Global Interpreter Lock (GIL)** in standard CPython allows only one thread at a time to execute Python bytecode within a process.

This means CPU-bound Python threads generally don't achieve true parallel execution of Python bytecode.

However, threads are still useful for **I/O-bound work**, such as:

* Network requests
* File operations
* Database operations

For CPU-bound work, multiprocessing or other approaches can provide parallelism.

---

# 2. Strings

### 21. Are Python strings mutable?

No.

Strings are immutable.

```python
s = "hello"
```

You cannot modify an individual character:

```python
s[0] = "H"   # TypeError
```

Instead, a new string must be created.

---

### 22. What is string slicing?

Slicing extracts a portion of a sequence.

```python
s = "Python"

print(s[0:3])
```

Output:

```text
Pyt
```

Syntax:

```python
sequence[start:stop:step]
```

Example:

```python
s[::-1]
```

reverses the string.

---

### 23. How do you reverse a string?

Using slicing:

```python
s = "Python"
reverse = s[::-1]
```

Output:

```text
nohtyP
```

---

### 24. How do you check whether a string is a palindrome?

```python
s = "madam"

if s == s[::-1]:
    print("Palindrome")
```

---

### 25. What is the difference between `split()` and `join()`?

`split()` converts a string into a list.

```python
"hello world".split()
```

Result:

```python
["hello", "world"]
```

`join()` combines strings.

```python
" ".join(["hello", "world"])
```

Result:

```text
hello world
```

---

### 26. What are f-strings?

F-strings provide a convenient way to insert expressions into strings.

```python
name = "Mradul"
age = 22

print(f"My name is {name} and I am {age}")
```

They were introduced in Python 3.6.

---

### 27. What is the difference between `str()` and `repr()`?

`str()` is intended for a **human-readable representation**.

`repr()` is intended to provide a more **developer-oriented/unambiguous representation**.

Example:

```python
x = "hello"

print(str(x))
print(repr(x))
```

Conceptually:

```text
hello
'hello'
```

---

### 28. How do you remove whitespace from a string?

```python
s = "  hello  "

s.strip()    # both sides
s.lstrip()   # left
s.rstrip()   # right
```

---

### 29. How do you count occurrences in a string?

```python
s = "banana"

print(s.count("a"))
```

Output:

```text
3
```

---

### 30. How do you check whether a string contains a substring?

```python
s = "Hello Python"

if "Python" in s:
    print("Found")
```

---

# 3. Lists, Tuples, Sets and Dictionaries

### 31. What is a list?

A list is an **ordered, mutable collection**.

```python
numbers = [1, 2, 3, 4]
```

It can contain different types:

```python
data = [10, "hello", 3.14, True]
```

---

### 32. List vs tuple?

| List                          | Tuple                           |
| ----------------------------- | ------------------------------- |
| Mutable                       | Immutable                       |
| `[]`                          | `()`                            |
| Generally more flexible       | Generally more memory-efficient |
| More methods for modification | Fewer methods                   |

Example:

```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
```

---

### 33. Why are tuples generally faster than lists?

Tuples are immutable, so Python can use a simpler representation and doesn't need to support operations that modify the collection.

As a result, tuples are generally more memory-efficient and can be slightly faster for iteration/access.

Don't claim that tuples are **always** faster; the difference depends on the operation.

---

### 34. What is a set?

A set is an **unordered collection of unique hashable elements**.

```python
s = {1, 2, 3, 3}

print(s)
```

Result:

```text
{1, 2, 3}
```

Sets are useful for membership testing and removing duplicates.

---

### 35. Why doesn't a set contain duplicates?

A set is implemented using hash-table-based machinery.

When an element is inserted, Python uses its hash and equality semantics to determine whether an equivalent element is already present.

Therefore, duplicate elements are not stored.

---

### 36. What is a dictionary?

A dictionary stores data as **key-value pairs**.

```python
user = {
    "name": "Mradul",
    "age": 22
}
```

Access:

```python
print(user["name"])
```

Output:

```text
Mradul
```

Modern Python dictionaries preserve insertion order.

---

### 37. How does a dictionary work internally?

Python dictionaries use a **hash table**.

For:

```python
data["name"]
```

Python hashes `"name"` and uses that hash to efficiently locate the corresponding entry.

Average-case lookup, insertion and deletion are approximately:

```text
O(1)
```

although worst-case behavior can differ.

---

### 38. What can be used as a dictionary key?

Dictionary keys must be **hashable**.

Examples:

```python
int
str
float
tuple
frozenset
```

provided their contents are hashable.

This is invalid:

```python
d = {
    [1, 2]: "hello"
}
```

because lists are mutable and unhashable.

---

### 39. What is hashing?

Hashing converts an object into an integer hash value.

```python
hash("hello")
```

Hashing allows structures such as dictionaries and sets to perform efficient lookup.

An important requirement is that objects considered equal must have compatible hash values.

---

### 40. Difference between `dict.get()` and `dict[key]`?

```python
d = {"name": "Mradul"}
```

Using:

```python
d["age"]
```

raises:

```text
KeyError
```

But:

```python
d.get("age")
```

returns:

```text
None
```

You can also specify a default:

```python
d.get("age", 0)
```

---

### 41. Difference between `remove()`, `pop()` and `del`?

For lists:

```python
numbers.remove(2)
```

removes the first matching value.

```python
numbers.pop(1)
```

removes and returns the element at index 1.

```python
del numbers[1]
```

deletes the element at index 1.

`del` is a Python statement and can also delete names or slices.

---

### 42. What is list comprehension?

List comprehension provides a concise way to create lists.

Normal:

```python
squares = []

for i in range(5):
    squares.append(i * i)
```

Comprehension:

```python
squares = [i * i for i in range(5)]
```

---

### 43. What is dictionary comprehension?

```python
squares = {x: x*x for x in range(5)}
```

Result:

```python
{
    0: 0,
    1: 1,
    2: 4,
    3: 9,
    4: 16
}
```

---

### 44. What is set comprehension?

```python
squares = {x*x for x in range(5)}
```

It produces a set rather than a list.

---

### 45. How do you remove duplicates from a list?

Simple approach:

```python
numbers = [1, 2, 2, 3, 3]

unique = list(set(numbers))
```

But this does not preserve the original order.

To preserve order:

```python
unique = list(dict.fromkeys(numbers))
```

---

### 46. How do you count the frequency of elements?

Using `Counter`:

```python
from collections import Counter

numbers = [1, 2, 2, 3, 3, 3]

print(Counter(numbers))
```

Result:

```text
Counter({3: 3, 2: 2, 1: 1})
```

---

### 47. How do you sort a list?

```python
numbers = [4, 1, 3, 2]

numbers.sort()
```

or:

```python
sorted_numbers = sorted(numbers)
```

---

### 48. Difference between `sort()` and `sorted()`?

`sort()` modifies the existing list.

```python
numbers.sort()
```

`sorted()` returns a new sorted list.

```python
new_numbers = sorted(numbers)
```

`sorted()` can work with many iterable objects, not just lists.

---

### 49. What is shallow copy vs deep copy?

A **shallow copy** creates a new outer object but keeps references to nested objects.

A **deep copy** recursively copies nested objects as well.

```python
import copy

b = copy.copy(a)       # shallow
c = copy.deepcopy(a)   # deep
```

This matters especially with nested lists/dictionaries.

---

### 50. What is the difference between assignment and copying?

This is a very common interview trap.

```python
a = [1, 2, 3]
b = a
```

`a` and `b` refer to the **same object**.

```python
b.append(4)

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

To create a separate outer list:

```python
b = a.copy()
```

---

# 4. Functions

### 51. How do you define a function?

```python
def add(a, b):
    return a + b
```

Calling:

```python
result = add(2, 3)
```

---

### 52. What are positional and keyword arguments?

Positional arguments depend on order:

```python
add(2, 3)
```

Keyword arguments use parameter names:

```python
add(a=2, b=3)
```

---

### 53. What are default arguments?

A function can provide default values:

```python
def greet(name="Guest"):
    print("Hello", name)
```

Calling:

```python
greet()
```

produces:

```text
Hello Guest
```

---

### 54. What are `*args` and `**kwargs`?

`*args` collects extra positional arguments into a tuple.

```python
def func(*args):
    print(args)

func(1, 2, 3)
```

`**kwargs` collects extra keyword arguments into a dictionary.

```python
def func(**kwargs):
    print(kwargs)

func(name="Mradul", age=22)
```

---

### 55. What is a lambda function?

A lambda is an anonymous function expression.

```python
square = lambda x: x * x

print(square(5))
```

Output:

```text
25
```

For complex logic, a normal `def` function is usually clearer.

---

### 56. What are first-class functions?

In Python, functions are objects.

They can be:

* Stored in variables
* Passed as arguments
* Returned from functions
* Stored in data structures

Example:

```python
def greet():
    print("Hello")

x = greet
x()
```

---

### 57. What is a higher-order function?

A higher-order function either:

1. Accepts a function as an argument, or
2. Returns a function.

Examples include:

```python
map()
filter()
sorted()
```

when used with key/functions.

---

### 58. What is a closure?

A closure occurs when an inner function remembers variables from its enclosing scope even after the outer function has finished.

```python
def outer(x):
    def inner():
        return x

    return inner

f = outer(10)

print(f())
```

Output:

```text
10
```

---

### 59. What is recursion?

Recursion is when a function calls itself.

Example:

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)
```

Every recursive solution needs an appropriate **base case**.

---

### 60. Difference between `return`, `yield`, and `pass`?

`return` ends a function and returns a value.

```python
return x
```

`yield` produces a value from a generator while preserving its execution state.

```python
yield x
```

`pass` does nothing and is used as a placeholder.

```python
def future_function():
    pass
```

---

# 5. Object-Oriented Programming

### 61. What is OOP?

Object-Oriented Programming organizes software around **objects containing state and behavior**.

Python supports:

* Encapsulation
* Inheritance
* Polymorphism
* Abstraction

---

### 62. What is a class?

A class is a blueprint for creating objects.

```python
class Car:
    def drive(self):
        print("Driving")
```

---

### 63. What is an object?

An object is an instance of a class.

```python
car = Car()
```

Here:

```text
Car → class
car → object
```

---

### 64. Class vs object?

A class defines the structure/behavior.

An object is a concrete instance created from that class.

```python
class Student:
    pass

s1 = Student()
s2 = Student()
```

`Student` is the class, while `s1` and `s2` are objects.

---

### 65. What is `self`?

`self` refers to the current instance.

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Here `self.name` is an instance attribute.

`self` is a convention, not a reserved keyword.

---

### 66. What is `__init__()`?

`__init__()` is an initializer method called after an object has been created.

```python
class Student:
    def __init__(self, name):
        self.name = name
```

It is commonly used to initialize instance state.

Technically, object creation itself involves `__new__()`.

---

### 67. What are instance variables?

Instance variables belong to individual objects.

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Each object can have a different `name`.

---

### 68. What are class variables?

Class variables belong to the class and are shared unless an instance overrides the attribute.

```python
class Student:
    university = "DAVV"
```

Every instance can access `university`.

---

### 69. What is inheritance?

Inheritance allows one class to derive behavior from another.

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    pass
```

`Dog` inherits from `Animal`.

---

### 70. What types of inheritance does Python support?

Common forms are:

```text
Single
Multiple
Multilevel
Hierarchical
Hybrid
```

Example of multiple inheritance:

```python
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

---

### 71. What is multiple inheritance?

A class inherits from multiple parent classes.

```python
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

Python resolves method lookup using **MRO (Method Resolution Order)**.

---

### 72. What is method overriding?

A child class provides its own implementation of a method defined by its parent.

```python
class Animal:
    def speak(self):
        print("Animal")

class Dog(Animal):
    def speak(self):
        print("Bark")
```

Calling:

```python
Dog().speak()
```

produces:

```text
Bark
```

---

### 73. Does Python support method overloading?

Python does not support traditional compile-time method overloading like Java or C++.

If you define:

```python
def add(a):
    ...

def add(a, b):
    ...
```

the second definition replaces the first.

You can achieve similar behavior using:

* Default arguments
* `*args`
* Type checking
* `functools.singledispatch`

---

### 74. What is polymorphism?

Polymorphism means the same interface can work with different object types.

```python
class Dog:
    def speak(self):
        return "Bark"

class Cat:
    def speak(self):
        return "Meow"

for animal in [Dog(), Cat()]:
    print(animal.speak())
```

Both objects provide the same interface but behave differently.

---

### 75. What is encapsulation?

Encapsulation means keeping data and behavior together while controlling access to internal implementation details.

Python doesn't enforce strict private fields like some languages.

It uses conventions such as:

```python
_name
```

and name mangling for:

```python
__name
```

---

### 76. What is abstraction?

Abstraction means exposing the important interface while hiding implementation details.

Python commonly uses the `abc` module.

```python
from abc import ABC, abstractmethod

class Animal(ABC):

    @abstractmethod
    def speak(self):
        pass
```

---

### 77. What is an abstract class?

An abstract class is a class intended to define an interface or common behavior and may contain abstract methods that subclasses must implement.

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass
```

---

### 78. What is `super()`?

`super()` provides access to methods from a parent class according to the MRO.

```python
class Child(Parent):
    def __init__(self):
        super().__init__()
```

It is particularly useful in inheritance hierarchies.

---

### 79. What are dunder methods?

"Dunder" means **double underscore**.

Examples:

```python
__init__
__str__
__repr__
__len__
__eq__
__add__
```

They allow classes to integrate with Python's language features.

---

### 80. Difference between `__str__()` and `__repr__()`?

`__str__()` is intended for a readable representation.

`__repr__()` is intended to be more detailed and useful for debugging/development.

Example:

```python
class User:
    def __str__(self):
        return "User"

    def __repr__(self):
        return "User(name='Mradul')"
```

---

# 6. Exceptions

### 81. What is an exception?

An exception is an event that interrupts normal execution because something unexpected occurred.

Example:

```python
10 / 0
```

raises:

```text
ZeroDivisionError
```

---

### 82. Error vs exception?

An exception is a runtime condition that Python code can often handle.

Examples:

```text
ValueError
TypeError
KeyError
FileNotFoundError
ZeroDivisionError
```

"Error" is a broader term and can refer to various failures, including syntax errors and runtime exceptions.

---

### 83. How does `try-except` work?

```python
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")
```

The exception is caught by the matching `except` block.

---

### 84. What is `finally`?

`finally` executes whether or not an exception occurs.

```python
try:
    file = open("data.txt")
except FileNotFoundError:
    print("Not found")
finally:
    print("Finished")
```

It's commonly used for cleanup, although context managers are usually preferable for resources.

---

### 85. What is `else` in exception handling?

`else` executes only when the `try` block completes without raising an exception.

```python
try:
    x = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print("Success")
```

---

### 86. How do you create a custom exception?

Create a class derived from `Exception`.

```python
class InvalidAgeError(Exception):
    pass
```

Then:

```python
raise InvalidAgeError("Age cannot be negative")
```

---

### 87. Difference between `raise` and `assert`?

`raise` explicitly raises an exception.

```python
raise ValueError("Invalid value")
```

`assert` checks a condition and raises `AssertionError` if it is false.

```python
assert age >= 0
```

Assertions can be disabled with Python's optimization options, so they should not be used for essential runtime validation.

---

### 88. Can you have multiple `except` blocks?

Yes.

```python
try:
    x = int(input())

except ValueError:
    print("Invalid number")

except TypeError:
    print("Wrong type")
```

---

### 89. What happens if an exception is not handled?

The exception propagates up the call stack.

If nobody handles it, Python terminates the current program/thread and prints a traceback.

---

### 90. How should exceptions be handled in production?

Good practices include:

* Catch specific exceptions.
* Avoid bare `except`.
* Log useful context.
* Don't silently swallow failures.
* Clean up resources.
* Use custom exceptions where appropriate.
* Return appropriate errors at API boundaries.
* Avoid exposing sensitive information in error messages.

---

# 7. Advanced Python

### 91. What is an iterator?

An iterator is an object that produces values one at a time using:

```python
__iter__()
__next__()
```

Example:

```python
numbers = iter([1, 2, 3])

print(next(numbers))
print(next(numbers))
```

Output:

```text
1
2
```

When exhausted, it raises `StopIteration`.

---

### 92. What is a generator?

A generator is a convenient way to create an iterator using `yield`.

```python
def numbers():
    yield 1
    yield 2
    yield 3
```

Then:

```python
for x in numbers():
    print(x)
```

Generators produce values lazily.

---

### 93. Iterator vs generator?

An iterator is any object implementing the iterator protocol.

A generator is a particular, convenient way of creating an iterator using `yield`.

So:

> Every generator is an iterator, but not every iterator is a generator.

---

### 94. What is `yield`?

`yield` produces a value while preserving the generator's execution state.

```python
def count():
    yield 1
    yield 2
```

Calling:

```python
g = count()
```

doesn't execute the whole function immediately.

Values are generated as requested.

This makes generators useful for large datasets and streaming.

---

### 95. What is a decorator?

A decorator modifies or extends the behavior of a function or class without changing its core implementation.

Example:

```python
def decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")

    return wrapper

@decorator
def hello():
    print("Hello")
```

Calling:

```python
hello()
```

produces:

```text
Before
Hello
After
```

Decorators are widely used in frameworks such as Flask and Django.

---

### 96. What is a context manager?

A context manager manages setup and cleanup around a block of code.

Most commonly:

```python
with open("data.txt") as f:
    data = f.read()
```

The file is properly closed when leaving the `with` block, including when exceptions occur.

Custom context managers can be created using `__enter__` and `__exit__`, or `contextlib.contextmanager`.

---

### 97. Multithreading vs multiprocessing vs asynchronous programming?

### Multithreading

Multiple threads within one process.

Good for:

```text
I/O-bound tasks
```

Examples:

```text
Network requests
File I/O
Database calls
```

### Multiprocessing

Multiple processes.

Useful for CPU-intensive work because separate processes can execute Python code in parallel.

### Async programming

Uses cooperative concurrency with an event loop.

Example:

```python
async def fetch():
    ...
```

Useful when handling many concurrent I/O operations.

---

### 98. How does Python manage memory?

Python uses:

* Private heap for Python objects
* Reference counting in CPython
* Cyclic garbage collector
* Memory allocators
* Automatic memory management

Example:

```python
x = [1, 2, 3]
```

Python allocates memory for the list and manages its lifetime automatically.

---

### 99. What are modules and packages?

A **module** is generally a Python file containing code.

Example:

```text
math_utils.py
```

Import:

```python
import math_utils
```

A **package** organizes modules into a directory structure.

Example:

```text
myapp/
    __init__.py
    database.py
    api.py
```

Modern Python also supports namespace packages without requiring `__init__.py` in every package directory.

---

### 100. How do you make a Python application production-ready?

This is a particularly important question for **DevOps/backend interviews**.

A production Python application should typically have:

```text
Virtual environment / dependency management
Configuration management
Environment variables / secrets management
Logging
Exception handling
Testing
Linting / formatting
Dependency pinning
Security controls
Monitoring
Health checks
CI/CD
Containerization where appropriate
```

For example, instead of:

```python
password = "mypassword"
```

use environment/configuration management:

```python
import os

password = os.getenv("DB_PASSWORD")
```

For a web application, you would additionally consider:

```text
Reverse proxy
Application server
TLS
Database connection pooling
Rate limiting
Observability
Horizontal scaling
```

---

