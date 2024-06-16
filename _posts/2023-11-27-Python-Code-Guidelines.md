---
title: "Python Code Guidelines"
date: 2023-12-27
layout: post
author: jeevan
categories: [python]
image: "/assets/images/banner/python.jpg"
permalink: /python/:title
published: false
---

Common practices as per pep-8 standard

## Naming convention

- If something is important give it a name, can name non-important variables with i, j

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

## For loop

```python
cars = ["vw", "kia"]
for car in cars:
    print(car)
```

If we need the index or count

```python
for n, car in enumerate(cars):
    print(n, car)

# With starting index 1
for n, car in enumerate(cars, start = 1):
    print(n, car)
```
