#### [Back To Topics](readme.md)

# Java DSA


## Core DSA Concepts
- Data Structures
- Algorithms
- Time Complexity
- Space Complexity
- Big-O, Big-Theta, Big-Omega
- Amortized Analysis
- Asymptotic Analysis
- Best / Average / Worst Case
- Input Size (n)
- Trade-offs
- In-place vs Out-of-place
- Stable vs Unstable algorithms
- Deterministic vs Randomized

## Arrays & Strings
- Array
- Dynamic Array
- 1D / 2D Arrays
- Jagged Arrays
- Strings (immutable)
- StringBuilder, StringBuffer
- Keywords
	- Two Pointers
	- Sliding Window
	- Prefix Sum
	- Suffix Sum
	- Kadane’s Algorithm
	- Subarray vs Subsequence
	- Rotation
	- Partitioning
	- Dutch National Flag
	- Hashing for strings
	- Rabin-Karp

## Linked Lists
- Singly Linked List
- Doubly Linked List
- Circular Linked List
- Keywords
	- Fast & Slow pointers (Floyd Cycle)
	- Cycle detection
	- Reverse linked list
	- Merge two lists
	- Middle node
	- Intersection
	- Dummy node technique
	- In-place reversal
	
## Stack
- LIFO
- Stack implementation (array / linked list)
- Keywords
	- Monotonic Stack
	- Next Greater Element
	- Balanced Parentheses
	- Expression Evaluation
	- Infix / Postfix / Prefix
	- Recursion stack

## Queue / Deque
- FIFO
- Queue
- Deque (Double-ended queue)
- Circular Queue
- Priority Queue (Heap)
- Keywords
	- BFS
	- Sliding Window Maximum
	- Monotonic Queue
	- Level-order traversal
	
## Trees
- Binary Tree
- Binary Search Tree (BST)
- AVL Tree
- Red-Black Tree
- Segment Tree
- Fenwick Tree (Binary Indexed Tree)
- Trie (Prefix Tree)
- Heap (Min/Max Heap)
- Keywords
	- Traversals (Inorder, Preorder, Postorder, Level-order)
	- DFS / BFS
	- Height / Depth
	- Diameter
	- LCA (Lowest Common Ancestor)
	- Balanced tree
	- Tree rotations
	- Heapify
	- Top-K elements
	- Range queries
	
## Graphs
- Directed / Undirected Graph
- Weighted / Unweighted Graph
- Adjacency List / Matrix
- Algorithms
	- BFS
	- DFS
	- Dijkstra’s Algorithm
	- Bellman-Ford
	- Floyd-Warshall
	- Prim’s Algorithm
	- Kruskal’s Algorithm
	- Topological Sort
- Keywords
	- Cycle detection
	- Connected components
	- Strongly Connected Components (Kosaraju, Tarjan)
	- Shortest path
	- Minimum Spanning Tree (MST)
	- Bipartite graph
	- Union-Find (Disjoint Set)

## Searching Algorithms
- Linear Search
- Binary Search
- Keywords
	- Lower Bound / Upper Bound
	- Search space reduction
	- Binary search on answer
	- Ternary search

## Sorting Algorithms
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort
- Heap Sort
- Counting Sort
- Radix Sort
- Bucket Sort
- Keywords
	- Divide & Conquer
	- Stable vs Unstable
	- In-place sorting
	- Partitioning (Lomuto / Hoare)

## Recursion & Backtracking
- Recursion
- Base case
- Call stack
- Keywords
	- Backtracking
	- Subsets
	- Permutations
	- Combinations
	- N-Queens
	- Sudoku solver
	- Decision tree
	- State space tree

## Dynamic Programming (DP)
- Memoization (Top-down)
- Tabulation (Bottom-up)
- Keywords
	- Overlapping subproblems
	- Optimal substructure
	- State definition
	- Transition relation
	- DP table
- Patterns
	- Knapsack (0/1, Unbounded)
	- Longest Common Subsequence (LCS)
	- Longest Increasing Subsequence (LIS)
	- Coin Change
	- Matrix Chain Multiplication
	- DP on Trees
	- DP on Graphs

