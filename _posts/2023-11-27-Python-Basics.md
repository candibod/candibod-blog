---
title: "Python Basics"
date: 2023-11-27
layout: post
author: jeevan
categories: [python]
permalink: /python/:title
published: true
---

# Python Quick Reference

python program is given access to some of your computer's memory by the OS, that memory is used for the code of the program itself and the data that it uses. The operating system ensures that the program cannot read or write other memory locations without somehow getting permissions

#### Q/A

- how much memory will it allocate?
  - Note that the size and layout of an object is purely implementation-specific. CPython, for example, may use totally different internal data structures than IronPython. So the size of an object may vary from implementation to implementation.
  ```python
  > from sys import getsizeof
  > a = 42
  > getsizeof(a)
  ```
- what if we need more memory?
  - Python will manage it
- how to give access to other memory locations?

Some languages like C/C++, plunk(change) and plunk the raw values in memory, keeping track of the size and types. Instead of handling such raw data values directly. python wraps each data value-booleans, integers, floats, strings, event large data structures, functions, and programs in memory as an object.

In Python, an object is a chunk of data that contains at least the following:

- A type that defines what it can do (mentioned in table below)
- A unique id to distinguish it from other objects
- A value consistent with its type
- A reference count that tracks how often this object is used

## Types

| Name           | Type      | Mutable | Examples                              |
| :------------- | :-------- | :------ | ------------------------------------- |
| Boolean        | bool      | no      | True, False                           |
| Integer        | int       | no      | 47.25000, 25_000                      |
| Floating point | float     | no      | 3.14, 2.7e5                           |
| Complex        | complex   | no      | 3j, 5 + 9j                            |
| Text string    | str       | no      | 'alas', 'alack', '''a verse attack''' |
| List           | list      | yes     | ['Winken', 'Blinked', 'Nod']          |
| Tuple          | tuple     | no      | (2, 4, 8)                             |
| Bytes          | bytes     | no      | b'ab\xff'                             |
| ByteArray      | bytearray | yes     | bytearray(...)                        |
| Set            | set       | yes     | set([3, 5, 7])                        |
| Frozen Set     | frozenset | no      | frozenset(['Elas', 'Otto'])           |
| Dictionary     | dict      | yes     | {'game': 'bingo', 'dog': 'dingo'}     |

Note: 2.7e5, 1.0e8

### Mutability

The type also determined whether the data value contained by the box can be changed(mutable) or is constant(immutable)

Note: Python is strongly typed means that the type of an object does not change, even if its value is mutable

## Variables

Variables are containers for storing data values. Variables do not need to be declared with any particular type, and can even change type after they have been set.

### Variables are names, not places

Unlike programming languages like c, variables in python are just names.

In `x = 3`, Assignment(=) does not copy a value, it just attaches a name(x) to the object(3).

```
x = 4 # x is of type int
x = "Sally" # x is now of type str
```

### Example for behind the scenes

```python
>>> y = 5
>>> x = 12 - y
>>> x
7
```

In this code snippet, Python did the following:

- Created an integer object with the value 5
- Made a variable y point to that 5 object
- Incremented the reference count of the object with value 5
- Created another integer object with the value 12
- Subtracted the value of the object that y points to (5) from the value 12 in the (anonymous) object with that value
- Assigned this value (7) to a new (so far, unnamed) integer object
- Made the variable x point to this new object
- Incremented the reference count of this new object that x points to
- Looked up the value of the object that x points to (7) and printed it

When an object’s reference count reaches zero, no names are pointing to it, so it doesn’t need to stick around. Python has a charmingly named garbage collector that reuses the memory of things that are no longer needed. In this case, we no longer need the objects with the values 5, 12, or 7, or the variables x and y. The Python garbage collector may choose to send them to object heaven or keep some around for performance reasons given that small integers tend to be used a lot.

### Example of a mutable object behavior

```python
> a = [2, 4, 6]
> b = a
> print(a) # [2, 4, 6]
> print(b) # [2, 4, 6]

> a[0] = 99
> print(a) # [99, 4, 6]
> print(b) # [99, 4, 6]
```

### Variable Names

