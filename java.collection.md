#### [Back To Topics](readme.md)

# Java Collection

## Core Collection Framework Concepts

### Java Collections Framework (JCF)
A unified architecture for storing and manipulating groups of objects. It includes:
- **Interfaces** (e.g., `Collection`, `List`, `Set`, `Queue`, `Deque`, `Map`)
- **Implementations** (e.g., `ArrayList`, `HashSet`, `TreeMap`)
- **Algorithms** (e.g., sorting, searching, shuffling in `Collections`)

#### Collection vs Collections vs Arrays
| Term | Meaning |
|------|---------|
| **`Collection`** | Root interface in the collection hierarchy (extends `Iterable`). Represents a group of objects (elements). |
| **`Collections`** | A utility class with static methods that operate on or return collections (e.g., `sort()`, `synchronizedList()`, `unmodifiableList()`). |
| **`Arrays`** | A utility class for working with primitive and object arrays (e.g., `asList()`, `sort()`, `binarySearch()`). |

#### Iterable Interface
The topmost interface in the collection hierarchy. It has a single method `iterator()` that returns an `Iterator`.  
**Enhanced for‑loop** (`for (T item : iterable)`) works on any `Iterable`.

#### Iterator Pattern
A design pattern that provides a way to access elements of a container sequentially without exposing its underlying representation.  
In JCF, `Iterator` provides `hasNext()`, `next()`, and optional `remove()`.

#### Container / Data Structure
A generic term for any object that holds other objects. In JCF, collections are containers that implement specific data structures (e.g., dynamic array, linked list, hash table, tree).

#### Generics
A feature that enables **parameterized types** (e.g., `List<String>`).  
Benefits:
- Compile‑time type checking
- Elimination of explicit casts
- Enables writing reusable, type‑safe code.

#### Type Safety
Ensuring that operations on a collection are restricted to elements of a specific type. With generics, `List<Integer>` cannot accidentally accept a `String` – the compiler prevents it.

#### Autoboxing / Unboxing
| **Autoboxing** | Automatic conversion of a primitive type to its corresponding wrapper class (e.g., `int` → `Integer`) |
| **Unboxing**   | Automatic conversion of a wrapper to its primitive (e.g., `Integer` → `int`) |

This allows primitives to be used directly in collections (which store only objects).

#### Covariance / Contravariance (PECS)
- **Covariance** (`? extends T`): You can **get** elements as `T`, but cannot **put** (except `null`).  
  Example: `List<? extends Number>` – can contain `Integer`, `Double`, etc.
- **Contravariance** (`? super T`): You can **put** elements of type `T`, but when **getting**, you only know it’s an `Object`.  
  Example: `List<? super Integer>` – can hold `Integer`, `Number`, `Object`.

**PECS** (Producer `extends`, Consumer `super`):  
- If a parameter **produces** items (you read from it), use `? extends T`.  
- If it **consumes** items (you write to it), use `? super T`.

#### Immutability
An **immutable collection** cannot be modified after creation (no add, remove, set).  
- `Collections.unmodifiableList()` wraps a collection and throws `UnsupportedOperationException` on modification attempts.  
- Java 9+ provides `List.of()`, `Set.of()`, `Map.of()` for true immutability.

#### Fail‑fast vs Fail‑safe

| **Fail‑fast** | Iterators that throw `ConcurrentModificationException` if the collection is structurally modified after the iterator is created (except through the iterator’s own `remove`). Example: All collections in `java.util` (except concurrent ones). |
| **Fail‑safe** | Iterators that work on a **snapshot** or tolerate concurrent modification without throwing exceptions. Example: `CopyOnWriteArrayList`, `ConcurrentHashMap` iterators. |

#### Structural Modification
Any operation that changes the **size** of a collection (add, remove, clear) or that would cause an existing iterator to become inconsistent (e.g., sorting a `List`).  
Changing the value of an existing element is **not** a structural modification for most collections.

#### Concurrent Modification
Modifying a collection (structurally) while it is being iterated over by another thread or even by the same thread without using the iterator’s own methods.  
- In single‑threaded code: modifying the collection directly while iterating with an enhanced for‑loop or external iterator.  
- In multi‑threaded code: modifying a shared collection without proper synchronization.  

Fail‑fast iterators detect this and throw `ConcurrentModificationException` as a safety measure.

## Core Interfaces Hierarchy in Java Collections Framework

The Java Collections Framework (JCF) organizes its core interfaces into a well‑defined hierarchy. **`Map`** is a fundamental part of the framework but does **not** extend `Collection` – it stands alongside the `Collection` hierarchy.

### Simplified Hierarchy Diagram

```
Iterable (java.lang)
    │
    └── Collection (java.util)
            ├── List
            ├── Set
            │       └── SortedSet
            │               └── NavigableSet
            ├── Queue
            └── Deque (extends Queue)

Map (java.util) – separate root
    └── SortedMap
            └── NavigableMap
```


