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

> splitme = 'a/b//c/d///e'
> splitme.split('/')  # ['a', 'b', '', 'c', 'd', '', '', 'e']
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

#### range()

The range() function returns a stream of numbers within a specified range. without first having to create and store a large data structure such as a ist or tuple. This lets you create huge ranges without using all the memory in your computer and crashing a program.

syntax: `range(start, stop, step)`

```python
> for x in range(0, 3):
>   print(x)
# 0
# 1
# 2

> list(range(0, 3))
# [0, 1, 2]
```

Q/A:

- Does python store each character in a string in different objects & reuse them?
  - https://stackoverflow.com/questions/57002606/is-string-internally-stored-as-individual-characters-each-character-in-memory-s

## Tuples

Tuples are immutable, when you assign elements to a tuple, it can't be changed

```python
# Create a tuple
> empty_tuple = ()
# ()
```

For creating a one element tuple we need to be careful & declare it with a comma

```python
> one_mark = 'grande',
# ('grande',)

> one_mark = ('grande',)
# ('grande',)

> one_mark = ('grande')
# 'grande'
# This declares the type as string
```

Assign more than one value

```python
> marx_table = 'grande', 'checo', 'marco'
# ('grande', 'checo', 'marco')

> marx_table = ('grande', 'checo', 'marco')
# ('grande', 'checo', 'marco')
```

Tuple Packing/Unpacking

```python
> fruits = ("apple", "banana", "cherry", "strawberry") # Packing
> green, yellow, red, white = fruits                   # Unpacking

> a = '10'
> b = '20'
> a, b = b, a
> print(a, b)  # '20', '10'

> (green, yellow, *red) = fruits
> green   # 'apple'
> yellow  # 'banana'
> red     # ['cherry', 'strawberry']

> (green, *tropic, red) = fruits
> green   # 'apple'
> tropic  # ['banana', 'cherry']
> red     # 'strawberry'
```

Convert a list to tuple

```python
> marx_list = ["apple", "banana", "cherry"]
> tuple(marx_list)  # ("apple", "banana", "cherry")
```

### Tuple Manipulations

```python
# Combine tuples using +
> ('grande', ) + ('chico', 'tree')
# ('grande', 'chico', 'tree')

# Duplicate items with *
> ('yada',) * 3
# ('yada', 'yada', 'yada')
```

## Lists

Lists are good for keeping track of things by their order, especially when the order and contents might change. Unlike strings, lists are mutable. You can change a list in place, add new elements, and delete or replace existing elements. The same value can occur more than once in a list.

```python
# Creation of list
> empty_list = []
> empty_list = list()
> weekdays = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
> big_birds = ['emu', 'ostrich', 'cassowary']
> first_names = ['Graham', 'John', 'Terry', 'Terry', 'Michael']
> leap_years = [2000, 2004, 2008]
> randomness = ['Punxsatawney", {"groundhog": "Phil"}, "Feb. 2"}
```

### list()

list() function also converts other iterable data types (such as tuples, string, sets, and dictionaries) to lists.

```python
> list('cat')
# ['c', 'a', 't']

> a_tuple = ('ready', 'fire', 'aim')
> list(a_tuple)
# ['ready', 'fire', 'aim']
```

#### Get items with list()

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes[0:2]   # ['Groucho', 'Chico']

> marxes[::2]   # ['Groucho', 'Harpo']
> marxes[::-2]  # ['Harpo', 'Groucho']

# reverse a list:
> marxes[::-1]  # ['Harpo', 'Chico', 'Groucho']

# None of these slices changed the marxes list itself, because we didn’t assign them to marxes.
# To reverse a list in place, use list.reverse():
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes.reverse()
> marxes  # ['Harpo', 'Chico', 'Groucho']
# The reverse() function changes the list but doesn’t return its value.
```

#### Add an Item to the End with append()

The traditional way of adding items to a list is to append() them one by one to the end.

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes.append('Zeppo')
> marxes  # ['Groucho', 'Chico', 'Harpo', 'Zeppo']
```

#### Add an Item by Oset with insert()