- A variable name must start with a letter or the underscore character
- A variable name cannot start with a number
- A variable name can only contain alpha-numeric characters and underscores (A-z, 0-9, and \_ ).
- Variable names are case-sensitive (age, Age and AGE are three different variables)

| Pattern                                | Example     | Meaning                                                                                                                                                                                  |
| :------------------------------------- | :---------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Single Leading Underscore              | \_var       | Naming convention indicating a name is meant for internal use. Generally not enforced by the Python interpreter (except in wildcard imports) and meant as a hint to the programmer only. |
| Single Trailing Underscore             | var\_       | Used by convention to avoid naming conflicts with Python keywords.                                                                                                                       |
| Double Leading Underscore              | \_\_var     | It causes the Python interpreter to rewrite the attribute name in order to avoid naming conflicts in subclasses. This is also called name mangling                                       |
| Double Leading and Trailing Underscore | \_\_var\_\_ | Indicates special methods defined by the Python language. Avoid this naming scheme for your own attributes.                                                                              |
| Single Underscore                      | \_          | Sometimes used as a name for temporary or insignificant variables (“don’t care”). Also: The result of the last expression in a Python REPL.                                              |

:information_source: Double underscores are often referred to as “dunders” in the Python community.

### Integer Operations

| Description                  | Operator | Example  | Result |
| :--------------------------- | :------- | :------- | ------ |
| Floating point division      | /        | 7 / 2    | 3.5    |
|                              |          | 10 / 2   | 5.0    |
| Integer(truncating) division | //       | 7 / 2    | 3      |
| Modulus(reminder)            | %        | 7 % 3    | 1      |
| Exponentiation               | \*\*     | 3 \*\* 4 | 81     |

Tip: Combination of arithmetic operators with assignment(=)

```python
> a -= 3 # a = a - 3
> a += 3 # a = a + 3
> a *= 3 # a = a * 3
> a /= 3 # a = a / 3
> a //= 3 # a = a // 3
```

### Bases

We can express literal integers in three bases besides decimal with these integer prefixes:

- 0b or 0B for binary (base 2)
- 0o or 0O for octal (base 8)
- 0x or 0X for hex (base 16)

```python
> 0b10 # 2
> 0o10 # 8
> 0x10 # 16

> a = 65
> bin(a) # '0b1000001'
> oct(a) # '0o101'
> hex(a) # '0x41'

chr() converts an integer to its single-character string equivalent, ord() goes the other way
> chr(65)  # 'A'
> ord('A') # 65
```

### Type Conversions

when you convert a data type to another, May also referred as **Casting**

```python
> int(True)  # 1
> int(False) # 0

> bool(1)    # True
> bool(0)    # False

> int(98.6)  # 98
> int(1.0e4) # 10000

Following will throw an error
> int('98.6')
> int('1.0e4')

> bool(1.0)  # True
> bool(0.0)  # False

> int('99')         # 99
> int('-23')        # -23
> int('+12')        # 12
> int('1_000_000')  # 1000000

> int('10', 2)      # 2
> int('10', 8)      # 8
> int('10', 16)     # 16

> float(3)          # 3.0

> str(3)            # '3'
> str(True)         # 'True'
```

Q/A:

- Max storage for int

### Python operators

| Type                 | Operators                                    | Description                                                                                                                 |
| :------------------- | :------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------- |
| Arithmetic operators | `+ - * / % ** //`                            | used with numeric values to perform common mathematical operations                                                          |
| Assignment operators | `= += -= *= /= %= //= **= &= \|= ^= >>= <<=` | used to assign values to variables                                                                                          |
| Comparison operators | `== != > < >= <=`                            | Used to compare two values                                                                                                  |
| Logical operators    | `and` `or` `not`                             | used to combine conditional statements                                                                                      |
| Identity operators   | `is` , `is not`                              | used to compare the objects, not if they are equal, but if they are actually the same object, with the same memory location |
| Membership operators | `in` , `not in`                              | used to test if a sequence is presented in an object                                                                        |
| Bitwise operators    | `& \| ^ ~ << >>`                             | used to compare (binary) numbers                                                                                            |

### What is True/False?

A false value doesn't necessarily need to explicitly be a boolean False. For example. all the following are considered False.