#### Iterable
- **Topmost interface** (in `java.lang`, not `java.util`).
- Defines `iterator()` – all collections inherit this, allowing enhanced for‑loop.
- Also defines `forEach()` (default) and `spliterator()`.

#### Collection
- **Root interface** of the collection hierarchy (excluding `Map`).
- Defines basic operations: `add()`, `remove()`, `size()`, `isEmpty()`, `contains()`, `clear()`, `toArray()`, etc.
- Subinterfaces add specific semantics: `List` (ordered, indexed), `Set` (no duplicates), `Queue` (FIFO, priority).

#### List
- Ordered collection (maintains insertion order).
- Allows duplicate elements, nulls (usually).
- Provides **index‑based** access: `get(index)`, `set(index, element)`, `add(index, element)`, `remove(index)`.
- Common implementations: `ArrayList`, `LinkedList`, `Vector`.

#### Set
- **No duplicate elements** (based on `equals()` / `hashCode()`).
- No ordering guarantee (unless using `SortedSet`/`LinkedHashSet`).
- Common implementations: `HashSet`, `LinkedHashSet`, `TreeSet`.

#### Queue
- Designed for holding elements **prior to processing** (FIFO by default, but not required).
- Provides: `offer(e)`, `poll()`, `peek()` (vs. `add()`, `remove()`, `element()` with different failure behaviour).
- Implementations: `PriorityQueue`, `ArrayDeque` (also a `Deque`), `LinkedList`.

#### Deque (Double Ended Queue)
- Extends `Queue` – supports element insertion/removal **at both ends**.
- Methods: `addFirst()`, `addLast()`, `removeFirst()`, `removeLast()`, `offerFirst()`, `offerLast()`, `pollFirst()`, `pollLast()`, `peekFirst()`, `peekLast()`.
- Can be used as a stack (`push()`, `pop()`) or queue.
- Implementations: `ArrayDeque`, `LinkedList`.

#### Map (not part of Collection but core)
- Stores key‑value pairs. **Does not extend `Collection`**.
- Core methods: `put(key, value)`, `get(key)`, `containsKey(key)`, `keySet()`, `values()`, `entrySet()`.
- Implementations: `HashMap`, `LinkedHashMap`, `Hashtable`, `TreeMap` (implements `SortedMap`), `ConcurrentHashMap`.

#### SortedSet
- Extends `Set` – maintains elements in **sorted order** (natural ordering or custom `Comparator`).
- Adds: `first()`, `last()`, `headSet(toElement)`, `tailSet(fromElement)`, `subSet(from, to)`.
- Implemented by `TreeSet`.

#### NavigableSet
- Extends `SortedSet` – adds **navigation methods** for closest matches:
  - `lower(e)`, `floor(e)`, `ceiling(e)`, `higher(e)`
  - `descendingSet()`, `pollFirst()`, `pollLast()`
- Implemented by `TreeSet` (and `ConcurrentSkipListSet`).

#### SortedMap
- Extends `Map` – maintains keys in **sorted order**.
- Adds similar range‑view methods: `firstKey()`, `lastKey()`, `headMap()`, `tailMap()`, `subMap()`.
- Implemented by `TreeMap`.

#### NavigableMap
- Extends `SortedMap` – adds navigation methods for keys:
  - `lowerKey()`, `floorKey()`, `ceilingKey()`, `higherKey()`
  - `descendingMap()`, `pollFirstEntry()`, `pollLastEntry()`
- Implemented by `TreeMap` (and `ConcurrentSkipListMap`).



#### Key Relationships Summary

| Interface | Extends | Added Semantics |
|-----------|---------|----------------|
| `Collection` | `Iterable` | Basic group of elements |
| `List` | `Collection` | Ordered, indexed, duplicates allowed |
| `Set` | `Collection` | No duplicates |
| `Queue` | `Collection` | For processing (usually FIFO) |
| `Deque` | `Queue` | Double‑ended queue (stack + queue) |
| `SortedSet` | `Set` | Sorted order |
| `NavigableSet` | `SortedSet` | Navigation & descending views |
| `SortedMap` | `Map` | Keys sorted |
| `NavigableMap` | `SortedMap` | Key navigation & descending |

> **Note:** `Iterable` is in `java.lang`; all others are in `java.util`. `Map` is a separate root, but `SortedMap` and `NavigableMap` are its direct extensions.

## List Implementations in Java

The Java Collections Framework provides several `List` implementations, each with different internal data structures, performance characteristics, and use cases.

### ArrayList
- **Underlying structure:** Dynamic (resizable) array  
- **Key features:**  
  - Implements **random access** – `get(index)` and `set(index, element)` are O(1)  
  - Index‑based operations are fast  
  - Adding/removing at the end is amortized O(1); inserting/deleting in the middle is O(n)  
  - **Capacity vs Size:**  
    - *Capacity* = length of the internal array  
    - *Size* = number of actual elements  
  - **Initial capacity** – default is 10 (can be specified)  
  - **Growth factor** – typically 1.5× (implementation‑specific; OpenJDK uses 1.5)  
  - **Memory overhead** – small (only the array reference plus capacity)

