---
title: "Python Basics"
date: 2023-11-27
layout: post
author: jeevan
categories: [python]
permalink: /python/:title
image: "/assets/images/banner/python.jpg"
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
> y = 5
> x = 12 - y
> x
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

#### Dictionary Comprehensions

```python
> word = 'letters'
> letter_counts = {letter: word.count(letter) for letter in word}
> letter_counts  # {'l': 1, 'e': 2, 't': 2, 'r': 1, 's': 1}

# {key_expression : value_expression for expression in iterable if condition}
> vowels = 'aeiou'
> word = 'onomatopoeia'
> vowel_counts = {letter: word.count(letter) for letter in set(word) if letter in vowels}
> vowel_counts  # {'e': 1, 'i': 1, 'o': 4, 'a': 2}
```

## Sets

A set is like a dictionary with its values thrown away, leaving only the keys

#### Create with set()

```python
> empty_set = set()
> empty_set  # set()

> even_numbers = {0, 2, 4, 6, 8}
> even_numbers  # {0, 2, 4, 6, 8}
```

#### Convert with set()

You can create a set from a list, string, tuple, or dictionary, discarding any duplicate values.

```python
> set( 'letters' )  # {'l', 'r', 's', 't', 'e'}

> set(['Dasher', 'Dancer', 'Prancer', 'Mason-Dixon'])
# {'Dancer', 'Dasher', 'Mason-Dixon', 'Prancer'}

> set(('Ummagumma', 'Echoes', 'Atom Heart Mother'))
# {'Ummagumma', 'Atom Heart Mother', 'Echoes'}

> set({'apple': 'red', 'orange': 'orange', 'cherry': 'red'})
# {'cherry', 'orange', 'apple'}
```

#### Add an Item & Delete an Item

```python
> s = set((1,2,3))
> s.add(4)
> s  # {1, 2, 3, 4}

> s = set((1,2,3))
> s.remove(3)
> s  # {1, 2}
```

#### Combinations and Operators

```python
> bruss = {'vodka', 'kahlua'},
> wruss = {'cream', 'kahlua', 'vodka'}

> bruss & wruss  # {'kahlua', 'vodka'}
> bruss.intersection(wruss)

> bruss | wruss  # {'kahlua', 'vodka', 'cream'}
> bruss.union(wruss)

> wruss - bruss  # {'cream'}
> wruss.difference(bruss)

> bruss.issubset(wruss)  # True
> wruss.issubset(bruss)  # False
```

## Functions

A function can take any number and type of input parameters and return any number and type of output results.

- Define it, with zero or more parameters
- Call it, and get zero or more results

```python
> def print_me():
>   print('python')
> print_me() # python
```

#### Parameters & Arguments

```python
def func(foo, bar=None, **kwargs): # Parameters
    pass

func(42, bar=314, extra=somevar) # Arguments
```

##### Positional Arguments

```python
> def menu(wine, entree, dessert):
>   return {'wine': wine, 'entree': entree, 'dessert': dessert}

> menu('chardonnay', 'chicken', 'cake')
# {'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'cake'}
```

##### Keyword Arguments

```python
> menu(entree='beef', dessert='bagel', wine='bordeaux')
# {'wine': 'bordeaux', 'entree': 'beef', 'dessert': 'bagel'}
```

##### Mix of Positional and Keyword Arguments

If you call a function with both positional and keyword arguments, the positional arguments need to come first.

```python
> menu('frontenac', dessert='flan', entree='fish')
# {'wine': 'frontenac', 'entree': 'fish', 'dessert': 'flan'}
```

#### Default Parameter Values

```python
> def menu(wine, entree, dessert='pudding'):
>   return {'wine': wine, 'entree': entree, 'dessert': dessert}

> menu('chardonnay', 'chicken')
# {'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'pudding'}

> menu('dunkelfelder', 'duck', 'doughnut')
# {'wine': 'dunkelfelder', 'entree': 'duck', 'dessert': 'doughnut'}
```

