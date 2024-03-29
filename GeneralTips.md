# General Tips
---
Clarify any assumptions you made subconsciously. Many questions are under-specified on purpose.

Always validate input first. Check for invalid/empty/negative/different type input. Never assume you are given the valid parameters. Alternatively, clarify with the interviewer whether you can assume valid input (usually yes), which can save you time from writing code that does input validation.

Are there any time/space complexity requirements/constraints?

Check for off-by-one errors.

In languages where there are no automatic type coercion, check that concatenation of values are of the same type: `int`/`str`/`list`.

After finishing your code, use a few example inputs to test your solution.

Is the algorithm meant to be run multiple times, for example in a web server? If yes, the input is likely to be preprocess-able to improve the efficiency in each call.

Use a mix of functional and imperative programming paradigms:

- Write pure functions as much as possible.
- Pure functions are easier to reason about and can help to reduce bugs in your implementation.
- Avoid mutating the parameters passed into your function especially if they are passed by reference unless you are sure of what you are doing.
- However, functional programming is usually expensive in terms of space complexity because of non-mutation and the repeated allocation of new objects. On the other hand, imperative code is faster because you operate on existing objects. Hence you will need to achieve a balance between accuracy vs efficiency, by using the right amount of functional and imperative code where appropriate.
- Avoid relying on and mutating global variables. Global variables introduce state.
- If you have to rely on global variables, make sure that you do not mutate it by accident.

Generally, to improve the speed of a program, we can either: (1) choose a more appropriate data structure/algorithm; or (2) use more memory. The latter demonstrates a classic space vs. time tradeoff, but it is not necessarily the case that you can only achieve better speed at the expense of space. Also, note that there is often a theoretical limit to how fast your program can run (in terms of time complexity). **For instance, a question that requires you to find the smallest/largest element in an unsorted array cannot run faster than O(N)**.

Data structures are your weapons. Choosing the right weapon for the right battle is the key to victory. Be very familiar about the strengths of each data structure and the time complexities for its various operations.

Data structures can be augmented to achieve efficient time complexities across different operations. **For example, a hash map can be used together with a doubly-linked list to achieve O(1) time complexity for both the `get` and `put` operation in an LRU cache.**

