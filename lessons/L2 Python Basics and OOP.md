# L2: Python Basics and OOP

### 2.1 Basic Syntax and Data Types

### Variables and Data Types

Python supports various data types, including integers, floats, strings, lists, tuples, dictionaries, and sets. Here are some examples and brief descriptions of each:

**Integer:**
Integers are whole numbers without a decimal point. They can be positive or negative.

```python
x = 5
print(type(x))  # Output: <class 'int'>
```

**Float:**
Floats are numbers that contain a decimal point. They are used for more precise calculations.

```python
y = 3.14
print(type(y))  # Output: <class 'float'>
```

**String:**
Strings are sequences of characters enclosed in quotes. They can be single, double, or triple quotes.

```python

name = 'Python'
name = "Python"
description = '''Python is a programming language that lets you work quickly
and integrate systems more effectively.
'''

print(f'Hello {name}')
```

**List:**
Lists are ordered collections of items. They are mutable, meaning their content can be changed. Lists allow duplicate elements.

```python
fruits = ["apple", "banana", "cherry"]
print(type(fruits))  # Output: <class 'list'>
```

**Tuple:**
Tuples are similar to lists, but they are immutable. Once created, their content cannot be changed.

```python
coordinates = (10, 20)
print(type(coordinates))  # Output: <class 'tuple'>
```

**Dictionary:**
Dictionaries are collections of key-value pairs. They are unordered and mutable.

```python
person = {"name": "Alice", "age": 25, "items":[1,2,3]}
print(type(person))  # Output: <class 'dict'>
```

**Set:**
Sets are collections of unique items. They are unordered and mutable. Sets do not allow duplicate elements.

```python
unique_numbers = {1, 2, 3, 4, 5}
print(type(unique_numbers))  # Output: <class 'set'>
```

### Differences Between Lists and Sets

- **Order**: Lists are ordered, meaning elements have a specific sequence. Sets are unordered.
- **Mutability**: Both lists and sets are mutable, but lists allow duplicates while sets do not.
- **Complexity**: Lists provide O(1) time complexity for indexing and **O(n) for searching**. Sets provide average O(1) time complexity for adding, removing, and checking for elements, sets are generally faster for membership tests due to their use of hash tables.

### Basic Operations

Python allows you to perform various operations on these data types:

**Arithmetic Operations:**

```python
a = 10
b = 3
print(a + b)  # Addition: 13
print(a - b)  # Subtraction: 7
print(a * b)  # Multiplication: 30
print(a / b)  # Division: 3.3333...
print(a % b)  # Modulus: 1
print(a ** b)  # Exponentiation: 1000
```

**String Operations:**

```python
s1 = "Hello"
s2 = "World"
print(s1 + " " + s2)  # Concatenation: "Hello World"
print(s1 * 3)  # Repetition: "HelloHelloHello"
print(s1[1])  # Indexing: "e"
print(s1[1:4])  # Slicing: "ell"
```

**List Operations:**

```python
numbers = [1, 2, 3, 4, 5]
print(numbers[2])  # Indexing: 3
numbers.append(6)  # Adding an element
print(numbers)  # Output: [1, 2, 3, 4, 5, 6]
```

### Advanced Data Types

For more advanced data types, Python provides the `collections` module, which includes namedtuples, deque, Counter, OrderedDict, defaultdict, and ChainMap. These are highly specialized data types that can improve the efficiency and readability of your code.