#### Explode/Gather Positional Arguments with \*

**Arbitrary Arguments - \*args**\
When used inside the function with a parameter, an asterisk groups a variable number of positional arguments into a single tuple of parameter values.

```python
> def print_args(*args):
>   print('Positional tuple:', args)

> print_args()
# Positional tuple: ()

> print_args(3, 2, 1, 'wait!', 'uh...')
# Positional tuple: (3, 2, 1, 'wait!', 'uh...')
```

If you do not know how many arguments that will be passed into your function, add a \* before the parameter name in the function definition.

```python
> def print_more(required1, required2, *args):
>   print('Need this one:', required1)
>   print('Need this one too:', required2)
>   print('All the rest:', args)

> print_more('cap', 'gloves', 'scarf', 'monocle', 'mustache wax')
# Need this one: cap
# Need this one too: gloves
# All the rest: ('scarf', 'monocle', 'mustache wax')
```

You can only use the \* syntax in a function call or definition:

```python
> print_args(2, 5, 7, 'x')
# Positional tuple: (2, 5, 7, 'x')

> args = (2,5,7,'x')
> print_args(args)
# Positional tuple: ((2, 5, 7, 'x'),)

> print_args(*args)
# Positional tuple: (2, 5, 7, 'x')

> *args
# File "<stdin>", line 1
# SyntaxError: can't use starred expression here
```

#### Explode/Gather Keyword Arguments with \*\*

**Arbitrary Keyword Arguments, \*\*kwargs**\

You can use two asterisks (\*\*) to group keyword arguments into a dictionary, where the argument names are the keys, and their values are the corresponding dictionary values

```python
> def print_kwargs(**kwargs):
>   print('Keyword arguments:', kwargs)

> print_kwargs()
# Keyword arguments: {}

> print_kwargs(wine='merlot', entree='mutton', dessert='macaroon')
# Keyword arguments:  {'dessert': 'macaroon', 'wine': 'merlot', 'entree': 'mutton'}
```

If you do not know how many keyword arguments that will be passed into your function, add two asterisk: \*\* before the parameter name in the function definition. This way the function will receive a dictionary of arguments.

```python
def my_function(**kid):
  print("His last name is " + kid["lname"])

my_function(fname = "Tobias", lname = "Refsnes")
```

Argument order is:

- Required positional arguments
- Optional positional arguments (\*args)
- Optional keyword arguments (\*\*kwargs)

#### Docstrings

documentation to a function definition

```python
> def echo(anything):
>   'echo returns its input argument'
>   return anything

>>> help(echo)
# Help on function echo in module __main__:
# echo(anything)
#  echo returns its input argument

> print(echo.__doc__)
# echo returns its input argument
```

#### Dunder

Double underscores (aka dunder in Python-speak) are used in many places to name Python internal variables, because programmers are unlikely to use them in their own variable names

#### Funtion as parameter

since function is also an object in python, we can pass the function similar to a normal data type

```python
> def answer():
>   print(42)

> anwser()
# 42

> def run_something(func):
>   func()

> run_something(answer)
# 42
```

```python
> def add_args(arg1, arg2):
>   print(arg1 + arg2)

> def run_something_with_args(func, arg1, arg2):
>   func(arg1, arg2)

> run_something_with_args(add_args, 5, 9)
# 14
```

#### Inner Functions

An inner function can be useful when performing some complex task more than once within another function, to avoid loops or code duplication.

```python
> def outer(a, b):
>   def inner(c, d):
>     return c + d
>   return inner(a, b)

> outer(4, 7)
# 11
```

#### Closures

An inner function can act as a closure. This is a function that is dynamically generated by another function and can both change and remember the values of variables that were created outside the function

```python
> def knights2(saying):
>   def inner2():
>     return "We are the knights who say: '%s'" % saying
>   return inner2

> a = knights2('Duck')
> b = knights2('Hasenpfeffer')

> a()
# "We are the knights who say: 'Duck'"
> b()
# "We are the knights who say: 'Hasenpfeffer'"
```