### LinkedList
- **Underlying structure:** Doubly linked list  
- **Node structure:** Each element is wrapped in a `Node` containing `item`, `prev`, and `next` references  
- **Key features:**  
  - **Sequential access** – getting an element by index is O(n)  
  - Fast insertions/deletions at both ends and in the middle (given a node reference)  
  - Implements `Deque` as well, so it can be used as a queue or stack  
  - **Memory overhead** – higher than `ArrayList` because of extra node pointers

### Vector (Legacy Class)
- **Underlying structure:** Dynamic array (similar to `ArrayList`)  
- **Legacy features:**  
  - Synchronized (thread‑safe) – every method uses `synchronized`  
  - Introduced in JDK 1.0, later retrofitted to implement `List`  
  - **Growth factor** – defaults to 2× (or can be set to a custom increment)  
  - Generally **not recommended** for new code – use `ArrayList` with explicit synchronization or `CopyOnWriteArrayList` if thread safety is needed

### Stack (Legacy Class)
- **Underlying structure:** Extends `Vector` (so it is a synchronized, resizable array)  
- **Key features:**  
  - LIFO (last‑in‑first‑out) stack operations: `push()`, `pop()`, `peek()`  
  - **Legacy** – `Deque` (e.g., `ArrayDeque`) is preferred for stack usage today because:  
    - `ArrayDeque` is faster (not synchronized, no legacy overhead)  
    - `Stack` inherits all `Vector` methods, allowing random access (breaks pure stack abstraction)

#### Keywords Summary

| Keyword / Concept | Meaning |
|-------------------|---------|
| **Dynamic Array** | Array that grows automatically when full |
| **Resizable Array** | Synonym for dynamic array |
| **Random Access** | Direct access to any element by index in O(1) – e.g., `ArrayList` |
| **Sequential Access** | Access that requires traversing elements in order – e.g., `LinkedList` |
| **Index‑based operations** | `get(index)`, `set(index, element)`, `add(index, element)`, `remove(index)` |
| **Capacity vs Size** | Capacity = current allocated array length; Size = number of stored elements |
| **Initial Capacity** | Starting array length (default for `ArrayList` is 10) |
| **Growth Factor** | How much the internal array expands (e.g., 1.5× for `ArrayList`, 2× for `Vector`) |
| **Memory Overhead** | Extra memory beyond storing the elements themselves (array slack, node pointers) |
| **Doubly Linked List** | Each node points to previous and next node |
| **Node structure** | For `LinkedList`: `Node<E> { E item; Node<E> prev; Node<E> next; }` |
| **Legacy classes** | `Vector` and `Stack` – from JDK 1.0/1.2; synchronized, but generally replaced by newer collections |


## Set Implementations in Java

The `Set` interface enforces **uniqueness** – no duplicate elements. Different implementations offer different ordering, performance, and special‑purpose behaviour.

---

#### HashSet
- **Underlying structure:** Hash table (actually a `HashMap` where values are dummy objects)
- **Key features:**
  - **No ordering guarantee** – elements appear in no predictable order (may change over time)
  - **O(1)** average time complexity for `add()`, `remove()`, `contains()`
  - Allows one `null` element
  - **Performance depends on:** initial capacity, load factor, good `hashCode()` distribution

#### LinkedHashSet
- **Underlying structure:** Hash table + doubly linked list (extends `HashSet`)
- **Key features:**
  - **Maintains insertion order** – iterates in the order elements were added
  - Slightly slower than `HashSet` for add/remove (due to linked list overhead)
  - Faster iteration than `HashSet` (because order is known without scanning the entire table)
  - Allows one `null`

#### TreeSet
- **Underlying structure:** Red‑black tree (self‑balancing binary search tree)
- **Key features:**
  - **Stores elements in sorted order** (natural ordering or custom `Comparator`)
  - **O(log n)** for basic operations (`add`, `remove`, `contains`)
  - Does **not** allow `null` (at least for Java 7+; historically null was allowed if comparator handled it)
  - Provides navigation methods: `lower()`, `floor()`, `ceiling()`, `higher()`, `first()`, `last()`, `descendingSet()`

#### EnumSet
- **Underlying structure:** Bit vector (extremely compact, using `long` or `long[]`)
- **Key features:**
  - **Specialised for enum types** – only works with elements of a single `Enum` class
  - **Very fast and memory‑efficient** (bitwise operations)
  - All elements must belong to the same enum type (checked at runtime)
  - **Null not allowed**
  - Maintains elements in the **natural order of enum constants** (declaration order)
  - Factory methods: `EnumSet.allOf()`, `noneOf()`, `of()`, `range()`, `complementOf()`

### Keywords

