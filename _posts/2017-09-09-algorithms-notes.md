---
layout: post
title: "Note from: Elements of Programming Interview in Python"
date: 2017-09-09
tags: ["python", "algorithms"]
draft: false
---

I'm working on the problems in the book "Elements of Programming
Interview in Python". The following is my notes. 

## Chapter 4. Primitive Types 

- Look for optimized solutions for both complexities in time and
  space. For example, when writing a program to check if an integer is
  palindrome, one can convert it into a string and iteratively compare
  the first and the last characters. This solution has complexity of
  O(n) both in time and space, with n is the number of digits. A
  better approach would be extracting the first and last digits directly
  from the integer and compare them, in this way, we still have O(n)
  time complexity, but the solution has only O(1) space. 

- *Caching*: caching is useful for recursive programs. Once the size
  of the problem reduces to some small number, we can use a lookup
  table. For example, to calculate the parity bit of 64-bit number, we
  can reduce the problem to 32-bit, 16-bit, etc. but it might be
  faster if we have a lookup table for values of 16-bit. 
  
## Chapter 5. Array 

- Array problems often have simple brute-force solutions that use O(n)
  space, but there are subtler solutions that use the array itself to
  reduce space complexity to O(1)

- One common pattern is doing in-array processing: after an element is
  processed, swap it to some part of the array that is reserved for
  processed elements. 
  
- Take advantage of list comprehension in Python, instead of writing
  long for loops. Problem 5.17 is a good example: to check row and
  column constraints of a Sudoku partial assignment: 
  
```python
if any(has_duplicate(partial_assignment[i][j] for j in range(n)]) or 
       has_duplicate(partial_assignment[j][i] for j in range(n)])
       for i in range(n)):
    return False 
```

## Chapter 6. String 
- Similar to arrays, string problems often have simple brute-force
  solutions that use O(n) space, but subtler solution that use the
  string itself to reduce space complexity to O(1).
  
- Understand the implication of a string type which is immutable,
  e.g., the need to allocate new string when concatenating immutable
  strings. Know alternatives to immutable string, e.g., a list in
  Python 
  
- Updating a mutable string from the front is slow, so see if it's
  possible to write values from the back. 

## Chapter 7. Linked Lists 
- List problems often have a simple brute-force solution that uses
  O(n) space, but a subtler solution that uses the *existing list
  nodes* to reduce space complexity to O(1)
- Very often, a problem on lists is conceptually simple, and is more
  about *cleanly coding what's specified*, rather than designing an
  algorithm
- Consider using a dummy head (sometimes referred to as a sentinel) to
  avoid having to check for empty lists. This simplifies code, and
  makes bugs less likely
- It's easy to forget to *update next* (and previous for double linked
  list) for the head and tail 
- Algorithms operating on singly linked lists often benefit from using
  *two iterators*, one ahead of the other, or one advancing quicker
  than the other. 

## Chapter 8. Stacks and Queues 

- Learn to recognize when the stack LIFO property is applicable. For
  example, parsing typically benefits from a stack. 
  
- Consider augmenting the basic stack or queue data structure to
  support additional operations, such as finding the maximum element. 
  
- In Python, use the built-in `list-type` for stack. `s.append(e)`
  pushes an element onto the stack. `s[-1]` will retrieve, but does
  not remove, the element at the top of the stack. `s.pop()` will
  remove and return the element at the top of the stack. `len(s)==0`
  tests if the stack is empty. 
  
- Learn to recognize when the queue FIFO property is applicable. For
  example, queues are ideal when order needes to be preserved. 
  
## Chapter 9. Binary Trees

- Recursive algorithms are well-suited to problems on trees. Remember
  to include space implicitly allocated on the function call stack
  when doing space complexity analysis. 
  
- Some tree problems have simple brute-force solutions that use O(n)
  space solution, but subtler solutions that uses the existing tree
  nodes to reduce space complexity to O(1) 
  