## Greedy Algorithms
- Greedy choice property
- Keywords
	- Activity selection
	- Fractional Knapsack
	- Huffman Coding
	- Interval scheduling
	- Local vs Global optimum

## Bit Manipulation
- Bitwise operators (&, |, ^, ~, <<, >>)
- Keywords
	- XOR tricks
	- Bit masking
	- Power of two
	- Set / clear / toggle bits
	- Subsets using bits
	
## Mathematics & Number Theory
- Prime numbers
- GCD / LCM
- Sieve of Eratosthenes
- Modular arithmetic
- Fast exponentiation
- Combinatorics
- Permutations / Combinations

## Advanced Data Structures
- Segment Tree
- Fenwick Tree
- Trie
- Suffix Array
- Suffix Tree
- Disjoint Set Union (Union-Find)
- Skip List
- B-Tree / B+ Tree

## Advanced Algorithms
- KMP Algorithm
- Rabin-Karp
- Z Algorithm
- Manacher’s Algorithm
- A- Search
- Meet-in-the-middle
- Mo’s Algorithm

## Patterns & Problem-Solving Techniques
- Sliding Window
- Two Pointers
- Divide & Conquer
- Greedy
- Backtracking
- DP patterns
- Graph traversal patterns
- Monotonic Stack/Queue
- Prefix/Suffix technique

## Pitfalls & Anti-Patterns
- Off-by-one errors
- Integer overflow
- Infinite loops
- Stack overflow (recursion)
- Wrong complexity assumption
- Not handling edge cases

## Testing & Edge Cases
- Empty input
- Single element
- Large input
- Duplicates
- Negative values
- Boundary conditions

## Java-Specific DSA Keywords
- ArrayList, LinkedList
- HashMap, HashSet
- TreeMap, TreeSet
- PriorityQueue
- Deque, ArrayDeque
- Collections.sort
- Arrays.sort
- Comparator / Comparable
- Streams for DSA
- Recursion limits (stack size)
- Autoboxing overhead

## Interview Deep-Dive Keywords
- Time vs Space trade-off
- Brute force → Optimized approach
- Pattern recognition
- Dry run
- Edge case handling
- Complexity justification
- Code readability
- Optimization strategies

## Competitive Programming Keywords
- Fast I/O
- Input parsing
- Constraints handling
- Modulo operations
- Precomputation
- Lazy propagation (Segment Tree)

## Real-World System Mapping
- Caching (LRU → LinkedHashMap)
- Search engines → Trie
- Networking → Graphs
- Scheduling → PriorityQueue
- Analytics → Sliding window








## Core DSA Concepts

Data Structures and Algorithms (DSA) form the foundation of efficient programming. This guide covers essential concepts for analysing and comparing algorithmic performance.

#### Data Structures
- **Definition:** A specific way of organising, storing, and managing data to enable efficient access and modification.
- **Examples:** Arrays, linked lists, stacks, queues, hash tables, trees, graphs.
- **Choice depends on:** Operations needed (search, insert, delete), order requirements, memory constraints.

#### Algorithms
- **Definition:** A finite sequence of well‑defined, step‑by‑step instructions to solve a specific problem or perform a computation.
- **Examples:** Sorting (quicksort, mergesort), searching (binary search), graph algorithms (Dijkstra, BFS).



#### Time Complexity
- **Definition:** The amount of **computational time** an algorithm takes to run, expressed as a function of the input size `n`.
- **Why it matters:** Predicts how an algorithm scales as input grows; helps compare algorithms before implementation.
- **Measured in:** Number of basic operations (comparisons, assignments, arithmetic) – not wall‑clock seconds.

#### Space Complexity
- **Definition:** The amount of **memory** an algorithm uses, expressed as a function of the input size `n`.
- **Includes:** Input space (often ignored for complexity analysis) + auxiliary space (extra memory used by the algorithm).
- **Trade‑off:** Sometimes we can trade space for time (e.g., memoisation in dynamic programming).