#### Uniqueness / No duplicates
- A `Set` never contains two elements `e1` and `e2` such that `e1.equals(e2)` is `true`
- Duplicate detection depends on proper `equals()` and `hashCode()` implementations

#### Hashing
- Mechanism to map an object to an integer index (its hash code) used by hash‑based collections (`HashSet`, `LinkedHashSet`)
- `hashCode()` contract: if `equals()` returns `true`, hash codes must be equal

#### Hash Table
- An array of buckets that stores elements based on their hash code
- Used by `HashSet`, `LinkedHashSet`, `HashMap`, `LinkedHashMap`

#### Load Factor
- Measures how full the hash table is before resizing (default = **0.75**)
- **Formula:** `load factor = number of stored elements / current capacity`
- Higher load factor saves memory but increases collisions (worse performance)
- Lower load factor wastes memory but reduces collisions

#### Capacity
- The number of **buckets** in the hash table (not the number of elements)
- Initial capacity can be specified in constructors (default = 16)

#### Hash Collision
- Occurs when two different objects produce the same hash code (modulo capacity)
- Collisions degrade performance because multiple elements land in the same bucket

#### Chaining (Linked List / Tree)
- **Collision resolution technique** used in Java’s hash‑based collections:
  - **Until Java 7:** each bucket is a linked list
  - **Java 8+:** when a bucket becomes too large (≥ 8 entries), the list is converted to a **balanced tree** (red‑black) for faster search (O(log n) instead of O(n))
  - When bucket size shrinks (≤ 6), it converts back to linked list

#### Ordering vs Sorting

| Term | Meaning | Example |
|------|---------|---------|
| **Ordering** | Any predictable sequence of iteration | Insertion order (`LinkedHashSet`), natural enum order (`EnumSet`) |
| **Sorting** | Order defined by element comparison (`Comparable` or `Comparator`) | `TreeSet` (sorted) |

#### Insertion Order
- The order in which elements were added to the collection
- Preserved by `LinkedHashSet` (and `ArrayList`/`LinkedList`)
- Not preserved by `HashSet`

#### Natural Ordering
- The order defined by the `Comparable` interface’s `compareTo()` method
- For numbers: numeric order; for strings: lexicographic order
- Used by `TreeSet` when no explicit `Comparator` is provided

#### Comparator vs Comparable

| Feature | `Comparable` | `Comparator` |
|---------|-------------|--------------|
| **Where defined** | Inside the class (`this` compared to another) | External separate class or lambda |
| **Method** | `int compareTo(T o)` | `int compare(T o1, T o2)` |
| **Single vs multiple** | One natural ordering per class | Many custom orderings possible |
| **Modification** | Cannot change without editing class | Can be passed at runtime |
| **Used by** | `TreeSet`, `Collections.sort()` (without comparator) | `TreeSet(Comparator)`, `Collections.sort(list, comparator)` |

**Example:**
```java
// Comparable (natural ordering)
class Person implements Comparable<Person> {
    public int compareTo(Person other) { return this.age - other.age; }
}

// Comparator (custom ordering)
Comparator<Person> byName = (p1, p2) -> p1.name.compareTo(p2.name);
TreeSet<Person> set = new TreeSet<>(byName);
```

## Map Implementations in Java

The `Map` interface stores **key‑value pairs**. Each key is unique, and each key maps to at most one value. Different implementations offer different ordering, concurrency, performance, and special‑purpose behaviours.

#### HashMap
- **Underlying structure:** Hash table (array of buckets)
- **Key features:**
  - **No ordering guarantee** – iteration order can change over time
  - **O(1)** average time for `put()`, `get()`, `remove()`
  - Allows **one `null` key** and **many `null` values**
  - Not thread‑safe (use `Collections.synchronizedMap()` or `ConcurrentHashMap` for concurrency)

#### LinkedHashMap
- **Underlying structure:** Hash table + doubly linked list (extends `HashMap`)
- **Key features:**
  - **Maintains insertion order** by default (or **access order** if configured)
  - Slightly slower than `HashMap` for put/get due to linked list overhead
  - Faster iteration (order is known)
  - Can be used to build **LRU caches** (see *Access Order vs Insertion Order*)

#### TreeMap
- **Underlying structure:** Red‑black tree (self‑balancing BST)
- **Key features:**
  - **Stores keys in sorted order** (natural ordering or custom `Comparator`)
  - **O(log n)** for `put()`, `get()`, `remove()`
  - **No `null` keys** (throws `NullPointerException` if natural ordering and key is `null`; comparators may allow it, but not recommended)
  - Provides navigation methods: `firstKey()`, `lastKey()`, `lowerKey()`, `floorKey()`, `ceilingKey()`, `higherKey()`, `subMap()`, `headMap()`, `tailMap()`