For more information, refer to the [official documentation for the `collections` module](https://docs.python.org/3/library/collections.html).

---

### 2.2 Control Structures and Functions

### **Conditions**

Python uses `if`, `elif`, and `else` statements to perform conditional operations. These statements help in decision-making by executing certain blocks of code based on the evaluation of conditions.

**Example:**

```python
pythonCopy code
x = 10
if x > 0:
    print("x is positive")
elif x == 0:
    print("x is zero")
else:
    print("x is negative")

```

**Shorthand If:**
You can write simple if statements on one line with shorthand if.

```python
pythonCopy code
x = 10
print("x is positive") if x > 0 else print("x is not positive")

```

**Using `and`, `or`, and `not`:**
These logical operators are used to combine multiple conditions.

```python
pythonCopy code
x = 5
y = 10

# Using 'and'
if x > 0 and y > 0:
    print("Both x and y are positive")

# Using 'or'
if x > 0 or y > 0:
    print("At least one of x or y is positive")

# Using 'not'
if not (x > 0):
    print("x is not positive")

```

For more information, refer to the [official documentation on conditionals](https://docs.python.org/3/tutorial/controlflow.html#if-statements).

### Iterables

An iterable is any Python object capable of returning its members one at a time, permitting it to be iterated over in a loop. Common iterables include lists, tuples, strings, and dictionaries.

**Examples of Iterables:**

- **List**: `fruits = ["apple", "banana", "cherry"]`
- **Tuple**: `coordinates = (10, 20)`
- **String**: `name = "Python"`
- **Dictionary**: `person = {"name": "Alice", "age": 25}`

For more information, refer to the [official documentation on iterables](https://docs.python.org/3/glossary.html#term-iterable).

### Loops

Python supports `for` and `while` loops to iterate over sequences (such as lists, tuples, strings) or perform a block of code multiple times.

**For Loop:**
The `for` loop in Python is used to iterate over a sequence (like a list, tuple, or string). It simplifies the process of iterating over items in a collection.

**Example:**

```python
for i in range(5):
    print(i)  # Output: 0 1 2 3 4
```

You can also iterate over other iterables like lists and strings:

```python
# Iterating over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Iterating over a string
name = "Python"
for char in name:
    print(char)
```

**While Loop:**
The `while` loop in Python is used to repeatedly execute a block of code as long as the condition is true.

**Example:**

```python
count = 0
while count < 5:
    print(count)
    count += 1  # Output: 0 1 2 3 4
```

For more information, refer to the [official documentation on loops](https://docs.python.org/3/tutorial/controlflow.html#for-statements).

### Functions

Functions in Python are defined using the `def` keyword. Functions help to modularize code, make it reusable, and improve readability.

**Defining a Function:**
A function in Python can be defined using the `def` keyword, followed by the function name, parentheses `()`, and a colon `:`. The function body is indented.

**Example:**

```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Output: Hello, Alice!
```

**Function with Default Arguments:**
Functions can have default arguments, which are used if no value is provided for the argument when the function is called.

**Example:**

```python
def greet(name, message="Hello"):
    return f"{message}, {name}!"

print(greet("Bob"))  # Output: Hello, Bob!
print(greet("Bob", "Good morning"))  # Output: Good morning, Bob!
```

**Lambda Functions:**
Lambda functions are small anonymous functions defined using the `lambda` keyword. They can have any number of arguments but only one expression.

**Example:**

```python
add = lambda a, b: a + b
print(add(2, 3))  # Output: 5
```

**Filtering a Dictionary using Lambda Function:**
You can use a lambda function along with `filter()` to filter a dictionary.

**Example:**

```python
# Dictionary of items with their prices
items = {
    'apple': 10,
    'banana': 5,
    'orange': 8,
    'pear': 12
}

# Filter items with price greater than 8
filtered_items = dict(filter(lambda item: item[1] > 8, items.items()))

print(filtered_items)  # Output: {'apple': 10, 'pear': 12}
```

**Built-in Functions:**
Python has many built-in functions like `len()`, `max()`, `min()`, `sum()`, etc., which perform common tasks.

**Example:**

```python
numbers = [1, 2, 3, 4, 5]
print(len(numbers))  # Output: 5
print(max(numbers))  # Output: 5
print(min(numbers))  # Output: 1
print(sum(numbers))  # Output: 15
```

**Docstrings:**
Docstrings are a type of comment used to explain the purpose of a function. They are placed as the first statement in the function body and are enclosed in triple quotes.

**Example:**

```python
def greet(name):
    """
    This function greets the person whose name is passed as a parameter.
    """
    return f"Hello, {name}!"

print(greet.__doc__)
```

For more information, refer to the [official documentation on functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions).

### 2.3 Modules and Packages

### Importing Modules

Modules are Python files that contain functions, classes, and variables. You can import them using the `import` statement.

**Importing a Module:**
To import a module, use the `import` statement followed by the module name.

```python
pythonCopy code
import math
print(math.sqrt(16))  # Output: 4.0

```

**Importing Specific Functions:**
You can import specific functions from a module using the `from` keyword.

```python
pythonCopy code
from math import sqrt, pi
print(sqrt(25))  # Output: 5.0
print(pi)  # Output: 3.141592653589793

```

**Aliasing Modules:**
You can give a module a different name using the `as` keyword.

```python
pythonCopy code
import math as m
print(m.sqrt(36))  # Output: 6.0

```

For more information, refer to the [official documentation on modules](https://docs.python.org/3/tutorial/modules.html).

### Creating and Using Packages

Packages are directories containing multiple modules. Each package must include an `__init__.py` file to be recognized as a package by Python.

**Creating a Package:**

1. Directory Structure:

```markdown
mypackage/
    __init__.py
    greetings.py
    farewells.py
```

**greetings.py**:

```python
def say_hello():
    return "Hello!"
```

**farewells.py**:

```python
def say_goodbye():
    return "Goodbye!"
```

**`__init__.py`**:
The `__init__.py` file is used to mark a directory as a Python package and can be used to initialize package-level variables. You can also define the `__all__` list to specify which modules should be accessible when using `from package import *`.

**Example `__init__.py`**:

```python
from .greetings import say_hello

__all__ = ["say_hello", "greetings", "farewells"]
```

**Using the Package:**
To use the package, import the modules or functions as follows:

```python
from mypackage import say_hello, greetings, farewells

print(say_hello())  # Output: Hello!
print(greetings.say_hello())  # Output: Hello!
print(farewells.say_goodbye())  # Output: Goodbye!
```

For more information, refer to the [official documentation on packages](https://docs.python.org/3/tutorial/modules.html#packages).

**Additional Resources:**

- [Python Modules](https://docs.python.org/3/tutorial/modules.html)
- [Python Packages](https://docs.python.org/3/tutorial/modules.html#packages)

### 2.4 Object-Oriented Programming

### Classes and Objects

Classes are blueprints for creating objects. An object is an instance of a class. A class defines attributes and methods that the created objects can use.

**Defining a Class:**
A class is defined using the `class` keyword followed by the class name and a colon. The class body contains attributes and methods.

**Example:**

```python
pythonCopy code
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        return f"{self.name} is barking"

# Creating an object
dog1 = Dog("Buddy", 3)
print(dog1.bark())  # Output: Buddy is barking

```

For more information, refer to the [official documentation on classes](https://docs.python.org/3/tutorial/classes.html).

### Inheritance

Inheritance allows a class to inherit attributes and methods from another class. The class that inherits is called the derived class, and the class from which it inherits is called the base class.

**Base Class:**

```python
pythonCopy code
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        raise NotImplementedError("Subclasses must implement this method")

```

**Derived Class:**

```python
pythonCopy code
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow"

# Creating an object
cat1 = Cat("Whiskers")
print(cat1.speak())  # Output: Whiskers says Meow

```

For more information, refer to the [official documentation on inheritance](https://docs.python.org/3/tutorial/classes.html#inheritance).

### Polymorphism and Encapsulation

Polymorphism allows different classes to be treated as instances of the same class through inheritance. Encapsulation hides the internal state of an object and requires all interaction to be performed through an object's methods.

**Polymorphism Example:**

```python
pythonCopy code
class Bird(Animal):
    def speak(self):
        return f"{self.name} says Tweet"

animals = [Dog("Buddy", 3), Cat("Whiskers"), Bird("Tweety")]
for animal in animals:
    print(animal.speak())

```

**Encapsulation Example:**
Encapsulation is achieved by prefixing an attribute with an underscore or double underscore. This makes it private to the class and not accessible from outside.

```python
pythonCopy code
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
            return amount
        else:
            return "Insufficient funds"

# Creating an object
account = BankAccount(1000)
account.deposit(500)
print(account.withdraw(200))  # Output: 200
print(account.withdraw(1500))  # Output: Insufficient funds

```

For more information, refer to the [official documentation on polymorphism and encapsulation](https://docs.python.org/3/tutorial/classes.html#tut-private).

### Mixins

Mixins are a kind of inheritance in which a class can inherit behaviors and attributes from multiple classes. This allows for code reuse and the creation of modular and extensible designs. Mixins typically provide specific functionality and are not intended to stand alone.

**Example of Mixins:**

```python
pythonCopy code
class CanFly:
    def fly(self):
        return "Flying"

class CanSwim:
    def swim(self):
        return "Swimming"

class Duck(Animal, CanFly, CanSwim):
    def speak(self):
        return f"{self.name} says Quack"

# Creating an object
duck = Duck("Donald")
print(duck.speak())  # Output: Donald says Quack
print(duck.fly())    # Output: Flying
print(duck.swim())   # Output: Swimming

```

In this example, the `Duck` class inherits from the `Animal` class and two mixins: `CanFly` and `CanSwim`. The `Duck` class can now use the `fly` and `swim` methods in addition to its own methods.

For more information, refer to the [official documentation on multiple inheritance](https://docs.python.org/3/tutorial/classes.html#multiple-inheritance).

### Special Methods

Special methods in Python are defined with double underscores at the beginning and end of their names. These methods are also known as dunder methods. They allow you to define the behavior of your objects for built-in operations.

**Example:**

```python
pythonCopy code
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    def __str__(self):
        return f"{self.title} by {self.author}"

    def __len__(self):
        return len(self.title)

# Creating an object
book = Book("1984", "George Orwell")
print(str(book))  # Output: 1984 by George Orwell
print(len(book))  # Output: 4

```

For more information, refer to the [official documentation on special methods](https://docs.python.org/3/reference/datamodel.html#special-method-names).