- Consider left- and right-skewed trees when doing complexity
  analysis. Note that O(h) complexity, where h is the tree height,
  translates into O(logn) complexity for balanced trees, but O(n)
  complexity for skewed trees. 

- If each node has a parent field, use it to make your code simpler,
  and to reduce time and space complexity. 
  
- It's easy to make the mistake of treating a node that has a single
  child as a leaf. 

- There are some problems in this chapter worth reimplement: 9.11
  (Implement an inorder traversal with O(1) space),
  9.12 (Reconstruct a binary tree from traversal data), 9.16 (Compute
  the right sibling tree). 
  

## Chapter 10. Heap 

- A heap is a specialized binary tree: it is a complete binary tree,
  and  the keys must satisfy the heap
  property--the key at each node is at least as great as the keys
  stored at its children. 
  
-  max-heap supports O(logn) insertion, O(1) time look up for the the
  max element, and O(logn) deletion of the max element. The
  extract-max operation is defined to delete and return the maximum
  element. 
  
- Heap functionality in Python is provided by the `heapq` module.

- `heapq.heapify(L)` transforms the elements in L into a heap
  in-place.
  
- `heapq.nlargest(k,L)`, `heapq.nsmallest(k,L)` returns the k largest
  (smallest) elements in L 
  
- `heapq.heappush(h, e)` pushes a new element on the heap. 

- `heapq.heappop(h)` pops the smallest element from the heap. 

- `heapq.heappushpop(h, a)` pushes a on the heap and then pops and
  returns the smallest element. 
  
- `e = h[0]` returns the smalest element on the heapwithout popping
  it. 
  
- `heapq` only provides min-heap functionality.

- Use the heap when all you care about is the largest or smallest
  elements, and you do not need to support fast lookup, delete, or
  search operations for arbitrary elements. 
  
- A heap is a good choice when you need to compute the k largest or k
  smallest elements in a colletion. For the former, use a min-heap,
  for the latter, use a max-heap. 

## Chapter 11. Searching 

- Questions based on binary search are ideal from the interviewers
  perspective. It is basic, but is much trickeier to implement
  correctly than it appears---you should implement it as well as write
  corner case tests to ensure you undersntad it properly 
  
```python 
def bsearch(t, A):
    L, U = 0, len(A) - 1
    while L <= U 
        M = (L + U) // 2
        if A[M] < t: 
            L = M + 1
        elif A[M] == t:
            return M 
        else: 
            U = M - 1
    return -1 
```

- A disadvantage of binary search is that it requires a sorted array
  and sorting an array takes O(nlogn) time. However, if there are many
  searches to perform, the time taken to sort is not an issue. 
  
- User-defined types used in sorted collection must explicitly
  implement comparison, en unsure this comparison has basic properties
  such as transitivity. 
  
- Binary search  tree is an effective search tool. It is applicable to
  more than just searching in sorted arrays, e.g., it can be used to
  search an interval of real numbers or integers.
  
- If your solution uses sorting, and the computation performed after
  sorting is faster than sorting, e.g., O(n) or O(logn), look for a
  solutions that do not perform a complete sort. 
  
- Consider time/space tradeoff, such as making multiple passes through
  the data. 
  
- The `bisect` module provides binary search functions for sorted
  list. To find the first element that is not less than a targeted
  value, use `bisect.bisect_left(a,x)`. To find the first element that
  is greater than a tergeted value, use `bisect.bisect_right(a,x)`. 
  
- Should review again: problem 11.8 (Find the kth largest element),
  problem 11.10 (Find the duplicate and missing elements )

- Worth
  reviewing:
  [Median of two sorted arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/). 
## Chapter 12. Hash tables 

- *Key points*: O(1) insertions, deletions and lookups. Key
  disadvantages: not suitable for order-related queries; need for
  resizing; poor worst-case performance. Understand implementatino
  using array of buckets and collision chains. Know hash functions for
  integers, strings, objects. 
  
