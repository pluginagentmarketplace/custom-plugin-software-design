---
name: computer-science
description: Data structures, algorithms, complexity analysis, and CS theory. Master algorithmic problem-solving and computational thinking.
---

# Computer Science Fundamentals

## Quick Start

CS fundamentals are essential for all developers.

### Data Structures
```python
# Lists/Arrays - Ordered, indexed
arr = [1, 2, 3, 4, 5]
arr.append(6)  # O(1) amortized

# Linked Lists - Sequential, pointer-based
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Stacks - LIFO (Last In First Out)
stack = []
stack.append(1)  # push O(1)
stack.pop()      # pop O(1)

# Queues - FIFO (First In First Out)
from collections import deque
queue = deque()
queue.append(1)   # enqueue O(1)
queue.popleft()   # dequeue O(1)

# Hash Tables - Key-value mapping
dict_map = {}
dict_map['key'] = 'value'  # O(1) average

# Trees - Hierarchical
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# Graphs - Connected nodes
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A']
}
```

### Algorithms
```python
# Binary Search - O(log n)
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Merge Sort - O(n log n)
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

# Dynamic Programming - Fibonacci
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib(n-1, memo) + fib(n-2, memo)
    return memo[n]

# Graph DFS
def dfs(node, visited, graph):
    visited.add(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(neighbor, visited, graph)
```

### Complexity Analysis
```
Time Complexity:
O(1) - Constant time
O(log n) - Logarithmic
O(n) - Linear
O(n log n) - Linearithmic
O(n²) - Quadratic
O(2ⁿ) - Exponential
O(n!) - Factorial

Space Complexity:
Follow similar analysis for memory usage
```

## Core Concepts

- **Big O Notation** - Upper bound on complexity
- **Recursion** - Functions calling themselves
- **Sorting** - Arranging data in order
- **Searching** - Finding specific data
- **Graph Theory** - Connected nodes
- **Complexity Theory** - Analyzing algorithm efficiency

## Best Practices

- Choose appropriate data structures
- Write efficient algorithms
- Consider time-space tradeoffs
- Profile and optimize bottlenecks
- Understand worst-case scenarios
- Practice problem-solving

## Resources

- [LeetCode](https://leetcode.com)
- [Introduction to Algorithms (Book)](https://en.wikipedia.org/wiki/Introduction_to_Algorithms)
- [MIT OpenCourseWare](https://ocw.mit.edu)

## Related Skills

- **Algorithms Interviews** - Technical preparation
- **System Design** - Applied CS concepts
- **Competitive Programming** - Advanced problem-solving
