---
title: "Python DS Functions"
date: 2023-11-23
layout: post
author: jeevan
featured: true
image: "/assets/images/banner/python.jpg"
categories: [python]
permalink: /python/:title
---

## Arrays

Import
: `import array`

Creation
: `demo_array = array.array("i", [10, 20, 30, 40, 50])`

Insertion
: `demo_array.insert(5, 60)`

Append &rarr; add at the end of the array
: `demo_array.append(70)`

Extend
: `demo_array1.extend(demo_array)`

Remove
: `demo_array.remove(40)`

pop &rarr; remove last element
: `demo_array.pop() # 70`

Searching
: `demo_array.index(60) # 4`

Traverse
: `for i in demo_array: print(i)`

Traverse with index
: `for i in range(len(demo_array)): print(demo_array[i])`

Accessing
: `array[2]`

Reverse
: `demo_array.reverse()`

buffer_info &rarr; returns the start address and length
: `print(demo_array.buffer_info()) # (2186174443952, 5)`

count &rarr; no of occurrences of the element
: `demo_array.count(60) # 1`

Convert List to Array
: `demo_array.tolist()`

Append List to Array &rarr; Will append to the existing list
: `demo_array.fromList([1, 2, 3])`

Slice
: `demo_array[1:4]`, `demo_array[1:]`, `demo_array[:4]`, `demo_array[:]`

## Lists

Creation
: `a = []`, `b = list()`, `demo_list = [1, 2, 3, 4, 'a', 'b', 'a']`

Update
: `demo_list[1] = 30`

Insertion
: `demo_list.insert(4, 5)`

Append &rarr; add at the end of the array
: `demo_list.append('c')`

Extend
: `demo_list.extend(['d', 'e'])`

Delete
: `del demo_list[1]`

Remove &rarr; If there are duplicate values it will only remove the first value
: `demo_list.remove('a')`
: `demo_list.remove('z') # ValueError: list.remove(x): x not in list`

pop &rarr; remove last element
: `demo_list.pop() # 'e'`, `demo_list.pop(0) # 1`

Concatenation
: `[1, 2, 3] + ['A', 'B', 'C']`

Replication
: `['1', '2', '3'] * 3 # ['1', '2', '3', '1', '2', '3', '1', '2', '3']`

Searching
: `demo_list.index("a") # 4`
: `demo_list.index("f") # ValueError: 'f' is not in list`

Finding &rarr; in and not in operators
: `'f' in demo_list # False`
: `'f' not in demo_list # True`

Traverse
: `for i in demo_list: print(i)`

Traverse with index
: `for i in range(len(demo_list)): print(demo_list[i])`
: `for index, car in enumerate(demo_list): print(f'index: {index} - car: {car}')`

**Accessing**&nbsp;

```python
demo_list[1] # 4
demo_list[-1] # "d"
demo_list[-2] # "c"
```

Reverse
: `demo_list.reverse()`, `demo_list[::-1]`

count &rarr; no of occurrences of the element
: `demo_list.count('a') # 1`

Length of list
: `len(demo_list)`

**Sorting**&nbsp;

```python
cars = ["vw", "ford", "kia"]
cars1 = cars.sort()
print(cars)
# ['ford', 'kia', 'vw']
print(cars1)
# None
```

**Slice (or) Sub-list**&nbsp;

```python
cars = ["vw", "ford", "kia"]

cars[0:3] # same as cars[:3], cars[:], cars[0:]
# ["vw", "ford", "kia"]

cars[0:2] # same as cars[:2]
# ["vw", "ford"]

cars[0:4]
# ["vw", "ford", "kia"]
# @Note: It will not throw any error if it exceeds length

cars[0:-1]
# ["vw", "ford"]

cars[1:3] # Same as cars[1:]
# ["ford", "kia"]

cars[2:3] # Same as cars[2:]
# ["kia"]

# Slicing can also be used as a copy function for lists
cars2 = cars[:]

cars.append("honda")
print(cars)
# ["vw", "ford", "kia", "honda"]

print(cars2)
# ["vw", "ford", "kia"]
```

Double Colon (::) Syntax &rarr; `collection[start:stop:step]`
: `print(numbers[::2]) # [1, 3, 5]`

List to String
: `b = list('python') # ['p','y','t','h','o','n']`

String to List
: `"".join(['p','y','t','h','o','n']) # python`