### Anonymous Functions

#### Lambda

A lambda function is a small anonymous function which can take any number of arguments, but can only have one expression.

```python
> x = lambda a : a + 10
> print(x(5))
# 15
```

The power of lambda is better shown when you use them as an anonymous function inside another function. function definition that takes one argument, and that argument will be multiplied with an unknown number

```python
> def myfunc(n):
>   return lambda a : a * n

> mydoubler = myfunc(2)
> mytripler = myfunc(3)

> print(mydoubler(11))
# 121
> print(mytripler(11))
# 1331
```

#### Generators

A generator is a Python sequence creation object. With it, you can iterate through potentially huge sequences without creating and storing the entire sequence in memory at once. Generators are often the source of data for iterators.

Every time you iterate through a generator, it keeps track of where it was the last time it was called and returns the next value. This is different from a normal function, which has no memory of previous calls and always starts at its first line with the same state.

```python
> sum(range(1, 101))
# 5050
```

##### Generator functions

```python
> def my_range(first=0, last=10, step=1):
>   number = first
>   while number < last:
>     yield number
>     number += step

> ranger = my_range(1, 4)
> ranger
# <generator object my_range at 0x101a0a168>

> for x in ranger:
>   print(x)
# 1
# 2
# 3

# A generator can be run only once. Lists, sets, strings, and dictionaries exist in memory, but a generator creates its values on the fly and hands them out one at a time through an iterator. It doesn’t remember them, #so you can’t restart or back up a generator. If you try to iterate this generator again, you’ll find # that it’s tapped out:
> for try_again in ranger:
>   print(try_again)
#
```

##### Generator Comprehensions

It’s like a shorthand version of a generator function, doing the yield invisibly, and also returns a generator object

```python
> genobj = (pair for pair in zip(['a', 'b'], ['1', '2']))
> for thing in genobj:
>   print(thing)

# ('a', '1')
# ('b', '2')
```

#### Decorators

A decorator is a function that takes one function as input and returns another function.

Sometimes, you want to modify an existing function without changing its source code. A common example is adding a debugging statement to see what arguments were passed in.

```python
> def document_it(func):
>   def new_function(*args, **kwargs):
>     print('Running function:', func.__name__)
>     print('Positional arguments:', args)
>     print('Keyword arguments:', kwargs)
>     result = func(*args, **kwargs)
>     print('Result:', result)
>     return result
>   return new_function
```

```python
> def add_ints(a, b):
>   return a + b
> add_ints(3, 5)
# 8

> cooler_add_ints = document_it(add_ints) # manual decorator assignment
> cooler_add_ints(3, 5)
# Running function: add_ints
# Positional arguments: (3, 5)
# Keyword arguments: {}
# Result: 8
# 8
```

As an alternative to the manual decorator we can add @decorator_name before the function that you want to decorate:

```python
> @document_it
> def add_ints(a, b):
>   return a + b
```

#### Namespaces and Scope

Each function defines its own namespace

The main part of a program defines the global namespace; thus, the variables in that namespace are global variables

```python
> animal = 'fruitbat'
> def change_local():
>   animal = 'wombat'
>   print('inside change_local:', animal, id(animal))

> change_local()
# inside change_local: wombat 4330406160
> animal
# 'fruitbat'
> id(animal)
# 4330390832
```

```python
> animal = 'fruitbat'
> def change_and_print_global():
>   global animal
>   animal = 'wombat'
>   print('inside change_and_print_global:', animal)

> animal
# 'fruitbat'
> change_and_print_global()
# inside change_and_print_global: wombat
> animal
# 'wombat'
```

##### locals & globals functions

```python
> animal = 'fruit'
> def change_local():
>   animal = 'wombat'
>   print('locals:', locals())

> animal
# 'fruit'
> change_local()
# locals: {'animal': 'wombat'}
> print('globals', globals())
# globals {'__name__': '__main__',
# '__doc__': None,
# '__package__': None,
# '__loader__': <class '_frozen_importlib.BuiltinImporter'>,
# '__spec__': None,
# '__annotations__': {},
# '__builtins__': <module 'builtins' (built-in)>,
# 'animal': 'fruit',
# 'change_local': <function change_local at 0x000002B5211C1940>}
```