The append() function adds items only to the end of the list. When you want to add an item before any offset in the list, use insert(). Offset 0 inserts at the beginning. An offset beyond the end of the list inserts at the end, like append(), so you don’t need to worry about Python throwing an exception:

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes.insert(2, 'Gummo')
> marxes  # ['Groucho', 'Chico', 'Gummo', 'Harpo']

> marxes.insert(10, 'Zeppo')
> marxes  # ['Groucho', 'Chico', 'Gummo', 'Harpo', 'Zeppo']
```

#### Combine Lists by Using extend() or +

You can merge one list into another by using extend().

```python
> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> others = ['Gummo', 'Karl']
> marxes.extend(others)
> marxes  # ['Groucho', 'Chico', 'Harpo', 'Zeppo', 'Gummo', 'Karl']

> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> others = ['Gummo', 'Karl']
> marxes += others
> marxes  # ['Groucho', 'Chico', 'Harpo', 'Zeppo', 'Gummo', 'Karl']

# If we had used append(), others would have been added as a single list item rather than merging its items:
> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> others = ['Gummo', 'Karl']
> marxes.append(others)
> marxes  # ['Groucho', 'Chico', 'Harpo', 'Zeppo', ['Gummo', 'Karl']]
```

#### Change Items with a Slice

```python
> numbers = [1, 2, 3, 4]
> numbers[1:3] = [8, 9]
> numbers  # [1, 8, 9, 4]

> numbers = [1, 2, 3, 4]
> numbers[1:3] = [7, 8, 9]
> numbers  # [1, 7, 8, 9, 4]

> numbers = [1, 2, 3, 4]
> numbers[1:3] = []
> numbers  # [1, 4]

# Actually, the righthand thing doesn’t even need to be a list. Any Python iterable will do, separating its items and assigning them to list elements:
> numbers = [1, 2, 3, 4]
> numbers[1:3] = (98, 99, 100)
> numbers  # [1, 98, 99, 100, 4]

> numbers = [1, 2, 3, 4]
> numbers[1:3] = 'wat?'
> numbers  # [1, 'w', 'a', 't', '?', 4]
```

#### Delete an Item by Offset with del

```python
> marxes = ['Groucho', 'Chico', 'Harpo', 'Gummo', 'Karl']
> marxes[-1]  # 'Karl'
> del marxes[-1]
> marxes  # ['Groucho', 'Chico', 'Harpo', 'Gummo']

When you delete an item by its position in the list, the items that follow it move back to take the deleted item’s space, and the list’s length decreases by one.
> marxes = ['Groucho', 'Chico', 'Harpo', 'Gummo']
> del marxes[1]
> marxes  # ['Groucho', 'Harpo', 'Gummo']
```

#### Delete an Item by Value with remove()

If you’re not sure or don’t care where the item is in the list, use remove() to delete it by value. Goodbye, Groucho:

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes.remove('Groucho')
> marxes  # ['Chico', 'Harpo']
# If you had duplicate list items with the same value, remove() deletes only the first one it finds
```

#### Get an Item by Oset and Delete It with pop()

You can get an item from a list and delete it from the list at the same time by using pop(). If you call pop() with an offset, it will return the item at that offset; with no argument, it uses -1.

```python
> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> marxes.pop()   # 'Zeppo'
> marxes         # ['Groucho', 'Chico', 'Harpo']
> marxes.pop(1)  # 'Chico'
> marxes         # ['Groucho', 'Harpo']
```

#### Delete All Items with clear()

```python
> work_quotes = ['Working hard?', 'Quick question!', 'Number one priorities!']
> work_quotes  # ['Working hard?', 'Quick question!', 'Number one priorities!']
> work_quotes.clear()
> work_quotes  # []
```

#### Find an Item’s Offset by Value with index()

```python
> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> marxes.index('Chico')  # 1

# If the value is in the list more than once, only the offset of the first one is returned:
> simpsons = ['Lisa', 'Bart', 'Marge', 'Homer', 'Bart']
> simpsons.index('Bart')  # 1
```

#### Test for a Value with in

