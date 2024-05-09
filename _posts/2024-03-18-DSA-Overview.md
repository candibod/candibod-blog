---
title: "DSA Overview"
date: 2023-03-18
layout: post
author: jeevan
---

# DSA Overview

## Contents:

1. Types of Asymptotic Notations (Big O)
2. [Types of DS](#DsTypes)
3. How to Pick the right DS
4. [Problem Solving Techniques](#PSTechniques)
5. [Problem Solving Process](#PSProcess)
6. [Python Data Structures](#PythonDS)

## Types of Asymptotic Notations

### Theta - Θ

Lower bound of an algorithm

### Omega - Ω

Average case complexity of an algorithm

### Big-O - O

Upper bound of an algorithm

- Most Efficient/Constant time complexity
  - A constant-time complexity is O(1)
- Good
  - A logarithmic complexity is Log(N)
- Fair/Linear Time Complexity
  - A linear time Complexity is O(N)
- Bad
  - A super-linear time complexity is O(N\*Log(N))
- Most inefficient
  - A quadratic-time Complexity is O(N^2) or O(N^k) or O(2^N) or O(N!)

## Types of Data Structures<a id="DsTypes">:</a>

- Arrays and Lists
- 2D Arrays
- Strings
- Linked List
- Stack
- Queue
- Hash Table & Hash Set
- Heap
- Graphs
- Binary Tree
- Binary Search Tree
- Trie

## Problem Solving Techniques<a id="PSTechniques">:</a>

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

## Problem Solving Steps<a id="PSProcess">:</a>

- Understand the problem.
- Create a step-by-step plan for how you’ll solve it.
- Carry out the plan and write the actual code.
- Look back and possibly refactor your solution if it could be better.

### If we got a requirement saying don't create a new data structure

- We need to switch the elements inside the DS
- We need to update the elements once those are traversed, if we don't use those elements again

## Top 5 Data Structures from 127 interviews:

1. Graph
   - Think Graph when you see entities and relationships
   - Bus Routes: https://lnkd.in/gP8dKC_N
2. Stack and Queue
   - Think Stack and Queue when you need to store information of a window
   - Largest Rectangle in Histogram: https://lnkd.in/gvKUB_YA
3. Hash Map
   - Think Hash Map when you want fast lookups at the cost of extra space
   - Two Sum: https://lnkd.in/gA7h3KXk
4. Binary Tree
   - Think recursion for Binary Tree problems
   - Lowest Common Ancestor: https://lnkd.in/gjXScf4m
5. Heap
   - Think Heap when you want maximum or minimum fast
   - k Most Frequent Elements in an Array: https://lnkd.in/g3T6BTqX

There are always exceptions to the rules but it's good to have a starting point

## Process:

### Classification by Implementation Method:

1. Recursion or Iteration: A recursive algorithm is an algorithm which calls itself again and again until a base condition is achieved whereas iterative algorithms use loops and/or data structures like stacks, queues to solve any problem. Every recursive solution can be implemented as an iterative solution and vice versa.
2. Exact or Approximate: Algorithms that are capable of finding an optimal solution for any problem are known as the exact algorithm. For all those problems, where it is not possible to find the most optimized solution, an approximation algorithm is used. Approximate algorithms are the type of algorithms that find the result as an average outcome of sub outcomes to a problem.
3. Serial or Parallel or Distributed Algorithms: In serial algorithms, one instruction is executed at a time while parallel algorithms are those in which we divide the problem into subproblems and execute them on different processors. If parallel algorithms are distributed on different machines, then they are known as distributed algorithms.

### Classification by Design Method:

1. Greedy Method: In the greedy method, at each step, a decision is made to choose the local optimum, without thinking about the future consequences.
2. Divide and Conquer: The Divide and Conquer strategy involves dividing the problem into sub-problem, recursively solving them, and then recombining them for the final answer.
3. Dynamic Programming: The approach of Dynamic programming is similar to divide and conquer. The difference is that whenever we have recursive function calls with the same result, instead of calling them again we try to store the result in a data structure in the form of a table and retrieve the results from the table. Thus, the overall time complexity is reduced. “Dynamic” means we dynamically decide whether to call a function or retrieve values from the table.<br>
   Example: 0-1 Knapsack, subset-sum problem.
4. Linear Programming: In Linear Programming, there are inequalities in terms of inputs and maximizing or minimizing some linear functions of inputs.<br>
   Example: Maximum flow of Directed Graph
5. Reduction(Transform and Conquer): In this method, we solve a difficult problem by transforming it into a known problem for which we have an optimal solution. Basically, the goal is to find a reducing algorithm whose complexity is not dominated by the resulting reduced algorithms.<br>
   Example: Selection algorithm for finding the median in a list involves first sorting the list and then finding out the middle element in the sorted list. These techniques are also called transform and conquer.
6. Backtracking: This technique is very useful in solving combinatorial problems that have a single unique solution. Where we have to find the correct combination of steps that lead to fulfillment of the task. Such problems have multiple stages and there are multiple options at each stage. This approach is based on exploring each available option at every stage one-by-one. While exploring an option if a point is reached that doesn’t seem to lead to the solution, the program control backtracks one step, and starts exploring the next option. In this way, the program explores all possible course of actions and finds the route that leads to the solution.<br>
   Example: N-queen problem, maize problem.
7. Branch and Bound: This technique is very useful in solving combinatorial optimization problem that have multiple solutions and we are interested in find the most optimum solution. In this approach, the entire solution space is represented in the form of a state space tree. As the program progresses each state combination is explored, and the previous solution is replaced by new one if it is not the optimal than the current solution.<br>
   Example: Job sequencing, Travelling salesman problem.

### Classification by Design Approaches : There are two approaches for designing an algorithm. these approaches include

1. Top-Down Approach: In the top-down approach, a large problem is divided into small sub-problem. and keep repeating the process of decomposing problems until the complex problem is solved.
2. Bottom-up Approach: The bottom-up approach is also known as the reverse of top-down approaches. In approach different, part of a complex program is solved using a programming language and then this is combined into a complete program.

## Python Data Structures<a id="PythonDS">:</a>

- Complexity?
- Storage?
- Search, Insertion/Deletion operations?

### Array

More memory efficient compared to list, since they are stored in continuous blocks of memory rather than using pointers

**Note:** It can be only used, if all the elements in the array of the same data type

```python
import array

demo_array = array.array('i', [1,2,3,4])

# Inserting element
demo_array.insert(1, 6)
```

### Lists

Collection of data(Might not be of a single data type)

```python
# Creating a List
demo_list = ['candibod', 'python', 'blog']

# Creating a 2D List
demo_2d_list = [['candibod', 'python'], ['blog']]

# Last element of list
demo_list[-1]
```

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

### Dictionary (Hash Table)

Python dictionary is like hash tables in any other language

```python
# Creating a Dictionary
demo_dict = {'name': 'candibod', 'demo_list': [1, 2, 3, 4]}

# Accessing a element using key
demo_dict['name']

# Accessing a element using get() method
demo_dict.get(0)

# creation using Dictionary comprehension
myDict = {x: x**2 for x in [1,2,3,4,5]}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
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

[[1]](https://www.enjoyalgorithms.com/blog/problem-solving-approaches-in-data-structures-and-algorithms) Techniques<br>
[[2]](https://www.enjoyalgorithms.com/blog/steps-of-problem-solving-for-cracking-the-coding-interview) Process<br>
[[3]](https://www.hackerearth.com/blog/developers/7-steps-to-improve-your-data-structure-and-algorithm-skills/) Process<br>
[[4]](https://medium.com/enjoy-algorithm/popular-problem-solving-approaches-in-data-structures-and-algorithms-6b4d30a0823d) Examples<br>
[[5]](https://hackernoon.com/data-structures-and-algorithms-20-problem-solving-techniques-qz1q3z1o) Process + Examples<br>