#### Uses of \_ and \_\_ in Names

Names that begin and end with two underscores (\_\_) are reserved for use within Python, so you should not use them with your own variables.

#### Recursion

```python
> def flatten(lol):
>   for item in lol:
>     if isinstance(item, list):
>       for subitem in flatten(item):
>         yield subitem
>     else:
>       yield item

> lol = [1, 2, [3,4,5], [6,[7,8,9], []]]
> flatten(lol)
# <generator object flatten at 0x10509a750>
> list(flatten(lol))
# [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Updated in python3.3
> def flatten(lol):
>   for item in lol:
>     if isinstance(item, list):
>       yield from flatten(item)
>     else:
>       yield item

> lol = [1, 2, [3,4,5], [6,[7,8,9], []]]
> list(flatten(lol))
# [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Exceptions

```python
> short_list = [1, 2, 3]
> try:
>   short_list[5]
> except:
>   print('Need a position between 0 and', len(short_list)-1)
# Need a position between 0 and 2
```

But we can use multiple exceptions & use a default one

```python
> while True:
>   value = input('Position [q to quit]? ')
>   if value == 'q':
>     break
>   try:
>     position = int(value)
>     print(short_list[position])
>   except IndexError as err:
>     print('Bad index:', position)
>   except Exception as other:
>     print('Something else broke:', other)
# Position [q to quit]? 3
# Bad index: 3
# Position [q to quit]? 2
# 3
# Position [q to quit]? two
# Something else broke: invalid literal for int() with base 10: 'two'
```

## Classes & Objects

Python is an object oriented programming language. Almost everything in Python is an object, with its properties and methods. A Class is like an object constructor, or a "blueprint" for creating objects.

An object is a custom data structure containing both data (variables, called attributes) and code (functions, called methods). you can have multiple objects (often referred to as instances) at the same time, each with potentially different attributes.

```python
> class Cat():
>   pass

>  a_cat = Cat()
```

### Attributes

An attribute is a variable inside a class or object. During and after an object or class is created, you can assign attributes to it

```python
> a_cat.age = 3
> a_cat.name = "Mr. Fuzzybuttons"

> a_cat.age
# 3
> a_cat.name
# 'Mr. Fuzzybuttons'
```

### Methods

A method is a function in a class or object

#### Initialization

If you want to assign object attributes at creation time, you need the special Python object initialization method \*\*init\*\*():

```python
# Without initialization
> class Cat():
>   pass

> t1 = Cat()
> t1.name = "test"
> t1.age = 3
> t1.name
# 'test'

# With initialization
> class Cat1():
>   def __init__(self, name, age):
>     self.name = name
>     self.age = age

> t2 = Cat1("test", 3)
> t2.name
# 'test'

> del p1.name # Delete Attribute
> del p1 # Delete object
```

It’s not what some other languages would call a “constructor.” Python already constructed the object for you. Think of \*\*init\*\*() as an initializer

The `self` parameter is a reference to the current instance of the class, and is used to access variables that belongs to the class. It does not have to be named `self` , you can call it whatever you like, but it has to be the first parameter of any function in the class

#### Python Inheritance

Inheritance allows us to define a class that inherits all the methods and properties from another class. Parent class is the class being inherited from, also called base/super class. Child class is the class that inherits from another class, also called derived/sub class.

```python
> class Person:
>   def __init__(self, fname, lname):
>     self.firstname = fname
>     self.lastname = lname

> def printname(self):
>   print(self.firstname, self.lastname)

> x = Person("John", "Doe")
> x.printname()
# "John", "Doe"


> class Student(Person):
>   pass # Use the pass keyword when you do not want to add any other properties or methods to the class.

