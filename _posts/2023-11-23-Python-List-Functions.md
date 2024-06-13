---
title: "Python List Functions"
date: 2023-11-23
layout: post
author: jeevan
featured: true
image: "/assets/images/banner/python.jpg"
categories: [python]
permalink: /python/:title
---

Uncover the power of manipulating lists in Python. Learn essential functions to simplify your code and boost your programming skills effortlessly

> Lists are mutable

> Lists are heterogeneous, it may contain data types like Integers, Strings, as well as Objects.

## Declare Empty List

```python
a = []
b = list()
```

## Declare List

```python
a = [1, 2, 3]
b = [1, 'table', 3.14]
```

## Accessing elements

```python
cars = ["vw", "ford", "kia"]

cars[1]
# "ford"

cars[-1]
# "kia"
```

## Updating elements

```python
cars = ["vw", "ford", "kia"]

cars[1] = "honda"
# ["vw", "honda", "kia"]

cars[-1] = "nissan"
# ["vw", "honda", "nissan"]
```

## Length of list

```python
cars = ["vw", "ford", "kia"]
len(cars)
# 3
```

## Sub-list

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

## Concatenation and Replication

```python
[1, 2, 3] + ['A', 'B', 'C']
# [1, 2, 3, 'A', 'B', 'C']

['1', '2', '3'] * 3
# ['1', '2', '3', '1', '2', '3', '1', '2', '3']
```

## For loop

```python
cars = ["vw", "ford", "kia"]

for car in cars:
    print(car)
# vw
# ford
# kia

for index, car in enumerate(cars):
    print(f'index: {index} - car: {car}')
# index: 0 - item: vw
# index: 1 - item: ford
# index: 2 - item: kia
```

## in and not in operators

```python
cars = ["vw", "ford", "kia"]
"vw" in cars
# True

"VW" in cars
# False

"VW" not in cars
# True
```

## List functions

```python
cars = ["vw", "ford", "kia"]

# Search for an element in the list
cars.index("food")
# 1

cars.index("honds")
# ValueError: 'kiaa' is not in list
# It will raise an exception

# Adding values at the end of the list
cars.append("honda")
# ["vw", "ford", "kia", "honda"]

# Adding values at a specific index
cars.insert(1, "nissan")
# ["vw", "nissan", "ford", "kia", "honda"]

# Remove values from the list
cars.remove("kia")
# ["vw", "nissan", "ford", "honda"]

cars.append("ford")
# ["vw", "nissan", "ford", "honda", "ford"]

cars.remove("ford")
# ['vw', 'nissan', 'honda', 'ford']
# If there are duplicate values it will only remove the first value

# Remove element using index
del cars[1]
# ['vw', 'honda', 'ford']

# pop() will remove and return the value of the element that got removed
cars.pop()
# "ford"
print(cars)
# ['vw', 'honda']

cars.pop(0)
# "vw"
print(cars)
# ['honda']
```

## Sorting Lists

```python
cars = ["vw", "ford", "kia"]
cars.sort()
print(cars)
# ['ford', 'kia', 'vw']
```

## Python Double Colon (::) Syntax

Here's what the syntax for the double colons looks like:\
`collection[start:stop:step]`

```python
numbers = [1,2,3,4,5,6]

print(numbers[::2])
# [1, 3, 5]
```

Reverse a list

```python
cars = ["vw", "ford", "kia"]

cars.reverse()

# Syntax: cars[start:stop:step]
cars[::-1]
# ["kia", "ford", "vw"]
```