```python
> marxes = ['Groucho', 'Chico', 'Harpo', 'Zeppo']
> 'Groucho' in marxes  # True
> 'Bob' in marxes      # False

# The same value may be in more than one position in the list. As long as it’s in there at least once, in will return True:
> words = ['a', 'deer', 'a' 'female', 'deer']
> 'deer' in words  # True
```

#### Count Occurrences of a Value with count()

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> marxes.count('Harpo')  # 1
> marxes.count('Bob')    # 0

> snl_skit = ['cheeseburger', 'cheeseburger', 'cheeseburger']
> snl_skit.count('cheeseburger')  # 3
```

#### Reorder Items with sort() or sorted()

Python provides two functions:

- The list method sort() sorts the list itself, in place.
- The general function sorted() returns a sorted copy of the list.

```python
> marxes = ['Groucho', 'Chico', 'Harpo']
> sorted_marxes = sorted(marxes)
> sorted_marxes  # ['Chico', 'Groucho', 'Harpo']
# sorted_marxes is a new list, and creating it did not change the original list:
> marxes  # ['Groucho', 'Chico', 'Harpo']

# But calling the list function sort() on the marxes list does change marxes:
> marxes.sort()
> marxes  # ['Chico', 'Groucho', 'Harpo']

# mix of data types
> numbers = [2, 1, 4.0, 3]
> numbers.sort()
> numbers  # [1, 2, 3, 4.0]

# The default sort order is ascending, but you can add the argument reverse=True
> numbers = [2, 1, 4.0, 3]
> numbers.sort(reverse=True)
> numbers  # [4.0, 3, 2, 1]
```

#### Copy with copy(), list(), or a Slice

You can copy the values of a list to an independent, fresh list by using any of these methods:

- The list copy() method
- The list() conversion function
- The list slice [:]

```python
>>> a = [1, 2, 3]
>>> b = a.copy()
>>> c = list(a)
>>> d = a[:]
```

#### Copy Everything with deepcopy()

The copy() function works well if the list values are all immutable. As you’ve seen before, mutable values (like lists, tuples, or dicts) are references. A change in the original or the copy would be reflected in both.

```python
> a = [1, 2, [8, 9]]
> b = a.copy()
> a[2][1] = 10
> a  # [1, 2, [8, 10]]
> b  # [1, 2, [8, 10]]
```

The value of a[2] is now a list, and its elements can be changed. All the list-copying methods we used were shallow. To fix this, we need to use the deepcopy() function:

```python
> import copy
> a = [1, 2, [8, 9]]
> b = copy.deepcopy(a)
> a  # [1, 2, [8, 9]]
> b  # [1, 2, [8, 9]]
> a[2][1] = 10
> a  # [1, 2, [8, 10]]
> b  # [1, 2, [8, 9]]
# deepcopy() can handle deeply nested lists, dictionaries, and other objects.
```

#### Iterate Multiple Sequences with zip()

There’s one more nice iteration trick: iterating over multiple sequences in parallel by using the zip() function:

```python
> days = ['Monday', 'Tuesday', 'Wednesday']
> fruits = ['banana', 'orange', 'peach']
> drinks = ['coffee', 'tea', 'beer']
> desserts = ['tiramisu', 'ice cream', 'pie', 'pudding']
> for day, fruit, drink, dessert in zip(days, fruits, drinks, desserts):
>  print(day, ": drink", drink, "- eat", fruit, "- enjoy", dessert)
# Monday : drink coffee - eat banana - enjoy tiramisu
# Tuesday : drink tea - eat orange - enjoy ice cream
# Wednesday : drink beer - eat peach - enjoy pie
```

zip() stops when the shortest sequence is done.

```python
> english = 'Monday', 'Tuesday', 'Wednesday'
> french = 'Lundi', 'Mardi', 'Mercredi'
> list(zip(english, french))
# [('Monday', 'Lundi'), ('Tuesday', 'Mardi'), ('Wednesday', 'Mercredi')]
> dict(zip(english, french) )
# {'Monday': 'Lundi', 'Tuesday': 'Mardi', 'Wednesday': 'Mercredi'}
```

#### List comprehension

offers a shorter syntax when you want to create a new list based on the values of an existing list.
`[expression for item in iterable]`

```python
> newlist = [x for x in range(10)]
> newlist  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

