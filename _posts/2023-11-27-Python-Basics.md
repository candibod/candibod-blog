---
title: "Python Basics"
date: 2023-11-13
layout: post
author: jeevan
categories: [python]
permalink: /python/:title
published: false
---

Common practices as per pep-8 standard

## Naming convention

```python
# Variable Names
cars = ["vw", "kia"]
car_companies = ["vw", "kia"]

# Constants
COLOR = "white"
BG_COLOR = "black"

# Function Names
def get_cars(): pass

# Class Names
class Base:
    pass

class BaseClass:
    pass
```

Python runs on an interpreter system(No need to compile and convert into machine language program), meaning that code can be executed as soon as it is written. This means that prototyping can be very quick.

<br>

**Variables** are containers for storing data values. Variables do not need to be declared with any particular type, and can even change type after they have been set.

```
x = 4 # x is of type int
x = "Sally" # x is now of type str
```

<br>

**Casting** is when you convert a variable value from one type to another

```python
x = str(3)    # x will be '3'
y = int(3)    # y will be 3
z = float(3)  # z will be 3.0
```

## Variable Names

- A variable name must start with a letter or the underscore character
- A variable name cannot start with a number
- A variable name can only contain alpha-numeric characters and underscores (A-z, 0-9, and \_ ). Variable names are case-sensitive (age, Age and AGE are three different variables)

| Pattern                                | Example     | Meaning                                                                                                                                                                                  |
| :------------------------------------- | :---------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Single Leading Underscore              | \_var       | Naming convention indicating a name is meant for internal use. Generally not enforced by the Python interpreter (except in wildcard imports) and meant as a hint to the programmer only. |
| Single Trailing Underscore             | var\_       | Used by convention to avoid naming conflicts with Python keywords.                                                                                                                       |
| Double Leading Underscore              | \_\_var     | It causes the Python interpreter to rewrite the attribute name in order to avoid naming conflicts in subclasses. This is also called name mangling                                       |
| Double Leading and Trailing Underscore | \_\_var\_\_ | Indicates special methods defined by the Python language. Avoid this naming scheme for your own attributes.                                                                              |
| Single Underscore                      | \_          | Sometimes used as a name for temporary or insignificant variables (“don’t care”). Also: The result of the last expression in a Python REPL.                                              |

:information_source: Double underscores are often referred to as “dunders” in the Python community.

## Python operators

| Type                 | Operators                                    | Description                                                                                                                 |
| :------------------- | :------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------- |
| Arithmetic operators | `+ - * / % ** //`                            | used with numeric values to perform common mathematical operations                                                          |
| Assignment operators | `= += -= *= /= %= //= **= &= \|= ^= >>= <<=` | used to assign values to variables                                                                                          |
| Comparison operators | `== != > < >= <=`                            | Used to compare two values                                                                                                  |
| Logical operators    | `and` `or` `not`                             | used to combine conditional statements                                                                                      |
| Identity operators   | `is` `is not`                                | used to compare the objects, not if they are equal, but if they are actually the same object, with the same memory location |
| Membership operators | `in` `not in`                                | used to test if a sequence is presented in an object                                                                        |
| Bitwise operators    | `& \| ^ ~ << >>`                             | used to compare (binary) numbers                                                                                            |

**List comprehension** offers a shorter syntax when you want to create a new list based on the values of an existing list.

```
newlist = [x for x in range(10)]
newlist = [x for x in range(10) if x < 5]
newlist = [x if x != "banana" else "orange" for x in fruits]
```

**Packing/Unpacking Tuples:**

```
fruits = ("apple", "banana", "cherry", "strawberry") # Packing
(green, yellow, red, white) = fruits # Unpacking
(green, yellow, *red) = fruits # Unpacking
(green, *tropic, red) = fruits # Unpacking
```

<br>

**Parameters & Arguments**

```
def func(foo, bar=None, **kwargs): # Parameters
    pass

func(42, bar=314, extra=somevar) # Arguments
```

<br>

**Arbitrary Arguments, \*args**\
If you do not know how many arguments that will be passed into your function, add a \* before the parameter name in the function definition. This way the function will receive a tuple of arguments

```
def my_function(*kids):
  print("The youngest child is " + kids[2])

my_function("Emil", "Tobias", "Linus")
```

<br>

**Arbitrary Keyword Arguments, \*\*kwargs**\
If you do not know how many keyword arguments that will be passed into your function, add two asterisk: \*\* before the parameter name in the function definition. This way the function will receive a dictionary of arguments.

```
def my_function(**kid):
  print("His last name is " + kid["lname"])

my_function(fname = "Tobias", lname = "Refsnes")
```

<br>

**Python Lambda**\
A lambda function is a small anonymous function which can take any number of arguments, but can only have one expression.

```
x = lambda a : a + 10
print(x(5))

# The power of lambda is better shown when you use them as an anonymous function inside another function. function definition that takes one argument, and that argument will be multiplied with an unknown number

def myfunc(n): # Example 2
  return lambda a : a * n

mydoubler = myfunc(2)
mytripler = myfunc(3)

print(mydoubler(11))
print(mytripler(11))
```

<br>

**Classes & Objects**\
Python is an object oriented programming language. Almost everything in Python is an object, with its properties and methods. A Class is like an object constructor, or a "blueprint" for creating objects.

```
class Person:
  # name and age are object properties
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self): # Object Method
    print("Hello my name is " + self.name)

p1 = Person("John", 36) # Create Object
p1.myfunc()

del p1.name # Delete Property
del p1 # Delete object
```

The `self` parameter is a reference to the current instance of the class, and is used to access variables that belongs to the class. It does not have to be named `self` , you can call it whatever you like, but it has to be the first parameter of any function in the class

<br>

**Python Inheritance**\
Inheritance allows us to define a class that inherits all the methods and properties from another class. Parent class is the class being inherited from, also called base class. Child class is the class that inherits from another class, also called derived class.

```
class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname

  def printname(self):
    print(self.firstname, self.lastname)

x = Person("John", "Doe")
x.printname()

class Student(Person):
  pass # Use the pass keyword when you do not want to add any other properties or methods to the class.

# Now the Student class has the same properties and methods as the Person class.
x = Student("Mike", "Olsen")
x.printname()
```

<br>

**Add the \_\_init\_\_() Function**\
If We want to add the \_\_init\_\_() function to the child class (instead of the pass keyword). the child class will no longer inherit the parent's \_\_init\_\_() function. The child's \_\_init\_\_() function overrides the inheritance of the parent's \_\_init\_\_() function.

To keep the inheritance of the parent's \_\_init\_\_() function, add a call to the parent's \_\_init\_\_() function:

```
class Student(Person):
  def __init__(self, fname, lname):
    Person.__init__(self, fname, lname)
```

By using the super() function, you do not have to use the name of the parent element, it will automatically inherit the methods and properties from its parent.

```
class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)
```

<br>

| The ENDDDDD! |
| ------------ |
