---
title: "DSA Overview"
date: 2023-03-18
layout: post
author: jeevan
image: "assets/images/banner/dsa.jpg"
---

## Contents

1. [What is DSA?](#what-is-dsa)
2. [Asymptotic Notations (Big O)](#types-of-asymptotic-notations)
3. [Problem Solving Techniques](#problem-solving-techniques)
4. How to Pick the right DS
5. [Problem Solving Process](#problem-solving-steps)
6. [DS Implementation](#ds-implementation)
   1. [Array](#array)
   2. [List](#lists)
   3. [Tuple](#tuple)

## What is DSA?

Data structures are different ways of organizing data on your computer, that can be used efficiently

### Types of DS

Python has 2 types of DS

1. Primitive data types are the simplest forms of data representation(cannot be broken intro simpler data types)
   1. Built In: **Integer, Float, String, Boolean**
2. Non-Primitive data types are more complex and can store collections of data.
   1. Linear: Elements are arranged in a sequential order
      1. Built In: **List, Tuple**
      2. User Defined: **Array, LinkedList, Stack, Queue**
   2. Non-Linear: Elements are not arranged in a sequential order
      1. Built In: **Set, Dictionary**
      2. User Defined: **Tree, Graph**

| Primitive                              | Non-Primitive                     |
| :------------------------------------- | :-------------------------------- |
| Fixed Size                             | Can shrink or grow                |
| Represented in memory as simple values | Represented in memory as pointers |
| Simple                                 | Complex                           |

### A in DSA

Algorithm: Set of instructions to perform a task

To solve a problem,

1. We need to clean the input data or make it easy to perform tasks on it
2. We need to choose a right data structure for it and should be familiar with implementation and usage
3. Then decide upon a algorithm to solve the problem

### Why are algorithms better than brute force

- Efficient
- Accuracy

## Types of Asymptotic Notations

Asymptotic Notation is used to describe the running time(efficiency) of an algorithm that don’t depend on machine-specific constants

There are mainly three asymptotic notations:

1. Theta - Θ
   - It represents the upper and the lower bound of the running time of an algorithm & used for analyzing the average-case complexity of an algorithm.
2. Omega - Ω
   - It represents the lower bound of the running time of an algorithm & provides the best case complexity of an algorithm
3. Big-O - O
   - It represents the upper bound of the running time of an algorithm & gives the worst-case complexity of an algorithm.

### Runtime Complexities

![Runtime Complexities](/assets/images/runtime-complexities.jpg)

Most Efficient/Constant time complexity - A constant-time complexity is O(1)

```python
def square(n):
  return n * n
```

Good - A logarithmic complexity is Log(N)

```python

```

Fair/Linear Time Complexity - A linear time Complexity is O(N) (As the input grows runtime increases along with it)

```python
for i in range(n):
  print(n * n)

# Even if the function doesn't execute anything inside, code will still loop through
for i in range(n):
  print("Nothing happens here")
```

Bad - A super-linear time complexity is O(N\*Log(N))

```python

```

Most inefficient - A quadratic-time Complexity is O(N^2) or O(N^k) or O(2^N) or O(N!)

```python
for i in range(n):
  for j in range(n):
    print(i + j)
```

### Problem Solving Techniques

- Pointer based
  - Two/Three pointer
  - Sliding window
- Recursion (Top down)
  - Dynamic programming (Bottom up)
  - Memoization
  - Tabulation
  - Backtracking
- Sorting (Bubble, Insertion, Selection, Merge, Quick, Heap)
- Searching
  - Linear
  - Binary Search
  - Naive Binary Search
  - Modified binary search
  - BFS/DFS
- Strings
  - Substrings, subsequences
  - Pattern matching
  - Lexicographic ordering
- Trees
  - Binary trees & Binary search trees
  - Trie
  - Traversals like Inorder, preorder, postorder, and morris traversal (both iterative & recursive)
- Graphs
  - Topological sort, cycle detection, minimum spanning tree (MST)
  - Prims & Kruskals, Dijkstra, Bellman-Ford, Floyd Warshall, disjoint set union (union)
- Divide & Conquer
- Greedy
- Hash Table + Linked List combination
- Searching a Binary Tree
- Exhaustive search
- Bit manipulation
- Segment trees
- Number theory
- Dequeue

## Problem Solving Steps

- Understand the problem.
- Create a step-by-step plan for how you’ll solve it.
- Carry out the plan and write the actual code.
- Look back and possibly refactor your solution if it could be better.

### If we got a requirement saying don't create a new data structure

- We need to switch the elements inside the DS
- We need to update the elements once those are traversed, if we don't use those elements again

### Top 5 Data Structures from 127 interviews

1. Graph
   - Think Graph when you see entities and relationships
   - Bus Routes: [Example](https://lnkd.in/gP8dKC_N)
2. Stack and Queue
   - Think Stack and Queue when you need to store information of a window
   - Largest Rectangle in Histogram: [Example](https://lnkd.in/gvKUB_YA)
3. Hash Map
   - Think Hash Map when you want fast lookups at the cost of extra space
   - Two Sum: [Example](https://lnkd.in/gA7h3KXk)
4. Binary Tree
   - Think recursion for Binary Tree problems
   - Lowest Common Ancestor: [Example](https://lnkd.in/gjXScf4m)
5. Heap
   - Think Heap when you want maximum or minimum fast
   - k Most Frequent Elements in an Array: [Example](https://lnkd.in/g3T6BTqX)

There are always exceptions to the rules but it's good to have a starting point

### Classification by Implementation Method

1. Recursion or Iteration: A recursive algorithm is an algorithm which calls itself again and again until a base condition is achieved whereas iterative algorithms use loops and/or data structures like stacks, queues to solve any problem. Every recursive solution can be implemented as an iterative solution and vice versa.
2. Exact or Approximate: Algorithms that are capable of finding an optimal solution for any problem are known as the exact algorithm. For all those problems, where it is not possible to find the most optimized solution, an approximation algorithm is used. Approximate algorithms are the type of algorithms that find the result as an average outcome of sub outcomes to a problem.
3. Serial or Parallel or Distributed Algorithms: In serial algorithms, one instruction is executed at a time while parallel algorithms are those in which we divide the problem into sub-problems and execute them on different processors. If parallel algorithms are distributed on different machines, then they are known as distributed algorithms.

### Classification by Design Method

1. Greedy Method: In the greedy method, at each step, a decision is made to choose the local optimum, without thinking about the future consequences.
2. Divide and Conquer: The Divide and Conquer strategy involves dividing the problem into sub-problem, recursively solving them, and then recombining them for the final answer.
3. Dynamic Programming: The approach of Dynamic programming is similar to divide and conquer. The difference is that whenever we have recursive function calls with the same result, instead of calling them again we try to store the result in a data structure in the form of a table and retrieve the results from the table. Thus, the overall time complexity is reduced. “Dynamic” means we dynamically decide whether to call a function or retrieve values from the table.
   Example: 0-1 Knapsack, subset-sum problem.
4. Linear Programming: In Linear Programming, there are inequalities in terms of inputs and maximizing or minimizing some linear functions of inputs.
   Example: Maximum flow of Directed Graph
5. Reduction(Transform and Conquer): In this method, we solve a difficult problem by transforming it into a known problem for which we have an optimal solution. Basically, the goal is to find a reducing algorithm whose complexity is not dominated by the resulting reduced algorithms.
   Example: Selection algorithm for finding the median in a list involves first sorting the list and then finding out the middle element in the sorted list. These techniques are also called transform and conquer.
6. Backtracking: This technique is very useful in solving combinatorial problems that have a single unique solution. Where we have to find the correct combination of steps that lead to fulfillment of the task. Such problems have multiple stages and there are multiple options at each stage. This approach is based on exploring each available option at every stage one-by-one. While exploring an option if a point is reached that doesn’t seem to lead to the solution, the program control backtracks one step, and starts exploring the next option. In this way, the program explores all possible course of actions and finds the route that leads to the solution.
   Example: N-queen problem, maize problem.
7. Branch and Bound: This technique is very useful in solving combinatorial optimization problem that have multiple solutions and we are interested in find the most optimum solution. In this approach, the entire solution space is represented in the form of a state space tree. As the program progresses each state combination is explored, and the previous solution is replaced by new one if it is not the optimal than the current solution.
   Example: Job sequencing, Traveling salesman problem.

### Classification by Design Approaches : There are two approaches for designing an algorithm. these approaches include

1. Top-Down Approach: In the top-down approach, a large problem is divided into small sub-problem. and keep repeating the process of decomposing problems until the complex problem is solved.
2. Bottom-up Approach: The bottom-up approach is also known as the reverse of top-down approaches. In approach different, part of a complex program is solved using a programming language and then this is combined into a complete program.

## DS Implementation

- Complexity?
- Storage?
- Search, Insertion/Deletion operations?

### Array

More memory efficient compared to list, since they are stored in continuous blocks of memory rather than using pointers

_Note:_ It can be only used, if all the elements in the array of the same data type

#### Creation {#array-creation}

Using built in array library

```python
import array

# first parameter 'i' represents that the array will be consisting of integers
demo_array = array.array('i') # Empty Array
demo_array = array.array('i', [1,2,3,4])
```

```python
from array import *

demo_array = array('i') # Empty Array
demo_array = array('i', [1,2,3,4])
```

Using Numpy

```python
import numpy as np

# first parameter 'i' represents that the array will be consisting of integers
np_demo_array = np.array([], dtype=int) # Empty Array
np_demo_array = np.array([1,2,3,4])
```

**Operations Complexity**:

Time Complexity

- Empty Array &rarr; **O(1)**
- n elements Array &rarr; **O(n)**

Space Complexity

- Empty Array &rarr; **O(1)**
- n elements Array &rarr; **O(n)**

#### Insertion {#array-insertion}

```python
demo_array = array.array('i', [1,2,3,4])
demo_array.insert(1, 6)
print(demo_array)
# array('i', [1, 6, 2, 3, 4])
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)** - Since we need to shift all the elements one position to the right if we are inserting the new element in the first position

Space Complexity &rarr; **O(1)**

> What if the next block of memory is not available in the memory?
>
> - Allocate memory area (current size + one (element size))
> - Copy data to the new area
> - Free old area
> - Additional small operations done anyway (like size (counters) update, ...)

#### Traverse {#array-traverse}

```python
for i in demo_array:
  print(i)
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Accessing {#array-access}

Since we know the address of the first element of the array and the index of the element we need, It can sum those and get the exact address we need to access that particular element without traversal

```python
demo_array[2]
```

**Operations Complexity**:

Time Complexity &rarr; **O(1)**

Space Complexity &rarr; **O(1)**

#### Searching {#array-search}

Using Linear search

```python
search = 30
demo_array = array('i', [10, 20, 30, 40, 50])
for i in demo_array:
  if i = search:
    print("found")
    break
```

> len() - Retrieve the value of the length that is already stored in the DS
>
> range() - It returns iterator rather than the entire list which generates the elements on demand which makes the time and space complexity O(1)

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Deleting {#array-delete}

To maintain the efficiency of arrays, we can just simply delete some element in between and leave it, we need to shift all the elements to the left to restore the continuous block of memory

```python
demo_array = array.array('i', [10, 20, 30, 40, 50])
array.remove(2)
print(array)
# [10, 20, 40, 50]
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

### Lists

Collection of data(Might not be of a single data type)

#### Creation {#list-creation}

```python
demo_list = [1, 2, 3]
demo_list1 = [1, 2, 'blog', 1.5]
demo_list2 = ['candibod', 'python', 'blog']
demo_2d_list = [['candibod', 'python'], ['blog']]
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(n)**

#### Insertion {#list-insertion}

```python
demo_list.insert(2, 5)
# [1, 2, 5, 3]
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)** - Since we need to shift all the elements one position to the right if we are inserting the new element in the first position

Space Complexity &rarr; **O(1)**

#### Update {#list-update}

```python
demo_list[2] = 40
# [1, 2, 40, 3]
```

**Operations Complexity**:

Time Complexity &rarr; **O(1)**

Space Complexity &rarr; **O(1)**

#### Traverse {#list-traverse}

```python
for i in demo_list:
  print(i)
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Accessing {#list-access}

```python
demo_array[2]
```

**Operations Complexity**:

Time Complexity &rarr; **O(1)**

Space Complexity &rarr; **O(1)**

#### Searching {#list-search}

Using Linear search

```python
search = 30
if search in demo_list:
  print("found")
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Deleting {#list-delete}

```python
demo_list.pop(1)
# 2

del demo_list[0]

demo_list.remove(40)
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

### Dictionary (Hash Table)

Python dictionary is like hash tables in any other language

```python
# Accessing a element using key
demo_dict['name']

# Accessing a element using get() method
demo_dict.get(0)

# creation using Dictionary comprehension
myDict = {x: x**2 for x in [1,2,3,4,5]}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

Collection of data(Might not be of a single data type)

#### Creation {#dict-creation}

```python
demo_dict = dict()
demo_dict = {}
demo_dict = {'name': 'candibod', 'demo_list': [1, 2, 3, 4]}
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(n)**

#### Add/Update {#dict-update}

```python
demo_list[2] = 40
# [1, 2, 40, 3]
```

**Operations Complexity**:

Time Complexity &rarr; **O(1)+**
: Amortized complexity: Normally adding an item takes constant time (that is, O(1)). But each time the array is full, you allocate twice as much space, copy your data into the new region, and free the old space. Assuming allocates and frees run in constant time, this enlargement process takes O(n) time where n is the current size of the array

Space Complexity &rarr; **O(1)**

#### Traverse {#dict-traverse}

```python
for i in demo_list:
  print(i)
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Accessing {#dict-access}

```python
demo_array[2]
```

**Operations Complexity**:

Time Complexity &rarr; **O(1)**

Space Complexity &rarr; **O(1)**

#### Searching {#dict-search}

Using Linear search

```python
search = 30
if search in demo_list:
  print("found")
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

#### Deleting {#dict-delete}

```python
demo_list.pop(1)
# 2

del demo_list[0]

demo_list.remove(40)
```

**Operations Complexity**:

Time Complexity &rarr; **O(n)**

Space Complexity &rarr; **O(1)**

### Tuple

Tuples are immutable

```python
# Creating a Tuple
demo_tuple = ('Candibod', 'Python')

demo_list = [1, 2, 3]
demo_tuple_1 = tuple(demo_list)

# Accessing element from last
demo_tuple[-1]
```

### Sets

- Compare performance with list?
- How to access elements in a set?

Python Set is an unordered collection of data that is mutable and does not allow any duplicate element. Used in this is Hashing

```python
# Creating a Set
demo_set = set([1, 2, 'candibod'])

# A frozen set - immutable
frozen_set = frozenset(["1", "2", "candibod"])
```

### Strings

### Linked List

- append - Time: O(1), Space: O(1)
  - Add the element at the end of the linked list
- prepend - Time: O(1), Space: O(1)
  - Add the element at the beginning of the linked list
- insert - Time: O(n), Space: O(1)
  - Add the element at the particular index
- get_value - Time: O(n), Space: O(1)
  - Get the value based on the index
- set_value - Time: O(n), Space: O(1)
  - Update the value of the index
- traversal - Time: O(n), Space: O(1)
  - Loop through all the elements of the Linked list
- search - Time: O(n), Space: O(1)
  - Search for the value
- pop_first - Time: O(1), Space: O(1)
  - Pop the beginning element of the Linked list
- pop - Time: O(n), Space: O(1)
  - Pop the end element of the linked list
- remove - Time: O(n), Space: O(1)
  - remove element based on the index
- delete_all - Time: O(1), Space: O(1)
  - Delete all the elements of the Linked list

### Stack

### Queue

### Heap

### Graphs

### Binary Tree

### Binary Search Tree

### Trie

## References

[[1]](https://www.enjoyalgorithms.com/blog/problem-solving-approaches-in-data-structures-and-algorithms) Techniques
[[2]](https://www.enjoyalgorithms.com/blog/steps-of-problem-solving-for-cracking-the-coding-interview) Process
[[3]](https://www.hackerearth.com/blog/developers/7-steps-to-improve-your-data-structure-and-algorithm-skills/) Process
[[4]](https://medium.com/enjoy-algorithm/popular-problem-solving-approaches-in-data-structures-and-algorithms-6b4d30a0823d) Examples
[[5]](https://hackernoon.com/data-structures-and-algorithms-20-problem-solving-techniques-qz1q3z1o) Process + Examples