> number_list = [number-1 for number in range(1,6)]
> number_list  # [0, 1, 2, 3, 4]

> newlist = [x for x in range(10) if x < 5]
> newlist  # [0, 1, 2, 3, 4]

> newlist = [x if x % 2 == 0 else False for x in range(10)]
> newlist  # [0, False, 2, False, 4, False, 6, False, 8, False]
```

```python
> rows = range(1,3)
> cols = range(1,3)
> for row in rows:
>  for col in cols:
>    print(row, col)
# 1 1
# 1 2
# 2 1
# 2 2

# Now, let’s use a comprehension and assign it to the variable cells
> cells = [(row, col) for row in rows for col in cols]
> for row, col in cells:
>   print(row, col)
# 1 1
# 1 2
# 2 1
# 2 2
```

Note: del is a Python statement, not a list method you don’t say marxes[-1].del(). It’s sort of the reverse of assignment (=): it detaches a name from a Python object and can free up the object’s memory if that name were the last reference to it

Tip: If you use append() to add new items to the end and pop() to remove them from the same end, you’ve implemented a data structure known as a LIFO (last in, first out) queue. This is more commonly known as a stack. pop(0) would create a FIFO (first in, first out) queue. These are useful when you want to collect data as they arrive and work with either the oldest first (FIFO) or the newest first (LIFO).

Q/A:

- is it okay to use del at the end of every function in python to free up space
  - https://stackoverflow.com/questions/49065803/python-delete-objects-and-free-up-space

## Dictionary

```python
> empty_dict = {}
> acme_customer = {'first': 'Wile', 'middle': 'E', 'last': 'Coyote'}
> acme_customer = dict(first="Wile", middle="E", last="Coyote")
```

Convert with dict()

```python
> lol = [ ['a', 'b'], ['c', 'd'], ['e', 'f'] ]
> dict(lol)  # {'a': 'b', 'c': 'd', 'e': 'f'}

> tos = ( 'ab', 'cd', 'ef' )
> dict(tos)  # {'a': 'b', 'c': 'd', 'e': 'f'}
```

Remember that dictionary keys must be unique. That’s why we used last names for keys instead of first names here—two members of Monty Python have the first name 'Terry'! If you use a key more than once, the last value wins:

```python
> some_pythons = {
>  'Graham': 'Chapman',
>  'John': 'Cleese',
>  'Eric': 'Idle',
>  'Terry': 'Gilliam',
>  'Michael': 'Palin',
>  'Terry': 'Jones',
>  }
> some_pythons
# {'Graham': 'Chapman', 'John': 'Cleese', 'Eric': 'Idle', 'Terry': 'Jones', 'Michael': 'Palin'}
```

#### Get an Item by [key] or with get()

```python
> some_pythons['John']  # 'Cleese'

# If the key is not present in the dictionary, you’ll get an exception:
> some_pythons['Groucho']
# KeyError: 'Groucho'

> 'Groucho' in some_pythons  # False

> some_pythons.get('John')   # 'Cleese'
> some_pythons.get('Groucho', 'Not a Python')  # 'Not a Python'