#### Big‑O, Big‑Theta, Big‑Omega

These are mathematical notations describing the **asymptotic behaviour** of functions (typically runtime or memory).

| Notation | Name | Meaning | Analogy |
|-||||
| **O** (Big‑O) | Upper bound | Worst‑case growth rate (at most) | “Algorithm will not be slower than …” |
| **Ω** (Big‑Omega) | Lower bound | Best‑case growth rate (at least) | “Algorithm will not be faster than …” |
| **Θ** (Big‑Theta) | Tight bound | Both upper and lower bound (same order) | “Algorithm grows exactly like …” |

**Example (linear search in an unsorted array):**
- **Best case** (Ω(1)): element is first.
- **Worst case** (O(n)): element is last or absent.
- **Average case** (Θ(n)): on average, ~n/2 comparisons.

**Common Big‑O classes (fastest to slowest):**
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)
```

#### Amortized Analysis
- **Definition:** Averaging the time (or space) taken over a **sequence of operations**, rather than considering each operation individually.
- **Use case:** Some operations are expensive but rare; amortised analysis gives a realistic average cost.
- **Example:** `ArrayList` / `vector` – most `add` operations are O(1), but when capacity is full, resizing (copying all elements) is O(n). Amortised over many additions, each `add` is still O(1).
- **Methods:** Aggregate analysis, accounting method, potential method.

#### Asymptotic Analysis
- **Definition:** Analysing algorithm performance as the input size `n` approaches **infinity**, ignoring constant factors and lower‑order terms.
- **Focus:** Growth rate (how runtime changes with `n`), not absolute runtime.
- **Why ignore constants?** They depend on hardware, language, compiler – asymptotic analysis gives a platform‑independent comparison.



#### Best / Average / Worst Case

| Case | Description | When used |
||-|--|
| **Best case** | Minimum time for any input of size `n` | Rarely used for guarantees; sometimes for lower bound (Ω) |
| **Worst case** | Maximum time for any input of size `n` | Most common; provides **guarantee** that algorithm will not exceed this time |
| **Average case** | Expected time over random inputs of size `n` | More realistic but harder to compute; requires probability distribution |

**Example (Quicksort):**
- Best case: O(n log n) – pivot always median
- Worst case: O(n²) – pivot always smallest/largest (already sorted input)
- Average case: O(n log n) – with random pivots

#### Input Size (n)
- **Definition:** The number of elements or the measure of the data that the algorithm processes.
- **Examples:** Length of an array, number of nodes in a graph, number of bits in a number.
- **Important:** Complexity is expressed **in terms of n**; doubling n gives insight into scaling behaviour.



#### Trade‑offs
- **Definition:** A situation where improving one aspect (e.g., time) degrades another (e.g., space, readability, simplicity).
- **Common trade‑offs in DSA:**
  - **Time vs Space:** Use a hash table (more memory) for faster lookups vs a sorted array (less memory) with binary search.
  - **Readability vs Performance:** Simple linear search (readable) vs complex binary search (faster for sorted data).
  - **Implementation complexity:** Balanced trees (complex) vs hash tables (simpler average case).

#### In‑place vs Out‑of‑place

| Term | Definition | Example |
||||
| **In‑place algorithm** | Uses **O(1) extra space** (modifies the input directly) | Bubble sort, quicksort (with careful implementation), reversing an array |
| **Out‑of‑place algorithm** | Requires **extra space** proportional to the input size (often O(n)) | Mergesort (needs temporary array), stable sorts that copy |

**Note:** In‑place does **not** mean “no extra memory” – it means constant or very small extra memory (usually O(1) or O(log n)).

#### Stable vs Unstable algorithms

| Term | Definition | Example |
||||
| **Stable sort** | Preserves the relative order of equal elements (based on original order) | Mergesort, bubble sort, insertion sort |
| **Unstable sort** | May change the relative order of equal elements | Quicksort (typical implementation), heapsort, selection sort |

**Why stability matters:** Sorting by multiple keys (e.g., first sort by name, then by age) – stable sort keeps the previous ordering.

#### Deterministic vs Randomized

| Term | Definition | Pros / Cons |
|||--|
| **Deterministic algorithm** | For a given input, the algorithm always follows the same sequence of steps and produces the same output. | Predictable, easier to debug, worst‑case guarantees may be poor. |
| **Randomized algorithm** | Uses random numbers (or pseudo‑random) to make decisions; output or runtime may vary between runs. | Often simpler to design, excellent average‑case performance, can avoid worst‑case inputs (e.g., randomised quicksort). |

**Examples:**
- Deterministic: Binary search, mergesort.
- Randomized: Quickselect (random pivot), Monte Carlo algorithms, randomised primality testing.

#### Summary Table

| Concept | Core Idea |
|||
| **Time Complexity** | How runtime scales with input size |
| **Space Complexity** | How memory usage scales with input size |
| **Big‑O** | Upper bound (worst‑case growth) |
| **Amortized Analysis** | Average cost over a sequence of operations |
| **In‑place** | O(1) extra space (modifies input) |
| **Stable** | Preserves order of equal elements |
| **Randomized** | Uses randomness to make decisions |












| Type | Context | Best case | Worst case | Average case | 
| --- | --- | --- | --- | --- |
| Sorting Algorithms | Quicksort |  O(n log n) | O(n²) | O(n log n) |




| Implementation | When to Use | Ordering | Thread-Safe |
|---|---|---|---|
| `HashMap` | General purpose, fast lookup | Unordered | No |
| `LinkedHashMap` | Insertion order + LRU cache | Insertion order | No |
| `TreeMap` | Sorted keys, range queries | Sorted | No |
| `ConcurrentHashMap` | High concurrency | Unordered | Yes |
| `EnumMap` | Enum keys | Declaration order | No |
| `WeakHashMap` | Cache with GC-friendly keys | Unordered | No |





### Sorting Algorithms

**Quicksort**

* Best case: O(n log n)
* Worst case: O(n²)
* Average case: O(n log n)

**Merge Sort**

* Best case: O(n log n)
* Worst case: O(n log n)
* Average case: O(n log n)

**Heap Sort**

* Best case: O(n log n)
* Worst case: O(n log n)
* Average case: O(n log n)

**Bubble Sort**

* Best case: O(n)
* Worst case: O(n²)
* Average case: O(n²)

**Insertion Sort**

* Best case: O(n)
* Worst case: O(n²)
* Average case: O(n²)

**Selection Sort**

* Best case: O(n²)
* Worst case: O(n²)
* Average case: O(n²)

**Counting Sort**

* Best case: O(n + k)
* Worst case: O(n + k)
* Average case: O(n + k)

**Radix Sort**

* Best case: O(nk)
* Worst case: O(nk)
* Average case: O(nk)

**Bucket Sort**

* Best case: O(n + k)
* Worst case: O(n²)
* Average case: O(n + k)

**Tim Sort**

* Best case: O(n)
* Worst case: O(n log n)
* Average case: O(n log n)



## Searching Algorithms

**Linear Search**

* Best case: O(1)
* Worst case: O(n)
* Average case: O(n)

**Binary Search**

* Best case: O(1)
* Worst case: O(log n)
* Average case: O(log n)

**Jump Search**

* Best case: O(1)
* Worst case: O(√n)
* Average case: O(√n)

**Interpolation Search**

* Best case: O(1)
* Worst case: O(n)
* Average case: O(log log n)

**Exponential Search**

* Best case: O(1)
* Worst case: O(log n)
* Average case: O(log n)



## Graph Algorithms

**Breadth-First Search (BFS)**

* Best case: O(V + E)
* Worst case: O(V + E)
* Average case: O(V + E)

**Depth-First Search (DFS)**

* Best case: O(V + E)
* Worst case: O(V + E)
* Average case: O(V + E)

**Dijkstra’s Algorithm**

* Best case: O((V + E) log V)
* Worst case: O((V + E) log V)
* Average case: O((V + E) log V)

**Bellman-Ford Algorithm**

* Best case: O(VE)
* Worst case: O(VE)
* Average case: O(VE)

**Floyd-Warshall Algorithm**

* Best case: O(V³)
* Worst case: O(V³)
* Average case: O(V³)

**Kruskal’s Algorithm**

* Best case: O(E log E)
* Worst case: O(E log E)
* Average case: O(E log E)

**Prim’s Algorithm**

* Best case: O(E log V)
* Worst case: O(E log V)
* Average case: O(E log V)

**Topological Sort**

* Best case: O(V + E)
* Worst case: O(V + E)
* Average case: O(V + E)



## Dynamic Programming

**Fibonacci (DP)**

* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)

**0/1 Knapsack**

* Best case: O(nW)
* Worst case: O(nW)
* Average case: O(nW)

**Longest Common Subsequence (LCS)**

* Best case: O(mn)
* Worst case: O(mn)
* Average case: O(mn)

**Longest Increasing Subsequence (LIS)**

* Best case: O(n log n)
* Worst case: O(n²)
* Average case: O(n log n)

**Matrix Chain Multiplication**

* Best case: O(n³)
* Worst case: O(n³)
* Average case: O(n³)

**Coin Change**

* Best case: O(n * amount)
* Worst case: O(n * amount)
* Average case: O(n * amount)



## Tree Algorithms

**Tree Traversal (Inorder, Preorder, Postorder)**

* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)

**Level Order Traversal**

* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)

**Binary Search Tree Operations**

* Best case: O(log n)
* Worst case: O(n)
* Average case: O(log n)

**AVL Tree Operations**

* Best case: O(log n)
* Worst case: O(log n)
* Average case: O(log n)

**Red-Black Tree Operations**

* Best case: O(log n)
* Worst case: O(log n)
* Average case: O(log n)



## String Algorithms

**Naive Pattern Matching**

* Best case: O(n)
* Worst case: O(nm)
* Average case: O(nm)

**KMP Algorithm**

* Best case: O(n + m)
* Worst case: O(n + m)
* Average case: O(n + m)

**Rabin-Karp Algorithm**

* Best case: O(n + m)
* Worst case: O(nm)
* Average case: O(n + m)

**Z Algorithm**

* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)



## Greedy Algorithms

**Activity Selection**

* Best case: O(n log n)
* Worst case: O(n log n)
* Average case: O(n log n)

**Huffman Coding**

* Best case: O(n log n)
* Worst case: O(n log n)
* Average case: O(n log n)



## Backtracking

**N-Queens**

* Best case: O(n!)
* Worst case: O(n!)
* Average case: O(n!)

**Sudoku Solver**

* Best case: O(1)
* Worst case: O(9^(n*n))
* Average case: O(9^(n*n))



## Core Data Structures (Operations)

**Array**

* Access: O(1)
* Search: O(n)
* Insert: O(n)
* Delete: O(n)

**Linked List**

* Access: O(n)
* Search: O(n)
* Insert: O(1)
* Delete: O(1)

**Stack**

* Push: O(1)
* Pop: O(1)
* Peek: O(1)

**Queue**

* Enqueue: O(1)
* Dequeue: O(1)

**Hash Table**

* Search: O(1) average, O(n) worst
* Insert: O(1) average
* Delete: O(1) average

**Heap (Priority Queue)**

* Insert: O(log n)
* Delete: O(log n)
* Peek: O(1)

**Trie**

* Insert: O(L)
* Search: O(L)
* Delete: O(L)



## Advanced Data Structures

**Segment Tree**

* Build: O(n)
* Query: O(log n)
* Update: O(log n)

**Fenwick Tree (Binary Indexed Tree)**

* Update: O(log n)
* Query: O(log n)

**Disjoint Set (Union-Find)**

* Find: O(α(n))
* Union: O(α(n))

**Suffix Tree**

* Build: O(n)
* Search: O(m)

**Suffix Array**

* Build: O(n log n)
* Search: O(m log n)



## Misc Algorithms

**Sliding Window**
* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)

**Two Pointers**
* Best case: O(n)
* Worst case: O(n)
* Average case: O(n)