- Hash tables have the best theoretical and real-world performance for
  lookup, insert and delete. Each of these operation has O(1) time
  complexity. The O(1) time complexity for insertion is for the
  average case---a single insert can take O(n) if the hash table has
  to be resized 
  
- Consider using a hash code as a signature to enhance performance,
  e.g., to filter out candidates. 

- Consider using a precomputed lookup table instead of boilerplate
  if-then code for mappings, e.g. from character to value, or
  character to character 
  
- When defining your own type that will be put in a hash table, be
  sure you understand the relationship between logical equality and
  the fields the hash table must inspect. Specificically, anytime
  equality is implemented, it is imperative that the correct hash
  function is also implemented, otherwise when objects are placed in
  hash tables, logically equivalent objects may appear in different
  buckets, leading to lookups returning false, even when the searched
  item is present. 
  
- Sometimes you'll need a multimap, i.e., a map that contains multiple
  values for a single key, or a bi-directional map. If the language's
  standard libraries do not provide the functionality you need, learn
  how to implement a multimap using lists as values, or find a third
  party library that has a multimap. 
  
- Example of hash function suitable for strings 

```python 
def string_hash(s, modulus):
    MULT = 997
    return functools.reduce(lambda v,c: (v * MULT + ord(c)) % modulus,
    s, 0)
```

- Anytime you need to store a set of strings, a hash table is an
  excellent choice. For example, to find groups of anagrams from an
  input of a set of words: 
  
```python 
def find_anagrams(dictionary):
    sorted_string_to_anagrams = collections.defaultdict(list)
    for s in dictionary:
        sorted_string_to_anagrams[''.join(sorted(s))].append(s)
    return [
        group for group in sorted_string_to_anagrams.values() if
        len(group) >= 2]
```

- Hash table libraries in Python: There are multiple hash table-based
  data structures commonly used in Python---`set`, `dict`,
  `collections.defaultdict`, and `collections.Counter`. The difference
  between `set` and the other three is that `set` simply store keys,
  whereas the others store key-value pairs. All have the property that
  they do not allow for duplicate keys, unlike, for example, `list`. 

- In a `dict`, accessing value associated with a key that is not
  present leads to a `KeyError` exception. However, a
  `collection.defaultdict` returns the default value of the type that
  was specified when the collection was instantiated, e.g., if `d =
  collections.defaultdict(list)`, then if `k not in d` then `d[k] =
  []`. 
  
- A `collections.Counter` is used for counting the number of
  occurences of keys, with a number of set-like operations. 
  
```python 
c = collections.Counter(a=3, b=1)
d = collections.Counter(a=1, b=2)
c+d
c-d
c&d
c|d
```

- The most important operations for sets are `s.add(42)`,
  `s.remove(42)`, `s.discard(123)`, `x in s`, as well as `s <= t` (is
  s a subset of t), and `s-t` (elements in s that are not in t)

- The basic operations on the key-value collections are similar to
  those on `set`. One difference is with iterators---iteration over a
  key-value collection yields the keys. To iterate over the key-value
  pairs, iterate over `items()`; to iterate over values, use
  `values()`. (The `keys`method returns an iterator to the keys.) 
  
- Problems worth reviewing: 12.7 (Find the smallest subarray coverting
  all values).   
  
  
## Chapter 13 Sorting 

- Sorting problems come in two flavors: (1) use sorting to make
  subsequent steps in an algorithm simpler, and (2) design a custom
  sorting routine. For the former, it's fine to use a library sort
  function, possibly with a custom comparator. For the latter, use a
  data structure like a BST, heap, or array indexed by values. 
  
- Certain problems become easier to understand, as well as solve, when
  the input is sorted. The most natural reason to sort is if the
  inputs have a natural ordering, and sorting can be used as a
  preprocessing step to speed up searching. 
  
- For specialized input, e.g., a very small range of values, or a
  small number of values, it's possible to sort in O(n) time rather
  than O(nlogn) time. 
  