| Type    | Value |
| :------ | :---- |
| Boolean | False |
| null    | None  |
| Integer | 0     |
| Float   | 0.0   |
| String  | ''    |
| List    | []    |
| Tuple   | ()    |
| dict    | {}    |
| set     | set() |

Anything else is considered True.

### Walrus

walrus operator: `name := expression`

```python
a = 1
b = 3
diff = a - b
if diff >= 0:
    print("A")
else:
    print("B")

# Can be replaced with
a = 1
b = 3
if diff:= a - b >= 0:
    print("A")
else:
    print("B")
```

## Strings

### Types of strings

- f or F -> Formatting
- r or R -> Raw String, used to prevent escape characters in string
- fr -> Raw f-string
- u -> Unicode string
- b -> Bytes

### String manipulations

#### Combine by using **+**

```python
> a = 'Duck.'
> b = 'Grey'
> a + b         # 'Duck.Grey'
> print(a + b)  # 'Duck. Grey'
```

#### Duplicate with **\***

```python
> start = 'Na ' * 4
> start
'Na Na Na Na '
```

#### Get a character with []

Need to specify its offset inside square brackets after the strings name(0 , 1, so on). The last offset can be specified with -1.

```python
> letters = 'abcdef'
> letters[0]   # a
> letters[1]   # b
> letters[-1]  # f
```

Since string are immutable we can't change a character of a string with the square brackets

```python
> name = 'Henny'
> name[0] = 'P'
 TypeError: 'str' object does not support item assignment

# Instead we need to use string functions or slice
> name.replace('H', 'P') # Penny
> 'P' + name[1:]         # Penny
```

### Get a substring with a **slice**

We can extract a substring from a string by using a slice. we can define a slice using square brackets `[start:stop:step]`

You can omit some of these, the slice will include character from offset start to one before end:

- [:] extracts the entire sequence from start to end.
- [ start :] specifies from the start offset to the end.
- [: end ] specifies from the beginning to the end offset minus 1.
- [ start : end ] indicates from the start offset to the end offset minus 1.
- [ start : end : step ] extracts from the start offset to the end offset minus 1, skipping characters by step.

```python
> letters = 'abcdefghijklmnopqrstuvwxyz'
> letters[:]       # 'abcdefghijklmnopqrstuvwxyz'
> letters[20:]     # 'uvwxyz'
> letters[12:15]   # 'mno'
> letters[-3:]     # 'xyz'
> letters[18:-3]   # 'stuvw'
> letters[-6:-2]   # 'uvwx'
> letters[::7]     # 'ahov'
> letters[4:20:3]  # 'ehknqt'
> letters[19::4]   # 'tx'
> letters[:21:5]   # 'afkpu'
> letters[-1::-1]  # 'zyxwvutsrqponmlkjihgfedcba'
> letters[::-1]    # 'zyxwvutsrqponmlkjihgfedcba'

# A slice offset earlier than the beginning of a string is treated as 0, and one after the end is treated as -1
> letters[-50:]    # 'abcdefghijklmnopqrstuvwxyz'
> letters[-51:50]  # ''
> letters[:70]     # 'abcdefghijklmnopqrstuvwxyz'
> letters[70:71]   # ''
```

### Python built in functions

#### len()

```python
> len(letters) # 26
> empty = ''
> len(empty)   # 0
```

#### split()

Unlike len(), some functions are specific to strings. We can use split() function to break a string into a list of smaller strings based on some separator

```python
> tasks = 'get gloves,get mask,give cat vitamins,call ambulance'
> tasks.split(',')  # ['get gloves', 'get mask', 'give cat vitamins', 'call ambulance']

# If you don’t specify a separator, split() uses any sequence of white space characters—newlines, spaces, and tabs
> tasks.split()     # ['get', 'gloves,get', 'mask,give', 'cat', 'vitamins,call', 'ambulance']
```

#### join()

```python
> crypto_list = ['Yeti', 'Bigfoot', 'Loch Ness Monster']
> crypto_string = ', '.join(crypto_list)
> print(crypto_string) # Yeti, Bigfoot, Loch Ness Monster
```

#### replace()