# Now the Student class has the same properties and methods as the Person class.
> y = Student("Mike", "Olsen")
> y.printname()
# "Mike", "Olsen"
```

##### Override a Method

```python
> class Student(Person):
>   def printname(self):
>     print(self.firstname + " - " + self.lastname)

> z = Student("Mike", "Olsen")
> z.printname()
# "Mike - Olsen"
```

##### Override \_\_init\_\_() Function

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

#### Multiple Inheritance

Inheritance in Python depends on method resolution order. Each Python class has a special method called mro() that returns a list of the classes that would be visited to find a method or attribute for an object of that class. A similar attribute, called \_\_mro\_\_, is a tuple of those classes

```python
> class Animal:
>   def says(self):
>     return 'I speak!'

> class Horse(Animal):
>   def says(self):
>     return 'Neigh!'

> class Donkey(Animal):
>   def says(self):
>     return 'Hee-haw!'

> class Mule(Donkey, Horse):
>   pass

> class Hinny(Horse, Donkey):
>   pass

> mule = Mule()
> hinny = Hinny()
> mule.says()
# 'hee-haw'
> hinny.says()
# 'neigh'
```

##### Mixins

The difference is subtle, but in the above examples, the mixin classes weren't made to stand on their own. In more traditional multiple inheritance, the AuthenticationMixin (for example) would probably be something more like Authenticator. That is, the class would probably be designed to stand on its own.

```python
> class Request(BaseRequest):
>    pass

# If I want to add accept header support, I would make that
> from werkzeug import BaseRequest, AcceptMixin
> class Request(AcceptMixin, BaseRequest):
>    pass

# If I wanted to make a request object that supports accept headers, etags, authentication, and user agent support, I could do this:
> from werkzeug import BaseRequest, AcceptMixin, ETagRequestMixin, UserAgentMixin, AuthenticationMixin
> class Request(AcceptMixin, ETagRequestMixin, UserAgentMixin, AuthenticationMixin, BaseRequest):
>    pass
```

### Attribute Access

object attributes and methods are public

#### Direct Access

```python
> class Duck:
>   def __init__(self, input_name):
>     self.name = input_name

> fowl = Duck('Daffy')
> fowl.name
# 'Daffy'
> fowl.name = 'Daphne'
> fowl.name
# 'Daphne'
```

#### Getters and Setters

Python doesn’t have private attributes, but you can write getters and setters with obfuscated attribute names to get a little privacy

By default, no one knows that "hidden_name" attribute exists inside the class

```python
> class Duck():
>   def __init__(self, input_name):
>     self.hidden_name = input_name
>   def get_name(self):
>     return self.hidden_name
>   def set_name(self, input_name):
>     self.hidden_name = input_name

> don = Duck('Donald')
> don.get_name()
# 'Donald'
> don.set_name('Donna')
> don.get_name()
# 'Donna'
```

#### Properties for Attribute Access

The Pythonic solution for attribute privacy is to use properties.

```python
> class Duck():
>   def __init__(self, input_name):
>     self.hidden_name = input_name
>   def get_name(self):
>     return self.hidden_name
>   def set_name(self, input_name):
>     self.hidden_name = input_name
>   name = property(get_name, set_name)

> class Duck1():
>   def __init__(self, input_name):
>     self.hidden_name = input_name
>   @property
>   def name(self):
>     return self.hidden_name
>   @name.setter
>   def name(self, input_name):
>     self.hidden_name = input_name

> fowl = Duck('Howard')
> fowl.name
# 'Howard'
> fowl.name = 'Donald'
> fowl.name
# 'Donald'
```

#### Properties for Computed Values

A property can return a computed value

```python
> class Circle():
>   def __init__(self, radius):
>     self.radius = radius
>   @property
>   def diameter(self):
>     return 2 * self.radius