- It's often the case that sorting can be implemented in less space
  than required by a brute-force approach. 
  
- Sometime it is not obvious what to sort on, e.g., should a
  collection of intervals be sorted on starting points or endpoints? 
  
- To sort a list in-place, use the `sort()` method; to sort an
  iterable, use the function `sorted()`. 

- Review again: problem 13.10 (Implement a fast sorting algorithm for
  lists), problem 13.8 (Partitioning and sorting an array with many
  repeated entries). 
  
## Chapter 14 Binary Search Tree 

- BST property: the key stored at a node is greater than or equal to
  the keys stored at the nodes of its left subtree and less than or
  equal to the keys stored in the nodes of its right subtree. 
  
- Key lookup, insertion, and deletion take time proportional to the
  height of the tree, which can in worst-case be O(n), if insertions
  and deletions are naively implemented. However, there are
  implementation of insert and delete which guarantee that the tree
  has height O(logn).

- As a rule, avoid putting mutable objects in a BST. Otherwise, when a
  mutable object that's in a BST is to be updated, always first remove
  it from the tree, then update it, then add it back. 
  
- Unlike a hash table, a BST offers the ability to find the min and
  max elements, and find the next largest/smallest element. 
  
- With a BST you can iterate through elements in sorted order in time
  O(1) (regardless of whether it is balanced). 
  
- Some problems need a combination of a BST and a hashtable. For
  example, if you insert student objects into a BST and entries are
  ordered by GPA, and then a student's GPA needs to be updated and all
  we have is the student's name and new GPA, we cannot find the
  student by name without a full traversal. However, with an
  additional hash table, we can directly go to the corresponding entry
  in the tree. 
  
- Sometimes, it's necessary to augment a BST to make it possible to
  manipulate more complicated data, e.g., intervals, and efficiently
  support more complext queries, e.g., the number of elements in a
  range. 
  
- The BST property is a global property---a binary tree may have the
  property that each node's key is greater than the key at its left
  child and smaller than the key at its right child, but it may not be
  a BST.   
  
- Binary search tree libraries: `sortedcontainers` module or
  `bintrees` module. They are used for sorted sets and sorted
  dictionaries.
  
- `bintrees` functionalities: `insert(e)` inserts new element e in the
  BST, `discard(e)` removes e in the BST if present,
  `min_item()/max_item()` yield the smallest and largest key-value
  pair in the BST, `min_key()/max_key()` yield the smallest and
  largest key in the BST, `pop_min()/pop_max()` remove and return the
  smallest and largest key-value pair in the BST. These operations
  take O(logn), since they are backed by the underlying tree. 

- Review problems: 14.5 (Reconstruct a BST from traversed data), 14.8
  (The most visited page problem), 14.7 (enumerate numbers of the form a+b*$\sqrt(2)$)  

## Chapter 15 Recusrsion

- Recursion is especilly suited when the input is expressed using
  recursive rules such as a computer grammar.
  
- Recursion is a good choice for search, enumeration, and
  divide-and-conquer.
  
- Use recursion as alternative to deeply nested iteration loops. For
  example, recursion is much better when you have an undefined number
  of levels, such as the IP address problem generalized to k
  substrings. 
  
- If you are asked to remove recursion from a program, consider
  mimicking call stack with the stack data structure. 
  
- Recursion can be easily removed from a tail-recursive program by
  using a while-loop---no stack is needed (Optimizing compilers do
  this).
  
- If a recursive function may end up being called with the same
  arguments more than once, cache the results---this is the idea
  behind Dynamic Programming. 
  
- Review problems: 15.2 (Generate all nonattacking placements of
  n-queens), 15.4 (Generate the power set) 

## Chapter 16 Dynamic Programming 

- Consider using DP whenever you have to make choices to arrive at the
  solution. Specifically, DP is applicable when you can construct a
  solution to the given instance from solution to subinstances of
  smaller problem of the same kind. 
  