#### Hashtable (Legacy)
- **Underlying structure:** Hash table (similar to `HashMap`)
- **Key features:**
  - **Synchronized** – thread‑safe (every method is `synchronized`)
  - **Does not allow `null` keys or `null` values** (throws `NullPointerException`)
  - Legacy class from JDK 1.0 – **not recommended** for new code; use `ConcurrentHashMap` for thread safety or `HashMap` otherwise

#### ConcurrentHashMap
- **Underlying structure:** Hash table with **fine‑grained locking** (lock striping) or **CAS** (compare‑and‑swap) operations
- **Key features:**
  - **Thread‑safe** without locking the whole table (supports high concurrency)
  - **No `null` keys or values** (throws `NullPointerException`)
  - **O(1)** average for `put()`, `get()` (with some concurrency overhead)
  - Iterators are **fail‑safe** (do not throw `ConcurrentModificationException`)
  - **Java 8+** improvements: uses treeification for collision buckets, `compute()`, `merge()`, `forEach()` etc.

#### WeakHashMap
- **Underlying structure:** Hash table with **weak references** for keys
- **Key features:**
  - Keys are held via `WeakReference` – when no strong references exist to a key, it becomes eligible for garbage collection and is automatically removed from the map
  - Used for **caches** that should not prevent memory reclamation
  - Allows `null` keys and values
  - Not thread‑safe

#### IdentityHashMap
- **Underlying structure:** Hash table that uses **reference equality (`==`)** instead of `equals()` for keys
- **Key features:**
  - Two keys are considered equal only if `key1 == key2` (same object reference)
  - Uses `System.identityHashCode()` instead of `hashCode()`
  - Useful for **serialization, debugging, or when you need exact object identity**
  - Allows `null` keys (only one, because `null == null`)
  - Not thread‑safe

#### EnumMap
- **Underlying structure:** Array of values indexed by enum ordinal (bit‑like, very compact)
- **Key features:**
  - **Specialised for enum keys** – all keys must belong to the same enum type
  - **Extremely fast and memory‑efficient** (array access by ordinal)
  - Maintains **natural order of enum constants** (declaration order)
  - **No `null` keys** (throws `NullPointerException`); allows `null` values
  - Factory creation: `new EnumMap(EnumClass.class)`

### Keywords

#### Key‑Value pairs
- Fundamental unit of a `Map`: each key is associated with exactly one value
- Keys must be unique; values can be duplicated

#### Entry (Map.Entry)
- Inner interface of `Map` representing a single key‑value pair
- Methods: `getKey()`, `getValue()`, `setValue()`
- Accessible via `entrySet()`: `Set<Map.Entry<K,V>>`

#### Hash Bucket
- A slot in the hash table array that stores one or more entries (via chaining)
- Index is computed as `hashCode(key) & (capacity - 1)` (when capacity is power of two)

#### Hash Collision Resolution
- Technique to handle multiple keys hashing to the same bucket
- **Java uses chaining:** each bucket contains a linked list (or tree) of entries
- Alternative methods: open addressing (not used in `HashMap`)

#### Rehashing
- Process of **resizing** the hash table (increasing capacity) and re‑inserting all entries into new buckets
- Triggered when `size > load factor × capacity`
- Costly operation – O(n) time, but amortised O(1) over many insertions

#### Load Factor (default 0.75)
- **0.75** – balances memory usage and performance
- Lower factor (e.g., 0.5) → fewer collisions, more memory waste
- Higher factor (e.g., 0.9) → more collisions, less memory

#### Capacity (power of 2)
- Number of buckets; for `HashMap`/`ConcurrentHashMap`/`LinkedHashMap`, capacity is always a **power of two** (e.g., 16, 32, 64…)
- Allows fast modulo via bitwise AND: `hash & (capacity - 1)`
- `Hashtable` does **not** enforce power‑of‑two (uses `int` index directly)

#### Treeification (Java 8+)
- When a single bucket’s linked list length exceeds a threshold (default **8**), the list is converted to a **balanced tree** (red‑black tree)
- Improves worst‑case performance from O(n) to O(log n) for that bucket
- Reverts to linked list when the bucket size drops below **6**

#### Red‑Black Tree
- A self‑balancing binary search tree used by `TreeMap` and for treeified buckets in `HashMap`
- Guarantees O(log n) for insertion, deletion, lookup
- Properties: root is black, red nodes have black children, all paths from root to leaves have same number of black nodes

#### Access Order vs Insertion Order

| Order Type | Meaning | Used by |
|------------|---------|---------|
| **Insertion Order** | Elements iterated in the order they were added | `LinkedHashMap` (default) |
| **Access Order** | Elements ordered from least‑recently accessed to most‑recently accessed | `LinkedHashMap` with `accessOrder=true`; used for LRU caches |

#### LRU Cache
- **Least Recently Used** cache – evicts the oldest accessed entry when capacity is exceeded
- Implemented by extending `LinkedHashMap` and overriding `removeEldestEntry()`

#### Null Keys / Values rules