> c = Circle(5)
> c.diameter()
# 10
> c.diameter
# 10
```

#### Name Mangling for Privacy

Python has a naming convention for attributes that should not be visible outside of their class definition: begin with two underscores (\_\_).

```python
> class Duck():
>   def __init__(self, input_name):
>     self.__name = input_name
>   @property
>   def name(self):
>     print('inside the getter')
>     return self.__name
>   @name.setter
>   def name(self, input_name):
>     print('inside the setter')
>     self.__name = input_name

> fowl = Duck('Howard')
> fowl.name
# inside the getter
# 'Howard'
> fowl.name = 'Donald'
# inside the setter
> fowl.name
# inside the getter
# 'Donald'

> fowl.__name
# Traceback (most recent call last):
# File "<stdin>", line 1, in <module>
# AttributeError: 'Duck' object has no attribute '__name'
```

This naming convention doesn’t make it completely private, but Python does mangle the attribute name to make it unlikely for external code to stumble upon it.

```python
> fowl._Duck__name
# 'Donald'
```

Notice that it didn’t print inside the getter. Although this isn’t perfect protection, name mangling discourages accidental or intentional direct access to the attribute.

#### Class and Object Attributes

You can assign attributes to classes, and they’ll be inherited by their child objects. But if you change the value of the attribute in the child object, it doesn’t affect the class attributeIf you change the class attribute later, it won’t affect existing child objects. But it will affect new ones:

```python
> class Fruit:
>   color = 'red'
> blueberry = Fruit()
> Fruit.color
# 'red'
> blueberry.color
# 'red'
> blueberry.color = 'blue'
> blueberry.color
# 'blue'
> Fruit.color
# 'red'
> Fruit.color = 'orange'
> Fruit.color
# 'orange'
> blueberry.color
# 'blue'
> new_fruit = Fruit()
> new_fruit.color
# 'orange'
```

#### Method Types

Some methods are part of the class itself, some are part of the objects that are created from that class, and some are none of the above:

- If there’s no preceding decorator, it’s an instance method, and its first argument should be self to refer to the individual object itself.
- If there’s a preceding @classmethod decorator, it’s a class method, and its first argument should be cls (or anything, just not the reserved word class), referring to the class itself.
- If there’s a preceding @staticmethod decorator, it’s a static method, and its first argument isn’t an object or class.

##### Instance Methods

When you see an initial self argument in methods within a class definition, it’s an instance method. These are the types of methods that you would normally write when creating your own classes. The first parameter of an instance method is self, and Python passes the object to the method when you call it. These are the ones that
you’ve seen so far.

##### Class Methods

In contrast, a class method affects the class as a whole. Any change you make to the class affects all of its objects. Within a class definition, a preceding @classmethod decorator indicates that that following function is a class method. Also, the first parameter to the method is the class itself. The Python tradition is to call the parameter cls, because class is a reserved word and can’t be used here. Let’s define a class method
for A that counts how many object instances have been made from it:

```python
> class A():
>   count = 0
>   def __init__(self):
>     A.count += 1
>   def exclaim(self):
>     print("I'm an A!")
>   @classmethod
>   def kids(cls):
>     print("A has", cls.count, "little objects.")

> easy_a = A()
> breezy_a = A()
> wheezy_a = A()
> A.kids()
# A has 3 little objects.
```

Notice that we referred to A.count (the class attribute) in \*\*init\*\*() rather than self.count (which would be an object instance attribute). In the kids() method, we used cls.count, but we could just as well have used A.count.

##### Static Methods

A third type of method in a class definition affects neither the class nor its objects; it’s just in there for convenience instead of floating around on its own. It’s a static method, preceded by a @staticmethod decorator, with no initial self or cls parameter.

```python
> class CoyoteWeapon():
>   @staticmethod
>   def commercial():
>     print('This CoyoteWeapon has been brought to you by Acme')
>
> CoyoteWeapon.commercial()
# This CoyoteWeapon has been brought to you by Acme
```

#### Duck Typing

Python has a loose implementation of polymorphism; it applies the same operation to different objects, based on the method’s name and arguments, regardless of their class.

```python
> class Quote():
>   def __init__(self, person, words):
>     self.person = person
>     self.words = words
>   def who(self):
>     return self.person
>   def says(self):
>     return self.words + '.'
>
> class QuestionQuote(Quote):
>   def says(self):
>     return self.words + '?'