**Hashmaps are probably the most commonly used data structure for algorithm questions.** If you are stuck on a question, your last resort can be to enumerate through the possible data structures (thankfully there aren't that many of them) and consider whether each of them can be applied to the problem. This has worked for me sometimes.

If you are cutting corners in your code, state that out loud to your interviewer and say what you would do in a non-interview setting (no time constraints). E.g., I would write a regex to parse this string rather than using `split()` which may not cover all cases.

# Sequence
---
## Notes
Arrays and strings are considered sequences (a string is a sequence of characters). There are tips relevant for dealing with both arrays and strings which will be covered here.

Are there duplicate values in the sequence, would it affect the answer?

Check for sequence out of bounds.

Be mindful about slicing or concatenating sequences in your code. Typically, slicing and concatenating sequences require O(n) time. Use start and end indices to demarcate a subarray/substring where possible.

Sometimes you can traverse the sequence from the right rather than from the left.

Master the [sliding window technique](https://leetcode.com/problems/minimum-window-substring/discuss/26808/here-is-a-10-line-template-that-can-solve-most-substring-problems) that applies to many substring/subarray problems.

When you are given two sequences to process, it is common to have one index per sequence to traverse/compare the both of them. For example, we use the same approach to merge two sorted arrays.

**Corner Cases**
- Empty sequence.
- Sequence with 1 or 2 elements.
- Sequence with repeated elements.

# Arrays
---
Is the array sorted or partially sorted? If it is, some form of binary search should be possible. This also usually means that the interviewer is looking for a solution that is faster than O(n).

Can you sort the array? Sometimes sorting the array first may significantly simplify the problem. Make sure that the order of array elements do not need to be preserved before attempting a sort.

For questions where summation or multiplication of a subarray is involved, pre-computation using hashing or a prefix/suffix sum/product might be useful.

If you are given a sequence and the interviewer asks for O(1) space, it might be possible to use the array itself as a hash table. For example, if the array only has values from 1 to N, where N is the length of the array, negate the value at that index (minus one) to indicate presence of that number.

**AGAIN:** For array problems, sorting the array first may significantly simplify the problem.

# Dynamic programming
---
7 steps to solve a DP problem:
1. How to recognize a DP problem
2. Identify problem variables
3. Clearly express the recurrence relation
4. Identify the base cases
5. Decide if you want to implement it iteratively or recursively
6. Add memoization
7. Determine time complexity

## Step 1
Recognizing a Dynamic Programming problem is often the most difficult step in solving it. Can the problem solution be expressed as a function of solutions to similar smaller problems?

## Step 2
Identify the changing parameters and determine the number of subproblems.

## Step 3
How do problems relate to each other? In other words, let’s assume that you have computed the subproblems. How would you compute the main problem?

## Step 4
A base case is a subproblem that doesn’t depend on any other subproblem. In order to find such subproblems, you typically want to try a few examples, see how your problem simplifies into smaller subproblems, and at what point it cannot be simplified further.  

The reason a problem cannot be simplified further is that one of the parameters would become a value that is not possible given constraints of a problem.

## Step 5
To decide whether to go iteratively or recursively, you want to carefully think about the trade-offs.

| | Recursive | Iterative |
|---|---|---|---|
| Asymptotic time complexity | Same, assuming memoization | Same |
| Memory usage | Recursive stack, sparse memoization | Full memoization |
| Execution speed | Often faster, depending on input | Slower. Needs to do the same amount of work regardless of input |
| Stack overflow | Problem | No issues as long as enough memory for full  memoization |
| More intuitive/easier to implement | Often easier to reason | Harder |

**Stack overflow issues are typically a deal breaker and a reason why you would not want to have recursion in a (backend) production system.**

## Step 6
Memoization is a technique that is closely associated with DP. It is used for storing the results of expensive function calls and returning the cached result when the same inputs occur again. Why are we adding memoization to our recursion? We encounter the same subproblems which without memoization are computed repeatedly. Those repetitions very often lead to exponential time complexities.

This means that you should:

- Store your function result into your memory before every return statement
- Look up the memory for the function result before you start doing any other computation

## Step 7
There are some simple rules that can make computing time complexity of a dynamic programming problem much easier. Here are two steps that you need to do:

1. Count the number of states – this will depend on the number of changing parameters in your problem
2. Think about the work done per each state. In other words, if everything else but one state has been computed, how much work do you have to do to compute that last state

**Brute Force --> Memoization --> DP**
**Note**: For circular arrays, can use similar DP method as dealing with a straight array, just do it twice over the two different cases for a circular array.

# Geometry
---
## Notes
When comparing euclidean distance between two pairs of points, using dx2 + dy2 is sufficient. It is unnecessary to square root the value.

To find out if two circles overlap, check that the distance between the two centers of the circles is less than the sum of their radii.

# Graph
---
## Study Links
- [Representing Graphs](https://medium.com/basecs/from-theory-to-practice-representing-graphs-cfd782c5be38)
- [DFS Traversal](https://medium.com/basecs/deep-dive-through-a-graph-dfs-traversal-8177df5d0f13)
- [BFS Traversal](https://medium.com/basecs/going-broad-in-a-graph-bfs-traversal-959bd1a09255)

Be familiar with the various graph representations, graph search algorithms and their time and space complexities.

You can be given a list of edges and tasked to build your own graph from the edges to perform a traversal on. The common graph representations are:

- Adjacency matrix.
- Adjacency list.
- Hashmap of hashmaps.

A tree-like diagram could very well be a graph that allows for cycles and a naive recursive solution would not work. In that case you will have to handle cycles and keep a set of visited nodes when traversing.

Graph search algorithms:
- Common - Breadth-first Search, Depth-first Search
- Uncommon - Topological Sort, Dijkstra's algorithm
- Rare - Bellman-Ford algorithm, Floyd-Warshall algorithm, Prim's algorithm, Kruskal's algorithm

In coding interviews, graphs are commonly represented as 2-D matrices where cells are the nodes and each cell can traverse to its adjacent cells (up/down/left/right). Hence it is important that you be familiar with traversing a 2-D matrix.

When recursively traversing the matrix, always ensure that your next position is within the boundary of the matrix.

More tips for doing depth-first searches on a matrix can be found [here](https://discuss.leetcode.com/topic/66065/python-dfs-bests-85-tips-for-all-dfs-in-matrix-question/). A simple template for doing depth-first searches on a matrix goes like this:

```
def traverse(matrix):
  rows, cols = len(matrix), len(matrix[0])
  visited = set()
  directions = ((0, 1), (0, -1), (1, 0), (-1, 0))
  def dfs(i, j):
    if (i, j) in visited:
      return
    visited.add((i, j))
    # Traverse neighbors
    for direction in directions:
      next_i, next_j = i + direction[0], j + direction[1]
      if 0 <= next_i < rows and 0 <= next_j < cols: # Check boundary
        # Add any other checking here ^
        dfs(next_i, next_j)

  for i in range(rows):
    for j in range(cols):
      dfs(i, j)
```

## Corner Cases
- Empty graph.
- Graph with one or two nodes.
- Disjoint graphs.
- Graph with cycles.

# Interval
---
## Notes
Interval questions are questions where you are given an array of two-element arrays (an interval) and the two values represent a start and an end value. Interval questions are considered part of the array family but they involve some common techniques hence they are extracted out to this special section of their own.

An example interval array: `[[1, 2], [4, 7]]`.

Interval questions can be tricky to those who have not tried them before because of the sheer number of cases to consider when they overlap.

Do clarify with the interviewer whether `[1, 2]` and `[2, 3]` are considered overlapping intervals as it affects how you will write your equality checks.

A common routine for interval questions is to sort the array of intervals by each interval's starting value.

Be familiar with writing code to check if two intervals overlap and merging two overlapping intervals:

```
def is_overlap(a, b):
  return a[0] < b[1] and b[0] < a[1]

def merge_overlapping_intervals(a, b):
  return [min(a[0], b[0]), max(a[1], b[1])]
```

## Corner Cases
- Single Interval
- Non-overlapping intervals
- An interval totally consumed within another interval
- Duplicate intervals

# Linked List
---
## Notes
Like arrays, liked lists are used to represent sequential data.

**Benefit of linked lists**
Insertion and deletion from anywhere in the list is O(1) whereas in arrays the following elements will have to be shifted.

**Adding a dummy node at the head and/or tail might help to handle many edge cases where operations have to be performed at the head or the tail.** The presence of dummy nodes essentially ensures that operations will never have be done on the head or the tail, thereby removing a lot of headache in writing conditional checks to dealing with null pointers. Be sure to remember to remove them at the end of the operation.

Sometimes linked lists problem can be solved without additional storage. Try to borrow ideas from reverse a linked list problem.

For deletion in linked lists, you can either modify the node values or change the node pointers. You might need to keep a reference to the previous element.

For partitioning linked lists, create two separate linked lists and join them back together.

Linked lists problems share similarity with array problems, think about how you would do it for an array and try to apply it to a linked list.

Two pointer approaches are also common for linked lists. For example:

- Getting the kth from last node - Have two pointers, where one is k nodes ahead of the other. When the node ahead reaches the end, the other node is k nodes behind.
- Detecting cycles - Have two pointers, where one pointer increments twice as much as the other, if the two pointers meet, means that there is a cycle.
- Getting the middle node - Have two pointers, where one pointer increments twice as much as the other. When the faster node reaches the end of the list, the slower node will be at the middle.

Be familiar with the following routines because many linked list questions make use of one or more of these routines in the solution:

- Counting the number of nodes in the linked list.
- Reversing a linked list in-place.
- Finding the middle node of the linked list using fast/slow pointers.
- Merging two lists together.

## Corner Cases
- Single node.
- Two nodes.
- Linked list has cycle. Clarify with the interviewer whether there can be a cycle in the list. Usually the answer is no.

# Math
---
If code involves division or modulo, remember to check for division or modulo by 0 case.

When a question involves "a multiple of a number", perhaps modulo might be useful.

Check for and handle overflow/underflow if you are using a typed language like Java and C++. At the very least, mention that overflow/underflow is possible and ask whether you need to handle it.

Consider negative numbers and floating point numbers. This may sound obvious, but under interview pressure, many obvious cases go unnoticed.

**If the question asks to implement an operator such as power, squareroot or division and want it to be faster than O(n), binary search is usually the approach to go.**

## Some common formulas:
- Sum of 1 to N = (n+1) * n/2
- Sum of GP = 20 + 21 + 22 + 23 + ... 2n = 2n+1 - 1
- Permutations of N = N! / (N-K)!
- Combinations of N = N! / (K! * (N-K)!)

# Matrix
---
## Notes
A matrix is a 2-dimensional array. Questions involving matrices are usually related to dynamic programming or graph traversal.

For questions involving traversal or dynamic programming, you almost always want to make a copy of the matrix with the same dimensions that is initialized to empty values to store the visited state or dynamic programming table. Be familiar with such a routine:

```
rows, cols = len(matrix), len(matrix[0])
copy = [[0 for _ in range(cols)] for _ in range(rows)]
```

Many grid-based games can be modeled as a matrix, such as Tic-Tac-Toe, Sudoku, Crossword, Connect 4, Battleship, etc. It is not uncommon to be asked to verify the winning condition of the game. For games like Tic-Tac-Toe, Connect 4 and Crosswords, where verification has to be done vertically and horizontally, one trick is to write code to verify the matrix for the horizontal cells, transpose the matrix and reuse the logic for horizontal verification to verify originally vertical cells (which are now horizontal).

Transposing a matrix in Python is simply:
```
transposed_matrix = zip(*matrix)
```
## Corner Cases
- Empty matrix. Check that none of the arrays are 0 length.
- 1 x 1 matrix.
- Matrix with only one row or column.

# Recursion
---
## Notes
Recursion is useful for permutation, because it generates all combinations and tree-based questions. You should know how to generate all permutations of a sequence as well as how to handle duplicates.

Remember to always define a base case so that your recursion will end.

Recursion implicitly uses a stack. Hence all recursive approaches can be rewritten iteratively using a stack. Beware of cases where the recursion level goes too deep and causes a stack overflow (the default limit in Python is 1000). You may get bonus points for pointing this out to the interviewer. Recursion will never be O(1) space complexity because a stack is involved, unless there is [tail-call optimization](https://stackoverflow.com/questions/310974/what-is-tail-call-optimization) (TCO). Find out if your chosen language supports TCO.

# String
---
## Notes
Please read the above tips on sequence. They apply to strings too.

Ask about input character set and case sensitivity. Usually the characters are limited to lowercase Latin characters, for example a to z.

When you need to compare strings where the order isn’t important (like anagram), you may consider using a HashMap as a counter. If your language has a built-in Counter class like Python, ask to use that instead.

If you need to keep a counter of characters, a common mistake is to say that the space complexity required for the counter is O(n). The space required for a counter is O(1) not O(n). This is because the upper bound is the range of characters, which is usually a fixed constant of 26. The input set is just lowercase Latin characters.

Common data structures for looking up strings efficiently are:
- Trie / Prefix Tree
- Suffix Tree

Common string algorithms are:
- Rabin Karp for efficient searching of substring using a rolling hash.
- KMP for efficient searching of substring.

Corner Cases:
- Strings with only one distinct character.

Non-repeating Characters:
- Use a 26-bit bitmask to indicate which lower case latin characters are inside the string.

```
mask = 0
for c in set(word):
  mask |= (1 << (ord(c) - ord('a')))
```

To determine if two strings have common characters, perform & on the two bitmasks. If the result is non-zero, `mask_a & mask_b > 0`, then the two strings have common characters.

## Anagram
An anagram is word switch or word play. It is the result of re-arranging the letters of a word or phrase to produce a new word or phrase, while using all the original letters only once. In interviews, usually we are only bothered with words without spaces in them.

To determine if two strings are anagrams, there are a few plausible approaches:

- Sorting both strings should produce the same resulting string. This takes O(nlgn) time and O(lgn) space.
- If we map each character to a prime number and we multiply each mapped number together, anagrams should have the same multiple (prime factor decomposition). This takes O(n) time and O(1) space.
- Frequency counting of characters will help to determine if two strings are anagrams. This also takes O(n) time and O(1) space.

## Palindrome
A palindrome is a word, phrase, number, or other sequence of characters which reads the same backward as forward, such as madam or racecar.

Here are ways to determine if a string is a palindrome:
- Reverse the string and it should be equal to itself.
- Have two pointers at the start and end of the string. Move the pointers inward till they meet. At any point in time, the characters at both pointers should match.

The order of characters within the string matters, so HashMaps are usually not helpful.

When a question is about counting the number of palindromes, a common trick is to have two pointers that move outward, away from the middle. Note that palindromes can be even or odd length. For each middle pivot position, you need to check it twice: Once that includes the character and once without the character.

- For substrings, you can terminate early once there is no match.
- For subsequences, use dynamic programming as there are overlapping subproblems. Check out [this question](https://leetcode.com/problems/longest-palindromic-subsequence/).

# Tree
---
## Study Links
- [Leaf It Up To Binary Trees](https://medium.com/basecs/leaf-it-up-to-binary-trees-11001aaf746d)

## Notes
A tree is an undirected and connected acyclic graph.

Recursion is a common approach for trees. When you notice that the subtree problem can be used to solve the entire problem, try using recursion.

When using recursion, always remember to check for the base case, usually where the node is `null`.

When you are asked to traverse a tree by level, use breadth-first search.

Sometimes it is possible that your recursive function needs to return two values.

If the question involves summation of nodes along the way, be sure to check whether nodes can be negative.

You should be very familiar with writing pre-order, in-order, and post-order traversal recursively. As an extension, challenge yourself by writing them iteratively. Sometimes interviewers ask candidates for the iterative approach, especially if the candidate finishes writing the recursive approach too quickly.

## Corner Cases
- Empty tree.
- Single node.
- Two nodes.
- Very skewed tree (like a linked list).

## Binary Tree
In-order traversal of a binary tree is insufficient to uniquely serialize a tree. Pre-order or post-order traversal is also required.

## Binary Search Tree (BST)
In-order traversal of a BST will give you all elements in order.

Be very familiar with the properties of a BST and validating that a binary tree is a BST. This comes up more often than expected.

When a question involves a BST, the interviewer is usually looking for a solution which runs faster than O(n).

# Trie
---
## Study Links
- [Trying to Understand Tries](https://medium.com/basecs/trying-to-understand-tries-3ec6bede0014)
- [Implement Trie (Prefix Tree)](https://leetcode.com/articles/implement-trie-prefix-tree/)

## Notes
Tries are special trees (prefix trees) that make searching and storing strings more efficient. Tries have many practical applications, such as conducting searches and providing autocomplete. It is helpful to know these common applications so that you can easily identify when a problem can be efficiently solved using a trie.

Sometimes preprocessing a dictionary of words (given in a list) into a trie, will improve the efficiency of searching for a word of length k, among n words. Searching becomes O(k) instead of O(n).

Be familiar with implementing, from scratch, a `Trie` class and its `add`, `remove` and `search` methods.

# Heap
---
## Study Links
- [Learning to Love Heaps](https://medium.com/basecs/learning-to-love-heaps-cef2b273a238)

## Notes
If you see a top or lowest k being mentioned in the question, it is usually a signal that a heap can be used to solve the problem, such as in [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/).

If you require the top k elements use a Min Heap of size k. Iterate through each element, pushing it into the heap. Whenever the heap size exceeds k, remove the minimum element, that will guarantee that you have the k largest elements.