| Implementation | Null Keys | Null Values |
|----------------|-----------|-------------|
| `HashMap` | 1 allowed | many allowed |
| `LinkedHashMap` | 1 allowed | many allowed |
| `TreeMap` | ❌ (unless comparator handles it) | allowed (if key not null) |
| `Hashtable` | ❌ | ❌ |
| `ConcurrentHashMap` | ❌ | ❌ |
| `WeakHashMap` | 1 allowed | many allowed |
| `IdentityHashMap` | 1 allowed (null == null) | many allowed |
| `EnumMap` | ❌ | allowed |

> **Note:** For `TreeMap`, a `Comparator` can be written to allow `null` keys, but it is not the default behaviour and can lead to inconsistencies.

## Queue & Deque Implementations in Java

The `Queue` interface represents a collection designed for **holding elements prior to processing** (typically FIFO). The `Deque` (Double‑Ended Queue) extends `Queue` to support insertion/removal at **both ends**. Java provides several implementations, including general‑purpose, special‑purpose, and **blocking** queues for concurrent programming.

---

#### PriorityQueue
- **Underlying structure:** Binary **heap** (array‑based)
- **Key features:**
  - **Priority ordering** – elements are ordered by their natural ordering or a `Comparator`
  - **Head** is the smallest element (min‑heap by default)
  - **No `null`** elements (throws `NullPointerException`)
  - **Unbounded** – grows dynamically
  - **Not thread‑safe** (use `PriorityBlockingQueue` for concurrency)
  - Iteration order is **not** the priority order; use `poll()` repeatedly to get sorted order

#### ArrayDeque
- **Underlying structure:** **Circular array** (resizable)
- **Key features:**
  - Implements `Deque` – can be used as **stack (LIFO)** or **queue (FIFO)**
  - **No capacity restrictions** – grows as needed
  - **Faster** than `LinkedList` for most scenarios (better cache locality, less memory overhead)
  - **No `null` elements** (throws `NullPointerException`)
  - Not thread‑safe

#### LinkedList (as Queue/Deque)
- **Underlying structure:** Doubly linked list
- **Key features:**
  - Implements both `List` and `Deque` – can be used as queue, deque, or list
  - Allows **`null`** elements
  - **Higher memory overhead** (node objects with prev/next pointers)
  - Slower than `ArrayDeque` for general queue/deque operations
  - Not thread‑safe

---

#### Blocking Queues

Blocking queues are designed for **producer‑consumer** scenarios. They support operations that wait (block) until the queue becomes non‑empty (when retrieving) or has space available (when inserting).

##### ArrayBlockingQueue
- **Underlying structure:** Fixed‑size **circular array**
- **Key features:**
  - **Bounded** – capacity is fixed at creation
  - **Fairness policy** – optional (if `true`, threads are granted access in FIFO order)
  - Supports optional **time‑out** methods (`offer(e, time, unit)`, `poll(time, unit)`)
  - One lock for both put and take (can be less scalable than `LinkedBlockingQueue`)

##### LinkedBlockingQueue
- **Underlying structure:** Singly linked list of nodes
- **Key features:**
  - **Optionally bounded** (default capacity = `Integer.MAX_VALUE`)
  - Two separate locks (one for put, one for take) – higher throughput than `ArrayBlockingQueue` under contention
  - Allows `null`? **No** – `null` is not permitted (reserved for failure indication)

##### PriorityBlockingQueue
- **Underlying structure:** Binary heap (like `PriorityQueue`) + blocking behaviour
- **Key features:**
  - **Unbounded** – can grow until memory exhaustion
  - Elements are ordered by priority (natural or `Comparator`)
  - **No `null`** allowed
  - Uses `ReentrantLock` internally

##### DelayQueue
- **Underlying structure:** Uses a `PriorityQueue` internally
- **Key features:**
  - Contains only elements that implement `Delayed` interface
  - An element can be taken **only when its delay has expired** (`getDelay(TimeUnit.NANOSECONDS) <= 0`)
  - **Unbounded**
  - Useful for **scheduled task execution** or **time‑based caching**

##### SynchronousQueue
- **Underlying structure:** No internal storage – **each insert must wait for a matching remove** (and vice versa)
- **Key features:**
  - **Capacity = 0** – it is a handoff mechanism
  - Ideal for **direct hand‑off** between threads (e.g., `ExecutorService` with `newCachedThreadPool()`)
  - Supports **fairness** mode (using a queue) or non‑fair (stack‑based)
  - `put()` blocks until another thread calls `take()`; `offer()` fails immediately if no waiting consumer

### Keywords

#### FIFO / LIFO
- **FIFO (First‑In‑First‑Out):** Standard queue behaviour – elements are removed in the order they were added. Example: `ArrayDeque` used as queue.
- **LIFO (Last‑In‑First‑Out):** Stack behaviour – last element added is the first removed. `Deque` with `push()`/`pop()` (e.g., `ArrayDeque` as stack).