> hunter = Quote('Elmer Fudd', "I'm hunting wabbits")
> print(hunter.who(), 'says:', hunter.says())
# Elmer Fudd says: I'm hunting wabbits.
> hunted1 = QuestionQuote('Bugs Bunny', "What's up, doc")
> print(hunted1.who(), 'says:', hunted1.says())
# Bugs Bunny says: What's up, doc?
```

#### Magic Methods

Python special methods, The names of these methods begin and end with double underscores (\_\_) because They’re very unlikely to have been chosen by programmers as variable names. (dunder)

```python
> class Word():
>   def __init__(self, text):
>     self.text = text

> def equals(self, word2):
>   return self.text.lower() == word2.text.lower()

> first = Word('ha')
> second = Word('HA')
> third = Word('eh')
> first.equals(second)
# True
> first.equals(third)
# False
```

Replace equal function with \_\_eq\_\_

```python
> class Word():
>   def __init__(self, text):
>     self.text = text
>   def __eq__(self, word2):
>     return self.text.lower() == word2.text.lower()
```

Magic Mathods for comparision

| Method                  | Description   |
| :---------------------- | :------------ |
| \_\_eq\_\_(self, other) | self == other |
| \_\_ne\_\_(self, other) | self != other |
| \_\_lt\_\_(self, other) | self < other  |
| \_\_gt\_\_(self, other) | self > other  |
| \_\_le\_\_(self, other) | self <= other |
| \_\_ge\_\_(self, other) | self >= other |

Magic methods for math

| Method                  | Description   |
| :---------------------- | :------------ |
| \_\_eq\_\_(self, other) | self == other |
| \_\_ne\_\_(self, other) | self != other |
| \_\_lt\_\_(self, other) | self < other  |
| \_\_gt\_\_(self, other) | self > other  |
| \_\_le\_\_(self, other) | self <= other |
| \_\_ge\_\_(self, other) | self >= other |

Miscellaneous magic methods

| Method               | Description  |
| :------------------- | :----------- |
| \_\_str\_\_( self )  | str( self )  |
| \_\_repr\_\_( self ) | repr( self ) |
| \_\_len\_\_( self )  | len( self )  |

If you fail to define either \_\_str\_\_() or \_\_repr\_\_(), you get Python’s default string version of your object:

```python
> first = Word('ha')
> first
# <__main__.Word object at 0x1006ba3d0>
> print(first)
# <__main__.Word object at 0x1006ba3d0>

> class Word():
>   def __init__(self, text):
>     self.text = text
>   def __eq__(self, word2):
>     return self.text.lower() == word2.text.lower()
>   def __str__(self):
>     return self.text
>   def __repr__(self):
>     return 'Word("' + self.text + '")'

> first = Word('ha')
> first # uses __repr__
# Word("ha")
> print(first) # uses __str__
# ha
```

Other python magic functions: http://bit.ly/pydocs-smn

### Aggregatoin and Composition

Unline inheritance, composiotion is not a type of the parent class but a part of the parent class

```python
> class Bill():
>   def __init__(self, description):
>     self.description = description
> class Tail():
>   def __init__(self, length):
>     self.length = length
> class Duck():
>   def __init__(self, bill, tail):
>     self.bill = bill
>     self.tail = tail
>   def about(self):
>     print('This duck has a', self.bill.description, 'bill and a', self.tail.length, 'tail')

> a_tail = Tail('long')
> a_bill = Bill('wide orange')
> duck = Duck(a_bill, a_tail)
> duck.about()
# This duck has a wide orange bill and a long tail
```

### When to Use Objects or Something Else

- Objects are most useful when you need a number of individual instances that have similar behavior (methods), but differ in their internal states (attributes).
- If you have a number of variables that contain multiple values and can be passed as arguments to multiple functions, it might be better to define them as classes.

#### Dataclasses

```python
> class TeenyClass():
>   def __init__(self, name):
>     self.name = name