- In addition to optimization problems, DP is also applicable to
  counting and decision problems---any problem where you can express a
  solution recursively in terms of the same computation on smaller
  instances. 
  
- Although conceptually DP involves recursion, often for efficiency
  the cache is built "bottom-up", i.e., iteratively. 
  
- When DP is implemented recursively the cache is typically a dynamic
  data structure such as a hash table or a BST; when it is implemented
  iteratively the cache is usually a one- or multi-dimenional array. 
  
- To save space, cache space may be recycled once it is known that a
  set of entries will not be looked up again. 
  
- Sometimes, recursion may out-perform a bottom-up DP solution, e.g.,
  when the solution is found early or subproblems can be pruned
  through bounding. 
  
- A common mistake in solving DP problems is trying to think of the
  recursive case by splitting the problem into two equal halves, a la
  quicksort, i.e., solve the subproblems for subarrays A[0, n/2] and
  A[n/2+1,n] and combine the results. However, in most cases, these
  two subproblems are not sufficient to solve the original problem. 
  
- DP is based on combining solutions to subproblems to yield a
  solution to the original problem. However, for some problems DP will
  not work. For example, if you need to compute the longest path from
  City 1 to City 2 without repeating an intermediate city, and this
  longest path passes through City 3, then the subpaths from City 1
  to City 3 and City 2 may not be individually longest paths without
  repeated cities. 
  
- Review problems: 16.1 (count the number of score combinations), 16.5
  (Search for a sequence in a 2D array), 16.6 (The knapsack problem).
  
## Chapter 17. Greedy algorithms and Invariants 

- A greedy algorithm is often the right choice for an optimized
  problem where there's a natural set of choices to select from. 
  
- It's often easier to conceptualize a greedy algorithm recursively,
  and then implement it using iteration for higher performance. 
  
- Even if the greedy approach does not yield an optimum solution, it
  can give insights into optimum algorithm, or serve as a heuristic 
  
- Sometimes the correct greedy algorithm is not obvious. 

- Review problems: 17.8 (Compute the largest rectangle under the
  skyline). 
  
## Chapter 18. Graphs

- It's natural to use a graph when the problem involves spatially
  connected objects, e.g., road segments between cities.
  
- More generally, consider using a graph when you need to analyze any
  binary relationship, between objects, such as interlinked webpages,
  followers in a social graph, etc. In such cases, quite often the
  problem can be reduced to a well-known graph problem.
  
- Some graph problems entail analyzing structure, e.g., looking for
  cycles or connected components. DFS works particularly well for
  these applications. 
  
- Some graph problems are related to optimization, e.g., find the
  shortest path from one vertex to another. BFS, Dijkstra's shortest
  path algorithm, and minimum spanning tree are examples of graph
  algorithms appropriate for optimization problems. 
  
- DFS and BFS differ from each other in terms of the additional
  information they provide, e.g., BFS can be used to compute distances
  from the start vertex and DFS can be used to check for the presence
  of cycles. Key notions in DFS include the concept of discovery time
  and finishing time for vertices. 
  
- Review problems: 18.1 (Search a maze), 18.9 (Compute a shortest path
  with fewest edges)