You use replace() for simple substring substitution. Give it the old substring, the new one, and how many instances of the old substring to replace.
It returns the changed string but does not modify the original string.

```python
> setup = "a duck goes into a bar..."
> setup.replace('duck', 'marmoset')     # 'a marmoset goes into a bar...'
> setup                                 # 'a duck goes into a bar...'

# Change up to 100 of them:
> setup.replace('a ', 'a famous ', 100) #'a famous duck goes into a famous bar...'
```

#### strip()

It’s very common to strip leading or trailing “padding” characters from a string, especially spaces. The strip() functions shown here assume that you want to get rid of whitespace characters (' ', '\t', '\n') if you don’t give them an argument.

```python
> world = " earth "
> world.strip()    # 'earth'
> world.strip(' ') # 'earth'
> world.lstrip()   # 'earth '
> world.rstrip()   # ' earth'

> blurt = "What the...!!?"
> blurt.strip('.?!')  # 'What the'

> import string
> string.whitespace   # ' \t\n\r\x0b\x0c'
> string.punctuation  # '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
> blurt = "What the...!!?"
> blurt.strip(string.punctuation) 'What the'

> prospector = "What in tarnation ...??!!"
> prospector.strip(string.whitespace + string.punctuation)  # 'What in tarnation'
```

#### Search and Select

```python
> poem = '''All that doth flow we cannot liquid name
... Or else would fire and water be the same;
... But that is liquid which is moist and wet
... Fire that property can never get.
... Then 'tis not cold that doth the fire put out
... But 'tis the wet that makes it die, no doubt.'''

# How many characters are in this poem? (Spaces and newlines are included in the count.)
> len(poem)
250

# Does it start with the letters All?
> poem.startswith('All')  # True

# Does it end with That's all, folks!?
> poem.endswith('That\'s all, folks!')  # False
```

Python has two methods (find() and index()) for finding the offset of a substring,
and has two versions of each (starting from the beginning or the end). They work the
same if the substring is found. If it isn’t, find() returns -1, and index() raises an
exception.

```python
# the offset of the first occurrence of the word
> word = 'the'
> poem.find(word)
73
> poem.index(word)
73

# And the offset of the last occurrence:
> poem.rfind(word)
214
> poem.rindex(word)
214

> word = "duck"
> poem.find(word)   # -1
> poem.index(word)  # ValueError: substring not found

# How many times does the three-letter sequence the occur?
> word = 'the'
> poem.count(word)  # 3

# Are all of the characters in the poem either letters or numbers?
> poem.isalnum()  # False
# Nope, there were some punctuation characters.
```

#### case

```python
> setup = 'a duck goes into a bar...'

# Capitalize the first word:
> setup.capitalize()  # 'A duck goes into a bar...'

# Capitalize all the words:
> setup.title()       # 'A Duck Goes Into A Bar...'

# Convert all characters to uppercase:
> setup.upper()       # 'A DUCK GOES INTO A BAR...'

# Convert all characters to lowercase:
> setup.lower()       # 'a duck goes into a bar...'

# Swap uppercase and lowercase:
> setup = 'A Duck Goes Into A Bar...'
> setup.swapcase()    # 'a dUCK gOES iNTO a bAR...'
```

#### Formatting

```python
> thing = 'wereduck'
> place = 'werepond'
> f'The {thing} is in the {place}'  # 'The wereduck is in the werepond'
> f'The {thing.capitalize()} is in the {place.rjust(20)}'  # 'The Wereduck is in the werepond'

# f-strings use the same formatting language (width, padding, alignment) as new-style
> f'The {thing:>20} is in the {place:.^20}'  # 'The wereduck is in the ......werepond......'
> f'{thing =}, {place =}'  # thing = 'wereduck', place = 'werepond'
> f'{thing[-4:] =}, {place.title() =}'  # thing[-4:] = 'duck', place.title() = 'Werepond'
>>> f'{thing = :>4.4}'  # thing = 'were'
```

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

Python runs on an interpreter system(No need to compile and convert into machine language program), meaning that code can be executed as soon as it is written. This means that prototyping can be very quick.

| The ENDDDDD! |
| ------------ |