> teeny = TeenyClass('itsy')
> teeny.name
# 'itsy'

> from dataclasses import dataclass
> @dataclass
> class AnimalClass:
>   name: str
>   habitat: str
>   teeth: int = 0

> snowman = AnimalClass('yeti', 'Himalayas', 46)
> duck = AnimalClass(habitat='lake', name='duck')
> snowman
# AnimalClass(name='yeti', habitat='Himalayas', teeth=46)
> duck
# AnimalClass(name='duck', habitat='lake', teeth=0)
```

## Modules

A module is just a file of any Python code. You don’t need to do anything special—any Python code can be used as a module by others. We refer to code of other modules by using the Python import statement.

```python
# Filename - fast.py

> from random import choice

> places = ['McDonalds", "KFC", "Burger King", "Taco Bell", "Wendys", "Arbys", "Pizza Hut"]
> def pick(): # see the docstring below?
>   """Return random fast food place"""
>   return choice(places)
```

Importing the above file/module from another file

```python
# Filename - lunch.py
> import fast

> place = fast.pick()
> print("Let's go to", place)

> python lunch.py
# Let's go to Burger King
```

Import a Module with Another Name

```python
> import fast as f
> place = f.pick()
> print("Let's go to", place)

> from fast import pick as who_cares
> place = who_cares()
> print("Let's go to", place)

```

## Module vs function

```python
import test.py
```

## Miscellaneous

### Iterator

An iterable is anything you're able to iterate over, anything you can write a for loop

Ex: List, Tuple, Sets, String, dictionary, generator, files

```python
cars = ["vw", "kia"]

for car in cars:
  print(car)

list('hello world')

for n, car in enumerate(cars):
    print(n, car)

# With starting index 1
for n, car in enumerate(cars, start = 1):
    print(n, car)
```

### Range

Range objects don't store the value, they compute it on the go

```python
cars = ["vw", "kia"]
car_iterator = iter(cars)

```

### Sequence

iterables that can be indexed

### Range vs Iterator

Range object seems like iterator but not iterator

- Iterator will compute its next item if you loop over

```python
> cars = ["vw", "kia"]
> car_iterator = iter(cars)
> for car in car_iterator:
>   print(car)
# 'vw'
# 'kia'

> for car in car_iterator:
>   print(car)
# nothing will be printed here since iter has reached its end

> cars1 = range(3)
> for i in cars1:
>   print(i)
# 0
# 1
# 2

> for i in cars1:
>   print(i)
# 0
# 1
# 2
```

### Reverse

```python
cars = ["vw", "kia"]
cars[::-1]
```

The above slicing syntax works only with DS with index

```python
cars = ["vw", "kia"]
cars.reverse()

text = "Hello"
text.reverse()
# AttributeError: 'str' object has no attribute 'reverse'
```

The list reverse method is an in-place operation (modified the original list)

```python
cars = ["vw", "kia"]
reverse_cars = cars.copy()
reverse_cars.reverse()
for car in reverse_cars:
  print(car)
```

Better alternative is using reversed function

```python
for car in reversed(cars):
  print(car)
```

### Sorted

```python
sorted(cars)
sorted(reverse=True)
```

### Else - For

```python
student_records = [{"name": "jee", "marks": {"a": 80, "b": 60}}, {"name": "jee", "marks": {"a": 80, "b": 80}}]

# Find a candidate with less than 75 marks
outer_break = False
for student in student_records:
  for subject, mark in student["marks"].items():
    if mark < 75:
      print(student["name"])
      outer_break = True
      break

  if outer_break:
    break
```

Can be replaced this with the else - for

```python
for student in student_records:
  for subject, mark in student["marks"].items():
    if mark < 75:
      print(student["name"])
      break
  else:
    continue

  # Trigger the following break if the inner for-loop triggers break
  break
```