# Otherwise, you get None (which displays nothing in the interactive interpreter):
> some_pythons.get('Groucho')  #
```

#### Get All Keys with keys()

```python
> signals = {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera'}
> signals.keys()
# dict_keys(['green', 'yellow', 'red'])
```

Note: In Python 2, keys() just returns a list. Python 3 returns dict_keys(), which is an iterable view of the keys. This is handy with large dictionaries because it doesn’t use the time and memory to create and store a list that you might not use. But often you actually do want a list. In Python 3, you need to call list() to convert a dict_keys object to a list.
`list(signals.keys())  # ['green', 'yellow', 'red']`

#### Get All Values with values()

To obtain all the values in a dictionary, use values():

```python
> list( signals.values() )
# ['go', 'go faster', 'smile for the camera']
```

#### Get All Key-Value Pairs with items()

When you want to get all the key-value pairs from a dictionary, use the items()

```python
>>> list( signals.items() )
# [('green', 'go'), ('yellow', 'go faster'), ('red', 'smile for the camera')]
# Each key and value is returned as a tuple, such as ('green', 'go').
```

#### Combine Dictionaries with {**a, **b}

Starting with Python 3.5, there’s a new way to merge dictionaries, using the \*\* unicorn glitter

```python
> first = {'a': 'agony', 'b': 'bliss'}
> second = {'b': 'bagels', 'c': 'candy'}
> {**first, **second}
# {'a': 'agony', 'b': 'bagels', 'c': 'candy'}

> third = {'d': 'donuts'}
> {**first, **third, **second}
# {'a': 'agony', 'b': 'bagels', 'd': 'donuts', 'c': 'candy'}
```

Note: These are shallow copies. use deepcopy() for full copies of the keys and values, with no connection to their origin dictionaries

#### Combine Dictionaries with update()

```python
> first = {'a': 1, 'b': 2}
> second = {'c': 3}
> first.update(second)
> first  # {'a': 1, 'b': 2, 'c': 3}

> first = {'a': 1, 'b': 2}
> second = {'b': 'platypus'}
> first.update(second)
> first  # {'a': 1, 'b': 'platypus'}
```

#### del & pop()

```python
> names = {'a': 'agony', 'b': 'bagels', 'c': 'candy'}
> del names['b']
> names  # {'a': 'agony', 'c': 'candy'}

# Get an Item by Key and Delete It with pop()
> pythons.pop('c')  # 'candy'
> pythons.pop('d')  # KeyError: 'd'

# But if you give pop() a second default argument (as with get()), all is well and the
> pythons.pop('d', 'Hugo')  # 'Hugo'
```

#### clear()

```python
> pythons.clear()  # {}
> pythons = {}     # {}
```

#### in

```python
> pythons = {'Chapman': 'Graham', 'Cleese': 'John'}
> 'Chapman' in pythons  # True
> 'Palin' in pythons    # False
```

#### copy()

As with lists, if you make a change to a dictionary, it will be reflected in all the names that refer to it:

```python
> signals = {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera'}
> save_signals = signals
> signals['blue'] = 'confuse everyone'
> save_signals  # {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera', 'blue': 'confuse everyone'}

# To actually copy keys and values from a dictionary to another dictionary and avoid this, you can use copy():
> signals = {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera'}
> original_signals = signals.copy()
> signals['blue'] = 'confuse everyone'
> signals           # {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera', 'blue': 'confuse everyone'}
> original_signals  # {'green': 'go', 'yellow': 'go faster', 'red': 'smile for the camera'}
```

This is a shallow copy, and works if the dictionary values are immutable (as they are in this case). If they aren’t, you need deepcopy().

```python
> signals = {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'smile']}
> signals_copy = signals.copy()
> signals['red'][1] = 'sweat'
> signals       # {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'sweat']}
> signals_copy  # {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'sweat']}

# You get the usual change-by-either-name behavior. The copy() method copied the values as-is. The solution is deepcopy():
> import copy
> signals = {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'smile']}
> signals_copy = copy.deepcopy(signals)
> signals['red'][1] = 'sweat'
> signals       # {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'sweat']}
> signals_copy  # {'green': 'go', 'yellow': 'go faster', 'red': ['stop', 'smile']}
```

#### Iterate with for and in

Iterating over a dictionary (or its keys() function) returns the keys.

```python
> accusation = {'room': 'ballroom', 'weapon': 'lead pipe', 'person': 'Col. Mustard'}
> for card in accusation: # or, for card in accusation.keys():
>  print(card)
# room
# weapon
# person

# To iterate over the values rather than the keys, you use the dictionary’s values()
> for value in accusation.values():
>  print(value)
# ballroom
# lead pipe
# Col. Mustard

# To return both the key and value as a tuple, you can use the items() function:
> for item in accusation.items():
>  print(item)
# ('room', 'ballroom')
# ('weapon', 'lead pipe')
# ('person', 'Col. Mustard')
> for card, contents in accusation.items():
>  print(card, content)
```

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