#### Heap (Min Heap / Max Heap)
- A binary tree‑based data structure where the parent node is **smaller** (min‑heap) or **larger** (max‑heap) than its children.
- **`PriorityQueue`** uses a **min‑heap** by default (smallest element at head).
- A max‑heap can be achieved with a `Comparator.reverseOrder()`.

#### Priority Ordering
- Elements are ordered not by insertion time but by their **priority** (natural order or custom `Comparator`).
- The **head** of the queue is the element with the **highest priority** (lowest value for min‑heap).

#### Comparator‑based ordering
- Priority can be defined by passing a `Comparator` to the `PriorityQueue` (or `PriorityBlockingQueue`) constructor.
- Example: `new PriorityQueue<>((a, b) -> b - a)` for max‑heap.

#### Double‑ended queue (Deque)
- Supports insertion/removal at **both ends**.
- Methods: `addFirst()`, `addLast()`, `removeFirst()`, `removeLast()`, `offerFirst()`, `offerLast()`, `pollFirst()`, `pollLast()`, `getFirst()`, `getLast()`.

#### Circular Array
- An array used with head and tail pointers that wrap around when reaching the end.
- Used by `ArrayDeque` and `ArrayBlockingQueue` to efficiently use memory and avoid shifting elements.

#### Bounded vs Unbounded Queue

| Type | Meaning | Examples |
|------|---------|----------|
| **Bounded** | Has a fixed maximum capacity | `ArrayBlockingQueue`, `LinkedBlockingQueue` (if capacity specified) |
| **Unbounded** | Can grow dynamically (limited only by memory) | `PriorityQueue`, `LinkedBlockingQueue` (default), `DelayQueue`, `PriorityBlockingQueue` |

> **Note:** For unbounded blocking queues, `put()` never blocks because there is always “room” (theoretical capacity is `Integer.MAX_VALUE`). However, memory exhaustion is still possible.

### Summary Table of Queue/Deque Implementations

| Implementation | Deque | Bounded | Blocking | Null Allowed | Thread‑safe | Ordering |
|----------------|-------|---------|----------|--------------|-------------|----------|
| `PriorityQueue` | ❌ | ❌ (unbounded) | ❌ | ❌ | ❌ | Priority |
| `ArrayDeque` | ✅ | ❌ | ❌ | ❌ | ❌ | FIFO/LIFO |
| `LinkedList` | ✅ | ❌ | ❌ | ✅ | ❌ | FIFO/LIFO |
| `ArrayBlockingQueue` | ❌ | ✅ (fixed) | ✅ | ❌ | ✅ | FIFO |
| `LinkedBlockingQueue` | ❌ | ✅ (optionally) | ✅ | ❌ | ✅ | FIFO |
| `PriorityBlockingQueue` | ❌ | ❌ | ✅ | ❌ | ✅ | Priority |
| `DelayQueue` | ❌ | ❌ | ✅ | ❌ (requires `Delayed`) | ✅ | Delay expiry |
| `SynchronousQueue` | ❌ | ✅ (capacity 0) | ✅ | ❌ | ✅ | Handoff |


## Iteration Mechanisms in Java Collections Framework

Java provides multiple ways to traverse collections, each with different capabilities, safety guarantees, and use cases.

---

#### Iterator
- **Introduced in:** Java 2 (JDK 1.2) as part of the Collections Framework
- **Interface:** `java.util.Iterator<E>`
- **Core methods:**
  - `boolean hasNext()` – returns `true` if more elements exist
  - `E next()` – returns the next element (throws `NoSuchElementException` if none)
  - `void remove()` – **optional** operation; removes the last element returned by `next()`
- **Direction:** Forward‑only
- **Fail‑fast:** Most implementations throw `ConcurrentModificationException` if collection is structurally modified after iterator creation (except via the iterator’s own `remove()`)

#### ListIterator
- **Extends** `Iterator<E>`
- **Additional capabilities:**
  - **Bidirectional iteration** – `hasPrevious()`, `previous()`
  - **Index access** – `nextIndex()`, `previousIndex()`
  - **Element modification** – `set(E e)`, `add(E e)`
- **Availability:** Only for `List` implementations (including `ArrayList`, `LinkedList`, `Vector`)
- **Positioning:** Can start at any index using `listIterator(int index)`

#### Enumeration (legacy)
- **Introduced in:** JDK 1.0 (before the Collections Framework)
- **Interface:** `java.util.Enumeration<E>`
- **Methods:** `hasMoreElements()`, `nextElement()`
- **Legacy use cases:** `Vector`, `Hashtable`, `Stack` (older code)
- **Limitations:** No `remove()` method; no fail‑fast guarantee; not extendable
- **Modern alternative:** `Iterator`