- Leetcode
  problems:
  [Combination Sums](https://leetcode.com/problems/combination-sum/).
  
## Chapter 19. Parallel Computing 

- Two primary models for parallel computation: shared memory model
  (good for multi-core settings), distributed memory model (good for
  cluster settings).

- Challenges in parallel computation: races, starvation, deadlock,
  livelock. 
  
- A semaphore is a very powerful synchronization construct. It
  maintains a set of permits. A thread calling `acquire()` on a
  semaphore waits, if necessary, until a permit is available, and then
  takes it. A thread calling `release()` on a semaphore adds a permit
  and notifies threads waiting on that semaphore, potentially
  releasing a blocking acquirer. 
  
  
## Python specific 

- To get max value of a certain data type 
```python
float('inf')
```

- Get a random integer in some range:
```python
import random 
r = random.randint(m, n)
```

- Check if an array contains duplicate elements: 

```python 
len(A) != len(set(A))
```

- Initialize an array length n of all zeros: 

```python 
A = [0] * n
```

- Remove the leading zeros in an array of digits (from problem 5.3):

```python
result = result[next((i for i, x in enumerate(result) if x!=0),
len(result)):] or [0]
``` 
The last `or [0]` is for the case where `result` only has 0s; in that
case, we return a list of single 0. 

- Syntax for `get()` method of Python dictionary: 
```python
dict.get(key, default=None)
```

- Convert an array of chars to a string: 
```python 
''.join(array)
```

- `fold` in Python: 

```python 
functools.reduce(function, iterable[, initializer])
```

For example, `reduce(lambda x, y: x + y, [1,2,3,4,5])` calculates
`((((1+2)+3)+4)+5)`.

- Python has an array for hex digits:

``` python
string.hexdigits[10] # will be 'a'
```

- Python named tuple: 

``` python 
import collections 

ElementWithCachedMax = collections.namedtuple('ElementWithCachedMax',
('element', 'max'))
```

- To build a hash table where value is the index of the key inside
another list: 

```python
# A: list, B: dictionary (hash table)
B = {data: i for i in enumerate(A)}
```

- Iterator object in Python is an object representing a stream of
  data. Repeated calls to the iterator's `next()` return successive
  items in the stream. when no more data are available a
  `StopIteration` exception is raised instead. 
  
```python 
it = iter([1,2,3,4])
x = next(it) # return 1 
y = next(it) # return 2 
```

- `itertools` implements a number of iterator building block. 
- In `collections` module, there is a data structure called
  `OrderedDict`. It is a hash table that remembers the order in which
  keys and values are added. The functions of this data structure
  include: `OrderedDict.popitem(last=False)` returns the oldest (key,
  value) pair that was added, and `OrderedDict.pop(key)` returns the
  value of this key if existed, or `KeyError` if not existed. 
  
- The elements of a set must be hashable. So we cannot make a set of
  mutable objects like lists or other sets.   
  
- Semaphore example: 

```python 
import threading 
class Semaphore():
    def __init__(self,max_available):
        self.cv = threading.Condition()
        self.MAX_AVAILABLE = max_available
        self.taken = 0 
    
    def acquire(self):
        self.cv.acquire()
        while (self.taken == self.MAX_AVAILABLE):
            self.cv.wait()
        self.taken += 1
        self.cv.release()
    
    def release(self):
        self.cv.acquire()
        self.taken -= 1
        self.cv.notify()
        self.cv.release()
```

- `threading.Thread` class: represents an activity that is run in a
  separate thread of control. Two ways to specify activity: by passing
  a callable object to the constructor, or by overrding the `run()`
  method in a subclass. Only override the `__init__()` and `run()`
  methods of this class. Once a thread object is created, its activity
  must be started by calling the thread's `start()` method. This
  invokes the `run()` method in a separate thread of control. 
  
- `threading.Condition` class: A conditiona variable is always
  associated with some kind of lock; this can be passed in or one will
  be created by default. A condition variable has `acquire()` and
  `release()` methods that call the corresponding methods of the
  associated lock. It also has a `wait()` method, and `notify()` and
  `notifyAll()` methods. These three must only be called when the
  calling thread has acquired the lock, otherwise a `RunTimeError` is
  raised. 
  
- Using locks in the `with` statement: All of the objects provided by
  a module that has `acquire()` and `release()` methods can be used as
  context managers for a `with` statement. The `acquire()` method will
  be called when the block is entered, and `release()` will be called
  when the block is exited. 
  
- lambda function syntax: `lambda arguments: expression`. Example:  

```python 
double = lambda x: x * 2

# Output: 10
print(double(5))
```