#### for‑each loop (enhanced for loop)
- **Introduced in:** Java 5
- **Syntax:** `for (ElementType e : iterable) { ... }`
- **Works on:** Any `Iterable` (all `Collection` subinterfaces) and arrays
- **Under the hood:** Compiler translates it into an `Iterator` loop (for collections)
- **Limitations:**
  - Cannot remove elements directly (no access to iterator’s `remove()`)
  - Cannot modify the collection structurally during iteration (risk of `ConcurrentModificationException`)
  - Cannot access the current index

#### Spliterator
- **Introduced in:** Java 8
- **Interface:** `java.util.Spliterator<T>`
- **Purpose:** Designed for **parallel traversal** of elements (used internally by the Stream API)
- **Key characteristics:**
  - Can split itself (`trySplit()`) for parallel processing
  - Provides characteristics (e.g., `ORDERED`, `DISTINCT`, `SIZED`, `SORTED`, `CONCURRENT`, `IMMUTABLE`)
  - Methods: `tryAdvance()`, `forEachRemaining()`, `estimateSize()`, `getExactSizeIfKnown()`
- **Use directly?** Rarely – used indirectly via streams or `Collection.spliterator()`

#### Stream API iteration
- **Introduced in:** Java 8
- **Types:** `Stream<T>` (sequential) and `parallelStream()` (parallel)
- **Terminal operations for iteration:**
  - `forEach(Consumer)` – may execute in any order for parallel streams
  - `forEachOrdered(Consumer)` – preserves encounter order
  - `collect()`, `toArray()`, `reduce()`, etc.
- **Characteristics:**
  - **Internal iteration** – you provide the action, the framework controls the loop
  - **Lazy evaluation** – intermediate operations are not executed until a terminal operation is invoked
  - **Pipelining** – chain operations without creating intermediate collections
  - **Parallelism** – easy to parallelise via `parallelStream()`
- **Example:** `list.stream().filter(x -> x > 0).map(...).forEach(System.out::println)`

### Keywords

#### Fail‑fast behavior
- Iterators that throw `ConcurrentModificationException` when they detect that the collection has been structurally modified (outside the iterator’s own `remove()`) during iteration.
- Implemented by maintaining a **modCount** (modification counter) in the collection and checking it against an expected value stored in the iterator.
- Applies to all non‑concurrent collections in `java.util` (e.g., `ArrayList`, `HashSet`, `HashMap` key sets).

#### ConcurrentModificationException
- A `RuntimeException` thrown by fail‑fast iterators when concurrent modification is detected.
- Can occur in **single‑threaded** code (e.g., removing an element directly from a list while iterating over it with for‑each) and **multi‑threaded** code (modifying a shared collection without proper synchronisation).

#### remove() safe operation
- The **only safe way** to remove an element from a collection while iterating is to use the iterator’s own `remove()` method.
- Example:
  ```java
  Iterator<String> it = list.iterator();
  while (it.hasNext()) {
      if (condition) it.remove(); // safe
  }
  ```
- Using `list.remove(index)` or `list.remove(element)` inside a for‑each loop throws `ConcurrentModificationException`.

#### Bidirectional iteration
- The ability to traverse a collection **both forward and backward**.
- Provided by `ListIterator`.
- Allows `next()` and `previous()` interleaved, as well as moving by index.

#### Lazy iteration
- Elements are computed or fetched **on‑demand**, not all at once.
- Stream API intermediate operations (e.g., `filter`, `map`) are **lazy** – they do nothing until a terminal operation (e.g., `forEach`, `collect`) is invoked.
- Allows infinite streams (`Stream.iterate()`, `Stream.generate()`) combined with short‑circuiting (`limit()`, `findFirst()`).

#### Parallel iteration
- Processing elements **simultaneously** across multiple CPU cores.
- Achieved via:
  - `parallelStream()` – splits the source using `Spliterator`
  - `Spliterator.trySplit()` – recursively splits the data for work‑stealing
- **Caution:** Not always faster; overhead of splitting and combining can outweigh benefits for small collections or simple operations. Must be thread‑safe (no shared mutable state).

### Comparison Table

| Mechanism | Bidirectional | Modification | Fail‑fast | Parallel | Lazy | Works on |
|-----------|---------------|--------------|-----------|----------|------|----------|
| `Iterator` | ❌ | `remove()` only | ✅ | ❌ | ❌ | All `Collection` |
| `ListIterator` | ✅ | `add()`, `set()`, `remove()` | ✅ | ❌ | ❌ | `List` only |
| `Enumeration` | ❌ | ❌ | ❌ (legacy) | ❌ | ❌ | `Vector`, `Hashtable`, `Stack` |
| for‑each loop | ❌ | ❌ | ✅ | ❌ | ❌ | `Iterable` + arrays |
| `Spliterator` | ❌ | ❌ | depends | ✅ | ❌ | Any `Collection` |
| Stream API | ❌ | ❌ (immutable) | depends (for non‑concurrent sources) | ✅ | ✅ | Any `Collection`, arrays, generators |

> **Note:** Stream API does not modify the source; if you need to modify, use `Iterator` or collect into a new collection.

