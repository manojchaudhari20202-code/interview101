
# Java Complete Interview Reference — Full Edition

> **All topics merged:** Original source file (Java Concurrency · Java Collections · Java IO/NIO) + all remaining Java topics
> Every section includes subtopics, keywords, and interview notes.

---

## TABLE OF CONTENTS

### Java Core
- 1. Java OOP (Object-Oriented Programming)
- 2. Java Generics
- 3. Java Exception Handling
- 4. Java Strings
- 5. Java Primitives, Wrappers & Type System
- 6. Java Arrays
- 7. Java Operators & Control Flow
- 8. Java Functional Programming & Streams
- 9. Java Memory Management & JVM
- 10. Java Design Patterns
- 11. Java Annotations & Reflection
- 12. Java Modules (JPMS)
- 13. Java Version Features (Java 5–26) ← EXPANDED
- 14. Java Records
- 15. Java Sealed Classes
- 16. Java Pattern Matching
- 17. Java Switch Expressions
- 18. Java `var` & Type Inference
- 19. Java Date & Time API
- 20. Java Regex
- 21. Java Networking
- 22. Java JDBC
- 23. Java Security
- 24. Java Logging
- 25. Java XML & JSON Processing
- 26. Java Testing
- 27. Java Build Tools
- 28. Java Enum
- 29. Java Concurrency (full)
- 30. Java Collections (full)
- 31. Java IO & NIO (full)
- 32. Java Internals & Advanced Topics
- 33. Java Interview Master Keywords

### Data Structures & Algorithms
- 34. Core DSA Concepts
- 35. Arrays & Strings
- 36. Linked Lists
- 37. Stack
- 38. Queue & Deque
- 39. Trees
- 40. Graphs
- 41. Searching Algorithms
- 42. Sorting Algorithms
- 43. Recursion & Backtracking
- 44. Dynamic Programming (DP)
- 45. Greedy Algorithms
- 46. Bit Manipulation
- 47. Mathematics & Number Theory
- 48. Advanced Data Structures
- 49. Advanced Algorithms
- 50. Patterns & Problem-Solving Techniques
- 51. Java-Specific DSA
- 52. Pitfalls, Edge Cases & Testing
- 53. Competitive Programming Essentials
- 54. Real-World System Mapping

### Design & Architecture
- 55. Object-Oriented Design (OOD)
- 56. Static Analysis & Code Quality
- 57. Engineering Principles
- 58. Design Patterns (Comprehensive)
- 59. System Design
- 60. Domain-Driven Design (DDD)
- 61. Microservices Architecture

### Frameworks & Infrastructure
- 62. Spring Framework & Spring Boot
- 63. Apache Kafka
- 64. Databases
- 65. Enterprise Architecture
- 66. Event-Driven Architecture (EDA)
- 67. Stream Processing
- 68. Reactive Programming
- 69. Messaging Systems (RabbitMQ & Beyond)
- 70. Observability & Monitoring

### Engineering & Design Principles (Master Reference)
- 71. Engineering Principles Master Reference (NEW)

### Database (Master Reference)
- 72. Database Master Reference (NEW)

### Assorted Patterns (Master Reference)
- 73. Assorted Patterns Master Reference (NEW)

---

## 1. Java OOP (Object-Oriented Programming)

### Core OOP Principles
- **Encapsulation** → Bundling data + behavior into a class; hide internals via access modifiers.
- **Abstraction** → Expose only relevant details; hide complexity via abstract classes/interfaces.
- **Inheritance** → Child inherits state/behavior from parent (`extends`). Promotes reuse.
- **Polymorphism** → One interface, many implementations. Compile-time (overloading) + Runtime (overriding).
- **Keywords**: IS-A vs HAS-A; code reuse vs tight coupling tradeoff; Liskov Substitution Principle (LSP).

### Classes & Objects
- **Class** → Blueprint/template. **Object** → Instance; lives on heap.
- **Constructor** → Initializes object; same name, no return type. Default provided if none defined.
- **Copy Constructor** → Creates object from another (must be written manually in Java).
- **this** → Current object ref; chain constructors with `this()` (must be first statement).
- **super** → Parent class ref; `super()` chains to parent constructor (must be first statement).
- **static** → Class-level; shared; static methods can't access instance members directly.
- **final** → Variable (constant), method (no override), class (no subclass).
- **Keywords**: Initialization order: static blocks → instance blocks → constructor (parent first).

### Inheritance
- Single (one parent), Multilevel (A→B→C), Hierarchical (multiple children from one parent).
- **Multiple via Interface** → A class can implement multiple interfaces.
- **Diamond Problem** → Resolved: class implementation wins over interface default methods.
- **Method Overriding** → Same signature in subclass; `@Override` recommended.
- **Covariant Return Type** → Override can return subtype of parent's return type.
- **Keywords**: Can't override `private`/`static`; `final` prevents inheritance/override.

### Polymorphism
- **Compile-time** → Overloading; resolved by parameter signature (not return type).
- **Runtime** → Overriding; JVM calls most specific method via vtable dispatch.
- **Upcasting** → `Animal a = new Dog()` — implicit, safe. **Downcasting** → `(Dog) a` — needs `instanceof` check.
- **Keywords**: Overloading resolution: widening > autoboxing > varargs; return type alone can't overload.

### Abstraction
- **Abstract Class** → Cannot instantiate; abstract + concrete methods; can have state; single inheritance.
- **Interface** → Contract; multiple implementation; fields implicitly `public static final`.
- **Default Methods (Java 8)** → Method body in interface; backward compatibility.
- **Static Interface Methods (Java 8)** → Utility; not inherited by implementations.
- **Private Interface Methods (Java 9)** → Code sharing between default methods.
- **Functional Interface** → Exactly one abstract method; target for lambdas; `@FunctionalInterface`.
- **Keywords**: Interface = capability/contract; Abstract class = shared partial implementation.

### Encapsulation
- Private fields + controlled getters/setters. Validation logic in setters.
- **Immutable Class** → All fields `private final`; no setters; defensive copy in constructor/getters.
- **JavaBeans** → `getX()`, `setX()`, `isX()` for booleans.
- **Keywords**: Encapsulation != immutability; access modifier ladder: private → default → protected → public.

### Access Modifiers

| Modifier | Same Class | Same Package | Subclass (diff pkg) | Everywhere |
|---|---|---|---|---|
| `private` | Yes | No | No | No |
| default | Yes | Yes | No | No |
| `protected` | Yes | Yes | Yes | No |
| `public` | Yes | Yes | Yes | Yes |

### Interfaces vs Abstract Classes

| Aspect | Interface | Abstract Class |
|---|---|---|
| Multiple Inheritance | Yes | No |
| State (fields) | `public static final` only | Yes |
| Constructor | No | Yes |
| Default methods | Yes (Java 8+) | Yes |
| Use when | Contract/capability | Shared base behavior |

### Object Class Methods
- `equals()` + `hashCode()` (always override together), `toString()`, `clone()` (Cloneable; shallow).
- `finalize()` → deprecated Java 9; use `Cleaner`. `getClass()` → runtime Class object.
- `wait()` / `notify()` / `notifyAll()` → monitor-based thread coordination; must hold monitor.

### Inner Classes
- **Static Nested** → No outer instance; `Outer.Inner`; no implicit outer ref.
- **Non-static Inner** → Tied to outer; accesses outer private members; holds outer ref (memory leak risk).
- **Local** → Inside method; accesses effectively final locals.
- **Anonymous** → Nameless; inline; replaced by lambda for SAM interfaces.

### SOLID Principles
- **S** → Single Responsibility: one reason to change.
- **O** → Open/Closed: extend, don't modify.
- **L** → Liskov Substitution: subtypes substitutable for base.
- **I** → Interface Segregation: small focused interfaces.
- **D** → Dependency Inversion: depend on abstractions; inject dependencies.

---

## 2. Java Generics

### Core Concepts
- Type-safe parameterized classes/methods; `ClassCastException` avoided; compile-time checking.
- **Type Erasure** → Generic type info erased at runtime; bytecode uses `Object` or bound type.
- **Raw Type** → Generic class without parameter (legacy; avoid; unchecked warnings).
- **Keywords**: Generics only at compile time; cannot use primitives (`List<int>` illegal → use `List<Integer>`).

### Generic Classes & Methods
- `class Box<T> { T value; }`, `<T> T identity(T t)` (method), `interface Comparable<T>`.
- **Bounded** → `<T extends Number>` upper bound; `<T extends Comparable<T> & Serializable>` multiple.
- **Keywords**: Java 7 diamond `<>`; cannot create `new T[]`; use `(T[]) new Object[n]`.

### Wildcards & PECS
- `<?>` → unbounded; read-only effectively.
- `<? extends T>` → upper bound; Producer (reading from collection).
- `<? super T>` → lower bound; Consumer (writing to collection).
- **PECS** → **Producer Extends, Consumer Super** — key interview rule.
- **Keywords**: `List<?>` accepts any List; `List<Object>` only accepts `List<Object>`.

### Type Erasure Details
- **Bridge Methods** → Compiler generates to maintain polymorphism after erasure.
- **Reification** → Arrays ARE reified (type known at runtime); generics are NOT.
- **Heap Pollution** → Mixing raw + generic types; `ClassCastException` at unexpected places.
- **Keywords**: Cannot: `instanceof List<String>`, `new T()`, `catch(T e)`, `new T[]`.

---

## 3. Java Exception Handling

### Exception Hierarchy
```
Throwable
├── Error (unrecoverable: OutOfMemoryError, StackOverflowError)
└── Exception
    ├── Checked (IOException, SQLException — must handle/declare)
    └── RuntimeException (NullPointerException, IllegalArgumentException — unchecked)
```

### try-catch-finally
- Catch most-specific first. `finally` always runs (not on `System.exit()`).
- **Multi-catch** (Java 7) → `catch (IOException | SQLException e)` — types must be unrelated.
- **try-with-resources** (Java 7) → auto-closes `AutoCloseable`; multiple resources closed in reverse order.
- **Keywords**: `finally` runs before `return`; exception in `finally` overrides original.

### throw, throws, Chaining
- `throw new IAE("msg")` → explicit throw; `throws` → declare checked on method signature.
- **Exception chaining** → `new RuntimeException("context", cause)` — preserves root cause.
- **Keywords**: Wrap checked in unchecked common in frameworks (Spring `DataAccessException`).

### Custom Exceptions & Best Practices
- `extends Exception` (checked) or `extends RuntimeException` (unchecked).
- Include `message` + `cause`; add `serialVersionUID`.
- Catch specific; don't swallow; don't use for flow control (stack trace expensive).
- Log OR throw; avoid both (double logging).

---

## 4. Java Strings

### Fundamentals
- **Immutable** → All ops return new String; backed by `byte[]` (Java 9+ compact strings: LATIN-1 or UTF-16).
- **String Pool** → Literals cached in heap; `"a" == "a"` true. `intern()` → add to pool manually.
- `new String("abc")` → bypasses pool; creates new heap object.
- **Keywords**: `==` = reference; `.equals()` = content; thread-safe due to immutability.

### Key Methods
- `charAt`, `length`, `substring(start, end)`, `indexOf`, `contains`, `startsWith`, `endsWith`.
- `toUpperCase`, `toLowerCase`, `trim()` (ASCII WS), `strip()` (Java 11, Unicode WS).
- `split`, `replace`, `replaceAll(regex)`, `matches(regex)`.
- `isEmpty`, `isBlank()` (Java 11), `repeat(n)` (Java 11), `lines()` (Java 11).
- `String.format`, `String.valueOf`, `String.join(delim, parts)`.
- `chars()` → IntStream of char values.

### StringBuilder & StringBuffer
- **StringBuilder** → Mutable, not thread-safe; preferred. **StringBuffer** → synchronized, slower.
- `append`, `insert`, `delete`, `replace`, `reverse`, `toString`. Capacity starts at 16; doubles.
- **Keywords**: Use StringBuilder in loops; `+` in loop may not be optimized by compiler.

### Modern Features
- Java 11: `isBlank()`, `strip()`, `stripLeading/Trailing()`, `lines()`, `repeat(n)`.
- Java 12: `indent(n)`, `transform(fn)`. Java 15: **Text Blocks** stable (`"""..."""`).
- Java 21: String Templates preview (`STR."Hello \{name}"`).

---

## 5. Java Primitives, Wrappers & Type System

### Primitive Types

| Type | Size | Default | Range |
|---|---|---|---|
| byte | 8-bit | 0 | -128 to 127 |
| short | 16-bit | 0 | -32,768 to 32,767 |
| int | 32-bit | 0 | ±2.1 billion |
| long | 64-bit | 0L | ±9.2×10^18 |
| float | 32-bit | 0.0f | ~7 decimal digits |
| double | 64-bit | 0.0 | ~15 decimal digits |
| char | 16-bit | '\u0000' | 0–65,535 Unicode |
| boolean | JVM-dep | false | true/false |

### Wrapper Classes & Autoboxing
- `Integer`, `Long`, `Double`, `Float`, `Short`, `Byte`, `Character`, `Boolean`.
- **Autoboxing** → `Integer i = 42;` (auto-wrap). **Unboxing** → `int n = i;` (auto-unwrap).
- **Integer Cache** → -128 to 127 cached; `==` may be true in range. Outside range: always use `.equals()`.
- **Keywords**: Unboxing null → NPE; autoboxing in loops = performance overhead; `Integer.compare(a,b)` not `a-b`.

### BigInteger & BigDecimal
- `BigInteger` → arbitrary precision integers. `BigDecimal` → arbitrary precision decimals; use for money.
- `BigDecimal.valueOf(d)` preferred over `new BigDecimal(d)` (avoids floating-point artifacts).
- **Keywords**: Never use `float`/`double` for currency; `double` can't represent 0.1 exactly.

### Type Casting
- **Widening** → `int → long → float → double`; implicit; safe.
- **Narrowing** → `double → int`; explicit `(int)`; possible data loss.
- **Numeric promotion** → `byte + byte → int`; char ↔ int: `(char) 65` = 'A'.

---

## 6. Java Arrays

### Basics
- Fixed-size contiguous memory; `arr.length` (field not method); default: 0/false/null.
- Multi-dimensional: `int[][] grid = new int[3][4]`; jagged rows allowed.
- **Covariance** → `String[] s = ...; Object[] o = s;` → `ArrayStoreException` at runtime on wrong-type write.

### Arrays Utility Class
- `Arrays.sort(arr)` → quicksort (primitives), TimSort (objects; stable).
- `Arrays.binarySearch(arr, key)` → O(log n); must be pre-sorted.
- `Arrays.fill`, `Arrays.copyOf(arr, newLen)`, `Arrays.copyOfRange(arr, from, to)`.
- `Arrays.equals(a,b)`, `Arrays.deepEquals(a,b)` (multi-dim).
- `Arrays.toString(arr)`, `Arrays.stream(arr)`, `Arrays.asList(arr)` (fixed-size List backed by array).

### Array vs ArrayList

| | Array | ArrayList |
|---|---|---|
| Size | Fixed | Dynamic |
| Primitives | Yes | No (boxed) |
| Generics | No (covariant) | Yes |
| Utility | Arrays class | Collections class |

---

## 7. Java Operators & Control Flow

### Operators
- **Arithmetic**: `+`, `-`, `*`, `/`, `%`; integer division truncates; `%` can be negative.
- **Relational**: `==` (reference for objects!), `!=`, `<`, `>`, `<=`, `>=`.
- **Logical**: `&&` (short-circuit AND), `||` (short-circuit OR), `!`. `&`/`|` = no short-circuit.
- **Bitwise**: `&`, `|`, `^`, `~`, `<<`, `>>` (signed), `>>>` (unsigned).
- **Ternary**: `condition ? a : b`. **instanceof**: `obj instanceof Type`; Java 16+ pattern form.
- **Keywords**: Integer overflow wraps silently; `Math.addExact()` for overflow detection.

### Operator Precedence (High→Low, Key Levels)
Postfix `i++` → Unary `++i -i !` → Multiplicative `* / %` → Additive `+ -` → Shift `<< >> >>>` → Relational `< > instanceof` → Equality `== !=` → Bitwise `& ^ |` → Logical `&& ||` → Ternary `?:` → Assignment `=`

### Control Flow
- `if/else if/else`, `switch` (classic: fall-through + break; expression: arrow, no fall-through).
- `for (init; cond; update)`, `for (Type x : collection)` (enhanced; uses Iterator internally).
- `while`, `do-while` (at least once).
- `break [label]`, `continue [label]` → `outerLoop: for(...){ for(...){ break outerLoop; } }`.

---

## 8. Java Functional Programming & Streams

### Lambda Expressions
- `(params) -> expr` or `(params) -> { statements; }`. Target type = functional interface.
- **Variable Capture** → effectively final locals only; lambda may outlive stack frame.
- **Method References** → static `Math::abs`, bound instance `str::toUpperCase`, unbound `String::toUpperCase`, constructor `ArrayList::new`.

### Built-in Functional Interfaces (java.util.function)

| Interface | Signature | Use |
|---|---|---|
| `Function<T,R>` | `R apply(T)` | Transform |
| `BiFunction<T,U,R>` | `R apply(T,U)` | Two inputs |
| `Predicate<T>` | `boolean test(T)` | Filter |
| `Consumer<T>` | `void accept(T)` | Side-effect |
| `Supplier<T>` | `T get()` | Produce |
| `UnaryOperator<T>` | `T apply(T)` | T→T |
| `BinaryOperator<T>` | `T apply(T,T)` | (T,T)→T |

- **Composition** → `f.andThen(g)`, `f.compose(g)`, `Predicate.and/or/negate()`, `Consumer.andThen()`.
- **Primitive variants** → `IntFunction`, `ToIntFunction`, `IntPredicate`, etc. (avoid boxing overhead).

### Stream API

#### Creation
- `collection.stream()`, `Arrays.stream(arr)`, `Stream.of(...)`.
- `Stream.generate(Supplier)` (infinite), `Stream.iterate(seed, fn)` (infinite), `Stream.iterate(seed, hasNext, fn)` Java 9.
- `IntStream.range(0,10)` [0,10), `IntStream.rangeClosed(1,10)` [1,10]. `Files.lines(path)`.

#### Intermediate (Lazy — only run when terminal is called)
- `filter(Predicate)`, `map(Function)`, `flatMap(fn→Stream)`, `distinct()`, `sorted([Comparator])`.
- `peek(Consumer)`, `limit(n)`, `skip(n)`, `mapToInt/Long/Double()`.
- `takeWhile(Predicate)`, `dropWhile(Predicate)` (Java 9).

#### Terminal (Eager — trigger pipeline execution)
- `collect(Collector)`, `forEach`, `forEachOrdered`, `reduce(identity, BinaryOp)`.
- `count()`, `findFirst()`, `findAny()` → Optional.
- `anyMatch`, `allMatch`, `noneMatch` → short-circuit boolean.
- `min(Comparator)`, `max(Comparator)` → Optional. `toArray()`, `toList()` (Java 16).

#### Collectors
- `toList()`, `toSet()`, `toUnmodifiableList()` (Java 10).
- `toMap(keyFn, valFn [, mergeFunction])` → throws on dup key without merge.
- `groupingBy(classifier)` → `Map<K,List<V>>`; `groupingBy(k, downstream)`.
- `partitioningBy(Predicate)` → `Map<Boolean,List>`.
- `joining(delim, prefix, suffix)`, `counting()`, `summingInt()`, `averagingInt()`.
- `teeing(c1, c2, merger)` (Java 12) → apply two collectors, merge results.

### Optional
- `Optional.of(val)` (non-null), `ofNullable(val)`, `empty()`.
- `orElse(default)`, `orElseGet(Supplier)` (lazy!), `orElseThrow()`.
- `map(fn)`, `flatMap(fn)`, `filter(pred)`.
- `ifPresent(Consumer)`, `ifPresentOrElse(c, emptyAction)` (Java 9), `stream()` (Java 9).
- **Keywords**: `orElse(x)` always evaluates x; `orElseGet` is lazy — prefer for expensive defaults. Only use as return type.

### Comparator & Comparable
- `Comparable<T>` → natural ordering in class; `compareTo` returns negative/0/positive.
- `Comparator<T>` → external; `Comparator.comparing(fn).thenComparing(fn).reversed()`.
- `nullsFirst/nullsLast`, `naturalOrder()`, `reverseOrder()`.
- **Keywords**: `Integer.compare(a,b)` not `a-b` (overflow risk); used by TreeMap, PriorityQueue, sort.

---

## 9. Java Memory Management & JVM

### JVM Architecture
- **JVM** → Executes bytecode; platform-independent. JDK = JRE + tools; JRE = JVM + libraries.
- **ClassLoader** → Bootstrap (core JDK) → Extension/Platform → Application. Parent-first delegation.
- **Keywords**: `ClassNotFoundException` = classpath miss; `NoClassDefFoundError` = found at compile, missing at runtime.

### JVM Memory Areas
- **Heap** → All objects; Young Gen (Eden + S0 + S1) + Old Gen + Metaspace (native memory for class metadata).
- **Stack** → Per-thread; LIFO frames (locals, operand stack, return addr). `StackOverflowError` on deep recursion.
- **PC Register** → Per-thread current instruction. **Native Method Stack** → JNI calls.
- **Code Cache** → JIT native code. **Keywords**: OOM: heap space / Metaspace. PermGen removed Java 8 → Metaspace.

### Garbage Collection
- **GC Roots** → Stack vars, static fields, JNI refs. Reachable from roots = live.
- **Algorithms** → Mark-Sweep, Mark-Compact, Copying (Young gen). **Generational Hypothesis**: most objects die young.
- **Minor GC** → Young gen; fast; short STW. **Major/Full GC** → Old gen; slow; long STW.
- **Reference Types** → Strong (never collected), Soft (OOM pressure), Weak (next GC, WeakHashMap), Phantom (post-finalize).

### GC Collectors

| Collector | Default In | Key Strength |
|---|---|---|
| Serial GC | Small apps | Single-thread, simple |
| Parallel GC | Java 8 | Throughput |
| G1GC | Java 9+ | Balanced, predictable pauses |
| ZGC | Java 15+ | <10ms pauses, TB heaps |
| Shenandoah | RedHat | Low-pause concurrent compact |

### JIT Compilation
- **Tiered** → Interpreted → C1 (quick) → C2 (optimized hotspot).
- **Inlining** → Small methods inserted at call site. **Escape Analysis** → stack allocate + lock elision.
- **OSR** → Replace running loop with compiled version mid-execution.
- **Deoptimization** → Revert to interpreter when assumption violated.

### Memory Leaks
- Static collections, unclosed resources, listeners never removed, non-static inner class, ThreadLocal not cleared.
- **Tools** → Eclipse MAT, VisualVM, YourKit for heap dump analysis.

### JVM Flags
`-Xms`/`-Xmx` (heap), `-Xss` (stack), `-XX:MaxMetaspaceSize`, `-XX:+UseG1GC`, `-XX:+UseZGC`,
`-Xlog:gc*`, `-XX:+HeapDumpOnOutOfMemoryError`, `-XX:MaxGCPauseMillis=200`, `-XX:+PrintCompilation`.

---

## 10. Java Design Patterns

### Creational
- **Singleton** → Enum singleton (best: serialization+reflection safe); or DCL with `volatile`; or Holder idiom.
- **Factory Method** → Interface for creation; subclass decides type; decouples caller from implementation.
- **Abstract Factory** → Family of factories; factory-of-factories.
- **Builder** → Fluent step-by-step; avoids telescoping constructors; usually returns immutable object.
- **Prototype** → Clone existing; `Cloneable` or copy constructor.
- **Object Pool** → Reuse expensive objects (DB connections, threads).

### Structural
- **Adapter** → Convert interface; wraps incompatible (e.g., `InputStreamReader`: bytes→chars).
- **Decorator** → Add behavior dynamically; same interface (e.g., `BufferedInputStream`).
- **Proxy** → Control access; logging/security/lazy-init. JDK Dynamic Proxy (needs interface) vs CGLIB (subclass).
- **Facade** → Simplified interface over complex subsystem.
- **Composite** → Uniform tree; leaf + branch share same interface.
- **Bridge** → Decouple abstraction from implementation; both evolve independently.
- **Flyweight** → Share intrinsic state (String pool, Integer cache).
- **Keywords**: Decorator adds behavior; Proxy controls access. CGLIB used by Spring for classes without interface.

### Behavioral
- **Strategy** → Interchangeable algorithms encapsulated; `Comparator` is Strategy pattern.
- **Observer** → Subject notifies observers on state change; event listeners, pub/sub.
- **Command** → Encapsulate request as object; enables undo/queue/macro.
- **Template Method** → Algorithm skeleton in base; subclasses fill steps (inheritance-based).
- **Iterator** → Sequential access without exposing internals.
- **Chain of Responsibility** → Request passed along handler chain; each handles or forwards.
- **State** → Behavior changes with internal state; eliminates big if-else chains.
- **Mediator** → Centralize object-to-object communication.
- **Memento** → Save/restore state snapshot (undo feature).
- **Visitor** → Add operations to hierarchy without modifying classes; double dispatch.
- **Null Object** → Default behavior instead of null checks.
- **Keywords**: Strategy = composition (flexible); Template = inheritance (rigid).

### Architectural
- **MVC/MVP/MVVM** → UI patterns; Spring MVC uses Controller pattern.
- **Repository / DAO** → Abstraction over data access; Spring Data `@Repository`.
- **Service Layer** → Business logic separate from controllers.
- **CQRS** → Separate read (Query) and write (Command) models.
- **Event Sourcing** → Store events as truth; replay to rebuild state.
- **Hexagonal/Clean Architecture** → Domain isolated from infra; ports and adapters.

---

## 11. Java Annotations & Reflection

### Annotations
- **Built-in** → `@Override`, `@Deprecated`, `@SuppressWarnings`, `@FunctionalInterface`, `@SafeVarargs`.
- **Meta-annotations** → `@Retention(SOURCE/CLASS/RUNTIME)`, `@Target(TYPE/METHOD/FIELD/PARAMETER/...)`, `@Documented`, `@Inherited`, `@Repeatable`.
- **Custom** → `public @interface MyAnnotation { String value() default ""; }`.
- **APT** → Annotation processors at compile time: Lombok, MapStruct, Dagger.
- **Keywords**: RUNTIME retention needed for Spring/Hibernate/JUnit; SOURCE for Lombok (compile-only).

### Reflection API
- `Class.forName(name)`, `obj.getClass()`, `MyClass.class`.
- **Inspect** → `getDeclaredFields/Methods/Constructors()` (all, this class); `getFields/Methods()` (public+inherited).
- **Invoke** → `method.invoke(instance, args)`, `field.get/set(instance, value)`, `constructor.newInstance(args)`.
- `field.setAccessible(true)` → bypass private modifier.
- `getAnnotation(...)`, `isAnnotationPresent(...)`.
- **Keywords**: Used by Spring, Hibernate, JUnit, Jackson, Mockito; ~2-100x slower than direct calls; Java 9+ modules restrict deep reflection.

---

## 12. Java Modules (JPMS — Java 9+)

### Overview
- **JPMS** → Strong encapsulation at JVM level; reliable dependency declaration; solves classpath/JAR hell.
- `module-info.java` at source root; `jlink` creates minimal runtime image.

### Directives
- `requires [transitive] [static] moduleName;` → dependency (transitive: exposed to consumers; static: compile-only).
- `exports pkg [to moduleName];` → expose package for access.
- `opens pkg [to moduleName];` → allow reflective access at runtime (for frameworks like Spring, Hibernate).
- `uses ServiceInterface;` / `provides ServiceInterface with ImplClass;` → Service Provider Interface.

### Module Types & Migration
- **Named** → Has module-info.java. **Unnamed** → classpath code (backward compat). **Automatic** → JAR on module-path without descriptor.
- `--add-opens`, `--add-exports` runtime flags → bypass encapsulation for migration.
- **Keywords**: `ServiceLoader.load(Plugin.class)` for SPI; OSGi for advanced classloading isolation.

---

## 13. Java Version Features (Java 5–26)

> **Coverage:** Every major Java release from Java 5 (2004) through Java 26 (2026 roadmap). Each version includes subtopics, keywords, and interview-ready notes. LTS versions are highlighted.

---

### Java 5 (2004) — Generics & Concurrency Revolution

#### Generics
- Parameterize classes/methods by type: `List<String>`, `Map<K,V>`. Prevents raw-type `ClassCastException`.
- **Type erasure** → Generics are compile-time only; bytecode sees `Object`; no `new T()` or `T.class` at runtime.
- **Bounded wildcards** → `<? extends Animal>` (producer/upper), `<? super Dog>` (consumer/lower), PECS rule.
- **Interview Note**: "Why can't you create a generic array?" → Arrays are covariant + reified; generics are invariant + erased → incompatible.

#### Type Safety
- Compile-time checks via generics eliminate unchecked casts. `@SuppressWarnings("unchecked")` is code smell.
- Raw types (`List` instead of `List<String>`) retained for backward compat but unsafe.

#### Enhanced for-loop (for-each)
- `for (String s : list)` → works on any `Iterable` and arrays. Cleaner than indexed loop.
- **Limitation**: No index access, no concurrent modification, no reverse iteration.

#### Autoboxing / Unboxing
- Auto-convert between primitives and wrappers: `int ↔ Integer`, `double ↔ Double`, etc.
- **Trap**: `Integer a = 127; Integer b = 127; a == b` → true (cached); `Integer c = 200; Integer d = 200; c == d` → false (different objects). Always use `.equals()`.
- **Performance**: Autoboxing in tight loops = object allocation overhead; use primitive arrays or streams.

#### Varargs
- `void log(String... msgs)` — caller passes any number; received as array. Must be last parameter.
- `Arrays.asList(1,2,3)` → uses varargs. Heap pollution warning with generics + varargs.

#### Enums
- Type-safe constants with behavior: `enum Planet { MERCURY(3.303e+23, 2.4397e6); }`.
- Implicitly `public static final`; can have fields, methods, constructors, implement interfaces.
- `values()` → all constants; `ordinal()` → position (avoid for logic); `name()` → string name.
- **Interview Note**: Enums in switch, `EnumSet`/`EnumMap` for performance, `Enum.valueOf()`.

#### Annotations
- Metadata on code; processed at compile-time or runtime via reflection.
- Built-in: `@Override`, `@Deprecated`, `@SuppressWarnings`, `@FunctionalInterface`, `@SafeVarargs`.
- Custom: `@interface MyAnnotation { String value() default ""; }`. Retention: `SOURCE`, `CLASS`, `RUNTIME`.
- **Interview Note**: Annotation processors (APT) generate code at compile time (e.g., Lombok, MapStruct).

#### Static Import
- `import static java.lang.Math.PI;` → use `PI` directly. Useful for constants and utility methods; avoid overuse.

#### Concurrency Utilities (`java.util.concurrent`)
- `Executor`, `ExecutorService`, `ScheduledExecutorService` → thread pool management.
- `Future<T>` → async result; `get()` blocks; `isDone()` polls.
- `BlockingQueue` → `ArrayBlockingQueue`, `LinkedBlockingQueue` — producer-consumer pattern.
- `CountDownLatch`, `CyclicBarrier`, `Semaphore`, `Exchanger` → coordination primitives.
- `ConcurrentHashMap`, `CopyOnWriteArrayList` → thread-safe collections.
- `AtomicInteger`, `AtomicReference` → lock-free CAS operations.

#### Executor Framework
- Replace `new Thread(runnable).start()` with `Executors.newFixedThreadPool(10)`.
- `submit(Callable)` → returns `Future`; `execute(Runnable)` → no return.
- **Interview Note**: Always shut down executor (`shutdown()` graceful, `shutdownNow()` immediate).

---

### Java 6 (2006) — Tooling & Performance

#### Scripting API (`javax.script`)
- `ScriptEngine` → execute JavaScript (Rhino engine) or other JSR-223-compliant languages from Java.
- `ScriptEngineManager manager = new ScriptEngineManager(); ScriptEngine engine = manager.getEngineByName("js");`

#### Compiler API (`javax.tools`)
- Programmatically invoke `javac` at runtime. Used by IDEs, build tools, test frameworks.
- `JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();`

#### JDBC 4.0
- Auto-loading of JDBC drivers via `ServiceLoader` (no more `Class.forName()`).
- `SQLExceptionsubtypes` for better error classification. `RowId`, `SQLXML`, `NClob` types added.

#### Pluggable Annotations
- Annotation processors integrated into `javac` pipeline. Enables compile-time code generation.

#### Performance Improvements
- Improved startup time, HotSpot JIT improvements, faster `String.intern()`, synchronized block optimization.

#### Monitoring & Management APIs
- Enhanced JMX support. `java.lang.management` for heap, thread, and GC monitoring.
- `ManagementFactory.getMemoryMXBean()` → programmatic memory introspection.

---

### Java 7 (2011) — Project Coin & NIO.2

#### Try-with-resources
- `try (InputStream is = new FileInputStream(f)) { }` → auto-calls `close()` on any `AutoCloseable`.
- Replaces verbose `finally` blocks; exception suppression via `getSuppressed()`.
- **Interview Note**: Multiple resources closed in reverse order of declaration.

#### Multi-catch
- `catch (IOException | SQLException e)` → handle multiple exceptions in one block. `e` is implicitly `final`.

#### Diamond Operator
- `List<String> list = new ArrayList<>();` → infer generic type from left side. Reduces verbosity.

#### Strings in switch
- `switch (str) { case "HELLO": ... }` → compiler converts to `hashCode()` + `equals()` check. Case-sensitive.

#### NIO.2 (FileSystem API — `java.nio.file`)
- `Path`, `Paths`, `Files` → modern file I/O. Replace legacy `File` class.
- `Files.copy()`, `Files.move()`, `Files.walk()`, `Files.readAllLines()`, `WatchService` for directory events.
- Symbolic links, file attributes, file stores. `FileSystem` abstraction.

#### ForkJoin Framework
- `ForkJoinPool` + `RecursiveTask`/`RecursiveAction` → divide-and-conquer parallelism (work-stealing).
- Used internally by parallel streams (Java 8) and `Arrays.parallelSort()`.
- `pool.invoke(task)` → wait for result; `fork()` async submit; `join()` wait for subtask.

#### Binary Literals & Underscores in Numbers
- `int b = 0b1010_1010;` → binary literal. `long million = 1_000_000L;` → visual grouping.

---

### Java 8 (2014, LTS) — Functional Programming Era

#### Lambda Expressions
- `(params) -> expression` or `(params) -> { statements; }`. Enable functional-style code.
- Capture effectively final variables from enclosing scope. No access to non-effectively-final locals.
- **Interview Note**: Lambdas implement functional interfaces; they are not anonymous inner classes (no `this` shadowing, no separate `.class` file).

#### Functional Interfaces
- Interface with exactly one abstract method. `@FunctionalInterface` enforces this at compile time.
- Key built-ins in `java.util.function`:
  - `Predicate<T>` → `test(T)` → boolean
  - `Function<T,R>` → `apply(T)` → R
  - `Consumer<T>` → `accept(T)` → void
  - `Supplier<T>` → `get()` → T
  - `BiFunction<T,U,R>`, `UnaryOperator<T>`, `BinaryOperator<T>`
- **Interview Note**: Compose with `andThen()`, `compose()`, `and()`, `or()`, `negate()`.

#### Streams API
- Lazy pipeline: `source → intermediate ops → terminal op`. Data not processed until terminal triggered.
- **Intermediate** (lazy): `filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`, `limit`, `skip`.
- **Terminal** (eager): `collect`, `forEach`, `reduce`, `count`, `findFirst`, `anyMatch`, `toArray`.
- `Collectors.toList()`, `groupingBy()`, `joining()`, `partitioningBy()`, `toMap()`.
- **Parallel streams**: `list.parallelStream()` → uses `ForkJoinPool.commonPool()`; only beneficial for CPU-bound, large datasets with no shared mutable state.
- **Interview Note**: Streams are not reusable; `Stream.of()`, `IntStream.range()`, `Arrays.stream()`.

#### Method References
- Shorthand for lambdas calling a single method: `String::toUpperCase`, `System.out::println`, `Person::new`.
- Types: Static (`Class::staticMethod`), instance (`obj::method`), unbound (`Class::instanceMethod`), constructor (`Class::new`).

#### Optional
- `Optional<T>` → container that may or may not hold a value. Replaces `null` returns.
- `Optional.of(val)`, `Optional.ofNullable(val)`, `Optional.empty()`.
- `isPresent()`, `get()` (throws if empty), `orElse(default)`, `orElseGet(supplier)`, `orElseThrow()`, `map()`, `flatMap()`, `filter()`.
- **Interview Note**: Don't use `Optional` as method parameter or field; only as return type. `orElseGet` is lazy (preferred over `orElse` for expensive defaults).

#### Default Methods
- `default void sort(Comparator c) { ... }` in interface → add behavior without breaking existing implementations.
- Enables backward-compatible API evolution. Diamond ambiguity resolved: class wins over interface.

#### Static Interface Methods
- `static Optional<T> of(T value)` in interface → utility helpers tied to interface, not inherited by implementations.

#### Date & Time API (`java.time`)
- `LocalDate`, `LocalTime`, `LocalDateTime` (no timezone), `ZonedDateTime`, `Instant`, `Duration`, `Period`.
- Immutable, thread-safe. Replaces `java.util.Date`/`Calendar` (mutable, not thread-safe).
- `DateTimeFormatter` is thread-safe (unlike `SimpleDateFormat`).

#### Nashorn JS Engine
- Replaced Rhino; faster JS execution embedded in JVM. Deprecated in Java 11, removed in Java 15.

---

### Java 9 (2017) — Modularization

#### JPMS (Java Platform Module System)
- `module-info.java` declares module name, `requires`, `exports`, `opens`, `uses`, `provides`.
- Strong encapsulation: internal APIs (`sun.*`, `com.sun.*`) no longer accessible by default.
- `requires transitive` → transitive dependency; `opens` → reflective access; `exports ... to` → qualified export.

#### `module-info.java`
```java
module com.myapp {
    requires java.sql;
    requires transitive java.logging;
    exports com.myapp.api;
    opens com.myapp.model to jackson.databind;
}
```
- **Interview Note**: Unnamed module = classpath code; automatic modules = JARs on module path without `module-info`.

#### JShell (REPL)
- Interactive Java REPL. Evaluate expressions, test snippets without compiling a full class.
- `/list`, `/vars`, `/methods`, `/save`, `/open` commands. Great for exploration and teaching.

#### Reactive Streams (`Flow` API)
- `Flow.Publisher`, `Flow.Subscriber`, `Flow.Subscription`, `Flow.Processor` — standard interfaces for reactive streams (interop with RxJava, Project Reactor).
- `SubmissionPublisher` → built-in publisher implementation.

#### Multi-release JAR
- JAR can contain different class versions for different JVM versions. `META-INF/versions/11/` for Java 11-specific code.

#### Private Interface Methods
- `private` and `private static` methods in interfaces to share code between default methods without exposing in API.

#### Collection Factory Methods
- `List.of(1,2,3)`, `Set.of("a","b")`, `Map.of("k1","v1","k2","v2")` → immutable, null-hostile.
- `Map.ofEntries(Map.entry("k","v"), ...)` → for more than 10 entries.

#### Stream Enhancements
- `takeWhile(predicate)`, `dropWhile(predicate)`, `iterate(seed, hasNext, next)` (finite), `ofNullable(val)`.

---

### Java 10 (2018) — Local Type Inference

#### `var` (Local Variable Type Inference)
- `var list = new ArrayList<String>();` → type inferred at compile time, still statically typed.
- Valid: local variable with initializer, for/foreach, try-with-resources, lambda params (Java 11).
- Invalid: fields, method params, return types, `null` initializer, no initializer.
- `var` is a reserved type name, not a keyword → `int var = 5;` is still valid (don't do this).

#### Application CDS (Class Data Sharing)
- Share class metadata across JVM instances; faster startup. Extend with `AppCDS` for application classes.

#### Garbage Collector Improvements
- G1 GC can return unused heap memory to OS. Parallel full GC for G1. `PrintGCDetails` deprecated.

#### Unmodifiable Collection Copies
- `List.copyOf(list)`, `Set.copyOf(set)`, `Map.copyOf(map)` → unmodifiable shallow copies.
- `Collectors.toUnmodifiableList/Set/Map()`.

---

### Java 11 (2018, LTS) — String & HTTP

#### HTTP Client API (stable)
- `HttpClient`, `HttpRequest`, `HttpResponse` in `java.net.http`. Supports HTTP/1.1, HTTP/2, WebSocket.
- Synchronous (`send()`) and async (`sendAsync()` returns `CompletableFuture`).

#### `var` in Lambda Parameters
- `(var x, var y) -> x + y` → enables annotations on lambda params: `(@NotNull var s) -> s.trim()`.

#### String API Enhancements
- `isBlank()` → true if empty or whitespace. `strip()` / `stripLeading()` / `stripTrailing()` → Unicode-aware trim.
- `lines()` → `Stream<String>` split by line terminators. `repeat(n)` → repeat string n times.

#### Files API
- `Files.readString(path)`, `Files.writeString(path, content)` → convenient single-call I/O.

#### Single-file Program Launch
- `java Hello.java` → compile + run in one step. No class needed for simple scripts.

#### `Optional.isEmpty()`
- Complement to `isPresent()`. Cleaner for negative checks.

#### ZGC & Epsilon GC (experimental)
- ZGC: low-latency GC (sub-millisecond pauses). Epsilon: no-op GC (for benchmarking/short-lived apps).

#### Java EE & CORBA Removal
- `javax.xml.ws`, `javax.jws`, CORBA packages removed. Move to standalone Jakarta EE dependencies.

---

### Java 12 (2019)

#### Switch Expressions (Preview)
- Arrow syntax: `case MONDAY -> "Mon";` — no fall-through, no `break` needed.
- Still a preview; `--enable-preview` required.

#### Shenandoah GC (Experimental)
- Ultra-low-pause GC; concurrent compaction even during GC. Alternative to ZGC. Developed by Red Hat.

#### JVM Constants API
- `java.lang.constant` — model JVM constants (class, method, field descriptors) symbolically for frameworks/tools.

#### `String.indent()` and `String.transform()`
- `indent(n)` → add/remove leading whitespace per line + add trailing newline.
- `transform(f)` → apply function to string: `"hello".transform(String::toUpperCase)`.

---

### Java 13 (2019)

#### Text Blocks (Preview)
- Multi-line string literals with `"""`: preserve indentation, handle line endings automatically.
- Incidental whitespace stripped based on common leading whitespace.

#### Switch Expressions (2nd Preview)
- Refined based on feedback; closer to stable. `yield` keyword introduced for returning value from blocks.

#### Dynamic CDS (Class Data Sharing)
- Auto-generate CDS archive at application exit; use on next launch for faster startup.

---

### Java 14 (2020)

#### Records (Preview)
- `record Point(int x, int y) {}` → immutable data carrier; auto-generates constructor, accessors, `equals`, `hashCode`, `toString`.

#### Pattern Matching for `instanceof` (Preview)
- `if (obj instanceof String s) { s.toUpperCase(); }` → no explicit cast needed.

#### Switch Expressions (Stable)
- Arrow switch and `yield` are now production-ready (no `--enable-preview`).

#### Helpful NullPointerExceptions
- JVM message now says: `Cannot read field "name" because "person" is null` — pinpoints exact NPE location.
- Enabled by default in Java 14+. `NullPointerException.getMessage()` is useful in logs.

---

### Java 15 (2020)

#### Text Blocks (Stable)
- `"""..."""` multi-line strings are production-ready. `\` at line end = line continuation (no newline). `\s` = explicit space.
- Great for SQL, JSON, HTML in code. `formatted()` method for interpolation substitute.

#### Sealed Classes (Preview)
- `sealed class Shape permits Circle, Rectangle {}` → restrict which classes can extend.
- Permitted subtype must be `final`, `sealed`, or `non-sealed`. Must be in same package/module.

#### Hidden Classes
- Classes not discoverable by name; used by frameworks generating proxy/lambda classes at runtime. Not in classpath.

#### ZGC + Shenandoah (Production Ready)
- Both GCs exit experimental status. Sub-millisecond pause times. ZGC: `heap region`-based. Shenandoah: concurrent compaction.

---

### Java 16 (2021)

#### Records (Stable)
- Records are standard. Custom constructors, additional methods, implement interfaces allowed.
- `record` bodies can't have mutable instance fields. Components are `private final`.

#### Pattern Matching `instanceof` (Stable)
- `instanceof` binding variable is standard. Scope follows flow analysis (smart casts).

#### `Stream.toList()`
- `stream.toList()` → shorthand for `collect(Collectors.toUnmodifiableList())`. Returns unmodifiable list.

#### Unix-Domain Sockets
- `ServerSocket` and `Socket` can use Unix domain sockets (`UnixDomainSocketAddress`) — faster IPC on same machine.

#### Vector API (Incubator)
- SIMD operations on arrays; express vector math that JIT can optimize to hardware vector instructions.

---

### Java 17 (2021, LTS) — Enterprise Stability

#### Sealed Classes (Stable)
- Production-ready. Combine with `switch` pattern matching for exhaustive case analysis (compiler-verified).

#### Pattern Matching for Switch (Preview)
- `switch(obj) { case Integer i -> ...; case String s when s.isEmpty() -> ...; }` — type patterns + guards.

#### Strong Encapsulation of JDK Internals
- `--illegal-access` removed. Internal APIs (`sun.misc.Unsafe` via reflection) blocked by default.
- Framework authors must use `--add-opens` or migrate to public APIs.

#### Enhanced `RandomGenerator` API
- Unified interface for all random generators: `ThreadLocalRandom`, `SplittableRandom`, `Random`.
- `RandomGeneratorFactory` → choose algorithm (e.g., `Xoshiro256StarStar`, `L64X128MixRandom`).

#### Foreign Function & Memory API (Incubator)
- Access native memory and call native code without JNI. Preview of Project Panama.

#### **Interview Note — Java 17 as Enterprise Standard**
- Most major frameworks (Spring Boot 3, Quarkus, Micronaut) target Java 17+ as baseline.
- Strong encapsulation forces clean API usage; better security.

---

### Java 18 (2022)

#### Simple Web Server (`jwebserver`)
- `java -m jdk.httpserver` → one-command static file server for development/testing. Not production-grade.

#### UTF-8 Default Charset
- `Charset.defaultCharset()` → UTF-8 on all platforms (previously platform-dependent). Eliminates encoding bugs.

#### Code Snippets in JavaDoc (`@snippet`)
- `{@snippet : code here}` → syntax-highlighted, validated code in Javadoc. Replaces `<pre>{@code ...}</pre>`.

#### `finalize()` Deprecated for Removal
- `Object.finalize()` officially deprecated for removal. Use `Cleaner` API or `try-with-resources` instead.

---

### Java 19 (2022)

#### Virtual Threads (Preview — Project Loom)
- `Thread.ofVirtual().start(runnable)` → lightweight threads managed by JVM, not OS.
- Millions of virtual threads possible; blocked virtual thread unmounts from carrier (platform) thread.
- **Interview Note**: Virtual threads are not faster than platform threads per se; they enable higher *concurrency* for I/O-bound work without thread pool exhaustion.

#### Structured Concurrency (Incubator)
- `StructuredTaskScope` → launch subtasks; scope ensures all complete/cancel before scope exits.
- `ShutdownOnFailure`: cancel all if any fails. `ShutdownOnSuccess`: cancel all when first succeeds.

#### Record Patterns (Preview)
- Deconstruct record components in patterns: `case Point(int x, int y) ->`. Compose with `instanceof`.

---

### Java 20 (2023)

#### Virtual Threads (2nd Preview)
- Refinements; `Thread.sleep()`, `synchronized`, blocking I/O all compatible with virtual threads.

#### Scoped Values (Incubator)
- `ScopedValue<T>` → immutable, per-thread (and per-virtual-thread) context value. Replace `ThreadLocal` for virtual threads.
- `ScopedValue.where(KEY, val).run(() -> ...)` → scoped binding; no risk of memory leak.

#### Pattern Matching for Switch (4th Preview)
- Further refinement of exhaustiveness, dominance, and guarded patterns.

---

### Java 21 (2023, LTS) — Modern Concurrency Revolution

#### Virtual Threads (Stable)
- `Thread.ofVirtual().start(...)`, `Executors.newVirtualThreadPerTaskExecutor()`.
- Replace thread pools for I/O-bound tasks. Semaphore for rate limiting (not `synchronized`).
- **Interview Note**: Virtual threads + structured concurrency = new concurrency model. Reactive programming less necessary.

#### Structured Concurrency (Preview)
- `try (var scope = new StructuredTaskScope.ShutdownOnFailure()) { ... scope.join(); scope.throwIfFailed(); }`

#### Scoped Values (Preview)
- Finalized API shape; `ScopedValue.newInstance()` → replaces `ThreadLocal` for immutable inherited context.

#### Pattern Matching for Switch (Stable)
- `case Integer i when i > 0 ->`, `case null ->`. Exhaustiveness enforced for sealed types.

#### Record Patterns (Stable)
- `case Point(int x, int y) ->` in switch and instanceof. Nested record patterns supported.

#### Sequenced Collections
- New interfaces: `SequencedCollection`, `SequencedSet`, `SequencedMap`.
- Methods: `getFirst()`, `getLast()`, `addFirst()`, `addLast()`, `removeFirst()`, `removeLast()`, `reversed()`.
- Retrofitted to `List`, `Deque`, `LinkedHashSet`, `LinkedHashMap`, `SortedSet`, `SortedMap`.

#### String Templates (Preview)
- `STR."Hello \{name}"` → compile-time validated string interpolation (different from runtime string concat).
- `FMT`, `RAW` processors. Custom template processors possible.

---

### Java 22 (2024)

#### String Templates (2nd Preview)
- Refinements to template processor API. Still preview; syntax subject to change.

#### Foreign Function & Memory API (Stable)
- `MemorySegment`, `Arena`, `MethodHandle` via `Linker` → access native memory/functions safely without JNI.
- Project Panama milestone. Replaces JNI for most native interop use cases.

#### Unnamed Variables & Patterns (`_`)
- `catch (Exception _) { }` → unnamed variable when value unused.
- `for (var _ : list) { count++; }`, `case Point(int x, _) ->`.

#### Implicit Classes (Preview)
- Top-level class body without class declaration: `void main() { System.out.println("Hello"); }`.
- Lowers barrier for beginners. Not for production code.

#### Stream Gatherers (Preview)
- `Stream.gather(Gatherer)` → custom intermediate stream operations. Compose with `Gatherer.of(...)`.
- Fill gap between existing built-in ops and custom `Collector`-like logic mid-pipeline.

---

### Java 23 (2024)

#### Primitive Types in Patterns (Preview)
- Pattern matching with primitives: `case int i ->`, `case float f when f > 0 ->` in switch.
- Removes the artificial limitation of patterns only working with reference types.

#### Markdown in JavaDoc
- Write JavaDoc comments in Markdown syntax (GFM subset). `///` line comment starts Markdown doc block.
- Interops with existing `{@link}`, `{@code}` tags.

#### Scoped Values (3rd Preview)
- API stabilization. Thread-local replacement fully defined. Structured concurrency integration.

#### Performance Enhancements
- JIT (C2) improvements, G1 GC region pinning (reduces JNI latency spikes), startup optimizations.

---

### Java 24 (2025)

#### Value Objects (Project Valhalla Preview)
- `value class Point { int x; int y; }` → identity-free objects. No `==` identity; always compared by value.
- Can be stored in arrays without boxing overhead. Potential flattening in heap/stack (inline types roadmap).
- **Interview Note**: Value types = performance of primitives + expressiveness of objects. Long-awaited JVM evolution.

#### Enhanced Pattern Matching
- Primitive patterns stable. Improved exhaustiveness checking across sealed hierarchies.

#### Continuation Improvements (Project Loom)
- Internal `Continuation` API improvements underpinning virtual threads; not directly user-facing.

#### GC Enhancements
- ZGC and G1 improvements for throughput and pause time. ZGC: generational mode improvements.

#### Class-File API (Stable)
- Standard API to parse, generate, transform `.class` files. Replaces third-party ASM in many tool use cases.

---

### Java 25 (2025, LTS — Roadmap)

#### Loom Enhancements (Structured Concurrency & Scoped Values Stable)
- Structured Concurrency and Scoped Values expected to graduate to stable. Full virtual thread ecosystem mature.

#### Valhalla Updates (Value Types)
- Value classes closer to stable. Inline type representation in arrays (flat array layout) for primitive-like performance.

#### Panama Improvements (Native Interop)
- `jextract` tool improvements for auto-generating Java bindings from C headers. FFM API enhancements.

#### Performance & JVM Tuning
- Ongoing JIT (Graal-influenced) improvements, startup time reductions (Leyden/AOT), memory footprint reduction.

---

### Java 26 (2026 — Early Roadmap)

#### Advanced Value Types
- Value types potentially stable; flattening in generics (`List<Point>` stored without boxing).

#### Enhanced Foreign Memory Access
- FFM API further refinements; safer memory lifecycle management.

#### Unified Pattern Matching
- All pattern contexts (switch, instanceof, catch, bind) consistent and complete.

#### Advanced JIT Optimizations
- Profile-guided compilation improvements; faster warmup for cloud-native deployments.

#### AI-assisted JVM Optimizations (Experimental Direction)
- Exploration of ML-guided JIT decisions, adaptive GC tuning based on workload patterns.

---

### Cross-Version Keywords (IMPORTANT)

| Term | Meaning |
|------|---------|
| **LTS** | Long Term Support — Java 8, 11, 17, 21, 25. Vendor support for 8+ years. Use for production. |
| **Preview Features** | Must enable with `--enable-preview`. Can change in next version. Don't ship to prod. |
| **Incubator Features** | Module-level preview for APIs. `--add-modules jdk.incubator.xxx`. May change significantly. |
| **Backward Compatibility** | Java's core promise — old bytecode runs on new JVM. Rarely broken (modules/encapsulation are exceptions). |
| **Bytecode Evolution** | JVM bytecode version increments per release. `javac --release N` for cross-compilation. |
| **JVM Enhancements** | JVM improves independent of language (GC, JIT, startup). Bytecode spec stable. |
| **G1 GC** | Default since Java 9. Predictable pause times. Region-based. Tunable with `MaxGCPauseMillis`. |
| **ZGC** | Sub-millisecond pauses. Scales to terabytes. Concurrent. Java 15 production-ready. Generational in Java 21. |
| **Shenandoah GC** | Low-pause concurrent GC. Red Hat. Alternative to ZGC. Concurrent compaction. |
| **Project Loom** | Virtual Threads + Structured Concurrency. Main deliverable: Java 21. |
| **Project Valhalla** | Value Types (primitive-like objects). Main deliverable: Java 24+. |
| **Project Panama** | Native Interop (FFM API). Main deliverable: Java 22 (stable). |
| **Project Amber** | Language features (Records, Sealed, Patterns, var, Text Blocks). Delivered across Java 14–21. |

---

### Interview Power Keywords — Version Strategy

| Context | Answer |
|---------|--------|
| **Java 8 significance** | Functional paradigm shift — lambdas, streams, Optional, `java.time`. Most widely deployed LTS. |
| **Java 9 significance** | Modularization (JPMS) — strong encapsulation, dependency declaration, platform integrity. |
| **Java 17 significance** | Enterprise stability LTS. Sealed classes, strong JDK encapsulation. Spring Boot 3 baseline. |
| **Java 21 significance** | Concurrency revolution — virtual threads stable. Most impactful Java release since Java 8. |
| **Loom vs Traditional Threads** | Virtual threads: M:N with JVM scheduler; platform threads: 1:1 with OS. Virtual = better IO concurrency, not CPU. |
| **Records vs POJOs** | Records: immutable, concise, value semantics, no boilerplate. POJOs: mutable, verbose, `@Override` everywhere. |
| **Sealed Classes vs Inheritance** | Sealed: closed hierarchy, compiler-verified exhaustiveness. Open inheritance: extensible but uncontrolled. |
| **Reactive vs Virtual Threads** | Reactive: complex, callback-based, necessary pre-Loom. Virtual threads: structured sequential code, same scalability. |

---

### Staff+ Level Themes

- **Evolution of Java Language Design** → Java intentionally evolves slowly (preview → 2nd preview → stable). Stability > novelty.
- **Performance vs Safety Trade-offs** → Value types sacrifice identity for performance. Strong encapsulation sacrifices flexibility for security.
- **JVM Optimization Trends** → Shorter startup (Leyden/AOT), lower memory (value types), higher concurrency (Loom).
- **Cloud-native Java** → GraalVM Native Image for fast startup/low footprint. OpenJ9 for memory efficiency. Quarkus/Micronaut for cloud optimization.
- **Reactive vs Virtual Threads** → Virtual threads don't eliminate reactive; they eliminate the *need* for reactive in most cases.
- **Native Interoperability** → FFM API replaces JNI: safer, no `UnsatisfiedLinkError`, memory lifecycle managed.

---

## 14. Java Records (Java 16+)

### Basics
- `record Point(int x, int y) {}` → auto-generates: canonical constructor, accessors `x()` `y()`, `equals`, `hashCode`, `toString`.
- Components = `private final` fields. Accessors: `point.x()` not `getX()`.
- **Compact Constructor** → Validate/normalize: `record Range(int lo, int hi) { Range { if (lo > hi) throw new IAE(); } }` — assignments happen automatically.
- Implicitly `final`; cannot extend; can implement interfaces; can have static fields/methods.
- Cannot add mutable instance fields or setters.

### Records Use Cases & Patterns
- DTOs, value objects, return multiple values, configuration, pattern matching deconstruction.
- **vs Lombok @Value** → Records: built-in, no dependencies, native IDE support; Lombok: more customizable.
- `instanceof` pattern with record: `if (obj instanceof Point(int x, int y)) { ... }` (Java 21).

---

## 15. Java Sealed Classes (Java 17+)

### Concepts
- `sealed class Shape permits Circle, Rectangle {}` → restricted subtype set.
- Permitted subtypes: `final` (no further), `sealed` (restricted further), `non-sealed` (open).
- **Keywords**: Exhaustive switch with sealed (no default needed); models ADT/discriminated unions; same compilation unit or explicit permits.

### Sealed + Pattern Matching Power
```java
sealed interface Shape permits Circle, Rect {}
record Circle(double r) implements Shape {}
record Rect(double w, double h) implements Shape {}
// Compiler verifies exhaustiveness:
double area = switch (shape) {
    case Circle c -> Math.PI * c.r() * c.r();
    case Rect r -> r.w() * r.h();
};
```

---

## 16. Java Pattern Matching (Java 16–21+)

### instanceof Pattern (Java 16 stable)
- `if (obj instanceof String s) { ... }` — type test + binding in one step; no explicit cast.
- Scope in `&&` chain: `obj instanceof String s && s.length() > 5`.
- After negation: `if (!(obj instanceof String s)) return;` — `s` in scope after early return.

### switch Pattern (Java 21 stable)
- Type patterns: `case Integer i ->`, Guarded: `case Integer i when i > 0 ->`.
- Record deconstruction: `case Point(int x, int y) ->`.
- Null handling: `case null ->` (previously caused NPE).
- Exhaustiveness enforced with sealed types; `default` still valid fallback.
- **Keywords**: More specific cases must come before general; dominance check at compile time.

---

## 17. Java Switch Expressions (Java 14 stable)

### Classic vs Expression Switch
- **Classic statement** → fall-through; `break` required; no value.
- **Switch expression** → arrow `->` (no fall-through); or colon + `yield`; must be exhaustive; can return value.

```java
// Arrow form — preferred
String label = switch (day) {
    case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> "Weekday";
    case SATURDAY, SUNDAY -> "Weekend";
};

// Colon form with yield for multi-statement blocks
int result = switch (input) {
    case 1 -> 10;
    case 2 -> {
        System.out.println("processing...");
        yield 20;
    }
    default -> throw new IllegalArgumentException();
};
```
- `yield` returns value from block; `return` would exit the enclosing method.
- **Keywords**: Switch on int, byte, short, char, String, enum; Java 21: any type with patterns.

---

## 18. Java `var` & Local Variable Type Inference (Java 10+)

### Basics
- `var list = new ArrayList<String>();` → type inferred as `ArrayList<String>` at compile time.
- **Allowed** → local vars with initializer, `for`/`foreach` loop vars, `try`-with-resources, lambda params (Java 11).
- **NOT allowed** → fields, method params, return types, no initializer, `null` initializer, multiple declarators.
- `var` = reserved type name (not keyword); still statically typed; type fixed at compile time.

### Best Practices
- Use when RHS makes type obvious: `var reader = new BufferedReader(...)`.
- Avoid when return type not descriptive: `var x = process()` — reader doesn't know type.
- `var` in lambda (Java 11): `(var x, var y) -> x + y` — enables annotations on lambda params.

---

## 19. Java Date & Time API (java.time — Java 8+)

### Core Classes (all immutable + thread-safe)
- `LocalDate` → `2024-01-15`; date only. `LocalTime` → `14:30:00`; time only.
- `LocalDateTime` → date+time; no zone. `ZonedDateTime` → date+time+timezone (DST-aware).
- `OffsetDateTime` → date+time+fixed offset. `Instant` → epoch timestamp; UTC; machine time.
- `Duration` → time-based (hours/min/sec). `Period` → date-based (years/months/days).
- `ZoneId.of("Asia/Kolkata")`, `ZoneOffset.of("+05:30")`. `MonthDay`, `YearMonth` → partial dates.

### Operations
- `plusDays/minusWeeks/plus(Period)`, `withDayOfMonth(1)`, `isBefore/isAfter/isEqual`.
- `ChronoUnit.DAYS.between(d1, d2)` → difference. `LocalDate.now()`, `LocalDate.of(y,m,d)`, `LocalDate.parse(str)`.

### DateTimeFormatter
- `DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm")` — thread-safe (unlike `SimpleDateFormat`).
- `formatter.format(localDateTime)` → String; `LocalDate.parse("15/01/2024", formatter)` → LocalDate.
- `DateTimeParseException` on invalid input.

### Legacy Interop
- `date.toInstant()`, `Date.from(instant)`. `Timestamp.toLocalDateTime()`. Always specify `ZoneId` for conversion.

---

## 20. Java Regex

### Core API
- `Pattern p = Pattern.compile("\\d+")` → compile once; `Matcher m = p.matcher(input)`.
- `m.find()` → next match; `m.matches()` → full string; `m.group()` → matched text; `m.group(n)` → capture group n.
- `m.replaceAll(replacement)`, `m.results()` (Java 9) → Stream of MatchResult.
- `Pattern.matches(regex, input)` → one-shot full match; `String.matches(regex)` → recompiles each call (avoid in loops).

### Key Patterns

| Symbol | Meaning |
|---|---|
| `.` | Any char (except newline) |
| `\d` / `\D` | Digit / non-digit |
| `\w` / `\W` | Word char / non-word |
| `\s` / `\S` | Whitespace / non-whitespace |
| `^` / `$` | Start / end of string |
| `*` / `+` / `?` | 0+ / 1+ / 0-1 (greedy) |
| `*?` / `+?` | Lazy (non-greedy) |
| `{n,m}` | n to m repetitions |
| `(group)` | Capture group |
| `(?:group)` | Non-capturing group |
| `(?=...)` / `(?!...)` | Lookahead / negative lookahead |
| `[abc]` / `[^abc]` | Class / negated class |
| `a\|b` | Alternation |

- **Keywords**: Double backslash in Java strings (`"\\d"` = regex `\d`); compile Pattern outside loops; `CASE_INSENSITIVE`, `MULTILINE`, `DOTALL` flags.

---

## 21. Java Networking (java.net)

### Core Classes
- **Socket** → TCP client. **ServerSocket** → TCP server; `accept()` blocks.
- **DatagramSocket/DatagramPacket** → UDP. **InetAddress** → IP address.
- `URL`, `HttpURLConnection` → legacy; verbose; avoid in new code.

### HttpClient (Java 11 — java.net.http)
```java
HttpClient client = HttpClient.newBuilder()
    .version(Version.HTTP_2)
    .connectTimeout(Duration.ofSeconds(10))
    .build();
HttpRequest req = HttpRequest.newBuilder()
    .uri(URI.create("https://api.example.com/data"))
    .header("Accept", "application/json")
    .GET().build();
// Sync:
HttpResponse<String> resp = client.send(req, BodyHandlers.ofString());
// Async:
client.sendAsync(req, BodyHandlers.ofString())
      .thenApply(HttpResponse::body)
      .thenAccept(System.out::println);
```
- **Keywords**: HTTP/2 multiplexing; connection reuse; `BodyHandlers.ofInputStream/ofFile`; `SocketTimeoutException` → set `setSoTimeout(ms)`.

---

## 22. Java JDBC

### Core Workflow
```java
try (Connection conn = DriverManager.getConnection(url, user, pass);
     PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?")) {
    ps.setInt(1, userId);
    try (ResultSet rs = ps.executeQuery()) {
        while (rs.next()) { System.out.println(rs.getString("name")); }
    }
}
```

### Statement Types
- **Statement** → No params; SQL injection risk; use only for static DDL.
- **PreparedStatement** → Parameterized `?`; pre-compiled; prevents injection; reusable.
- **CallableStatement** → Stored procedures: `{call proc(?,?)}`.

### Transactions
- `setAutoCommit(false)`, `commit()`, `rollback()`, `Savepoint` for partial rollback.
- **Isolation Levels** → READ_UNCOMMITTED → READ_COMMITTED → REPEATABLE_READ → SERIALIZABLE (more isolation, less concurrency).

### ResultSet & Batch
- `rs.next()` → advance cursor; `rs.getString/getInt/getTimestamp(col)`.
- **Types** → TYPE_FORWARD_ONLY (default), TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE.
- **Batch** → `ps.addBatch()` per row; `ps.executeBatch()` → single round-trip; much faster for bulk.

### Connection Pooling
- **HikariCP** → Default in Spring Boot; fastest; `maximumPoolSize`, `minimumIdle`, `connectionTimeout`, `maxLifetime`.
- **Keywords**: Pool exhaustion → timeout exception; tune pool size to DB server + workload.

---

## 23. Java Security

### Core Concepts
- Authentication (who are you?), Authorization (what can you do?).
- CIA Triad: Confidentiality (encryption), Integrity (hashing/signing), Availability.

### JCA/JCE
- `MessageDigest.getInstance("SHA-256")` → hashing (never MD5/SHA-1 for security).
- `Cipher.getInstance("AES/GCM/NoPadding")` → authenticated encryption.
- `KeyGenerator.getInstance("AES")` → symmetric key. `KeyPairGenerator.getInstance("RSA")` → asymmetric.
- `SecureRandom` → cryptographic RNG; never `Math.random()` for security.
- **Keywords**: AES-256 symmetric; RSA-2048+ asymmetric; BCrypt/Argon2/PBKDF2 for passwords (never raw hash).

### TLS/HTTPS
- `SSLContext`, `TrustManager`/`KeyManager`, `KeyStore` (PKCS12). TLS 1.3 standard; disable 1.0/1.1.

### OWASP Top Issues
- SQL Injection → always PreparedStatement. XSS → encode output; CSP header.
- Deserialization → never trust untrusted data; `ObjectInputFilter` allowlist.
- XXE → disable DTD/entity processing in XML parsers.
- **Keywords**: CSRF tokens; Secure cookies; Strict-Transport-Security header; principle of least privilege.

---

## 24. Java Logging

### Frameworks
- **SLF4J** → Facade API; always code against SLF4J, swap implementation freely.
- **Logback** → Default in Spring Boot; native SLF4J; fast. Config: `logback-spring.xml`.
- **Log4j 2** → Async appenders; powerful; Log4Shell CVE-2021-44228 (JNDI RCE) — keep updated.
- **JUL (java.util.logging)** → Built-in; limited; avoid in modern apps.

### Levels
TRACE → DEBUG → INFO → WARN → ERROR → FATAL (Log4j only). Production: INFO or WARN.

### SLF4J Pattern
```java
private static final Logger log = LoggerFactory.getLogger(MyService.class);
log.debug("Processing id={}, user={}", id, userId);    // {} placeholders = lazy eval
log.error("Failed for id={}", id, exception);           // Last arg = Throwable for stack trace
```
- **MDC** → `MDC.put("requestId", uuid)` → per-request context auto-included in all log statements.
- **Keywords**: `{}` placeholders avoid string concat if level disabled; never log passwords/PII/credentials; correlation ID for tracing.

### Log Management
- **Appenders** → Console, File, RollingFile (time/size-based), AsyncAppender, Logstash appender.
- **ELK/EFK Stack** → Centralized log aggregation. **Structured logging** → JSON format for machine parsing.

---

## 25. Java XML & JSON Processing

### XML
- **DOM** → Full tree in memory; random access; bad for large files (`DocumentBuilderFactory`).
- **SAX** → Event-driven streaming; low memory; read-only (`SAXParser`, `DefaultHandler`).
- **StAX** → Pull-based; bidirectional; `XMLStreamReader/Writer` — preferred over SAX.
- **JAXB** → Marshal/unmarshal Java ↔ XML; `@XmlRootElement`, `@XmlElement`; removed from JDK Java 11 (add `jakarta.xml.bind`).
- **XPath** → Query nodes: `XPathFactory.newInstance().newXPath().evaluate(expr, doc)`.
- **Keywords**: XXE attack — always disable external entities; DOM for small files; SAX/StAX for large.

### JSON
- **Jackson** → Most popular; `ObjectMapper` thread-safe after config; reuse instances.
  - `writeValueAsString(obj)`, `readValue(json, Class)`.
  - `@JsonProperty("name")`, `@JsonIgnore`, `@JsonAlias`, `@JsonInclude(NON_NULL)`.
  - Generics: `readValue(json, new TypeReference<List<User>>(){})`.
  - Modules: `JavaTimeModule` for `java.time`, `ParameterNamesModule`.
- **Gson** → Simpler; `toJson(obj)`, `fromJson(json, Type.class)`.
- **JSON-P** → Standard `javax.json`/`jakarta.json`; `JsonObject`, `JsonArray`, `JsonObjectBuilder`.
- **JSON-B** → Standard binding; `Jsonb.toJson/fromJson`.
- **Keywords**: Jackson ObjectMapper is expensive to create; cache/reuse; Tree model: `JsonNode` for dynamic JSON.

---

## 26. Java Testing

### JUnit 5
- `@Test`, `@BeforeEach/AfterEach`, `@BeforeAll/AfterAll` (static, or `@TestInstance(PER_CLASS)`).
- `@Disabled`, `@DisplayName`, `@Nested`, `@Tag`, `@ExtendWith`.
- **Parameterized** → `@ParameterizedTest` + `@ValueSource/@CsvSource/@MethodSource/@EnumSource/@NullSource`.
- **Assertions** → `assertEquals`, `assertNotNull`, `assertThrows(Type.class, () -> code)`, `assertAll(...)`, `assertTimeout(Duration, () -> code)`.

### Mockito
- `@Mock`, `@Spy` (partial), `@Captor`, `@InjectMocks`; `@ExtendWith(MockitoExtension.class)`.
- `when(mock.method(arg)).thenReturn(val)` / `thenThrow()` / `thenAnswer(invocation -> ...)`.
- `verify(mock, times(n)).method(arg)`, `verifyNoInteractions(mock)`.
- `ArgumentCaptor<T>` → capture and inspect passed arguments.
- **Keywords**: `doReturn` for spies; Mockito can't mock final by default (MockMaker extension); `InOrder` for sequence verification.

### Patterns
- **AAA** → Arrange-Act-Assert. **GWT** → Given-When-Then (BDD-style).
- **Test Pyramid** → Unit (many) → Integration (some) → E2E (few).
- **TDD** → Red (failing test) → Green (minimal code) → Refactor.
- **FIRST** → Fast, Independent, Repeatable, Self-validating, Timely.
- **Testcontainers** → Real Docker services in integration tests; `@Container`, `@Testcontainers`.
- **JaCoCo** → Coverage; `mvn verify`; line/branch/method/class metrics.

---

## 27. Java Build Tools

### Maven
- `pom.xml`: `groupId:artifactId:version` (GAV). **Lifecycle** → `validate → compile → test → package → verify → install → deploy`.
- **Scopes** → `compile`, `test`, `provided` (container provides), `runtime`, `import` (BOM).
- **BOM** → `<dependencyManagement>` with `scope=import`; centralize versions (Spring BOM).
- **Multi-module** → Parent POM aggregates children; shared config in parent.
- **Keywords**: `mvn clean install -DskipTests`, `mvn dependency:tree`; Maven Wrapper `mvnw`; nearest-wins for version conflicts.

### Gradle
- `build.gradle.kts` (Kotlin DSL preferred) or `build.gradle` (Groovy).
- **Configs** → `implementation` (internal), `api` (exposed), `testImplementation`, `runtimeOnly`, `compileOnly`.
- **Incremental Build** → Re-runs only changed tasks; up-to-date checks.
- **Build Cache** → Reuse outputs across builds; speeds CI dramatically.
- **Keywords**: `./gradlew build test`; Gradle Wrapper ensures consistent version; Convention plugins for multi-project.

---

## 28. Java Enum

### Fundamentals
- Fixed set of type-safe constants; each = `public static final` singleton instance.
- `values()`, `valueOf(String)`, `name()`, `ordinal()` (avoid for persistence — fragile to reordering).
- Implicitly `extends java.lang.Enum`; cannot extend other class; can implement interfaces.

### Features
```java
enum Planet {
    MERCURY(3.303e+23), EARTH(5.976e+24);
    private final double mass;
    Planet(double mass) { this.mass = mass; }
    public double mass() { return mass; }
}
// Abstract method — each constant implements differently:
enum Operation {
    ADD { public int apply(int a, int b) { return a + b; } },
    MUL { public int apply(int a, int b) { return a * b; } };
    public abstract int apply(int a, int b);
}
// Best Singleton Pattern:
enum Singleton { INSTANCE; public void doWork() { } }
```
- **EnumSet** → BitSet-backed; fastest for sets of enums. **EnumMap** → Array-backed; fastest for enum keys.
- **Keywords**: Use explicit code field for DB persistence (not ordinal); `@JsonValue`/`@JsonCreator` for Jackson; enum in switch is exhaustive (no default needed).

---

## 29. Java Concurrency *(Full)*

### Core Thread Concepts
- **Thread** → Smallest unit of execution inside a process; shares heap, has its own stack.
- **Process vs Thread** → Process = isolated memory + heavy; Thread = shared memory + lightweight.
- **Multithreading** → Running multiple threads concurrently in a single process to improve utilization.
- **Concurrency vs Parallelism** → Concurrency = managing multiple tasks; Parallelism = executing simultaneously on multiple cores.
- **Context Switching** → CPU switching between threads; saves/restores state (costly).
- **CPU Scheduling** → OS decides which thread runs (preemptive, priority-based).
- **Time Slicing** → CPU allocates fixed time slots to threads.
- **Thread Lifecycle** → New → Runnable → Running → Blocked/Waiting/Timed Waiting → Terminated.
- **User vs Daemon Threads** → Daemon = background (GC), JVM exits when only daemons remain.
- **Thread Priority** → Hint to scheduler (not guaranteed).
- **Thread ID/Naming** → Useful for debugging/logging.
### Thread Creation & Execution
- **Thread class** → Extend Thread, override `run()` (tight coupling).
- **Runnable** → Functional interface; preferred separation of task.
- **Callable** → Returns result + throws checked exceptions.
- **Future** → Represents async result (`get()` blocks).
- **FutureTask** → Wrapper combining Runnable + Future.
- **Executor** → Decouples task submission from execution.
- **ExecutorService** → Thread pool management (submit, shutdown).
- **ScheduledExecutorService** → Run tasks periodically/delayed.
- **ForkJoinPool** → Optimized for recursive divide-and-conquer tasks.
- **ThreadFactory** → Custom thread creation (naming, priority).
- **CompletableFuture** → Non-blocking async pipelines (`thenApply`, `thenCompose`).
- **Virtual Threads (Loom)** → Lightweight threads (millions possible).
- **Structured Concurrency** → Treat multiple tasks as a unit (better lifecycle control).
### Thread Coordination & Communication
- **wait()** → Releases lock, waits for notification.
- **notify() / notifyAll()** → Wakes waiting threads.
- **join()** → Wait for thread completion.
- **sleep()** → Pause thread (does NOT release lock).
- **yield()** → Hint scheduler to switch thread.
- **Inter-thread communication** → Shared state + signaling (wait/notify).
- **Guarded Blocks** → Wait until condition becomes true.
- **Producer-Consumer Pattern** → Decouple production/consumption via queue.
- **BlockingQueue** → Thread-safe queue with blocking ops.
- **SynchronousQueue** → Direct handoff (no capacity).
- **Exchanger** → Swap data between two threads.
- **Phaser** → Flexible multi-phase barrier.
- **CountDownLatch** → Wait for N events (one-time).
- **CyclicBarrier** → Reusable barrier for threads.
### Synchronization & Locks
- **synchronized** → Built-in locking (method/block level).
- **Intrinsic Locks / Monitor** → Every object has a monitor lock.
- **Reentrant Locks / ReentrantLock** → Explicit lock with advanced features (tryLock, fairness).
- **ReadWriteLock** → Multiple readers, single writer.
- **StampedLock** → Supports optimistic reads.
- **Fair vs Non-Fair Locks** → Fair = FIFO; Non-fair = better throughput.
- **Lock Contention** → Multiple threads competing → performance issue.
- **Deadlock** → Circular waiting.
- **Livelock** → Threads active but no progress.
- **Starvation** → Thread never gets CPU/resources.
- **Lock Striping** → Multiple locks for segments.
- **Lock Splitting** → Separate locks for different resources.
- **Spin Locks** → Busy waiting instead of blocking.
- **Optimistic Locking** → Assume no conflict, validate later.
- **Pessimistic Locking** → Lock before access.
### Memory Model & Visibility
- **Java Memory Model (JMM)** → Defines how threads interact with memory.
- **Happens-Before** → Guarantees visibility + ordering.
- **Visibility** → Changes by one thread visible to others.
- **Atomicity** → Operation completes fully or not at all.
- **Ordering** → Execution order constraints.
- **Reordering** → Compiler/CPU optimizations may reorder.
- **Cache Coherence** → Ensures consistent CPU caches.
- **CPU Cache** → Per-core memory causing visibility issues.
- **volatile** → Ensures visibility + ordering (no atomicity).
- **Safe Publication** → Proper sharing (final, volatile, synchronized).
- **Escape Analysis** → JVM optimization (stack allocation, lock removal).
### Atomic & Concurrent Utilities
- **Atomic Variables** → Lock-free thread-safe primitives.
- **AtomicInteger/Long/Boolean/Reference** → CAS-based updates.
- **CAS** → Compare expected vs actual → update if match.
- **LongAdder / LongAccumulator** → Better performance under contention.
- **Concurrent Collections**
  - ConcurrentHashMap → Segmented locking, Java8+ Bucket Level Lock
  - CopyOnWriteArrayList → safe for reads
  - ConcurrentLinkedQueue → lock-free
  - ConcurrentSkipListMap → sorted concurrent map
- **Blocking Queues**
  - ArrayBlockingQueue → bounded
  - LinkedBlockingQueue → optionally bounded
  - PriorityBlockingQueue → priority-based
  - DelayQueue → time-based scheduling
### Executors & Thread Pools
- **Fixed Thread Pool** → Fixed threads, queued tasks
- **Cached Thread Pool** → Dynamic threads
- **Single Thread Executor** → Sequential execution
- **Scheduled Thread Pool** → Periodic execution
- **Work Stealing Pool** → Uses ForkJoinPool
- **Thread Pool Sizing** → CPU-bound: cores; IO-bound: cores * (1 + wait/compute)
- **Thread Pool Tuning** → core size, max size, queue type
- **Task Queue** → Buffer for tasks
- **RejectedExecutionHandler** → Handles overload (Abort, CallerRuns, etc.)
- **Backpressure** → Control task submission rate
- **Fork/Join Framework** → Recursive parallelism
- **Work Stealing Algorithm** → Idle threads steal tasks
### Parallelism & Streams
- **Parallel Streams** → Use ForkJoinPool internally
- **stream().parallel()** → Enable parallel execution
- **Spliterator** → Splits data for parallelism
- **ForkJoin Tasks** → Recursive computation
- **RecursiveTask** → returns result
- **RecursiveAction** → no result
- **Divide & Conquer** → break into subtasks
- **Data Parallelism** → same operation on data
- **Task Parallelism** → different tasks
- **SIMD vs MIMD** → Single vs multiple instruction streams
### Concurrency Patterns
- **Thread Confinement** → Data confined to one thread
- **ThreadLocal** → Per-thread storage
- **Immutable Objects** → inherently thread-safe
- **Safe Initialization** → avoid partially constructed objects
- **Double Checked Locking (DCL)** → lazy init with volatile
- **Producer-Consumer** → decoupled processing
- **Reader-Writer** → multiple readers, single writer
- **Future Pattern** → async result placeholder
- **Promise Pattern** → explicit completion
- **Bulkhead Pattern** → isolate failures
- **Actor Model** → message passing (no shared state)
- **Reactive Streams** → async stream processing with backpressure
- **Event Loop** → single-threaded async processing
### Problems & Anti-Patterns
- **Coffman Conditions** → mutual exclusion + hold/wait + no preemption + circular wait
- **Race Condition** → outcome depends on timing
- **Data Race** → unsynchronized shared access
- **Visibility Issues** → stale data
- **Lost Updates** → overwrite without sync
- **False Sharing** → cache line contention
- **Priority Inversion** → low-priority blocking high-priority
- **Thread Leak** → threads not released
- **Blocking in Async** → defeats async benefits
- **Over-synchronization** → unnecessary locking
- **Under-synchronization** → unsafe access
### Debugging & Monitoring
- **Thread Dump** → snapshot of thread states
- **Deadlock Detection** → identify cycles
- **Profiling Tools** → analyze CPU/memory
- **JConsole / VisualVM** → JVM monitoring
- **JFR (Java Flight Recorder)** → low-overhead profiling
- **Mission Control** → visualize JFR data
- **Thread Analyzer** → thread behavior analysis
- **Stack Trace Analysis** → identify blocking/issues
### Testing Concurrent Code
- **Race Condition Testing** → simulate concurrency
- **Stress Testing** → high load
- **Load Testing** → realistic traffic
- **Concurrency Testing Tools** → jcstress etc.
- **Deterministic Testing** → control execution order
- **Awaitility** → async testing DSL
- **JUnit + Multithreading** → test concurrent logic
- **Thread Sanitizer** → detect data races (concept)
### JVM & Performance Internals
- **Thread Scheduling** → OS-managed
- **Green vs Native Threads** → JVM vs OS threads
- **Safepoints** → pause points for GC
- **Biased Locking** → optimized for single thread
- **Lightweight Locking** → CAS-based
- **Heavyweight Locking** → OS mutex
- **Lock Elision** → remove unnecessary locks
- **Lock Coarsening** → merge locks
- **GC Impact** → pauses affect threads
- **Stop-The-World (STW)** → all threads paused
### Reactive & Async Programming
- **Non-blocking IO** → async IO (NIO)
- **Async Programming** → tasks without blocking
- **Callback Hell** → nested callbacks
- **CompletableFuture Chains** → fluent async
- **Reactive Programming** → stream-based async
- **Backpressure** → control data flow
- **Publisher-Subscriber** → event-driven
- **Flow API** → Java reactive interfaces
- **Project Reactor / RxJava** → reactive frameworks
### Project Loom
- **Virtual Threads** → lightweight threads
- **Fiber** → concept similar to virtual threads
- **Continuations** → suspend/resume execution
- **Structured Concurrency** → scoped tasks
- **Scoped Values** → thread-local alternative
- **Carrier Threads** → OS threads backing virtual threads
- **Lightweight Threads** → low memory overhead
### System Design Keywords
- **Throughput vs Latency** → volume vs response time
- **Scalability** → handle growth
- **Horizontal vs Vertical Scaling** → add machines vs upgrade
- **Thread-per-request** → traditional model
- **Event-driven architecture** → async messaging
- **Async vs Sync** → non-blocking vs blocking
- **Rate Limiting** → control requests
- **Circuit Breaker** → fail fast
- **Bulkhead Isolation** → isolate failures
- **Work Queue Pattern** → task buffering
### Keywords (Interview Comparisons)
- **Happens-before** → lock, volatile, thread start/join
- **Visibility vs Atomicity vs Ordering** → JMM pillars
- **CAS vs Locks** → lock-free vs blocking
- **synchronized vs ReentrantLock** → simple vs flexible
- **volatile vs Atomic** → visibility vs atomic ops
- **Parallel Stream pitfalls** → overhead, shared state
- **Thread Pool sizing** → CPU vs IO formula
- **ForkJoin vs ExecutorService** → recursive vs general
- **Blocking vs Non-blocking** → wait vs async
- **CPU-bound vs IO-bound** → compute vs wait
### Edge & Niche Topics
- **False Sharing (Padding)** → avoid cache line conflict
- **Disruptor Pattern (LMAX)** → high-performance ring buffer
- **Mechanical Sympathy** → align with hardware
- **Off-Heap Memory** → outside JVM heap
- **Unsafe API** → low-level ops (dangerous)
- **VarHandle** → modern Unsafe alternative
- **Lock-Free Algorithms** → no locks, CAS-based
- **Wait-Free Algorithms** → guaranteed progress

---

## 30. Java Collections *(Full)*

### Core Collection Framework Concepts
- **Java Collections Framework (JCF)** → Unified architecture for storing/manipulating groups of objects (interfaces + implementations + algorithms).
- **Collection vs Collections vs Arrays**
  - Collection → root interface
  - Collections → utility class
  - Arrays → fixed-size utility class
- **Iterable Interface** → Enables `for-each` loop via `iterator()`
- **Iterator Pattern** → Sequential access without exposing structure
- **Container/Data Structure** → Holds elements (List, Set, Map)
- **Generics** → Type-safe collections (`List<String>`)
- **Type Safety** → Compile-time checks, avoids casting
- **Autoboxing/Unboxing** → primitive ↔ wrapper auto conversion
- **Covariance/Contravariance (PECS)** → Producer Extends, Consumer Super
- **Immutability** → Objects cannot change (thread-safe)
- **Fail-fast vs Fail-safe**
  - Fail-fast → throws `ConcurrentModificationException`
  - Fail-safe → works on copy (no exception)
- **Structural Modification** → add/remove elements
- **Concurrent Modification** → modification during iteration
### Core Interfaces Hierarchy
- **Iterable → Collection → (List, Set, Queue, Deque)**
- **Map** → separate hierarchy (key-value)
- **Sorted/Navigable**
  - SortedSet / NavigableSet → sorted sets
  - SortedMap / NavigableMap → sorted maps
### List Implementations
- **ArrayList** → dynamic array, fast random access, slow insert/delete (O(n))
- **LinkedList** → doubly linked list, fast insert/delete, slow access
- **Vector** → synchronized ArrayList (legacy)
- **Stack** → LIFO (legacy, use Deque)
- **Keywords**
  - Dynamic/Resizable array → grows automatically
  - Random vs Sequential access
  - Index-based operations
  - Capacity vs Size → internal vs actual elements
  - Growth factor → ~1.5x resize
  - Memory overhead → LinkedList higher
  - Node structure → prev + next
  - Legacy classes → Vector, Stack
### Set Implementations
- **HashSet** → no order, uses hashing
- **LinkedHashSet** → maintains insertion order
- **TreeSet** → sorted (Red-Black tree)
- **EnumSet** → optimized for enums
- **Keywords**
  - Uniqueness → no duplicates
  - Hashing → fast lookup
  - Load factor → resize threshold
  - Collision → same bucket
  - Chaining → linked list/tree
  - Ordering vs Sorting
  - Comparator vs Comparable
### Map Implementations
- **HashMap** → fast, unordered, allows 1 null key
- **LinkedHashMap** → insertion/access order (LRU)
- **TreeMap** → sorted (log n)
- **Hashtable** → synchronized (legacy)
- **ConcurrentHashMap** → thread-safe, high concurrency
- **WeakHashMap** → GC removes weak keys
- **IdentityHashMap** → uses `==` instead of equals
- **EnumMap** → enum keys optimized
- **Keywords**
  - Key-value pairs (Map.Entry)
  - Hash bucket → storage unit
  - Collision resolution → chaining/tree
  - Rehashing → resize + redistribute
  - Load factor → default 0.75
  - Capacity → power of 2 (bitwise optimization)
  - Treeification → convert to tree (threshold 8)
  - Red-Black Tree → balanced BST
  - Access vs Insertion order
  - LRU Cache → LinkedHashMap
  - Null rules → Only HashMap allows
### Queue & Deque Implementations
- **PriorityQueue** → heap-based ordering
- **ArrayDeque** → faster than Stack/LinkedList
- **LinkedList** → supports Queue/Deque
- **Blocking Queues**
  - ArrayBlockingQueue → bounded
  - LinkedBlockingQueue → optionally bounded
  - PriorityBlockingQueue → priority-based
  - DelayQueue → delayed elements
  - SynchronousQueue → direct handoff
- **Keywords**
  - FIFO / LIFO
  - Heap → min/max
  - Comparator ordering
  - Deque → double-ended
  - Circular array
  - Bounded vs Unbounded
### Iteration Mechanisms
- **Iterator** → forward iteration
- **ListIterator** → bidirectional
- **Enumeration** → legacy
- **for-each** → syntactic sugar
- **Spliterator** → supports parallelism
- **Stream API** → functional iteration
- **Keywords**
  - Fail-fast behavior
  - ConcurrentModificationException
  - remove() safe usage
  - Lazy vs Parallel iteration
### Synchronization & Thread Safety
- **Synchronized Collections** → via `Collections.synchronizedX`
- **Concurrent Collections** → better scalability
- **ConcurrentHashMap** → lock striping / bucket-level locking
- **CopyOnWriteArrayList/Set** → safe for reads
- **Keywords**
  - Thread safety
  - Locking granularity
  - Lock-free reads
  - Copy-on-write
  - Weakly consistent iterators
### Internal Mechanics
- **HashMap Internals******
  - Hash function → spreads keys
  - Index → `(n-1) & hash`
  - Buckets → array of bins
  - Node vs TreeNode
  - Treeify at ≥ 8, untreeify ≤ 6
  - Resize threshold → capacity * load factor
  - Bitwise ops → fast index calc
- **TreeMap Internals****
  - Red-Black Tree → self-balancing
  - Properties → no two red adjacent, equal black height
  - Rotations → left/right
  - Complexity → O(log n)
- **ArrayList Internals**
  - Backing array
  - Resize via `Arrays.copyOf`
  - Fast access, slow resize
### Performance & Big-O
- **ArrayList** → get O(1), add amortized O(1), remove O(n)
- **LinkedList** → access O(n), insert O(1)
- **HashMap** → O(1) avg, O(log n) worst (tree)
- **TreeMap** → O(log n)
- **Concepts**
  - Amortized cost
  - Cache locality (arrays better)
  - Memory footprint
  - Trade-offs → ArrayList vs LinkedList
### Sorting & Searching
- **Collections.sort / List.sort** → uses TimSort
- **Arrays.sort** → dual-pivot quicksort / merge sort
- **Binary Search** → O(log n)
- **Keywords**
  - Stable sort
  - Comparator vs Comparable
  - Multi-level sorting
  - Natural vs Custom order
### Utility Class (Collections)
- unmodifiableList → immutable view
- emptyList / singletonList → optimized
- reverse / shuffle → utility ops
- frequency / min / max
- **Concepts**
  - Immutable collections
  - Wrapper classes
  - Defensive copying
### Streams & Collections
- **Stream API** → functional processing
- map/filter/reduce → core ops
- Collectors → toList, groupingBy
- **Keywords**
  - Lazy evaluation
  - Parallel streams
  - Side effects (avoid)
  - Intermediate vs Terminal ops
### Advanced & Niche Collections
- **Guava / Apache Commons** → extended utilities
- **Immutable Collections** → `List.of()`
- **Persistent Collections** → immutable data structures
- **MultiMap** → multiple values per key
- **BiMap** → bidirectional map
### Pitfalls & Anti-Patterns
- Mutable keys in HashMap → breaks lookup
- Incorrect equals/hashCode → bugs
- Memory leaks → unbounded collections
- ConcurrentModificationException
- Overuse of synchronized collections
- Wrong DS choice → performance issues
- Null handling pitfalls
- Modifying during iteration
### Testing & Debugging
- Unit tests for edge cases
- Test null, empty, duplicates
- Large dataset testing
- Memory profiling
- Debug hash collisions
### Design & Usage Patterns
- **LRU Cache** → LinkedHashMap
- **Frequency counting** → Map
- **Lookup tables** → HashMap
- **Indexing** → Map/List
- **Graph (Adjacency List)** → Map<List>
- **Deduplication** → Set
- **Top-K** → Heap (PriorityQueue)
- **Sliding window** → Queue/Deque
### Interview Deep-Dive Keywords
- HashMap vs ConcurrentHashMap → locking vs lock-free reads
- ArrayList vs LinkedList → access vs insert tradeoff
- HashSet vs TreeSet → unordered vs sorted
- Fail-fast vs Fail-safe
- Comparable vs Comparator
- Why power of 2 capacity → bit masking
- Load factor → memory vs performance
- Treeification (Java 8) → improves worst-case
- HashMap put/get flow → hash → index → bucket → compare
- Why Map not Collection → key-value structure
### Java Version Enhancements
- **Java 8** → Streams integration
- **Java 9** → `List.of()` immutable collections
- **Java 10+** → unmodifiable collectors
- **Java 21** → optimized for modern concurrency (virtual threads context)

---

## 31. Java IO & NIO *(Full)*


### Core I/O Concepts
- **Input / Output (I/O)** → Reading/writing data between program and external sources (files, network).
- **Stream vs Channel**
  - Stream → sequential, blocking, one-way
  - Channel → bidirectional, buffer-based, can be non-blocking
- **Blocking vs Non-blocking I/O**
  - Blocking → thread waits
  - Non-blocking → thread continues, checks later
- **Synchronous vs Asynchronous**
  - Sync → caller waits
  - Async → callback/future later
- **Byte vs Character Streams**
  - Byte → raw data
  - Character → text (Unicode)
- **Buffering** → Temporary storage to reduce I/O calls
- **Encoding/Decoding** → bytes ↔ characters
- **Charset** → encoding standard (UTF-8 etc.)
- **Endianness** → byte order (Big/Little endian)
- **File descriptors** → OS-level handle to file/socket
- **Resource management** → must close streams
- **Try-with-resources** → auto close (implements AutoCloseable)
### java.io Stream Hierarchy
- **InputStream / OutputStream** → byte streams
- **Reader / Writer** → character streams
- **Keywords**
  - Byte vs Character streams
  - Abstract base classes
  - Decorator Pattern → wrap streams
  - Filter Streams → add functionality
  - Chaining → combine multiple streams
### Byte Streams (java.io)
- `FileInputStream` / `FileOutputStream` → file bytes
- `BufferedInputStream` / `BufferedOutputStream` → faster I/O
- `ByteArrayInputStream` / Output → memory-based
- `DataInputStream` / Output → primitives read/write
- `ObjectInputStream` / Output → serialization
- `SequenceInputStream` → multiple streams combined
- `PushbackInputStream` → unread bytes
- **Keywords**
  - Raw binary data
  - Serialization streams
  - Primitive read/write
  - Buffering improves performance
### Character Streams (java.io)
- `FileReader` / `FileWriter` → text files
- `BufferedReader` / `BufferedWriter` → efficient text
- `InputStreamReader` / `OutputStreamWriter` → bridge (byte ↔ char)
- `PrintWriter` → formatted output
- `CharArrayReader/Writer`, `StringReader/Writer` → in-memory
- **Keywords**
  - Unicode support
  - Charset conversion
  - Line-based reading (`readLine`)
  - Text processing
### File Handling (java.io)
- `File` → abstraction for file/directory
- Path → location (absolute/relative)
- Metadata → size, lastModified
- Permissions → read/write/execute
- Directory ops → list/create/delete
- **Keywords**
  - `exists()`, `createNewFile()`
  - `mkdir()`, `mkdirs()`
  - `listFiles()`
  - File separator (`/` vs `\`)
  - Hidden/temp files
### Serialization & Deserialization
- **Serialization** → object → byte stream
- **Serializable** → marker interface
- **Externalizable** → custom control
- **Object graph** → entire object tree
- **transient** → skip field
- **SerialVersionUID** → version control
- **Keywords**
  - Security risks (deserialization attacks)
  - Custom methods → `writeObject/readObject`
  - Deep copy via serialization
### Performance & Buffering
- Buffered vs Unbuffered → fewer syscalls
- Buffer size tuning → affects performance
- Throughput vs Latency trade-off
- Disk I/O vs Memory I/O → disk slower
- Zero-copy → avoid user-space copying
### NIO Core Concepts (java.nio)
- **NIO** → non-blocking, scalable I/O
- **Channel** → connection to data source
- **Buffer** → data container
- **Selector** → multiplex multiple channels
- **Multiplexing** → single thread handles many channels
### Buffers (java.nio)
- `ByteBuffer`, `CharBuffer`, etc.
- **Core Concepts**
  - Capacity → total size
  - Position → current index
  - Limit → max readable/writable
  - Mark → saved position
- **Operations**
  - flip() → write → read
  - clear() → reset
  - rewind() → re-read
- **Types**
  - Direct buffer → off-heap (fast I/O)
  - Heap buffer → JVM memory
### Channels (java.nio.channels)
- `FileChannel` → file I/O
- `SocketChannel` → TCP client
- `ServerSocketChannel` → TCP server
- `DatagramChannel` → UDP
- `Pipe` → thread communication
- **Keywords**
  - Read/write operations
  - Scattering reads → multiple buffers
  - Gathering writes → combine buffers
  - transferTo/From → zero-copy
  - Close channel properly
### Selectors (Multiplexing)
- `Selector` → monitors multiple channels
- `SelectionKey` → channel registration
- **Events**
  - OP_READ, OP_WRITE, OP_ACCEPT, OP_CONNECT
- **Concepts**
  - Non-blocking multiplexing
  - Event-driven loop
  - Reactor pattern
### Networking (NIO)
- TCP → reliable
- UDP → fast, unreliable
- **Keywords**
  - SocketChannel vs Socket
  - ServerSocketChannel vs ServerSocket
  - DatagramChannel → UDP
### (java.nio.file) – Modern File API
- `Path`, `Paths` → file path abstraction
- `Files` → utility operations
- `FileSystem` → underlying FS
- **Keywords**
  - Copy, move, delete
  - Atomic operations
  - Symbolic/Hard links
### File Operations (NIO.2)
- `Files.copy/move/delete/exists`
- `Files.readAllLines/write`
- **Keywords**
  - StandardCopyOption
  - File attributes
  - Permissions
  - Temp files
  - Recursive operations
### File Walking & Traversal
- `Files.walk` → stream traversal
- `Files.walkFileTree` → visitor pattern
- `FileVisitor` → custom traversal
  **Keywords**
  - DFS traversal
  - Pre/post directory visit
  - Large directory handling
### Watch Service (File Monitoring)
- `WatchService`, `WatchKey`, `WatchEvent`
- **Keywords**
  - File system events
  - Directory monitoring
  - Polling vs event-driven
### Asynchronous I/O (NIO.2)
- `AsynchronousFileChannel`
- `AsynchronousSocketChannel`
- `AsynchronousServerSocketChannel`
- **Keywords**
  - Callback (CompletionHandler)
  - Future-based async
  - True async non-blocking
### Memory-Mapped Files
- `MappedByteBuffer`
- `FileChannel.map()`
- **Keywords**
  - OS-level mapping
  - Large file handling
  - Zero-copy optimization
### Charset & Encoding
- `Charset`, `StandardCharsets`
- **Keywords**
  - UTF-8, UTF-16
  - Encoding errors
  - Character conversion
### Pitfalls & Anti-Patterns
- Not closing streams → leaks
- Mixing byte/char incorrectly
- Blocking I/O in scalable systems
- Charset mismatch
- Serialization vulnerabilities
- Loading large files fully
- Wrong buffer handling
### Testing & Debugging
- Mock file I/O
- Use temp directories
- Detect leaks
- Profile I/O performance
### Design Patterns & Architectures
- **Reactor Pattern** → Selector-based
- **Proactor Pattern** → async I/O
- **Pipeline Pattern** → staged processing
- **Decorator Pattern** → stream chaining
- **Adapter Pattern** → Reader/Writer bridges
### Integration & Use Cases
- File processing (CSV/logs)
- Network servers
- Streaming large files
- ETL pipelines
- Log aggregation
- File upload/download
### Interview Deep-Dive Keywords
- IO vs NIO vs NIO.2 → blocking vs non-blocking vs async
- Channel vs Stream → buffer vs sequential
- Buffer lifecycle → flip/clear
- Selector working → event loop
- Zero-copy → OS-level transfer
- Memory-mapped pros/cons
- Serialization risks
- When to use NIO → high concurrency
### JVM & OS Interaction
- OS-level I/O → system calls
- Kernel vs User space
- File descriptors → OS handles
- Page cache → OS caching
- Direct vs Heap buffer
### Advanced & Niche Topics
- Zero-copy (`sendfile`)
- Netty → NIO-based framework
- Reactive I/O → async streams
- Backpressure → control flow
- Off-heap memory
- Unsafe / VarHandle → low-level ops

---

## 32. Java Internals & Advanced Topics

### ClassLoading Deep Dive
- **Loading** → Read `.class` bytecode; create `Class` object in method area.
- **Linking** → Verify (bytecode correctness) → Prepare (allocate static fields, assign defaults: 0/null/false) → Resolve (replace symbolic refs with direct refs).
- **Initialization** → Execute `<clinit>` static initializer; run static blocks in textual order.
- **Class Lifecycle** → Load → Verify → Prepare → Resolve → Initialize → Use → Unload.
- **Initialization Order**
  1. Parent static fields/blocks (first time class loaded)
  2. Child static fields/blocks
  3. Parent instance fields/blocks
  4. Parent constructor
  5. Child instance fields/blocks
  6. Child constructor
- **Keywords**
  - `Class.forName(name, initialize, loader)` → control initialization trigger
  - Custom ClassLoader for hot-deploy, plugin isolation
  - OSGi → advanced class isolation (bundle-level loaders)
  - `ClassCircularityError` → circular class dependency at load time

### equals() and hashCode() Contract
- `a.equals(b)` = true → `a.hashCode() == b.hashCode()` must be true.
- `a.hashCode() != b.hashCode()` → `a.equals(b)` must be false.
- **Reflexive** → `a.equals(a)` = true.
- **Symmetric** → `a.equals(b)` ↔ `b.equals(a)`.
- **Transitive** → `a=b` and `b=c` → `a=c`.
- **Consistent** → same result if no field changes.
- **Null-safe** → `a.equals(null)` = false (no NPE).
- **Implementation** → `Objects.equals(f1, o.f1)` and `Objects.hash(f1, f2)` for null-safe, readable code.
- **Keywords**: Breaking contract breaks `HashMap`/`HashSet`; Lombok `@EqualsAndHashCode`; `@Override` both or neither.

### Service Provider Interface (SPI)
- **SPI** → Define interface; implementations discovered at runtime by `ServiceLoader`; no compile-time coupling.
- **Registration** (classic) → `META-INF/services/com.example.MyInterface` file containing FQN of each impl.
- **Registration** (JPMS) → `provides com.example.MyInterface with com.example.impl.MyImpl` in `module-info.java`.
- `ServiceLoader<Plugin> loader = ServiceLoader.load(Plugin.class)` → lazy iterator over all impls.
- **Use cases** → JDBC drivers (`java.sql.Driver`), logging backends (SLF4J), `java.nio.file.spi.FileSystemProvider`, crypto providers.
- **Keywords**: Plugin architecture; hot-pluggable implementations; no static binding.

### Java Agent & Instrumentation
- **Java Agent** → JAR loaded before/alongside app via `-javaagent:agent.jar=args`.
- `premain(String agentArgs, Instrumentation inst)` → called before `main()`; static attach.
- `agentmain(String agentArgs, Instrumentation inst)` → dynamic attach via Attach API at runtime.
- **`Instrumentation` API**
  - `addTransformer(ClassFileTransformer)` → intercept/modify bytecode at class load time.
  - `retransformClasses(Class<?>...)` → re-instrument already-loaded classes.
  - `getObjectSize(obj)` → object size in bytes.
- **Use cases** → APM agents (Datadog, New Relic, Elastic), JaCoCo coverage, Lombok, profilers, distributed tracing.
- **Keywords**: ASM or Byte Buddy for bytecode manipulation; `-XX:+EnableDynamicAgentLoading` required in Java 21+.

### Varargs
- `void log(String fmt, Object... args)` → varargs = syntactic sugar for array; must be last parameter.
- Called as: `log("val={}", x)` or `log("val={}", new Object[]{x})`.
- `@SafeVarargs` → suppress heap pollution warning for generic varargs.
- **Keywords**: Fixed-arity overload preferred over varargs by compiler; varargs matched last in resolution.

### Static Imports
- `import static java.lang.Math.PI; import static java.util.Collections.*;`
- Used unqualified: `double c = 2 * PI * r; sort(list);`
- **Keywords**: Good for constants and test assertions (`import static org.junit.jupiter.api.Assertions.*`); overuse hurts readability.

### String Interning & Pool Deep Dive
- String pool since Java 7 in heap (not PermGen); GC can collect pool entries when unreachable.
- `String.intern()` → add to pool; return pooled reference; useful for memory reduction at scale.
- Pool size tunable: `-XX:StringTableSize=131072` (power of 2 or prime; default 65536 in Java 11+).
- G1 String Deduplication: `-XX:+UseStringDeduplication` → deduplicates identical `char[]`/`byte[]` arrays in heap.
- **Keywords**: Pool prevents GC only while referenced; heavy interning = large pool; profile before applying.

### Comparable vs Comparator (Deep Dive)
- **Comparable** → natural ordering embedded in class; `compareTo` called by `Collections.sort`, `TreeSet`, `PriorityQueue`.
- **Comparator** → external, composable, reusable; `Comparator.comparing(Person::getAge).thenComparing(Person::getName).reversed()`.
- **Contract** → `compareTo` must be consistent with `equals` for sorted collections to work correctly (TreeSet uses compareTo, not equals).
- **Keywords**: `Integer.compare(a,b)` not `a-b` (overflow); `Comparator.nullsFirst/Last`; `naturalOrder()/reverseOrder()`.

### Immutable Class Design
- `private final` all fields. No setters. `final` class (prevent subclass breaking immutability).
- **Defensive copy** → copy mutable inputs in constructor; copy mutable outputs in getters.
- **Constructor validation** → throw early on invalid state.
- Examples → `String`, `Integer`, `LocalDate`, `BigDecimal`, Java Records.
- **Keywords**: Thread-safe without synchronization; share freely; key for value objects and keys in Maps.

### ThreadLocal (Deep Dive)
- `ThreadLocal<T>` → each thread has its own independent copy of value.
- `set(val)` → store for current thread. `get()` → retrieve for current thread. `remove()` → delete (critical in thread pools!).
- **Use cases** → per-request context (user session, transaction ID, `DateFormat` instance, DB connection).
- **InheritableThreadLocal** → child threads inherit parent thread's value.
- **Memory leak risk** → thread pool reuses threads; old value retained if `remove()` not called.
- **Keywords**: Never `remove()` after use = leak in Tomcat/Spring; ScopedValue (Java 21) = safer immutable alternative.

### Reflection Performance & Alternatives
- `Method.invoke()` ~10–100x slower than direct call due to: security checks, argument wrapping/unwrapping, no JIT inlining.
- **Optimization** → cache `Method`/`Field` objects; call `setAccessible(true)` once; use `MethodHandle` (faster, JIT-friendly).
- **MethodHandle** → `java.lang.invoke`; nearly as fast as direct call; JIT can inline.
- **VarHandle** → typed `MethodHandle` for field access; supports atomic ops (`compareAndSet`, `getAndAdd`).
- **LambdaMetafactory** → generate lambda at runtime; extremely fast functional interface creation.
- **Keywords**: `java.lang.invoke` package; invokedynamic bytecode instruction; basis of lambda implementation.

### Java Memory Model — Advanced
- **Happens-before chain** → `unlock→lock`, `volatile write→read`, `thread.start()→thread.run()`, `thread.join()→after join()`, `static initializer→first use`.
- **Data Race** → two threads access same variable unsynchronized, at least one writes → undefined behavior in JMM.
- **Sequential Consistency** → no data races → program behaves as if all ops happen in some sequential order.
- **Out-of-thin-air reads** → JMM prohibits values appearing from nowhere (causality requirement).
- **Keywords**: `volatile` = visibility + ordering only (not atomicity); `synchronized` = mutual exclusion + visibility + ordering.

### Lock-Free Structures Internals
- **CAS (Compare-And-Swap)** → atomic: if `mem == expected` then `mem = newVal`; else retry.
- `AtomicInteger.compareAndSet(expected, update)` → single CAS instruction (x86 `CMPXCHG`).
- **ABA Problem** → value changes A→B→A; CAS sees A and succeeds incorrectly. Fix: `AtomicStampedReference` (version tag).
- **Keywords**: CAS = optimistic concurrency; spin loop on failure; `LongAdder` better than `AtomicLong` under high contention (cell striping).

### JVM Bytecode & Class File
- `.class` file structure: magic (`0xCAFEBABE`), minor/major version, constant pool, access flags, this/super class, interfaces, fields, methods, attributes.
- **Bytecode instructions** → `iload`, `istore`, `invokevirtual`, `invokestatic`, `invokespecial`, `invokedynamic`, `new`, `dup`, `areturn`.
- **invokedynamic** → enables lambda, method handles; bootstrap method resolves call site at first invocation.
- `javap -c MyClass.class` → disassemble bytecode.
- **Keywords**: Major version: Java 8 = 52, Java 11 = 55, Java 17 = 61, Java 21 = 65.

---

## 33. Java Interview Master Keywords

### Comprehensive Comparison Table

| Pair | A | B |
|---|---|---|
| `==` vs `.equals()` | Reference equality | Content equality |
| Abstract class vs Interface | State + partial impl + single inheritance | Contract + multiple + no state |
| Checked vs Unchecked exception | Compile-time enforced | Runtime; programmer error |
| `throw` vs `throws` | Throw instance (statement) | Declare on method (clause) |
| StringBuilder vs StringBuffer | Not thread-safe; fast | Thread-safe (synchronized); slow |
| `String.trim()` vs `strip()` | ASCII whitespace only | Unicode whitespace (Java 11) |
| ArrayList vs LinkedList | O(1) random access; O(n) insert | O(1) insert at node; O(n) access |
| HashMap vs TreeMap | O(1) avg unordered | O(log n) sorted |
| HashMap vs LinkedHashMap | Unordered | Insertion order preserved |
| HashMap vs ConcurrentHashMap | Not thread-safe | Bucket-level lock; lock-free reads |
| HashSet vs LinkedHashSet vs TreeSet | Unordered | Insertion order | Sorted |
| fail-fast vs fail-safe | CME thrown on structural change | Copy-based; no exception |
| `final` vs `finally` vs `finalize` | Modifier (var/method/class) | Cleanup block | Pre-GC method (deprecated) |
| Overloading vs Overriding | Compile-time polymorphism | Runtime polymorphism |
| Stack vs Heap | Per-thread; frames; fast | Shared; objects; GC managed |
| Shallow vs Deep copy | Copy references | Copy entire object graph |
| Serializable vs Externalizable | Auto (marker interface) | Custom readExternal/writeExternal |
| `volatile` vs `synchronized` | Visibility + ordering only | Visibility + atomicity + mutual exclusion |
| `synchronized` vs `ReentrantLock` | Simple; built-in | Flexible: tryLock, fairness, conditions |
| `wait()` vs `sleep()` | Releases monitor; must hold lock | Does NOT release lock |
| Runnable vs Callable | void run(); no exception | V call(); throws checked exceptions |
| Future vs CompletableFuture | Blocking `get()` | Async chaining; callbacks; non-blocking |
| Thread vs Virtual Thread | OS-managed; ~1MB stack; expensive | JVM-managed; ~few KB; millions possible |
| Comparable vs Comparator | Natural order inside class | External; composable; multiple orderings |
| `List.of()` vs `unmodifiableList()` | Truly immutable (NPE on null) | Unmodifiable view (original can change) |
| `Arrays.asList()` vs `List.of()` | Fixed-size; allows null; set OK | Immutable; no null; no set |
| DOM vs SAX vs StAX | In-memory tree | Event push-based | Pull-based streaming |
| IO vs NIO vs NIO.2 | Blocking stream | Non-blocking channel+buffer | Async + modern file API |
| `Path` vs `File` | Modern; immutable; operations via `Files` | Legacy; mutable state |
| JDK vs JRE vs JVM | Dev tools + runtime | Runtime only | Execution engine |
| GC Parallel vs G1 vs ZGC | Throughput-focused | Balanced; predictable pauses | Ultra-low latency (<10ms) |
| CAS vs synchronized | Lock-free; optimistic; spin | Blocking; pessimistic; OS thread wait |
| `HashMap.get()` null | Key absent OR value is null (use `containsKey`) | N/A |
| `ConcurrentHashMap` null | NPE — null keys/values NOT allowed | vs HashMap: null key/value allowed |
| Static nested vs Inner class | No outer ref; safe | Holds outer ref; memory leak risk |
| `@Override` purpose | Compile-time check; catches typos | Without it: silent new method, not override |

### JMM Pillars
- **Atomicity** → Operation indivisible (read/write of `long`/`double` NOT atomic without `volatile` on 32-bit JVM).
- **Visibility** → Changes propagated to all threads; broken by CPU caches without `volatile`/`synchronized`.
- **Ordering** → Execution order guarantees; compiler/CPU may reorder without sync.
- **Happens-before sources** → `unlock → lock`, `volatile write → volatile read`, `thread.start()`, `thread.join()`, `Object.<init>` (constructor completes before field visible via `final`).

### JVM Tuning Cheat Sheet

| Flag | Purpose |
|---|---|
| `-Xms256m` / `-Xmx4g` | Initial / max heap size |
| `-Xss512k` | Thread stack size |
| `-XX:MaxMetaspaceSize=256m` | Metaspace cap |
| `-XX:+UseG1GC` | Use G1 collector |
| `-XX:+UseZGC` | Use ZGC (low latency) |
| `-XX:MaxGCPauseMillis=200` | G1 pause time goal (soft) |
| `-Xlog:gc*` | GC logging (Java 9+) |
| `-XX:+HeapDumpOnOutOfMemoryError` | Heap dump on OOM |
| `-XX:+PrintCompilation` | JIT compilation events |
| `-XX:+UseStringDeduplication` | G1 dedup identical strings |
| `-XX:StringTableSize=131072` | String pool table size |
| `-XX:+EnableDynamicAgentLoading` | Allow runtime agent attach (Java 21+) |

### Big-O Quick Reference

| Structure | Access | Insert/Delete | Contains | Notes |
|---|---|---|---|---|
| ArrayList | O(1) | O(n) | O(n) | Amortized O(1) add-at-end |
| LinkedList | O(n) | O(1) at node | O(n) | Better as Deque than List |
| HashMap/HashSet | O(1) avg | O(1) avg | O(1) avg | O(log n) worst-case (tree bucket) |
| TreeMap/TreeSet | O(log n) | O(log n) | O(log n) | Red-Black tree; sorted |
| PriorityQueue | O(n) | O(log n) | O(n) | peek = O(1); poll = O(log n) |
| ArrayDeque | O(1) | O(1) amort | O(n) | Better than Stack + LinkedList |
| String (contains) | — | — | O(n×m) | Naive; use regex or specialized |

### Common Gotchas & Traps
- `Integer` `==` comparison true for -128..127 (cache), false outside range → always use `.equals()`.
- `ConcurrentHashMap` → null key/value throws NPE (unlike HashMap).
- `Arrays.asList()` → fixed-size List; `add`/`remove` throw `UnsupportedOperationException`.
- `Collections.unmodifiableList(list)` → mutation of original list still visible through the view.
- `HashMap.get()` returning `null` → ambiguous: key absent OR value is null; use `containsKey()` to distinguish.
- `String +` in loop → potentially O(n²); use `StringBuilder`.
- `Thread.sleep()` does NOT release lock; `wait()` does release lock.
- `static synchronized method` → locks the `Class` object. `synchronized instance method` → locks `this`.
- `int` overflow wraps silently; use `Math.addExact()` / `Math.multiplyExact()` to detect.
- Enhanced-for loop + `list.remove()` → `ConcurrentModificationException`; use `iterator.remove()` or `removeIf()`.
- Unboxing `null` `Integer` → `NullPointerException`.
- Recursive `toString()` in `LinkedList`-like classes → `StackOverflowError`.
- `finalize()` not guaranteed to run; never rely on it for resource cleanup.
- `Optional.get()` without `isPresent()` check → `NoSuchElementException`.
- Catching `Exception` broadly and swallowing it silently hides real bugs.

### Commonly Tested Algorithms & DS (Java Context)
- **Two pointers** → `int[]` or `List`; move from both ends.
- **Sliding window** → `ArrayDeque` (monotonic) or two pointers with `HashMap<char, count>`.
- **Frequency map** → `Map<T, Integer>` with `getOrDefault(k, 0) + 1` or `merge(k, 1, Integer::sum)`.
- **Top-K** → `PriorityQueue` min-heap of size K; `O(n log k)`.
- **Graph BFS/DFS** → `Map<Node, List<Node>>` adjacency list; `ArrayDeque` for BFS queue; `Set` for visited.
- **LRU Cache** → `LinkedHashMap` with `removeEldestEntry` override; or `LinkedHashMap(cap, 0.75f, true)`.
- **Trie** → `Map<Character, TrieNode>` per node.
- **Union-Find** → `int[] parent`; `find` with path compression; `union` with rank.

### Design Interview Keywords
- **Thread-safe Singleton** → Enum singleton (best); DCL with `volatile`; Holder idiom (static nested class).
- **Immutable value object** → `private final` fields; no setters; defensive copy; `final` class → use Records in Java 16+.
- **Producer-Consumer** → `LinkedBlockingQueue`; producers `put()`; consumers `take()`; sizes pool threads.
- **Connection Pool** → Fixed `ExecutorService` or dedicated pool (HikariCP); `maximumPoolSize` tuned to DB.
- **Cache** → `ConcurrentHashMap` + `computeIfAbsent`; or `LinkedHashMap` for LRU; or Caffeine/Guava Cache.
- **Event Bus** → `ExecutorService` + observer list; or Guava EventBus; or reactive `Flux`/`Observable`.

---

*End — Java Complete Interview Reference (Full Edition)*


---


---

## 34. Core DSA Concepts
##### Complexity Analysis
- **Big-O** → Upper bound; worst case; e.g. O(n log n) for merge sort
- **Big-Theta** → Tight bound; both upper and lower; e.g. Θ(n²) for bubble sort
- **Big-Omega** → Lower bound; best case; e.g. Ω(n) for any comparison sort
- **Amortized Analysis** → Average cost per operation over a sequence; e.g. ArrayList resize is O(1) amortized
- **Asymptotic Analysis** → Behavior as n→∞; ignore constants and low-order terms
- **Best / Average / Worst Case** → QuickSort: O(n log n) avg, O(n²) worst
- **In-place** → O(1) extra space; sorts data within original array (QuickSort, HeapSort)
- **Out-of-place** → Needs extra space (MergeSort: O(n))
- **Stable** → Equal elements maintain original order (MergeSort, TimSort)
- **Unstable** → May reorder equals (QuickSort, HeapSort)
- **Deterministic vs Randomized** → Randomized QuickSort avoids worst-case O(n²)
- **Trade-offs** → Time vs Space; simplicity vs performance; read-heavy vs write-heavy
##### Interview Deep-Dive Keywords
- Always state complexity before/after optimization
- Big-O is for upper bound — don't confuse with tight bound
- Amortized ≠ average-case; amortized guarantees sequence cost
- Space complexity includes call stack (recursion adds O(depth))

---

## 35. Arrays & Strings
##### Core Concepts
- **Array** → Contiguous memory; O(1) random access; O(n) insert/delete middle
- **Dynamic Array** → Resizable (ArrayList); amortized O(1) append; doubles capacity on resize
- **1D / 2D Arrays** → 2D: row-major storage; `arr[i][j]` → offset `i*cols + j`
- **Jagged Arrays** → Array of arrays; rows have different lengths
- **Strings (immutable)** → Java strings are immutable; `+` in loop → O(n²); use StringBuilder
- **StringBuilder** → Mutable; O(1) amortized append; not thread-safe
- **StringBuffer** → Thread-safe StringBuilder; use only when needed
##### Key Techniques
- **Two Pointers** → Left/right converge; O(n); used for pair sum, palindrome, container with most water
- **Sliding Window** → Fixed or variable window; O(n); max subarray sum, longest substring without repeat
- **Prefix Sum** → `prefix[i] = prefix[i-1] + arr[i]`; range sum query in O(1) after O(n) build
- **Suffix Sum** → From right; used with prefix for subarray problems
- **Kadane's Algorithm** → Max subarray sum; O(n); DP-style: `maxEndingHere = max(arr[i], maxEndingHere + arr[i])`
- **Subarray vs Subsequence** → Subarray: contiguous; Subsequence: not necessarily contiguous
- **Rotation** → Rotate by k: reverse full, reverse [0..k-1], reverse [k..n-1]
- **Partitioning** → In-place splitting around pivot
- **Dutch National Flag** → 3-way partition; O(n); sort array with 0s, 1s, 2s
- **Hashing for strings** → HashMap for frequency count, anagram check, two-sum
- **Rabin-Karp** → Rolling hash for pattern matching; O(n+m) avg
##### Interview Deep-Dive Keywords
- Two pointers only works on sorted arrays for pair-sum; otherwise use HashMap
- Sliding window: distinguish fixed vs variable; variable needs condition to shrink
- Prefix sum: precompute once, query many → amortize cost
- Dutch National Flag: 3 pointers (low, mid, high); swap-based
- StringBuilder in Java: use for string concatenation in loops

---

## 36. Linked Lists
##### Core Concepts
- **Singly Linked List** → Node has `data` + `next`; O(n) access; O(1) insert at head
- **Doubly Linked List** → Node has `prev` + `next`; O(1) delete given node; more space
- **Circular Linked List** → Tail points to head; used in round-robin scheduling
##### Key Techniques
- **Fast & Slow Pointers (Floyd's Cycle)** → Fast moves 2x; slow moves 1x; meet inside cycle
- **Cycle Detection** → Floyd's: O(n) time, O(1) space; detect + find cycle start
- **Reverse Linked List** → Iterative: 3 pointers (prev, curr, next); O(n) time O(1) space
- **Merge Two Sorted Lists** → Compare heads; recursion or iteration; O(m+n)
- **Middle Node** → Fast/slow pointers; slow is at middle when fast reaches end
- **Intersection** → Two pointers; switch heads when reaching null; meet at intersection
- **Dummy Node Technique** → Dummy head simplifies edge cases (empty list, head deletion)
- **In-place Reversal** → No extra list; reverse within groups (e.g. reverse k-group)
##### Interview Deep-Dive Keywords
- Dummy node pattern: always use for simplifying linked list problems with head changes
- Floyd's cycle: meeting point ≠ cycle start; need second pass to find cycle entry
- Reverse in groups: maintain prev, curr, tail pointers per group
- Java LinkedList: doubly linked; use ArrayDeque for stack/queue (faster)

---

## 37. Stack
##### Core Concepts
- **LIFO** → Last In First Out; push/pop/peek all O(1)
- **Stack Implementation** → Array-based (fixed size) or LinkedList-based (dynamic)
- **Call Stack** → JVM stack; each method call adds frame; stack overflow on deep recursion
##### Key Techniques
- **Monotonic Stack** → Stack maintaining monotonic order (increasing/decreasing); O(n) total
- **Next Greater Element** → Monotonic decreasing stack; for each element, pop while top < current
- **Balanced Parentheses** → Push open; pop and match on close; valid if empty at end
- **Expression Evaluation** → Two stacks (operands + operators); Shunting-yard algorithm
- **Infix / Postfix / Prefix** → Infix: a+b; Postfix (RPN): ab+; Prefix: +ab
- **Postfix Evaluation** → Single stack; push operands, pop two on operator
##### Interview Deep-Dive Keywords
- Monotonic stack is O(n) total — each element pushed/popped once
- NGE pattern: keep indices in stack, not values (for distance calculation)
- Expression problems: always clarify precedence and associativity rules
- Use Deque (ArrayDeque) in Java as stack — Stack class is legacy

---

## 38. Queue & Deque
##### Core Concepts
- **FIFO** → First In First Out; enqueue O(1), dequeue O(1)
- **Queue** → LinkedList or ArrayDeque in Java
- **Deque** → Double-ended; add/remove from both ends O(1); ArrayDeque preferred
- **Circular Queue** → Fixed-size array with front/rear pointers mod capacity
- **Priority Queue (Heap)** → Not FIFO; highest priority dequeued first; O(log n) ops
##### Key Techniques
- **BFS** → Queue-based; level-by-level traversal; shortest path in unweighted graphs
- **Sliding Window Maximum** → Monotonic deque; remove smaller elements from back; O(n)
- **Monotonic Queue** → Maintain order for range min/max queries
- **Level-order Traversal** → BFS on tree; process nodes level by level
##### Interview Deep-Dive Keywords
- BFS vs DFS: BFS = shortest path (unweighted); DFS = deep exploration, cycle detect
- Sliding window max: deque stores indices; front always has max for current window
- PriorityQueue in Java: min-heap by default; `Collections.reverseOrder()` for max-heap
- ArrayDeque is faster than LinkedList for queue/stack operations

---

## 39. Trees
##### Core Concepts
- **Binary Tree** → Each node has at most 2 children; not necessarily ordered
- **Binary Search Tree (BST)** → Left < Root < Right; O(log n) avg, O(n) worst (skewed)
- **AVL Tree** → Self-balancing BST; balance factor ∈ {-1, 0, 1}; O(log n) guaranteed
- **Red-Black Tree** → Self-balancing; less strict than AVL; used in Java TreeMap/TreeSet
- **Segment Tree** → Range queries and point updates; O(log n) query/update; O(n) build
- **Fenwick Tree (BIT)** → Binary Indexed Tree; simpler range sum / point update; O(log n)
- **Trie (Prefix Tree)** → Character-by-character tree; O(L) insert/search (L = word length)
- **Heap (Min/Max)** → Complete binary tree; parent ≤ children (min-heap); heapify O(n)
##### Key Techniques
- **Inorder Traversal** → Left → Root → Right; gives sorted order in BST
- **Preorder** → Root → Left → Right; used for tree copy, serialization
- **Postorder** → Left → Right → Root; used for tree deletion, expression trees
- **Level-order** → BFS; queue-based; used for level-by-level problems
- **Height / Depth** → Height: longest path to leaf; Depth: distance from root
- **Diameter** → Longest path between any two nodes; may not pass through root
- **LCA (Lowest Common Ancestor)** → Deepest node that is ancestor of both; O(n) naive, O(log n) binary lifting
- **Balanced Tree Check** → Height difference of subtrees ≤ 1 at every node
- **Tree Rotations** → LL/RR/LR/RL for AVL; preserve BST property
- **Heapify** → Build heap from array; O(n) using sift-down from n/2 to 0
- **Top-K Elements** → Min-heap of size K; O(n log K)
- **Range Queries** → Segment tree or Fenwick tree
##### Interview Deep-Dive Keywords
- Diameter: use post-order; at each node, `left_height + right_height`; track global max
- LCA: if root is between p and q (in BST), it's LCA; otherwise recurse into subtree
- Segment tree: node covers range; left child: [l, mid], right child: [mid+1, r]
- Trie vs HashMap for prefix search: Trie is better; HashMap can't share prefixes
- Heap in Java: `PriorityQueue`; to get top-K largest, use min-heap of size K

---

## 40. Graphs
##### Core Concepts
- **Directed / Undirected** → Directed: edges have direction; Undirected: bidirectional
- **Weighted / Unweighted** → Weighted: edges have cost; Unweighted: all cost = 1
- **Adjacency List** → `List<List<Integer>>`; space O(V+E); preferred for sparse graphs
- **Adjacency Matrix** → `int[V][V]`; space O(V²); fast edge lookup O(1); dense graphs
##### Algorithms
- **BFS** → O(V+E); shortest path unweighted; uses queue; explores level by level
- **DFS** → O(V+E); path finding, cycle detection, topological sort; uses stack/recursion
- **Dijkstra's** → Single-source shortest path; non-negative weights; O((V+E) log V) with min-heap
- **Bellman-Ford** → Handles negative weights; O(VE); detects negative cycles
- **Floyd-Warshall** → All-pairs shortest path; O(V³); DP on intermediate vertices
- **Prim's Algorithm** → MST; greedy; O(E log V); start from any vertex, grow tree
- **Kruskal's Algorithm** → MST; sort edges by weight, add if no cycle (Union-Find); O(E log E)
- **Topological Sort** → Linear ordering of DAG; DFS-based or Kahn's (BFS + in-degree)
##### Key Techniques
- **Cycle Detection** → Undirected: parent tracking in DFS; Directed: grey/white/black coloring
- **Connected Components** → BFS/DFS from each unvisited node; count starts
- **SCC (Tarjan / Kosaraju)** → Kosaraju: 2 DFS passes; Tarjan: single DFS with low-link values
- **Shortest Path** → Dijkstra (non-neg), Bellman-Ford (neg ok), BFS (unweighted)
- **MST** → Prim's (dense), Kruskal's (sparse with good Union-Find)
- **Bipartite Check** → BFS/DFS 2-coloring; graph is bipartite if no odd-length cycle
- **Union-Find (DSU)** → Disjoint Set Union; path compression + union by rank; near O(1) per op
##### Interview Deep-Dive Keywords
- Dijkstra fails with negative edges — use Bellman-Ford or Johnson's
- Topological sort only on DAG; if cycle exists, no valid ordering
- Union-Find: path compression makes find() nearly O(1) amortized
- SCC: Kosaraju needs reverse graph; Tarjan is single pass (more complex to implement)
- Bipartite = 2-colorable = no odd cycles

---

## 41. Searching Algorithms
##### Core Concepts
- **Linear Search** → O(n); works on unsorted; scan each element
- **Binary Search** → O(log n); requires sorted array; `mid = lo + (hi - lo) / 2`
##### Key Techniques
- **Lower Bound** → First index where `arr[i] >= target`
- **Upper Bound** → First index where `arr[i] > target`
- **Binary Search on Answer** → Search the answer space not the array; e.g. min capacity, min days
- **Ternary Search** → Find max/min of unimodal function; O(log n)
- **Search Space Reduction** → Eliminate half at each step; requires monotonic property
##### Interview Deep-Dive Keywords
- `mid = lo + (hi-lo)/2` avoids integer overflow vs `(lo+hi)/2`
- Binary search on answer: define `check(mid)` function, binary search on valid range
- Lower/upper bound: Java `Arrays.binarySearch()` returns negative for not-found; prefer manual
- Template: `while (lo < hi)` vs `while (lo <= hi)` — know which to use and why

---

## 42. Sorting Algorithms
##### Comparison Sorts
- **Bubble Sort** → O(n²); stable; swap adjacent; rarely used
- **Selection Sort** → O(n²); unstable; find min each pass; minimal swaps
- **Insertion Sort** → O(n²) worst, O(n) best; stable; good for nearly sorted data
- **Merge Sort** → O(n log n); stable; O(n) space; divide → sort → merge
- **Quick Sort** → O(n log n) avg, O(n²) worst; in-place; unstable; pivot selection matters
- **Heap Sort** → O(n log n); in-place; unstable; build max-heap then extract
##### Non-Comparison Sorts
- **Counting Sort** → O(n+k); stable; requires bounded integer keys; k = range
- **Radix Sort** → O(d·(n+k)); sort digit by digit; stable; d = digits, k = base
- **Bucket Sort** → O(n+k) avg; distribute into buckets; good for uniform distribution
##### Key Techniques
- **Divide & Conquer** → MergeSort / QuickSort fundamental paradigm
- **Lomuto Partition** → Pivot = last; simpler code; used in most textbooks
- **Hoare Partition** → Original pivot scheme; fewer swaps; harder to implement correctly
##### Interview Deep-Dive Keywords
- Java `Arrays.sort()`: primitives → dual-pivot QuickSort; objects → TimSort (stable merge+insertion)
- `Collections.sort()` → TimSort; stable
- QuickSort worst case: sorted input with last-element pivot → use random pivot
- Counting sort: only for small integer ranges; Radix sort: extend counting to large numbers
- Merge sort for linked lists (no random access needed)

---

## 43. Recursion & Backtracking
##### Core Concepts
- **Recursion** → Function calls itself; must have base case + progress toward base case
- **Base Case** → Termination condition; prevents infinite recursion
- **Call Stack** → Each recursive call adds frame; deep recursion → StackOverflowError
##### Key Techniques
- **Backtracking** → Explore all possibilities; undo choice on failure; prune invalid branches
- **Subsets** → Include/exclude each element; 2^n subsets; O(2^n)
- **Permutations** → All orderings; swap-based or used-array; O(n!)
- **Combinations** → Choose k from n; O(C(n,k))
- **N-Queens** → Place queens row by row; check column + diagonals; backtrack
- **Sudoku Solver** → Try 1–9 in empty cell; backtrack on conflict
- **Decision Tree** → Each node = choice; leaf = solution or dead end
- **State Space Tree** → Visualize all recursive calls as tree; prune branches early
##### Interview Deep-Dive Keywords
- Always define: what does the recursive function return? What is the state?
- Backtracking template: choose → explore → unchoose
- Pruning: early termination when constraint is already violated
- Memoize overlapping subproblems → converts backtracking to DP
- Java recursion limit: default ~500–1000 deep; iterative DFS for deep problems

---

## 44. Dynamic Programming (DP)
##### Core Concepts
- **Memoization (Top-down)** → Recursion + cache; solve subproblem once; O(states) time+space
- **Tabulation (Bottom-up)** → Fill DP table iteratively; no recursion overhead
- **Overlapping Subproblems** → Same subproblem solved multiple times → cache it
- **Optimal Substructure** → Optimal solution built from optimal solutions to subproblems
- **State Definition** → What does `dp[i]` or `dp[i][j]` represent? Define precisely
- **Transition Relation** → How to compute `dp[i]` from previous states
- **DP Table** → 1D, 2D, or higher-dimensional based on state parameters
##### Patterns
- **0/1 Knapsack** → Include or exclude item; `dp[i][w] = max(dp[i-1][w], val[i]+dp[i-1][w-wt[i]])`
- **Unbounded Knapsack** → Item can be reused; `dp[w] = max(dp[w], val[i]+dp[w-wt[i]])`
- **LCS** → `dp[i][j] = dp[i-1][j-1]+1` if match, else `max(dp[i-1][j], dp[i][j-1])`
- **LIS** → `dp[i] = max(dp[j]+1)` for all j < i where `arr[j] < arr[i]`; O(n²) or O(n log n) with patience sorting
- **Coin Change** → Min coins; `dp[amount] = min(dp[amount-coin]+1)` for all coins
- **Matrix Chain Multiplication** → Optimal parenthesization; `dp[i][j]` = min ops for matrices i..j
- **DP on Trees** → Post-order; child results feed parent; e.g. max path sum, house robber III
- **DP on Graphs** → Shortest path (Bellman-Ford), DAG longest path
##### Interview Deep-Dive Keywords
- First step: identify if DP applies — overlapping subproblems + optimal substructure
- State must encode all info needed to make the next decision
- Space optimization: often 2D DP can be reduced to 1D (rolling array)
- LIS in O(n log n): maintain patience-sort array; binary search for position
- Tabulation usually faster than memoization (no recursion overhead, better cache)

---

## 45. Greedy Algorithms
##### Core Concepts
- **Greedy Choice Property** → Locally optimal choice leads to global optimum
- **Optimal Substructure** → Subproblems have optimal solutions (same as DP)
- **Greedy vs DP** → Greedy: one decision at each step, no reconsideration; DP: explores all options
##### Key Techniques
- **Activity Selection** → Sort by end time; greedily pick non-overlapping intervals; O(n log n)
- **Fractional Knapsack** → Take highest value/weight ratio first; O(n log n)
- **Huffman Coding** → Frequency-based prefix codes; min-heap; O(n log n)
- **Interval Scheduling** → Maximize non-overlapping intervals; sort by end time
- **Local vs Global Optimum** → Greedy works when local optimum ≡ global optimum
##### Interview Deep-Dive Keywords
- Prove greedy correctness: exchange argument (assume non-greedy is better → contradiction)
- Greedy fails for 0/1 Knapsack → use DP instead
- Interval problems: sorting key matters — start vs end time changes the problem
- Huffman: two passes — build tree (min-heap), assign codes (tree traversal)

---

## 46. Bit Manipulation
##### Core Concepts
- **Bitwise Operators** → `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (left shift), `>>` (signed right shift), `>>>` (unsigned right shift)
- **Left Shift** → `x << k` = `x * 2^k`; fast multiply by power of 2
- **Right Shift** → `x >> k` = `x / 2^k`; preserves sign bit
##### Key Techniques
- **XOR Tricks** → `x ^ x = 0`; `x ^ 0 = x`; find single non-duplicate: XOR all elements
- **Bit Masking** → `x & (1 << k)` = check bit k; `x | (1 << k)` = set; `x & ~(1 << k)` = clear; `x ^ (1 << k)` = toggle
- **Power of Two** → `n > 0 && (n & (n-1)) == 0`
- **Set / Clear / Toggle Bits** → Common interview operations
- **Subsets using Bits** → For n elements, iterate 0..2^n-1; bit i set = element i included
- **Count Set Bits** → Brian Kernighan: `n &= (n-1)` removes lowest set bit; O(set bits)
##### Interview Deep-Dive Keywords
- XOR is commutative and associative; useful for pairwise cancellation
- `n & (n-1)` clears lowest set bit — fundamental pattern
- Subset enumeration: O(2^n) subsets, O(n) per subset → O(n·2^n) total
- Java `Integer.bitCount(n)`, `Integer.highestOneBit(n)`, `Integer.numberOfTrailingZeros(n)`
- Signed vs unsigned right shift: `>>` vs `>>>` (Java-specific distinction)

---

## 47. Mathematics & Number Theory
##### Core Concepts
- **Prime Numbers** → No divisors except 1 and itself; check up to √n: O(√n)
- **GCD** → Euclidean: `gcd(a,b) = gcd(b, a%b)`; O(log min(a,b))
- **LCM** → `lcm(a,b) = a*b / gcd(a,b)`
- **Sieve of Eratosthenes** → All primes up to n; O(n log log n); mark multiples of each prime
- **Modular Arithmetic** → `(a+b)%m = ((a%m)+(b%m))%m`; same for multiply; careful with subtraction
- **Fast Exponentiation** → `x^n` in O(log n); square-and-multiply; `(base^exp) % mod`
- **Combinatorics** → C(n,k) = n! / (k!(n-k)!); use Pascal's triangle or modular inverse for large n
- **Permutations / Combinations** → P(n,k) = n!/(n-k)!; C(n,k) = P(n,k)/k!
##### Interview Deep-Dive Keywords
- Sieve: outer loop to √n; inner loop marks from i² (smaller already marked)
- Modular inverse: needed for C(n,k) mod p; use Fermat's little theorem if p is prime: `a^(p-2) mod p`
- Overflow: `a*b` can overflow int/long; use `(long)a * b` or modular multiply
- GCD extended: Bezout's identity; used in modular inverse when p is not prime
- Java BigInteger: `gcd()`, `modPow()`, `isProbablePrime()`

---

## 48. Advanced Data Structures
##### Segment Tree
- **Purpose** → Range queries (sum/min/max) + point updates; O(log n) both
- **Build** → O(n); bottom-up from leaves
- **Query** → Traverse and combine relevant nodes; O(log n)
- **Update** → Point update propagates up; O(log n)
- **Lazy Propagation** → Defer range updates; mark nodes "lazy"; O(log n) range update
- **Use Cases** → Range sum, range min/max, count inversions
##### Fenwick Tree (BIT)
- **Purpose** → Prefix sum queries + point updates; simpler than segment tree
- **Update** → `i += i & (-i)` — move to parent
- **Query** → `i -= i & (-i)` — move to responsible ancestor
- **Space** → O(n); faster in practice than segment tree
##### Trie
- **Purpose** → Prefix search, autocomplete, word existence; O(L) operations
- **Structure** → Each node has up to 26 children (for lowercase English)
- **Insert** → Create nodes along character path
- **Search** → Follow path; check `isEnd` flag
- **Prefix Search** → Follow path; all words in subtree are completions
- **Use Cases** → Autocomplete, spell check, IP routing
##### Suffix Array & Suffix Tree
- **Suffix Array** → Sorted array of all suffixes; O(n log n) build; O(m log n) pattern match
- **Suffix Tree** → Compressed trie of all suffixes; O(n) build; O(m) search; complex
- **LCP Array** → Longest Common Prefix between adjacent suffixes; used with suffix array
##### Disjoint Set Union (Union-Find)
- **Purpose** → Track connected components; merge sets; check connectivity
- **Find** → With path compression: near O(1)
- **Union** → By rank/size: near O(1)
- **Applications** → Kruskal's MST, cycle detection, network connectivity
##### Skip List
- **Purpose** → Probabilistic sorted structure; O(log n) search/insert/delete expected
- **Structure** → Multiple levels of linked lists; upper levels skip more nodes
- **vs BST** → Simpler to implement lock-free; Java ConcurrentSkipListMap uses it
##### B-Tree / B+ Tree
- **Purpose** → Disk-optimized tree; minimize I/O; used in databases and file systems
- **B-Tree** → Keys in all nodes; O(log n) with large branching factor
- **B+ Tree** → Keys only in leaves; leaves linked for range scans; preferred in DBs
- **Use Cases** → MySQL InnoDB index, file system directory
##### Interview Deep-Dive Keywords
- Segment tree vs Fenwick: Fenwick simpler for sum; Segment tree more flexible (any associative op)
- Lazy propagation: required for range update queries (e.g. add 5 to all elements in [l..r])
- Union-Find: inverse Ackermann α(n) ≈ O(1); practically O(1) with both optimizations
- Trie memory: 26 children per node is expensive; use HashMap<Character, TrieNode> for sparse

---

## 49. Advanced Algorithms
##### String Algorithms
- **KMP Algorithm** → Failure function (prefix-suffix); O(n+m) pattern matching; no backtrack
- **Rabin-Karp** → Rolling hash; O(n+m) avg, O(nm) worst; multi-pattern search
- **Z Algorithm** → Z-array: longest substring from index i matching prefix; O(n+m)
- **Manacher's Algorithm** → All palindromic substrings in O(n); uses symmetry
##### Search Algorithms
- **A\* Search** → Heuristic-based shortest path; f(n) = g(n) + h(n); optimal if h is admissible
- **Meet-in-the-Middle** → Split problem into halves; solve each; combine; reduces O(2^n) to O(2^(n/2))
- **Mo's Algorithm** → Offline range queries; sort by blocks; O((n+q)√n)
##### Interview Deep-Dive Keywords
- KMP failure function: `lps[i]` = length of longest proper prefix that is also suffix up to i
- Rabin-Karp: hash collision → verify match; good for multiple pattern search
- Manacher: even/odd palindromes; trick is to insert `#` between chars
- A\*: heuristic must be admissible (never overestimates); Manhattan distance for grids
- Meet-in-middle: used for subset sum with n ≤ 40; generate all 2^(n/2) subsets for each half

---

## 50. Patterns & Problem-Solving Techniques
##### Core Patterns
- **Sliding Window** → Subarray/substring of variable/fixed size; O(n); avoid nested loops
- **Two Pointers** → Sorted arrays; converging or same-direction; O(n)
- **Divide & Conquer** → Split → solve → combine; MergeSort, QuickSort, binary search
- **Greedy** → Local optimum at each step; prove via exchange argument
- **Backtracking** → Exhaustive search with pruning; decision tree; undo choices
- **DP Patterns** → Identify state, transition, base case; tabulate or memoize
- **Graph Traversal** → BFS for shortest, DFS for paths/cycles/components
- **Monotonic Stack/Queue** → O(n) range queries; next greater/smaller element
- **Prefix/Suffix** → Precompute prefix/suffix arrays for O(1) range queries
##### Problem-Solving Framework
- Read → Understand constraints → brute force → identify pattern → optimize
- State time and space complexity at each step
- Consider: sorted? → binary search; subarray? → sliding window/prefix sum; graph? → BFS/DFS
##### Interview Deep-Dive Keywords
- Pattern recognition is the key skill: same technique solves many different-looking problems
- Always start with brute force → state complexity → then optimize
- Dry run on small example before coding
- Edge cases first: empty, single element, all same, negative, overflow

---

## 51. Java-Specific DSA
##### Collections for DSA
- **ArrayList** → Dynamic array; O(1) get; use for random-access lists
- **LinkedList** → Doubly linked; use ArrayDeque instead for stack/queue (faster)
- **HashMap / HashSet** → O(1) avg; frequency count, visited tracking, two-sum
- **TreeMap / TreeSet** → O(log n); sorted order; floor/ceiling operations
- **PriorityQueue** → Min-heap default; `new PriorityQueue<>(Collections.reverseOrder())` for max
- **Deque / ArrayDeque** → Use as stack (`push/pop`) or queue (`offer/poll`); faster than Stack/LinkedList
##### Sorting & Searching
- **Collections.sort()** → TimSort; stable; O(n log n)
- **Arrays.sort()** → Dual-pivot QuickSort for primitives; TimSort for objects
- **Comparator** → `(a,b) -> a-b` ascending; `(a,b) -> b-a` descending; careful with overflow — use `Integer.compare(a,b)`
- **Comparable** → `compareTo()` for natural ordering; implement in custom class
- **Streams for DSA** → `Arrays.stream(arr).sorted().distinct().toArray()`; use with caution (overhead)
##### Pitfalls
- **Autoboxing overhead** → `Integer` vs `int` in PriorityQueue; avoid in hot loops
- **Recursion limits** → Java default ~500–1000; use iterative DFS with explicit stack
- **Integer overflow** → Use `long` for large sums; `(long)a * b`
- **`Integer` cache** → `-128` to `127` cached; `==` comparison fails beyond
##### Interview Deep-Dive Keywords
- Use `Integer.compare(a, b)` in Comparator, not `a - b` (overflow risk)
- PriorityQueue: `peek()` = O(1), `poll()` = O(log n), `add()` = O(log n)
- TreeMap: `floorKey(k)`, `ceilingKey(k)`, `higherKey(k)`, `lowerKey(k)` — critical for interval problems
- ArrayDeque is the go-to for both stack and queue in competitive/interview coding

---

## 52. Pitfalls, Edge Cases & Testing
##### Common Pitfalls
- **Off-by-one errors** → Array bounds, loop termination (`< n` vs `<= n`)
- **Integer overflow** → `int` max = 2,147,483,647; use `long`; check `a + b` before adding
- **Infinite loops** → Ensure loop variable progresses; check while-loop condition
- **Stack overflow** → Deep recursion; increase stack or convert to iterative
- **Wrong complexity assumption** → Nested loops ≠ always O(n²); amortized analysis matters
- **Not handling edge cases** → Always check: empty, null, single element, duplicates
##### Edge Cases to Always Check
- **Empty input** → Return default value, not crash
- **Single element** → Often simplest valid input; algorithms must handle
- **Large input** → n = 10^5 to 10^9; ensure O(n log n) or better
- **Duplicates** → Sort? HashMap? BST behavior with duplicates?
- **Negative values** → Modulo with negatives: `((a % m) + m) % m`
- **Boundary conditions** → First/last element, min/max value, 0 and 1
##### Testing Strategy
- Start with provided examples
- Add edge cases manually
- Use dry run for small inputs
- Trace recursive calls for depth > 3
##### Interview Deep-Dive Keywords
- State edge cases out loud before coding — shows systematic thinking
- Negative modulo: Java `%` can return negative for negative dividend; normalize with `+m) % m`
- Overflow: `a + b > Integer.MAX_VALUE` → use `Long.MAX_VALUE` comparisons or cast early

---

## 53. Competitive Programming Essentials
##### Input & I/O
- **Fast I/O** → `BufferedReader` + `StringTokenizer` instead of Scanner in Java
- **Input Parsing** → `Integer.parseInt(st.nextToken())` from StringTokenizer
- **Constraints Handling** → Read constraints first; decide algorithm complexity before coding
##### Common Techniques
- **Modulo Operations** → `(a * b) % MOD`; apply after each multiply to prevent overflow
- **Precomputation** → Compute factorials, powers, prefix sums once; query in O(1)
- **Lazy Propagation** → Defer range updates in segment tree; critical for range-update range-query
##### Interview Deep-Dive Keywords
- MOD = 10^9+7 (prime) is standard; `(a - b + MOD) % MOD` for subtraction
- Precompute factorial array + inverse factorial for C(n,k) mod p
- BufferedReader in Java is ~10x faster than Scanner for large input

---

## 54. Real-World System Mapping
| DSA Concept | Real-World Use |
|---|---|
| LRU Cache (LinkedHashMap) | Browser cache, CPU cache eviction |
| Trie | Autocomplete, DNS resolution, IP routing |
| Graph (BFS/Dijkstra) | Google Maps, social network friend suggestions |
| Priority Queue (Heap) | OS process scheduling, event-driven simulation |
| Segment Tree / Fenwick | Database range queries, analytics aggregation |
| Sliding Window | Real-time rate limiting, network traffic analysis |
| Bloom Filter | Deduplication in distributed systems, CDN cache check |
| B+ Tree | MySQL/PostgreSQL index, file system metadata |
| Union-Find | Network connectivity, image segmentation |
| Topological Sort | Build systems (Gradle/Maven), task scheduling (Airflow) |
| Hashing | HashMaps, SHA hashing, consistent hashing in distributed systems |
| Suffix Array | Full-text search engines, DNA sequence alignment |

---

## 55. Object-Oriented Design (OOD)
##### Core OOP Concepts
- **Object** → Instance of a class; has state (fields) + behavior (methods) + identity
- **Class** → Blueprint for objects; defines structure and behavior
- **Instance** → Concrete object created from a class via `new`
- **State / Behavior / Identity** → State = field values; Behavior = methods; Identity = memory address / `==`
- **Attribute / Property / Field** → Variables that hold an object's state
##### Four Pillars
- **Encapsulation** → Bundle data + methods; hide internals via access modifiers; expose via getters/setters
- **Abstraction** → Expose essential behavior, hide implementation; achieved via abstract classes + interfaces
- **Inheritance** → IS-A relationship; subclass inherits parent fields/methods; promotes reuse
- **Polymorphism** → Same interface, different behavior; method overloading (compile-time) + overriding (runtime)
##### Encapsulation Keywords
- **Data Hiding** → `private` fields; only accessible via public API
- **Access Modifiers** → `public` (all) → `protected` (package + subclass) → default (package) → `private` (class only)
- **Immutable Object** → All fields `final`; no setters; safe to share; e.g. `String`, `LocalDate`
- **Read-only Object** → Expose getters only; no mutation after construction
##### Abstraction Keywords
- **Abstract Class** → Cannot instantiate; may have abstract + concrete methods; single inheritance
- **Interface** → Pure contract; all methods implicitly public; default/static methods since Java 8; multiple impl
- **Contract** → Callers depend on interface, not implementation → loose coupling
- **Loose Coupling / SoC** → Components depend on abstractions; change one without affecting others
##### Inheritance Keywords
- **Superclass / Subclass** → `extends`; child inherits non-private members of parent
- **Method Overriding** → Same signature in subclass; `@Override`; resolved at runtime (dynamic dispatch)
- **Multilevel Inheritance** → A → B → C; Java supports via classes
- **Multiple Inheritance** → Java: only via interfaces (avoids diamond problem)
- **Hybrid Inheritance** → Combination of above; Java achieves through interfaces
##### Polymorphism Keywords
- **Method Overloading** → Same name, different params; resolved at compile-time (static binding)
- **Method Overriding** → Same signature, subclass; resolved at runtime (dynamic binding / late binding)
- **Dynamic Dispatch** → JVM selects method based on actual runtime type, not declared type
- **Early Binding** → Compile-time; overloading, static methods, final methods
- **Late Binding** → Runtime; virtual methods; default in Java for non-static/non-final methods
##### Object Relationships
- **Association** → "uses-a" general relationship; can be 1:1, 1:N, N:M
- **Aggregation** → "has-a" weak ownership; parts can exist independently; e.g. Department has Employees
- **Composition** → "has-a" strong ownership; parts cannot exist independently; e.g. House has Rooms
- **Dependency** → "uses-a" short-lived; method parameter or local var; weakest coupling
##### Class Design
- **Constructor** → Special method for initialization; called on `new`
- **Default Constructor** → No-arg; auto-generated if no constructor defined
- **Copy Constructor** → Java: no built-in; implement manually; deep vs shallow copy
- **Static Method / Variable** → Class-level; shared across all instances; no `this` reference
- **Inner Class** → Non-static nested class; has access to outer instance; types: member, local, anonymous
- **Anonymous Class** → One-time-use subclass/implementation; common pre-lambdas
##### Advanced OOP
- **Delegation** → Object delegates responsibility to another; composition over inheritance pattern
- **Object Cloning** → `Cloneable` + `clone()`; deep copy copies nested objects; shallow copy shares refs
- **Reflection** → Inspect/invoke class members at runtime; used by frameworks; performance cost
- **Dynamic Typing vs Static Typing** → Java: statically typed at compile; dynamic dispatch at runtime
##### SOLID Principles
- **SRP** → One class, one reason to change; e.g. separate `InvoicePrinter` from `Invoice`
- **OCP** → Open for extension (new behavior), closed for modification (existing code stable); use interfaces
- **LSP** → Subtypes must be substitutable for base types; don't override to throw UnsupportedOperationException
- **ISP** → Clients shouldn't depend on methods they don't use; split fat interfaces
- **DIP** → High-level modules depend on abstractions, not concretions; inject dependencies
- **DRY** → Single source of truth; extract duplicated logic into shared method/class
- **KISS** → Simplest solution that works; avoid clever/complex code
- **YAGNI** → Don't add functionality until needed; defer decisions
##### Object Relationships (Architecture)
- **Favor Composition over Inheritance** → More flexible; avoids fragile base class problem; HAS-A over IS-A
- **Program to an Interface** → Code depends on abstraction; swap implementations without changing callers
- **Law of Demeter** → Only talk to immediate friends; `a.getB().getC().doX()` is a violation
- **High Cohesion** → Class does one thing well; related methods together
- **Low Coupling** → Minimal dependencies between classes/modules
##### Design Patterns (OOP)
- **Creational** → Singleton, Factory Method, Abstract Factory, Builder, Prototype — control object creation
- **Structural** → Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy — compose objects
- **Behavioral** → Observer, Strategy, Command, Chain of Responsibility, State, Template Method, Mediator, Memento, Visitor, Interpreter — define object interactions
##### Anti-Patterns
- **God Object** → One class does everything; violates SRP; hard to test and change
- **Spaghetti Code** → Tangled, unstructured; no clear separation of concerns
- **Tight Coupling** → Classes depend on concrete implementations; breaks OCP and DIP
- **Anemic Domain Model** → Objects hold data only, no behavior; logic leaks into service layer
- **Over-engineering** → Unnecessary patterns/abstractions; YAGNI violation
##### Java-Specific OOP Keywords
- **`this`** → Current instance reference; disambiguate fields from params
- **`super`** → Parent class reference; call parent constructor or overridden method
- **`final`** → Field: constant; Method: no override; Class: no subclass
- **`static`** → Class-level; no instance needed
- **`instanceof`** → Runtime type check; use with pattern matching in Java 16+
- **`transient`** → Exclude field from serialization
##### OOP in Frameworks
- **Entity** → Domain object with persistent identity (JPA `@Entity`)
- **Value Object** → Immutable; equality by value; no identity (e.g. Money, Address)
- **DTO** → Data Transfer Object; carries data across layers; no behavior
- **DAO** → Data Access Object; abstracts DB operations
- **Repository Pattern** → Collection-like interface for domain objects (Spring Data)
- **MVC / MVVM** → Architectural patterns built on OOP separation of concerns
##### Interview Deep-Dive Keywords
- Composition over Inheritance: Inheritance breaks encapsulation; prefer delegation
- Abstract class vs Interface: Use abstract class when sharing state/code; interface for pure contract
- OCP in practice: new behavior via new classes (Strategy pattern), not modifying old ones
- LSP violation: Square extends Rectangle breaks substitutability (setWidth affects height)
- Polymorphism without overriding: overloading is polymorphism but resolved at compile-time

---

## 56. Static Analysis & Code Quality
##### Core Concepts
- **Static Analysis** → Analyze source code without executing it; find bugs, smells, security issues
- **Linting** → Style and syntax checking; enforce coding standards
- **Abstract Syntax Tree (AST)** → Tree representation of source code structure; basis for all analysis
- **Control Flow Graph (CFG)** → Nodes = code blocks; edges = control paths; used for reachability analysis
- **Data Flow Analysis** → Track how values propagate through the program
- **Semantic Analysis** → Meaning beyond syntax; type checking, null analysis, scope resolution
##### Analysis Types
- **Syntactic Analysis** → Parse code structure; detect syntax errors
- **Semantic Analysis** → Type mismatches, undefined variables, scope violations
- **Control Flow Analysis** → Dead code, unreachable branches, infinite loops
- **Data Flow Analysis** → Uninitialized variables, use-after-free, null dereference paths
- **Taint Analysis** → Track untrusted input (source) to sensitive operation (sink)
- **Symbolic Execution** → Execute code symbolically with abstract values; find edge cases
- **Escape Analysis** → Determine if object escapes method scope; enables JVM stack allocation
- **Alias Analysis** → Multiple references to same object; affects optimization and safety
##### Bug & Defect Detection
- **Null Pointer Dereference** → Accessing field/method on null; `@NonNull` / `@Nullable` annotations
- **Memory Leak Detection** → Unclosed streams, uncleaned caches, static collections growing unbounded
- **Dead Code Detection** → Unreachable branches, unused methods/variables; code smell
- **Resource Leak** → `Connection`, `InputStream` not closed; use try-with-resources
- **Race Condition Detection** → Unsynchronized shared mutable state; `@GuardedBy` annotation
- **Integer Overflow** → Unchecked arithmetic; use `Math.addExact()` or `long`
- **Buffer Overflow** → Java arrays are bounds-checked; concern in JNI/native code
##### Security Analysis (SAST)
- **SAST** → Static Application Security Testing; finds vulnerabilities before runtime
- **OWASP Top 10** → SQL Injection, XSS, Broken Auth, IDOR, Security Misconfiguration, etc.
- **SQL Injection Detection** → String concatenation in queries → use PreparedStatement
- **XSS Detection** → Unsanitized user input in HTML output → encode output
- **Hardcoded Credentials** → Passwords/API keys in source → use Vault/env vars
- **Path Traversal** → User input in file paths → validate and sanitize
- **Cryptographic Misuse** → Weak algorithms (MD5, SHA1); hardcoded IVs; ECB mode
##### Code Quality Metrics
- **Cyclomatic Complexity** → Number of linearly independent paths; > 10 is high; measure of testability
- **Cognitive Complexity** → How hard code is to understand; penalizes nesting more than cyclomatic
- **Code Smells** → Indicators of deeper problems; Long Method, Large Class, Feature Envy, etc.
- **Code Duplication** → Clone detection; DRY violations; leads to maintenance issues
- **Coupling Metrics** → Afferent (Ca) = classes that depend on this; Efferent (Ce) = classes this depends on
- **Cohesion Metrics** → LCOM (Lack of Cohesion in Methods); low LCOM = high cohesion = good
- **Depth of Inheritance Tree (DIT)** → Deeper hierarchy = more complex; usually keep < 5
- **Maintainability Index** → Combined metric: Halstead volume + cyclomatic complexity + lines of code
##### OOP-Specific Static Checks
- **God Class Detection** → Too many methods/fields; high Ce; violates SRP
- **Long Method** → Refactor: extract method; > 20-30 lines is a smell
- **Feature Envy** → Method uses more data from another class than its own; move the method
- **Inappropriate Intimacy** → Two classes know too much about each other's internals
- **Shotgun Surgery** → One change requires many small changes in many classes; low cohesion
- **Refused Bequest** → Subclass doesn't use parent's methods/data; wrong inheritance hierarchy
- **Cyclic Dependencies** → A depends on B depends on A; hard to test/deploy independently
- **Interface Pollution** → Fat interfaces; violates ISP; force clients to implement unused methods
##### Architecture Analysis
- **Layer Violation Detection** → e.g. domain layer directly calling infrastructure layer
- **Package Cycles** → Cyclic package dependencies; prevent with dependency rules
- **Architecture Compliance** → Enforce Clean Architecture / Hexagonal layer rules
- **Microservice Boundary Violations** → Service directly accessing another service's DB
##### Performance Analysis (Static)
- **N+1 Query Detection** → Loop with DB call inside; use JOIN or batch loading
- **Excessive Object Creation** → Strings in loops, autoboxing in hot paths
- **Reflection Overuse** → Slow; avoid in performance-critical paths
- **Synchronization Overhead** → Over-synchronized code; ConcurrentHashMap vs synchronized block
##### Java Static Analysis Tools
- **SonarQube** → Comprehensive quality + security; CI/CD integration; quality gates
- **SpotBugs** → FindBugs successor; bytecode analysis; finds concurrency bugs, null derefs
- **PMD** → Source analysis; code style, design issues, unused code
- **Checkstyle** → Code formatting and style rules; Google/Sun style guides
- **Error Prone** → Google's compile-time checker; catches common Java mistakes
- **Semgrep** → Pattern-based; custom rules; multi-language
- **CodeQL** → Semantic code analysis; used in GitHub; find CVEs in open source
##### DevOps Integration
- **Shift Left Testing** → Find bugs early in development, not in production
- **Quality Gates** → SonarQube: fail build if coverage < X%, or new critical issues introduced
- **Pull Request Analysis** → Comment issues directly on PR; block merge on violations
- **Pre-commit Hooks** → Run Checkstyle/PMD before commit; fast feedback
- **Continuous Inspection** → Analysis on every push; track metrics over time
##### Interview Deep-Dive Keywords
- Cyclomatic complexity: each `if`/`for`/`while`/`case`/`&&`/`||` adds 1; start at 1
- SAST vs DAST: Static = no execution (fast, early); Dynamic = running app (realistic, slower)
- SonarQube quality gate: define thresholds; block deployment if violated
- Feature Envy + God Class are the most common OOP violations found in enterprise code
- Taint analysis: source (HTTP input) → propagation → sink (SQL/file/shell) = vulnerability path

---

## 57. Engineering Principles
##### Core Principles
- **Separation of Concerns (SoC)** → Each module has one well-defined responsibility; basis for all architecture
- **Modularity** → System divided into independent, interchangeable modules
- **Information Hiding** → Module exposes only what callers need; internals private
- **Abstraction** → Work with concepts, not implementations; hide irrelevant detail
- **Composition over Inheritance** → Build complex behavior by combining simpler objects; more flexible
- **Program to an Interface** → Depend on abstractions; swap implementations without changing callers
- **Law of Demeter** → Only talk to direct collaborators; avoid method chaining across objects
- **POLA (Principle of Least Astonishment)** → System behaves as users expect; no surprises
##### SOLID (Recap with Depth)
- **SRP** → Class has one reason to change; split fat classes; cohesion-driven
- **OCP** → Extend via new code; never modify stable working code; use Strategy/Template Method
- **LSP** → Substitutability; don't strengthen preconditions or weaken postconditions in subclass
- **ISP** → Split fat interfaces; clients implement only what they use; reduces coupling
- **DIP** → High-level policy doesn't depend on low-level detail; both depend on abstraction
##### Clean Code
- **DRY** → Every piece of knowledge has one representation; extract shared logic
- **KISS** → Simpler is better; avoid clever code; optimize for readability
- **YAGNI** → Don't speculate; build what's needed now; defer decisions
- **Boy Scout Rule** → Leave code cleaner than you found it; continuous small improvements
- **Self-Documenting Code** → Code reads like prose; meaningful names; no need for comments to explain "what"
- **Avoid Premature Optimization** → First make it work, then make it right, then make it fast
##### Architectural Principles
- **High Cohesion** → Elements of a module belong together; measure: LCOM
- **Low / Loose Coupling** → Modules depend on abstractions; change one without affecting others
- **Explicit Dependencies** → Don't hide dependencies; inject them; makes testing easy
- **Dependency Injection** → Provide dependencies from outside; don't create them inside
- **Inversion of Control (IoC)** → Framework calls your code; Hollywood Principle: "don't call us, we'll call you"
- **Layered Architecture** → Presentation → Application → Domain → Infrastructure; each layer has clear role
- **Clean Architecture** → Dependency rule: outer layers depend on inner layers; domain layer has no deps
- **Stable Dependencies Principle** → Depend on modules that change less often than you do
- **Acyclic Dependencies Principle (ADP)** → No cycles in package/module dependency graph
##### System Design Principles
- **Scalability First** → Design for growth; horizontal > vertical; stateless > stateful
- **Fault Isolation** → Failure in one component doesn't cascade; bulkhead pattern
- **Graceful Degradation** → System degrades partially under load rather than fully failing
- **Idempotency** → Same operation applied multiple times has same effect as once; critical for retries
- **Statelessness** → No server-side session; enables horizontal scaling; load balancer can route anywhere
- **Eventual Consistency** → Distributed systems allow temporary inconsistency; resolve over time
- **Backpressure** → Slow consumer signals slow producer; prevents buffer overflow
- **Data Locality** → Process data where it lives; minimize network hops
##### Security Principles
- **Principle of Least Privilege (PoLP)** → Grant minimum access needed; reduce blast radius
- **Defense in Depth** → Multiple security layers; no single point of failure
- **Fail Secure** → On error, deny access; never fail open
- **Zero Trust** → Never trust, always verify; even internal services authenticate
- **Secure by Design** → Security is not an afterthought; built in from day one
- **Input Validation** → Never trust user input; validate at all boundaries
- **Output Encoding** → Encode before rendering to prevent XSS
##### Distributed Systems Principles
- **CAP Theorem** → Cannot have Consistency + Availability + Partition Tolerance simultaneously; choose two
- **PACELC** → Extends CAP: when no partition (E), trade latency (L) vs consistency (C)
- **Immutable Data Preference** → Append-only logs; event sourcing; easier reasoning about state
- **Retry with Backoff** → Exponential backoff + jitter; avoid thundering herd
- **Circuit Breaker** → Stop calling failing service; recover gracefully; states: Closed/Open/Half-Open
- **Consensus over Coordination** → Use Raft/Paxos for agreement; avoid distributed locks where possible
##### Data & Database Principles
- **ACID** → Atomicity, Consistency, Isolation, Durability; relational DB guarantee
- **BASE** → Basically Available, Soft state, Eventually consistent; NoSQL trade-off
- **Normalization vs Denormalization** → Normalize for write consistency; denormalize for read performance
- **Write vs Read Optimization** → LSM tree (write optimized), B-tree (read optimized); pick per use case
- **Data Partitioning** → Horizontal (sharding) vs vertical (column split); affects scalability
##### Performance Principles
- **Minimize Latency** → Fewer hops, better algorithms, caching, connection pooling
- **Maximize Throughput** → Batching, async, parallelism, pipelining
- **Caching First** → Cache at multiple levels: CPU, in-process, distributed, CDN
- **Lazy Loading** → Load only when needed; defer expensive operations
- **Avoid Blocking** → Non-blocking I/O, async processing, reactive pipelines
##### Observability Principles
- **Logs + Metrics + Traces** → Three pillars; logs for events, metrics for aggregates, traces for request flow
- **Alert on Symptoms** → Alert on SLO breach (slow responses), not causes (high CPU)
- **SLO-driven Monitoring** → Define SLIs (what to measure), SLOs (targets), SLAs (contractual)
- **High Cardinality Awareness** → Many unique label values stress metrics systems; use tracing instead
##### DevOps & Delivery Principles
- **Shift Left** → Test, security, quality checks early in pipeline
- **CI/CD** → Automate build, test, deploy; fast feedback; small, frequent releases
- **Infrastructure as Code** → Version-controlled infra; reproducible environments
- **Immutable Infrastructure** → Never modify running infra; replace with new version
- **Small Batch Releases** → Less risk; easier rollback; faster feedback
##### OOP Design Principles
- **Encapsulate What Varies** → Identify variation points; hide behind interface; Strategy pattern
- **Tell, Don't Ask** → Objects should do things, not expose state for others to check-and-act
- **Hollywood Principle** → Framework controls flow; calls your hooks/callbacks
##### Domain-Driven Design Principles
- **Ubiquitous Language** → Business and tech share same vocabulary; reduces translation errors
- **Bounded Context** → Clear boundary where a model applies; each context owns its data
- **Aggregate Root Consistency** → Transactional consistency within aggregate boundary only
- **Anti-Corruption Layer** → Translate external model to internal domain model; protect domain integrity
##### Anti-Principles (Avoid)
- **Over-engineering** → Solutions more complex than the problem demands
- **Premature Optimization** → "Root of all evil" — Knuth; optimize only after profiling
- **Tight Coupling** → Hard to test, change, or deploy independently
- **Big Ball of Mud** → No structure; everything depends on everything
- **Golden Hammer** → Using one tool/pattern for every problem
##### Interview Deep-Dive Keywords
- SOLID + DRY + KISS are table stakes; depth shows in trade-off discussion
- SRP in practice: if you can't summarize a class in one sentence, it has multiple responsibilities
- CAP theorem: CP (PostgreSQL, ZooKeeper) vs AP (Cassandra, DynamoDB) — pick based on use case
- Idempotency: design APIs with PUT > POST for mutations; use idempotency keys
- Shift Left: cheaper to fix bug in code review than in production (10x–100x cost difference)

---

## 58. Design Patterns (Comprehensive)
##### Creational Patterns
- **Singleton** → One instance per JVM; enum-based is thread-safe and serialization-safe; double-checked locking needs `volatile`
- **Factory Method** → Subclass decides which class to instantiate; `createProduct()` in abstract class
- **Abstract Factory** → Family of related objects; `UIFactory → WindowsUI | MacUI`; change family by swapping factory
- **Builder** → Step-by-step construction of complex object; fluent API; separates construction from representation
- **Prototype** → Clone existing object; avoid expensive initialization; implement `Cloneable` or copy constructor
- **Object Pool** → Reuse expensive objects (DB connections, threads); check out/in pattern
- **Lazy Initialization** → Create object on first use; `if (instance == null) instance = new ...`; thread-safety concern
- **Dependency Injection** → Pass dependencies via constructor/setter; enables testability; IoC container manages lifecycle
- **Service Locator** → Registry of services; anti-pattern in most cases — hides dependencies; prefer DI
##### Structural Patterns
- **Adapter** → Convert interface A to interface B; class adapter (inheritance) vs object adapter (composition)
- **Bridge** → Separate abstraction from implementation; both vary independently; e.g. `Shape` + `RenderAPI`
- **Composite** → Tree structure; leaf and composite implement same interface; e.g. file system, UI component tree
- **Decorator** → Wrap object to add behavior dynamically; `BufferedInputStream` wraps `FileInputStream`
- **Facade** → Simplified interface to complex subsystem; e.g. `OrderService` hides inventory+payment+shipping
- **Flyweight** → Share common state across many fine-grained objects; e.g. character objects in text editor
- **Proxy** → Surrogate; types: Virtual (lazy load), Remote (network), Protection (access control), Cache proxy
- **Wrapper** → Generic term for Adapter/Decorator/Proxy; wraps another object
##### Behavioral Patterns
- **Observer** → Notify many subscribers of state change; `EventListener`, `ReactiveStreams`; push vs pull
- **Strategy** → Interchangeable algorithms; `Comparator` is Strategy; select at runtime
- **Command** → Encapsulate request as object; supports undo/redo, logging, queuing; `Runnable` is Command
- **Chain of Responsibility** → Pass request along handler chain; each decides to handle or pass; Servlet filters
- **State** → Object changes behavior when internal state changes; eliminates conditionals; e.g. traffic light
- **Template Method** → Define algorithm skeleton in base class; steps overridden by subclasses; `HttpServlet.service()`
- **Mediator** → Centralize object interactions; reduces direct coupling; e.g. chat room, air traffic control
- **Memento** → Capture and restore object state; undo mechanism; encapsulates snapshot without breaking encapsulation
- **Visitor** → Add operations to object structure without modifying classes; double dispatch
- **Interpreter** → Grammar for a language; AST-based; used in query parsers, expression evaluators
- **Iterator** → Sequential access without exposing internal structure; Java `Iterator<T>`, `Iterable<T>`
##### Enterprise Integration Patterns (EIP)
- **Message Channel** → Pipe connecting sender and receiver; typed channel per message type
- **Message Router** → Route message based on content or metadata; `ContentBasedRouter`
- **Message Filter** → Drop messages not matching criteria
- **Publish-Subscribe** → Broadcast to all interested subscribers; topic-based messaging
- **Dead Letter Channel** → Unprocessable messages; poison pill handling; DLQ in Kafka/RabbitMQ
- **Aggregator** → Combine related messages into one; e.g. gather order items before processing
- **Claim Check** → Store large payload externally; pass reference in message; S3 + SQS pattern
- **Idempotent Receiver** → Process message at-least-once safely; dedup via message ID
##### Microservices Patterns
- **API Gateway** → Single entry point; routing, auth, rate-limiting, aggregation; Kong, AWS API Gateway
- **Backend for Frontend (BFF)** → Separate API per client type (mobile/web/partner); tailored responses
- **Service Discovery** → Dynamic service location; Eureka (client-side), AWS ALB (server-side)
- **Circuit Breaker** → States: Closed (normal) → Open (failing) → Half-Open (testing recovery); Resilience4j
- **Bulkhead** → Isolate thread pools per downstream service; failure in one doesn't starve others
- **Saga Pattern** → Distributed transaction via sequence of local transactions; rollback via compensations
- **Database per Service** → Each service owns its data store; no direct DB sharing
- **Event Sourcing** → Persist events, not state; replay to reconstruct; immutable audit log
- **CQRS** → Separate read model (query) from write model (command); optimize each independently
- **Strangler Fig** → Incrementally replace legacy system; new system handles increasing traffic
- **Sidecar** → Deploy helper process alongside main service; handles logging, proxy, config
##### Distributed System Patterns
- **Leader Election** → One node coordinates; others follow; Raft/ZooKeeper/etcd
- **Consensus (Raft/Paxos)** → Agreement among distributed nodes despite failures; basis for distributed DBs
- **Distributed Locking** → Coordinate across services; Redis SETNX, ZooKeeper; careful with clock skew
- **Gossip Protocol** → Peer-to-peer state propagation; eventually consistent membership; Cassandra ring
- **Sharding** → Horizontal data partitioning; shard key determines partition; avoid hot shards
- **Consistent Hashing** → Distribute keys across nodes; minimal reshuffling on node add/remove
- **Two-Phase Commit (2PC)** → Prepare + Commit phases; coordinator + participants; single point of failure risk
##### Caching Patterns
- **Cache Aside (Lazy Loading)** → App manages cache; read: check cache → DB on miss → populate; most common
- **Read Through** → Cache handles DB fetch on miss; transparent to app
- **Write Through** → Write to cache and DB synchronously; consistent but higher write latency
- **Write Behind (Write Back)** → Write to cache; async flush to DB; fast writes; risk of data loss
- **Refresh Ahead** → Pre-populate cache before expiry; reduces cache miss spikes
- **Eviction Policies** → LRU (Least Recently Used), LFU (Least Frequently Used), TTL-based
##### Resilience Patterns
- **Retry** → Retry transient failures; with exponential backoff + jitter; max retries + timeout
- **Exponential Backoff** → Delay doubles each retry; add jitter to prevent thundering herd
- **Circuit Breaker** → Stop calls to failing service; self-healing; track error rate/window
- **Timeout** → Bound waiting time; prevents resource exhaustion from slow downstream
- **Fallback** → Return default/cached response when service fails; degrade gracefully
- **Bulkhead Isolation** → Separate resource pools; failure in one doesn't affect others
- **Health Check** → `/health` endpoint; liveness (is alive) vs readiness (can serve traffic)
##### Concurrency Patterns
- **Thread Pool** → Bounded workers; `ExecutorService`; reuse threads; avoid thread-per-request
- **Producer-Consumer** → Decouple production from consumption; `BlockingQueue` bridges them
- **Reader-Writer Lock** → Multiple concurrent readers; exclusive writer; `ReadWriteLock`
- **Future / Promise** → Async result placeholder; `CompletableFuture` in Java
- **Fork-Join** → Divide work recursively; parallel sub-tasks; merge results; `ForkJoinPool`
- **Actor Model** → Actors communicate via messages; no shared state; Akka
- **Immutability Pattern** → Immutable objects are inherently thread-safe; share freely
- **Double-Checked Locking** → `volatile` field required; checks before and inside `synchronized`
##### Event-Driven Patterns
- **Event Notification** → Notify that something happened; minimal payload; consumers fetch details
- **Event-Carried State Transfer** → Event contains all state; consumers don't need to call back
- **Event Sourcing** → Events are source of truth; project state from event stream
- **Event Replay** → Rebuild state by replaying historical events; enables temporal queries
- **Pub/Sub** → Publishers emit to topics; subscribers filter; decoupled
##### Cloud & Infrastructure Patterns
- **Blue-Green Deployment** → Two identical envs; switch traffic; instant rollback
- **Canary Deployment** → Route small % of traffic to new version; monitor; expand gradually
- **Rolling Deployment** → Replace instances incrementally; lower risk; no extra cost
- **Immutable Infrastructure** → Build new instead of patching; consistent, reproducible
- **Auto Scaling** → Add/remove instances based on load; horizontal elasticity
- **Service Mesh** → Sidecar proxy per service; handles traffic, mTLS, observability; Istio
##### UI / Frontend Patterns
- **MVC** → Model (data), View (UI), Controller (handler); classic web pattern
- **MVP** → Model, View (passive), Presenter (logic); testable; Android
- **MVVM** → Model, View (binds to ViewModel), ViewModel (state+commands); reactive UIs
- **Flux / Redux** → Unidirectional data flow; Action → Dispatcher → Store → View
- **Component-Based** → UI as composable, reusable components; React, Angular, Vue
##### Analytics & Data Patterns
- **Lambda Architecture** → Batch layer + Speed layer + Serving layer; handles historical + real-time
- **Kappa Architecture** → Stream processing only; simplification of Lambda; all data as stream
- **ETL / ELT** → Extract-Transform-Load vs Extract-Load-Transform; ELT leverages cloud DW power
- **Data Lake Pattern** → Raw data storage; schema-on-read; flexible for analytics
##### Anti-Patterns
- **God Object** → One class does everything; SRP violation; maintenance nightmare
- **Big Ball of Mud** → No structure; everything coupled; impossible to change safely
- **Distributed Monolith** → Microservices with shared DB or tight sync coupling; worst of both worlds
- **Chatty Services** → Excessive inter-service calls; high latency; aggregate at gateway
- **Lava Flow** → Dead code left because "too risky to remove"; accumulates technical debt
- **Tight Coupling** → Direct dependencies on concretions; no interface abstraction
##### Interview Deep-Dive Keywords
- Always justify pattern choice with trade-offs: Builder over constructor when > 4 params
- Singleton pitfalls: class loaders, serialization, reflection; enum-based Singleton solves all
- Factory vs Builder: Factory creates in one step; Builder for multi-step complex construction
- CQRS trade-off: separate models = eventual consistency between read/write; not for simple CRUDs
- Saga vs 2PC: Saga = eventual consistency + compensation; 2PC = synchronous + coordinator SPOF
- Circuit Breaker: don't set threshold too low or too high; tune per SLO

---

## 59. System Design
##### Core Process
- **Requirements First** → Functional (what system does) + Non-functional (how well it does it)
- **Constraints & Assumptions** → State what you assume; clarify ambiguities upfront
- **Back-of-Envelope Calculation** → Estimate QPS, storage, bandwidth before designing
- **Trade-off Analysis** → Every design choice trades something; articulate explicitly
- **HLD → LLD** → High-Level Design first (components, data flow), then Low-Level (schemas, APIs)
##### Non-Functional Requirements (NFRs)
- **Scalability** → Handle growing load; horizontal > vertical; stateless services enable this
- **Availability** → % uptime; 99.9% = 8.7 hrs/yr downtime; 99.99% = 52 min/yr
- **Reliability** → Consistent correct behavior over time; redundancy, retries, checkpointing
- **Durability** → Data survives failures; replication, WAL, backups
- **Latency** → P50/P95/P99; tail latency matters; P99 = 1 in 100 requests slow
- **Throughput** → Requests per second; increase via horizontal scaling + async
- **Consistency** → Strong (immediate) vs eventual; CAP theorem governs distributed systems
- **Fault Tolerance** → System continues operating despite partial failure
- **Observability** → Logs, metrics, traces; "you can't fix what you can't see"
- **Maintainability** → Easy to change; loose coupling, good abstractions, documentation
##### Architecture Styles
- **Monolith** → Single deployable; simple to start; harder to scale independently
- **Modular Monolith** → Monolith with clear internal module boundaries; better than unstructured
- **Microservices** → Independent services; independent deploy; adds operational complexity
- **Event-Driven Architecture** → Services communicate via events; decoupled; async
- **CQRS + Event Sourcing** → Separate read/write models; store events as source of truth
- **Serverless** → No server management; function-per-event; cold start trade-off
- **Hexagonal Architecture** → Core domain isolated; adapters for external systems; testable
##### System Components
- **API Gateway** → Entry point; routing, auth, rate limiting, aggregation; Kong, AWS API GW
- **Load Balancer** → Distribute requests; L4 (TCP) vs L7 (HTTP); round-robin, least-conn, IP-hash
- **Reverse Proxy** → Sits in front of backend; terminates SSL, caches, compresses; Nginx
- **CDN** → Cache static assets at edge; reduce latency globally; CloudFront, Fastly
- **Message Broker** → Async communication; Kafka (streaming), RabbitMQ (queuing), SQS
- **Cache** → In-process (Caffeine), distributed (Redis, Memcached); reduce DB load
- **Service Mesh** → Sidecar proxies; handles mTLS, retries, circuit breaking; Istio, Linkerd
##### Networking & Communication
- **REST** → Stateless; HTTP verbs; JSON; widely supported; simple
- **gRPC** → Protocol Buffers; HTTP/2; bidirectional streaming; lower latency; internal services
- **GraphQL** → Client specifies query shape; reduces over/under-fetching; single endpoint
- **WebSockets** → Full-duplex; persistent connection; real-time (chat, live updates)
- **Idempotency** → Safe to retry; PUT/DELETE are idempotent; POST is not by default
- **Keep-Alive** → Reuse TCP connections; reduces handshake overhead
##### Database Design
- **Schema Design** → Normalize for write; denormalize for read; choose per access pattern
- **Indexing** → B-Tree (range queries), Hash (equality), Covering (all fields in index), Composite
- **Partitioning** → Horizontal (rows by range/hash), Vertical (columns into separate tables)
- **Sharding** → Distribute data across multiple DB instances; shard key selection is critical
- **Replication** → Leader-Follower: leader writes, followers read; Multi-master: any node writes
- **Read Replicas** → Offload reads; eventual consistency; good for read-heavy workloads
- **ACID vs BASE** → RDBMS: ACID; NoSQL: typically BASE; choose per consistency requirement
##### Caching Strategy
- **Cache Aside** → App reads cache, falls back to DB, populates cache; most common
- **TTL** → Time-to-live; auto-expire stale data; balance freshness vs load
- **Cache Invalidation** → Hardest problem; event-driven invalidation or TTL
- **Eviction Policies** → LRU (most popular), LFU (frequency-based), TTL
- **Thundering Herd** → Mass cache expiry → all requests hit DB; stagger TTLs, add jitter
##### Data Consistency
- **Strong Consistency** → Every read sees latest write; requires coordination; higher latency
- **Eventual Consistency** → Reads may see stale data; resolves over time; higher availability
- **CAP Theorem** → Partition happens in distributed systems; choose CP or AP
- **Quorum** → W + R > N ensures consistency; e.g. N=3, W=2, R=2
- **MVCC** → Multiple versions; readers don't block writers; PostgreSQL, Cassandra
##### Distributed Systems
- **Consensus (Raft/Paxos)** → Agreement despite failures; Raft is more understandable
- **Leader Election** → One coordinator; others follow; etcd/ZooKeeper
- **Clock Synchronization** → Clocks drift; use logical clocks (Lamport), vector clocks for ordering
- **Distributed Locking** → Redis SETNX + TTL; or Zookeeper ephemeral nodes; beware of clock skew
- **Two-Phase Commit** → Prepare + Commit; coordinator failure = blocking; avoid in microservices
##### Messaging & Streaming
- **At-most-once** → No retries; messages may be lost; fire-and-forget analytics
- **At-least-once** → Retries; may duplicate; idempotent consumer required
- **Exactly-once** → Hardest; idempotent producer + transactional consumer; Kafka supports
- **Consumer Groups** → Multiple consumers share partition load; one partition → one consumer in group
- **Backpressure** → Slow consumer signals slow producer; Kafka: consumers pull (natural backpressure)
- **Dead Letter Queue** → Unprocessable messages; alert on DLQ depth
##### Scalability Patterns
- **Horizontal Scaling** → Add more instances; requires stateless services or external session store
- **Stateless Services** → No local state; any instance handles any request; enable horizontal scale
- **Database Sharding** → Partition data; enables write scaling; complex query patterns
- **Read Scaling** → Read replicas; caching; CDN for static
- **Write Scaling** → Sharding; async writes; CQRS write model
##### Fault Tolerance
- **Retry + Exponential Backoff** → Retry transient failures; back off exponentially with jitter
- **Circuit Breaker** → Stop calling failing dependency; fast-fail; recover when healthy
- **Bulkhead** → Isolate thread pools / connection pools per downstream
- **Graceful Degradation** → Serve partial/cached data when dependency is down
- **Health Checks** → Liveness (restart if dead), Readiness (route traffic only when ready)
##### Observability
- **Logging** → Structured (JSON); include trace ID; queryable; ELK / Splunk
- **Metrics** → Counters, gauges, histograms; Prometheus + Grafana; alert on SLO breach
- **Distributed Tracing** → Request spans across services; Jaeger, Zipkin, OpenTelemetry
- **SLI / SLO / SLA** → SLI: what you measure; SLO: target (99.9% < 200ms); SLA: contract with penalty
- **Alerting** → Alert on symptoms (SLO breach), not causes (high CPU)
##### Performance Engineering
- **Latency Optimization** → Connection pooling, caching, async, fewer hops, binary protocols
- **Throughput Optimization** → Batching, async processing, parallelism, horizontal scaling
- **Connection Pooling** → Reuse DB/HTTP connections; HikariCP for DB
- **Compression** → Gzip responses; reduce bandwidth; CPU trade-off
- **Async Processing** → Queue work; return 202 Accepted; worker processes later
##### Interview Keywords (Must Use)
- **QPS** → Queries Per Second; estimate: DAU × avg_requests/day ÷ 86400
- **P99 Latency** → 99th percentile; tail latency affects user experience
- **Read/Write Ratio** → Shapes database and caching strategy
- **Back-of-Envelope** → Storage: 1 tweet = 300 bytes; 100M tweets/day = 30 GB/day
- **Capacity Planning** → Peak vs average load; headroom for spikes (2–3x average)
- **Bottleneck Identification** → DB? Network? CPU? Memory? Identify and design around it
##### Advanced / Staff+ Topics
- **Multi-tenancy** → Shared vs isolated infrastructure; data isolation per tenant
- **Zero Downtime Deployment** → Blue-green, canary, rolling; feature flags for decoupling deploy from release
- **Active-Active** → Multiple regions handle writes; conflict resolution required
- **Active-Passive** → One region primary; failover to secondary; RPO/RTO trade-off
- **Geo-replication** → Data replicated across regions; latency vs consistency trade-off
- **Cost Optimization (FinOps)** → Right-size instances; reserved vs spot; data transfer costs
##### Anti-Patterns
- **Single Point of Failure (SPOF)** → Any component without redundancy; design out SPOFs
- **Tight Coupling** → Services directly call each other synchronously; add messaging layer
- **Chatty Services** → Too many fine-grained calls; aggregate or use BFF
- **Distributed Monolith** → Microservices sharing same DB; worst of both worlds
- **Premature Scaling** → Over-engineer for scale you don't have; YAGNI applies to infra too

---

## 60. Domain-Driven Design (DDD)
##### Core Concepts
- **Domain** → The problem space you're solving; business knowledge and rules
- **Subdomain** → Decomposition of domain; Core (competitive advantage), Supporting (necessary), Generic (commodity)
- **Domain Model** → Software abstraction of domain concepts; code mirrors business language
- **Ubiquitous Language** → Shared vocabulary between developers and domain experts; used in code, docs, conversations
- **Domain Knowledge** → Deep understanding of business rules, processes, constraints
##### Strategic Design
- **Bounded Context** → Explicit boundary where a domain model applies; model means different things in different contexts
- **Context Map** → Visual representation of bounded context relationships and integration patterns
- **Context Mapping Patterns**:
  - **Partnership** → Two teams collaborate closely; shared success/failure
  - **Shared Kernel** → Share subset of model; dangerous; coordinate changes carefully
  - **Customer-Supplier** → Upstream (supplier) drives API; downstream (customer) adapts
  - **Conformist** → Downstream conforms to upstream model; no translation
  - **Anti-Corruption Layer (ACL)** → Translation layer; protects your domain from external model corruption
  - **Open Host Service** → Publish a protocol/API for multiple consumers; versioned
  - **Separate Ways** → No integration; teams solve independently
##### Tactical Design — Building Blocks
- **Entity** → Has unique identity; mutable state; equality by identity (`orderId`); lifecycle matters
- **Value Object** → No identity; equality by value; immutable; self-validating; e.g. `Money`, `Address`
- **Aggregate** → Cluster of entities + value objects; transactional consistency boundary; one root
- **Aggregate Root** → Entry point to aggregate; external objects reference root only; enforces invariants
- **Repository** → Persistence abstraction; collection-like interface; one per aggregate root
- **Factory** → Creates complex aggregates/entities; encapsulates creation logic
- **Domain Service** → Business logic that doesn't belong to a single entity; stateless; e.g. `TransferService`
- **Application Service** → Orchestrates use cases; thin; coordinates domain objects + infrastructure
- **Domain Event** → Something significant that happened in the domain; past tense; e.g. `OrderPlaced`
##### Entity Deep Dive
- Identity persists through state changes; `equals()` by identity (ID)
- Lifecycle: created → active → archived/deleted
- Entities should be rich (behavior), not anemic (data-only)
##### Value Object Deep Dive
- Immutable: all fields `final`; no setters
- Equality by value: `equals()` compares all fields
- Self-validation: constructor rejects invalid state
- Avoid: using primitives where Value Objects would carry meaning (Primitive Obsession)
##### Aggregate Design Rules
- **Consistency Boundary** → All invariants maintained within one transaction per aggregate
- **Reference by ID** → Aggregates reference other aggregates by ID, not direct object reference
- **Small Aggregates** → Large aggregates = contention; design for single-entity aggregates usually
- **Invariants** → Business rules that must always be true within aggregate; enforced by root
##### CQRS (Command Query Responsibility Segregation)
- **Command Model** → Handles writes; validates business rules; emits events; consistency-focused
- **Query Model** → Handles reads; denormalized; optimized for specific read patterns
- **Separation** → Read and write models can use different databases (polyglot persistence)
- **Trade-off** → Complexity + eventual consistency between read/write models; not for simple CRUDs
##### Event Sourcing
- **Event Store** → Append-only log of all domain events; never update or delete
- **Event Replay** → Rebuild state by replaying events; enables point-in-time queries
- **Snapshotting** → Periodically save aggregate state; avoid replaying entire history
- **Event Versioning** → Events must be backward compatible; upcasting for old event formats
- **Immutable Log** → Source of truth; audit log for free; enables temporal reasoning
- **Trade-offs** → Complexity; eventual read model; schema evolution challenges
##### Architecture Patterns in DDD
- **Layered Architecture** → UI → Application → Domain → Infrastructure; Domain has no outward dependencies
- **Hexagonal Architecture** → Domain at center; ports (interfaces) define boundaries; adapters implement ports
- **Clean Architecture** → Dependency Rule: source code dependencies point inward toward domain
- **Onion Architecture** → Concentric rings; domain at core; progressively less stable outward
##### Microservices + DDD
- **Bounded Context = Microservice** → Natural boundary for service decomposition
- **Data Ownership** → Each service owns its aggregate data; no shared tables
- **Domain Events as Integration** → Publish events when aggregate state changes; consumers react
- **Saga Pattern** → Cross-aggregate/service workflows; orchestration or choreography
- **Choreography** → Services react to events; decoupled; harder to trace
- **Orchestration** → Central coordinator (Saga Orchestrator); easier to trace; central coupling
##### Consistency & Transactions
- **Strong Consistency** → Within aggregate; ACID transaction; single bounded context
- **Eventual Consistency** → Across aggregates/services; via domain events; accept temporary divergence
- **Distributed Transactions** → Avoid 2PC; prefer Saga; accept eventual consistency
##### Domain Modeling Techniques
- **Event Storming** → Workshop: all domain events on wall; identify aggregates, commands, bounded contexts
- **Domain Storytelling** → Describe domain as stories; identify actors, work objects, activities
- **Invariant Modeling** → Explicitly model what must always be true; drives aggregate boundaries
##### Anti-Patterns
- **Anemic Domain Model** → Objects are data bags; all logic in service layer; OOP anti-pattern
- **God Object** → One class/aggregate handles everything; violates SRP
- **Shared Database Across Contexts** → Two bounded contexts share tables; tight coupling; no autonomy
- **Tight Coupling Between Contexts** → Direct calls without ACL; one context change breaks another
- **Big Ball of Mud** → No clear bounded contexts; everything entangled
##### Interview Deep-Dive Keywords
- "Bounded Context defines clear ownership and consistent language within that boundary"
- "Aggregate Root enforces all invariants; external objects can only reference the root"
- "ACL prevents external model pollution; translate at the boundary"
- "CQRS helps when read/write access patterns diverge significantly"
- "Event Sourcing enables full audit trail and temporal queries but adds operational complexity"
- Anemic Domain Model: code smell; business logic scattered across service classes
- DDD is expensive; use for Core Domain; use CRUD for Generic/Supporting subdomains

---

## 61. Microservices Architecture
##### Core Concepts
- **Microservices** → Small, autonomous services; each owns its data; independently deployable
- **SOA vs Microservices** → SOA: shared DB, heavy ESB; Microservices: lightweight, decentralized
- **Service Decomposition** → By business capability (DDD Bounded Context), by subdomain, by team
- **Bounded Context** → Natural service boundary; model consistency within; integrate via events/APIs
- **Independent Deployability** → Deploy one service without touching others; CI/CD per service
- **Autonomy** → Each service owns code, data, deployment; no shared databases
- **Loose Coupling** → Services communicate via APIs/events; no direct internal access
- **High Cohesion** → Service does one thing well; all code inside relates to that capability
##### Service Design
- **Service Granularity** → Too coarse = monolith; too fine = chatty services; align with team size
- **Stateless Services** → No local state; session externalized to Redis; enables horizontal scaling
- **API-first Design** → Design contract before implementation; enables parallel development
- **Backward Compatibility** → Never break existing consumers; add new fields don't remove
- **Versioning** → URL versioning (`/v1/`), header versioning; version when breaking changes needed
##### Communication
- **Synchronous (REST/gRPC)** → Direct call; simple; tight temporal coupling; use for queries
- **Asynchronous (Events/Messaging)** → Via broker; decoupled; better for commands; Kafka/RabbitMQ
- **Request-Response** → Caller waits; `CompletableFuture` or blocking; simpler flow
- **Event-Driven** → Fire and forget; high scalability; harder to trace; choreography
- **Idempotency** → Critical for retries; use idempotency keys; make PUT safe to repeat
##### Service Discovery
- **Client-Side Discovery** → Client queries registry (Eureka); client does load balancing
- **Server-Side Discovery** → Load balancer queries registry; client doesn't need to know
- **Netflix Eureka** → Client-side; heartbeat-based; AP (available over consistent)
- **Consul** → Health checking + service discovery + KV store; CP or AP configurable
##### API Gateway
- **Routing** → Map external URL to internal service
- **Rate Limiting** → Token bucket; protect services from abuse
- **Authentication** → Validate JWT/OAuth2 at gateway; don't repeat in each service
- **Aggregation** → Combine multiple service calls into one response (BFF pattern)
- **Tools** → Kong, AWS API Gateway, Netflix Zuul, Spring Cloud Gateway
##### Security
- **OAuth2 / OpenID Connect** → Delegated authorization + identity; standard for modern apps
- **JWT** → Self-contained token; no DB lookup; verify signature; short expiry + refresh token
- **mTLS** → Mutual TLS; both sides authenticate; used in service mesh for service-to-service
- **Zero Trust** → No implicit trust; verify every request even inside network perimeter
##### Data Management
- **Database per Service** → Core principle; polyglot persistence; no shared tables
- **Data Consistency** → Eventual via events; immediate only within single service transaction
- **Data Replication** → Publish events; consumers maintain their own read-optimized store
- **Polyglot Persistence** → Each service picks best DB: orders→PostgreSQL, catalog→Elasticsearch
##### Distributed Transactions
- **Saga Pattern** → Series of local transactions; each publishes event; compensation on failure
- **Orchestration Saga** → Central orchestrator tells services what to do; easier trace; single point coupling
- **Choreography Saga** → Services react to events; decoupled; harder to visualize overall flow
- **Compensation Transactions** → Undo previously committed local transaction; must be idempotent
- **2PC (Avoid)** → Blocks resources; coordinator SPOF; use Saga instead in microservices
##### Resilience
- **Circuit Breaker** → Open on error threshold; fast fail; half-open to probe recovery; Resilience4j
- **Retry + Backoff** → Retry transient failures; exponential backoff + jitter; max retries
- **Timeout** → Every outbound call has timeout; prevents cascading slowness
- **Bulkhead** → Isolate thread pools; one slow service doesn't exhaust all threads
- **Fallback** → Return cached/default data when service unavailable
- **Graceful Degradation** → Core features work; non-critical features degrade
##### Configuration Management
- **Externalized Configuration** → No hardcoded config; 12-factor app principle
- **Config Server** → Centralized config store; Spring Cloud Config, HashiCorp Vault, AWS Parameter Store
- **Feature Flags** → Toggle features without deploy; LaunchDarkly, Unleash
- **Dynamic Config** → Update config without restart; watch for changes
##### Observability
- **Correlation ID** → Unique ID per request; pass through all service calls; tie logs together
- **Distributed Tracing** → Trace spans across services; Jaeger, Zipkin, AWS X-Ray
- **Log Aggregation** → Centralize logs; ELK (Elasticsearch + Logstash + Kibana), Splunk
- **Metrics** → Per-service latency, error rate, throughput; Prometheus + Grafana
- **SLO-Driven Monitoring** → Define what matters; alert on SLO breach, not infra metrics
##### Deployment
- **Containerization** → Docker; package app + dependencies; consistent environments
- **Orchestration** → Kubernetes; schedule, scale, heal containers; rolling updates
- **CI/CD per Service** → Independent build/test/deploy pipelines; trunk-based development
- **Blue-Green** → Instant cutover; instant rollback; double the infra cost
- **Canary** → Gradual rollout; catch issues before full release; traffic weighting
- **Rolling** → Replace instances incrementally; no extra cost; brief inconsistency during rollout
##### Service Mesh
- **Sidecar Proxy** → Envoy proxy per pod; intercepts all traffic
- **Traffic Management** → Retries, timeouts, circuit breaking at mesh level; not in app code
- **mTLS** → Automatic mutual TLS between services; zero-trust networking
- **Observability** → Traces, metrics from mesh layer automatically
- **Tools** → Istio (feature-rich, complex), Linkerd (simpler, less overhead)
##### Testing
- **Consumer Contract Testing** → Consumer defines expected API; provider verifies; Pact framework
- **Integration Testing** → Test service boundaries; WireMock for mocking downstream services
- **Chaos Engineering** → Deliberately inject failures; Chaos Monkey; verify resilience
- **End-to-End** → Full flow test; expensive; limited count; focus on critical paths
##### Anti-Patterns
- **Distributed Monolith** → Micro-services sharing DB or tightly synchronized; all complexity, no benefits
- **Chatty Services** → Service A calls B, C, D, E synchronously; high latency; use aggregation or events
- **Shared Database** → Two services share tables; breaks data ownership; hidden coupling
- **Over-fragmentation** → Too many tiny services; operational overhead exceeds benefit; team can't own them all
- **Tight Coupling via Events** → Event schema shared like a DB schema; backward compat nightmare
##### Interview Deep-Dive Keywords
- "Database per service ensures loose coupling and independent scaling"
- "Saga handles distributed transactions without 2PC by using compensating transactions"
- "API Gateway centralizes cross-cutting concerns: auth, rate limiting, routing"
- "Event-driven decouples services temporally and logically"
- "Service mesh moves operational concerns (retries, mTLS, tracing) out of application code"
- Bounded Context alignment: one microservice per bounded context (DDD marriage with microservices)
- Microservices cost: operational overhead; only worthwhile when team + deployment velocity demands it

---

## 62. Spring Framework & Spring Boot
##### Core IoC & DI
- **IoC (Inversion of Control)** → Framework controls object creation and lifecycle; you define "what", Spring does "how"
- **Dependency Injection** → Objects receive dependencies rather than creating them; constructor > setter > field injection
- **ApplicationContext** → Central Spring container; loads beans; manages lifecycle; wraps BeanFactory
- **BeanFactory** → Lazy-loading lightweight container; lower-level; ApplicationContext preferred
- **Bean Definition** → Metadata: class, scope, dependencies, init/destroy methods
- **Bean Scopes** → `singleton` (default, one per context), `prototype` (new per inject), `request`/`session` (web)
- **Environment / Profiles** → `@Profile("prod")`; activate different beans per environment
##### Bean Management
- **`@Component`** → Generic; auto-detected by classpath scan
- **`@Service`** → Service layer; semantically meaningful; same as `@Component`
- **`@Repository`** → DAO layer; enables exception translation (DataAccessException)
- **`@Controller` / `@RestController`** → Web layer; `@RestController` = `@Controller` + `@ResponseBody`
- **`@Configuration` + `@Bean`** → Java-based config; explicit bean declaration
- **`@Autowired`** → Inject dependency; prefer constructor injection (immutable, testable)
- **`@Qualifier`** → Disambiguate when multiple beans of same type
- **`@Primary`** → Default bean when multiple candidates
- **`BeanPostProcessor`** → Hook into bean initialization; used by `@Autowired`, AOP, etc.
- **Circular Dependency** → A depends on B depends on A; break with setter injection or `@Lazy`
##### Spring Boot Core
- **Auto-Configuration** → `@EnableAutoConfiguration`; detects classpath, configures beans automatically
- **`@SpringBootApplication`** → `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`
- **Starter Dependencies** → `spring-boot-starter-web`, `spring-boot-starter-data-jpa`; bundle related dependencies
- **Embedded Server** → Tomcat/Jetty/Netty bundled in JAR; `java -jar` to run; no WAR needed
- **application.properties / application.yml** → Externalized config; profiles override (`application-prod.yml`)
- **`@ConfigurationProperties`** → Type-safe config binding; prefer over `@Value` for groups
- **Auto-Configuration Internals** → `spring.factories` / `AutoConfiguration.imports`; `@Conditional` annotations
- **Custom Starter** → Package auto-configuration as reusable module; `META-INF/spring/` registration
##### Spring MVC
- **DispatcherServlet** → Front controller; routes all requests to handlers
- **Handler Mapping** → Maps URL to controller method; `@RequestMapping`
- **`@GetMapping` / `@PostMapping` etc.** → Shorthand for `@RequestMapping(method=...)`
- **`@PathVariable`** → Extract URL path segment; `GET /users/{id}`
- **`@RequestParam`** → Query param; `GET /users?page=1`
- **`@RequestBody` / `@ResponseBody`** → Serialize/deserialize JSON via Jackson
- **`@ControllerAdvice`** → Global exception handling; `@ExceptionHandler` methods
- **`@Valid`** → Trigger Bean Validation; `MethodArgumentNotValidException` on failure
- **ResponseEntity** → Full control over HTTP response (status, headers, body)
##### Spring WebFlux (Reactive)
- **Reactive Programming** → Non-blocking; event loop; backpressure support; Project Reactor
- **Mono** → 0 or 1 item; `Mono<User>` for single result
- **Flux** → 0 to N items; `Flux<User>` for stream of results
- **Non-blocking I/O** → Netty event loop; fewer threads; higher concurrency
- **Backpressure** → Consumer controls demand; `request(n)` signals producer
- **When to use** → I/O-bound with many concurrent connections; not CPU-bound tasks
##### Data Access (Spring Data / JPA)
- **Spring Data Repository** → `JpaRepository<T, ID>` provides CRUD + pagination for free
- **Query Methods** → `findByEmailAndStatus(String email, Status s)` → auto-generates SQL
- **`@Query`** → Custom JPQL or native SQL
- **`@Transactional`** → Declarative transaction; propagation (`REQUIRED`, `REQUIRES_NEW`), isolation, rollback rules
- **N+1 Problem** → Lazy loading in loop triggers N extra queries; fix with `JOIN FETCH` or `@EntityGraph`
- **Lazy vs Eager Fetching** → Lazy: load on access (default for collections); Eager: load with parent; prefer Lazy
- **Dirty Checking** → Hibernate tracks entity changes; auto-generates UPDATE on transaction commit
- **`@Entity` / `@Table`** → Map class to DB table; `@Id`, `@GeneratedValue`, `@Column`
- **Relationships** → `@OneToMany`, `@ManyToOne`, `@ManyToMany`; own side has `@JoinColumn`
##### Spring Security
- **Security Filter Chain** → Series of filters; each request passes through; authentication + authorization
- **Authentication** → Who are you? `UsernamePasswordAuthenticationToken`, JWT, OAuth2
- **Authorization** → What can you do? `@PreAuthorize("hasRole('ADMIN')")`, `HttpSecurity.authorizeRequests()`
- **SecurityContext** → Holds `Authentication`; `SecurityContextHolder.getContext().getAuthentication()`
- **OAuth2 / OpenID Connect** → Delegated auth; Spring Security OAuth2 Resource Server for JWT validation
- **JWT** → Validate signature + expiry in filter; stateless; pair with refresh token
- **CSRF** → Cross-Site Request Forgery; enabled by default for browser clients; disable for stateless APIs
- **CORS** → Cross-Origin Resource Sharing; configure `allowedOrigins` in `CorsConfigurer`
##### Spring Cloud (Microservices)
- **Service Discovery** → Eureka (Netflix); `@EnableEurekaClient`; heartbeat registration
- **Config Server** → Centralized config; `spring-cloud-config-server`; Git-backed
- **API Gateway** → Spring Cloud Gateway; reactive; routing + filters
- **Circuit Breaker** → Resilience4j integration; `@CircuitBreaker(name="service", fallbackMethod="fallback")`
- **Feign Client** → Declarative HTTP client; `@FeignClient(name="user-service")`; integrates with Ribbon/LB
- **Distributed Tracing** → Micrometer Tracing + OpenTelemetry; correlation ID propagation
##### Messaging
- **Spring Kafka** → `@KafkaListener`; `KafkaTemplate.send()`; consumer group config
- **Spring AMQP** → RabbitMQ integration; `@RabbitListener`; exchange + queue binding
- **Dead Letter Queue** → Configure via Spring; `@DltHandler` for Kafka; `x-dead-letter-exchange` for RabbitMQ
##### AOP (Aspect-Oriented Programming)
- **Aspect** → Module of cross-cutting concern (logging, security, transactions)
- **Advice** → What to do: `@Before`, `@After`, `@AfterReturning`, `@AfterThrowing`, `@Around`
- **Join Point** → Point in execution (method call); Spring AOP: method execution only
- **Pointcut** → Expression selecting join points; `execution(* com.example.service.*.*(..))`
- **Proxy-based AOP** → Spring wraps bean in proxy; works for public methods only; self-invocation bypasses AOP
##### Testing
- **`@SpringBootTest`** → Full integration test; loads complete ApplicationContext; slow
- **`@WebMvcTest`** → Test controllers only; MockMvc; no service/repo beans
- **`@DataJpaTest`** → Test repositories; embedded DB (H2); transaction per test (rollback)
- **MockMvc** → Test HTTP layer without real server; `perform(get("/users")).andExpect(status().isOk())`
- **`@MockBean`** → Replace real bean with Mockito mock in Spring context
##### Spring Boot Advanced
- **`@Conditional`** → Conditional bean registration; `@ConditionalOnClass`, `@ConditionalOnProperty`, etc.
- **Boot Lifecycle Events** → `ApplicationStartingEvent`, `ApplicationReadyEvent`; use `@EventListener`
- **Actuator** → `/actuator/health`, `/actuator/metrics`, `/actuator/env`; enable in production
- **Micrometer** → Metrics abstraction; integrates with Prometheus, Datadog, CloudWatch
##### Performance & Tuning
- **HikariCP** → Default Spring Boot connection pool; `spring.datasource.hikari.*` tuning
- **`@Cacheable`** → Cache method result; `@CacheEvict` to invalidate; backed by Redis/Caffeine
- **Thread Pool Tuning** → `server.tomcat.threads.max` for MVC; WebFlux uses event loop (don't block!)
- **Lazy Initialization** → `spring.main.lazy-initialization=true`; faster startup; lazy bean creation
##### Common Pitfalls
- **`@Transactional` on private method** → Proxy bypassed; no transaction; must be public
- **Circular Dependency** → Constructor injection fails at startup; break the cycle
- **Blocking in WebFlux** → Blocks event loop thread; wrap in `Schedulers.boundedElastic()`
- **N+1 Queries** → Fetch all with JOIN FETCH; use `@EntityGraph` on repository methods
- **Overusing `@Autowired` on fields** → Hard to test; prefer constructor injection
##### Interview Deep-Dive Keywords
- "Spring Boot auto-configuration uses `@Conditional` annotations to wire beans based on classpath"
- "Constructor injection is preferred: immutable, testable, no reflection, explicit dependencies"
- "`@Transactional` uses AOP proxy; works only for public methods called from outside the class"
- "WebFlux vs MVC: WebFlux for high concurrency I/O-bound; MVC for team familiarity and CPU-bound"
- "N+1 is the most common JPA performance issue; always check Hibernate SQL logs"

---

## 63. Apache Kafka
##### Core Concepts
- **Apache Kafka** → Distributed event streaming platform; high-throughput, low-latency, durable
- **Event Streaming** → Continuous flow of events; store and process in real-time and historically
- **Distributed Log** → Append-only, ordered, replicated log; the foundation of Kafka's model
- **Publish-Subscribe** → Producers publish to topics; consumers subscribe and read independently
##### Building Blocks
- **Topic** → Named category for events; logical grouping; like a database table for events
- **Partition** → Topic split into ordered, immutable log segments; unit of parallelism
- **Offset** → Sequential ID of each record within a partition; consumers track their position
- **Record / Message** → Key + Value + Headers + Timestamp; key determines partition (by default)
- **Key-based Partitioning** → Same key → same partition → ordering guarantee for that key
##### Producer
- **Partitioning Strategy** → Key hash (default), Round-robin (null key), Custom `Partitioner`
- **Batching** → Records buffered; sent in batches; `linger.ms` + `batch.size` control
- **Compression** → Snappy/LZ4/ZSTD; reduce network + disk; slight CPU cost
- **Idempotent Producer** → `enable.idempotence=true`; exactly-once within session; deduplicates retries
- **Transactional Producer** → `transactional.id`; atomic writes across multiple partitions/topics
- **Acknowledgments (acks)** → `acks=0` (fire+forget), `acks=1` (leader only), `acks=all` (all ISR)
##### Consumer
- **Consumer Group** → Multiple consumers sharing partitions of a topic; one partition → one consumer per group
- **Partition Assignment** → Range, RoundRobin, Sticky; `partition.assignment.strategy`
- **Rebalancing** → New consumer joins/leaves group → partitions redistributed; brief pause
- **Auto Commit** → `enable.auto.commit=true`; risk: message lost if crash before processing
- **Manual Commit** → `commitSync()` / `commitAsync()` after processing; at-least-once guarantee
- **Consumer Lag** → Difference between latest offset and consumer committed offset; monitor closely
##### Cluster Architecture
- **Broker** → Kafka server; stores partitions; handles producer/consumer connections
- **Controller** → One broker elected as controller; manages partition leadership, broker membership
- **Leader / Follower** → Each partition has one leader (handles reads/writes) + followers (replicate)
- **ISR (In-Sync Replicas)** → Replicas caught up to leader; `min.insync.replicas` for durability
- **Replication Factor** → How many copies of each partition; RF=3 standard for production
##### Storage Model
- **Append-only Log** → Write-only to end; O(1) writes; immutable once written
- **Log Segments** → Partition split into segment files; active segment + rolled segments
- **Log Retention** → Time-based (`log.retention.hours`) or size-based (`log.retention.bytes`)
- **Log Compaction** → Keep latest value per key; delete old records with same key; for CDC/changelog topics
##### Delivery Semantics
- **At-most-once** → No retries; messages may be lost; use when loss acceptable (metrics)
- **At-least-once** → Retries; may duplicate; consumer must be idempotent; most common
- **Exactly-once** → Idempotent producer + transactional consumer; `isolation.level=read_committed`
##### Performance & Scaling
- **Zero-copy** → `sendfile()` system call; Kafka bypasses user-space; direct disk-to-network
- **Sequential Disk I/O** → Kafka writes sequentially; HDD friendly; much faster than random I/O
- **Partition Scaling** → Add partitions for more parallelism; can't reduce later; plan upfront
- **Throughput Tuning** → Increase `batch.size`, `linger.ms`; tune `fetch.min.bytes`, `fetch.max.wait.ms`
- **Horizontal Scaling** → Add brokers; reassign partitions; no downtime
##### Kafka Streams
- **KStream** → Stateless record-by-record stream; each record independent
- **KTable** → Changelog stream; represents latest value per key; like a materialized view
- **Stateful Processing** → Aggregations, joins; state stored in RocksDB locally
- **Windowing** → Tumbling (fixed non-overlapping), Sliding (overlapping), Session (activity-based)
- **Aggregation** → `groupByKey().count()`, `.aggregate()`; backed by changelog topic
- **Join Operations** → Stream-Stream (windowed), Stream-Table (enrichment), Table-Table
##### Kafka Connect
- **Source Connector** → Pull data from external system into Kafka (JDBC, S3, Debezium)
- **Sink Connector** → Push Kafka data to external system (Elasticsearch, HDFS, JDBC)
- **Offset Storage** → Kafka topics (`__consumer_offsets`); tracks where connector is
- **Distributed Mode** → Multiple workers; fault-tolerant; auto-rebalances tasks
##### Schema & Serialization
- **Schema Registry** → Central schema store; Avro/Protobuf/JSON Schema
- **Avro** → Binary; compact; schema evolution with compatibility rules
- **Schema Evolution** → Backward (new reader, old writer), Forward (old reader, new writer), Full (both)
- **Protobuf** → Language-neutral; field numbers stable; good for evolution
##### KRaft (ZooKeeper Replacement)
- **KRaft** → Kafka Raft Metadata Mode; removes ZooKeeper dependency; Kafka 3.x+
- **Controller Quorum** → Raft-based; odd number of controllers; leader election built-in
- **Benefits** → Simpler ops; faster startup; larger cluster support; single security model
##### Monitoring
- **Consumer Lag** → Primary health metric; lag > threshold = consumer too slow
- **JMX Metrics** → `kafka.server:type=BrokerTopicMetrics`; integrate with Prometheus JMX exporter
- **Lag Monitoring** → Burrow (LinkedIn), kafka-consumer-groups.sh; alert on growing lag
##### Anti-Patterns
- **Large Messages** → Kafka optimized for small messages; large messages hurt throughput; use S3 + reference
- **Hot Partitions** → All traffic to one partition (bad key choice); spread load with better key strategy
- **Over-partitioning** → Too many partitions → too many file handles, slow rebalance; 10-20x consumers
- **Message Ordering Issues** → Key-based ordering only within partition; across partitions is not ordered
- **Unbounded Retention** → Set retention policy; disk fills up; use compaction for changelog topics
##### Interview Deep-Dive Keywords
- "Kafka provides ordering guarantees only within a partition, not across partitions"
- "Exactly-once requires idempotent producer + `read_committed` isolation on consumer"
- "`acks=all` + `min.insync.replicas=2` ensures durability even on broker failure"
- "Consumer group rebalancing is triggered by join/leave/crash; sticky assignor minimizes movement"
- "Log compaction retains the latest value per key; deleted records have a null (tombstone) value"
- Kafka vs RabbitMQ: Kafka = durable log, replay, high throughput; RabbitMQ = routing, transient queues

---

## 64. Databases
##### Core Concepts
- **DBMS** → Software managing databases; RDBMS (relational), NoSQL, NewSQL
- **Data Model** → How data is organized; relational, document, key-value, column-family, graph
- **Schema** → Structure definition; schema-on-write (SQL) vs schema-on-read (NoSQL/Parquet)
- **OLTP vs OLAP** → OLTP: transactional, many small ops, row-store; OLAP: analytical, few large scans, column-store
- **HTAP** → Hybrid: same system for OLTP + OLAP; TiDB, SingleStore
##### SQL & Querying
- **SELECT / INSERT / UPDATE / DELETE** → Basic CRUD; understand execution order: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
- **JOIN Types** → INNER (matching rows), LEFT OUTER (all left + matching right), RIGHT OUTER, FULL OUTER, CROSS
- **CTE (Common Table Expression)** → `WITH cte AS (...) SELECT ...`; readable; can be recursive
- **Window Functions** → `ROW_NUMBER()`, `RANK()`, `LEAD()`, `LAG()`, `SUM() OVER (PARTITION BY ...)`; no GROUP BY collapsing
- **Subquery vs JOIN** → JOIN usually faster; subquery can be correlated (runs per row) = expensive
- **MERGE / UPSERT** → Insert or update atomically; `ON CONFLICT DO UPDATE` in PostgreSQL
##### Indexing
- **B-Tree Index** → Default; balanced tree; supports equality + range queries; O(log n) lookup
- **Hash Index** → Equality only; O(1) lookup; no range; PostgreSQL heap tables
- **Composite Index** → Multi-column; column order matters; leftmost prefix rule
- **Covering Index** → All query columns in index; no table access; "index-only scan"
- **Clustered Index** → Data physically ordered by index; InnoDB primary key is clustered; one per table
- **Non-clustered** → Separate structure; pointer to row; multiple per table
- **Full-Text Index** → Tokenized search; `MATCH AGAINST` in MySQL; `tsvector` in PostgreSQL
- **When NOT to index** → High-cardinality writes; small tables; columns rarely in WHERE
##### Query Optimization
- **Execution Plan** → `EXPLAIN ANALYZE` in PostgreSQL; see index usage, row estimates, cost
- **Full Table Scan** → No index match; expensive on large tables; check with EXPLAIN
- **Index Scan vs Seq Scan** → Index scan for selective queries; seq scan for large % of table
- **Predicate Pushdown** → Apply filters early in query plan; reduce rows processed
- **Join Optimization** → Nested Loop (small tables), Hash Join (large unsorted), Merge Join (sorted)
- **Statistics** → `ANALYZE` updates table stats; CBO uses stats for plan decisions
- **N+1 Query Problem** → Loop in app triggers N queries; fix with JOIN, batch loading, or caching
##### Transactions & ACID
- **Atomicity** → All or nothing; rollback on failure
- **Consistency** → Constraints always satisfied before and after transaction
- **Isolation** → Concurrent transactions don't interfere; isolation levels control this
- **Durability** → Committed data survives crashes; WAL (Write-Ahead Log) ensures this
##### Isolation Levels
- **Read Uncommitted** → See uncommitted changes (dirty read); almost never used
- **Read Committed** → See only committed data; default in PostgreSQL, Oracle; non-repeatable reads possible
- **Repeatable Read** → Same row reads consistent in transaction; MySQL default; phantom reads possible
- **Serializable** → Strictest; transactions appear to execute serially; highest contention
- **Dirty Read** → Read uncommitted data that may be rolled back
- **Non-Repeatable Read** → Same query returns different data within same transaction
- **Phantom Read** → New rows appear between two reads in same transaction
##### Concurrency Control
- **MVCC (Multi-Version Concurrency Control)** → Each transaction sees snapshot; readers don't block writers; PostgreSQL, MySQL InnoDB
- **Optimistic Concurrency** → Assume no conflict; validate at commit; `version` column; retry on conflict
- **Pessimistic Concurrency** → Lock before read/write; `SELECT FOR UPDATE`; blocks others
- **Deadlock** → Circular lock dependency; DB detects and kills one transaction; app must retry
- **Row Locking vs Table Locking** → Row lock: high concurrency; Table lock: simple but blocks all
##### Storage Engine
- **Write-Ahead Log (WAL)** → Write to log before data pages; enables crash recovery + replication
- **LSM Tree** → Log-Structured Merge Tree; write-optimized; RocksDB, Cassandra, LevelDB
- **SSTable** → Sorted String Table; immutable; compaction merges SSTables; used with LSM
- **Row Store** → Store all columns of a row together; good for OLTP (full row reads)
- **Column Store** → Store each column separately; compress well; good for OLAP (scan few columns)
- **Buffer Cache** → In-memory pages; dirty pages flushed to disk; hit ratio should be > 95%
##### Data Distribution
- **Sharding** → Horizontal partitioning across multiple DB instances; shard key determines location
- **Shard Key Selection** → High cardinality; uniform distribution; avoid hot shards; ideally matches query pattern
- **Consistent Hashing** → Add/remove shards with minimal data movement
- **Replication** → Leader-Follower: one write node; Multi-master: write anywhere; conflict resolution needed
- **Read Replicas** → Offload reads; eventual consistency; replica lag monitoring critical
##### Consistency Models
- **Strong Consistency** → All reads see latest write; requires coordination (quorum); higher latency
- **Eventual Consistency** → Reads may be stale; converges over time; higher availability (Cassandra, DynamoDB)
- **Causal Consistency** → Operations that causally relate are seen in order; between strong and eventual
- **CAP Theorem** → CP (PostgreSQL, HBase) or AP (Cassandra, DynamoDB); partition always happens
- **PACELC** → Also considers latency vs consistency when no partition
##### NoSQL Systems
- **Key-Value** → Redis, DynamoDB; O(1) by key; no query flexibility; for caching, sessions
- **Document** → MongoDB, Couchbase; JSON documents; flexible schema; nested queries
- **Column-Family** → Cassandra, HBase; wide rows; optimized for time-series, write-heavy
- **Graph** → Neo4j; nodes + edges; optimized for relationship traversal; social networks, recommendations
- **Schema-less** → Flexible evolution; data integrity responsibility moves to application
##### Database Design
- **Normalization** → Eliminate redundancy; 1NF, 2NF, 3NF, BCNF; better for writes
- **Denormalization** → Add redundancy for read performance; pre-join data; common in OLAP
- **Star Schema** → Fact table + dimension tables; simple joins; data warehouse standard
- **Snowflake Schema** → Normalized dimensions; more joins; saves space
##### Change Data Capture (CDC)
- **CDC** → Capture DB changes (insert/update/delete) as events; Debezium + Kafka
- **Log-Based CDC** → Read WAL/binlog; non-intrusive; used for real-time data sync, event sourcing
- **Use Cases** → DB-to-DB sync, cache invalidation, event-driven integration
##### Cloud Databases
- **Managed DB** → RDS, Cloud SQL; no infra ops; automated backups, failover
- **Serverless DB** → Aurora Serverless, PlanetScale; auto-scale to zero; variable workloads
- **Multi-AZ** → Synchronous replication to standby AZ; automatic failover; high availability
- **Global Tables** → DynamoDB Global Tables; multi-region active-active; conflict resolution
##### Anti-Patterns
- **N+1 Query** → Most common; fix with JOIN FETCH, batch loading, or caching
- **Full Table Scan Abuse** → Missing index; or query not using index (function on indexed column)
- **Over-Normalization** → Excessive joins for every read; practical denormalization needed at scale
- **Hot Partition** → All reads/writes to one shard; bad shard key; uneven load
- **Missing Index** → Common on foreign keys, frequently-filtered columns
##### Interview Deep-Dive Keywords
- "Read Committed prevents dirty reads but allows non-repeatable reads; Repeatable Read prevents both"
- "MVCC enables high concurrency: readers don't block writers; each transaction sees a consistent snapshot"
- "LSM tree optimizes writes: sequential log append; B-tree optimizes reads: O(log n) random access"
- "Consistent Hashing minimizes reshuffling when adding/removing shards"
- "CDC with Debezium + Kafka enables event-driven integration without polling"
- Index trade-off: every index speeds reads but slows writes and uses space; index only what's queried

---

## 65. Enterprise Architecture
##### Business Architecture
- **Business Capability Modeling** → Map what business does (capabilities), not how (processes); stable foundation for IT alignment
- **Value Stream Mapping** → Visualize end-to-end flow of value; identify waste and bottlenecks
- **Operating Model** → How organization delivers value; centralized/federated/decentralized IT
- **Business Service Catalog** → Inventory of all business services; input for application portfolio
- **Business Capability Maturity** → Assess current vs target maturity; drives investment priority
- **Customer Journey Mapping** → End-to-end customer experience; identify digital touchpoints
- **Business KPI Frameworks** → OKRs, Balanced Scorecard; link IT outcomes to business outcomes
- **Change Management** → Manage human side of transformation; Kotter's 8-step, ADKAR
- **Portfolio Management** → Manage investments across programs; balance run/grow/transform
##### Data Architecture
- **Enterprise Data Strategy** → Vision, principles, roadmap for data as an asset
- **Data Governance** → Policies, standards, accountability for data quality and usage
- **Data Ownership & Stewardship** → Business data owners (accountability) + stewards (day-to-day)
- **Master Data Management (MDM)** → Single trusted version of key entities (customer, product, location)
- **Reference Data Management** → Manage shared lookup data (country codes, currencies, categories)
- **Metadata Architecture** → Data about data; technical + business metadata; data catalog
- **Data Lineage** → Track data from source to consumption; compliance + debugging
- **Data Quality Management** → Accuracy, completeness, consistency, timeliness; quality rules
- **Data Privacy & Compliance** → GDPR, CCPA; classify data; enforce access controls + retention
- **Data Warehousing** → Central analytical store; Kimball (star schema) vs Inmon (3NF) approaches
- **Data Lake** → Raw data in native format; schema-on-read; Hadoop, S3, Azure Data Lake
- **Lakehouse** → Combine data lake + DW; ACID on object storage; Delta Lake, Apache Iceberg
- **Real-time Data Pipelines** → Kafka + Flink/Spark Streaming; sub-second data availability
- **Data Interoperability** → Common formats and protocols; APIs for data sharing; canonical data model
- **Data Migration Architecture** → Lift-and-shift vs transform; big-bang vs phased; rollback plan
##### Application Architecture
- **Application Portfolio Management** → Inventory all applications; assess fit/value/cost; rationalize
- **Application Rationalization** → Retire/consolidate/replace/rehost decisions; reduce portfolio complexity
- **Application Lifecycle Management** → Plan, build, deploy, operate, retire; governance checkpoints
- **API Architecture** → API-first; versioning strategy; internal vs partner vs public APIs
- **Integration Architecture** → Point-to-point vs hub-and-spoke vs ESB vs event-driven; evolution path
- **Modular Architecture** → Break monolith into bounded modules; strangler fig pattern; prerequisite for microservices
- **Application Security Architecture** → Zero trust; defense in depth; shift-left security; OWASP
- **Identity and Access Management (IAM)** → Authentication, authorization, federation, SSO; enterprise-wide
- **Application Modernization** → Move to cloud-native; re-platform, re-architect, re-factor strategies
- **Legacy System Transformation** → Strangle, encapsulate, replace; minimize business risk
- **Software Architecture Governance** → Architecture review boards; fitness functions; guardrails
##### Technology Architecture
- **Infrastructure Architecture** → Compute, storage, network; physical, virtual, cloud layers
- **Cloud Architecture** → IaaS/PaaS/SaaS selection; shared responsibility model; well-architected frameworks
- **Hybrid Cloud** → On-premise + cloud; consistent governance; data residency; latency concerns
- **Multi-cloud** → Avoid lock-in; best-of-breed services; operational complexity trade-off
- **Network Architecture** → Zero trust network; microsegmentation; software-defined networking (SDN)
- **Container Orchestration** → Kubernetes; cluster management; service mesh overlay
- **Platform Engineering** → Internal Developer Platform (IDP); golden paths; self-service; reduce cognitive load
- **Security Architecture** → Identity (IAM), network (firewalls, WAF), data (encryption), application (SAST/DAST)
- **Zero Trust Architecture** → Never trust, always verify; identity as perimeter; least privilege everywhere
- **Disaster Recovery** → RTO (recovery time objective), RPO (recovery point objective); hot/warm/cold standby
- **High Availability Design** → Redundancy at every layer; active-active vs active-passive; multi-AZ
- **Observability Architecture** → Unified logs, metrics, traces; OpenTelemetry standard; centralized platform
- **Infrastructure as Code** → Terraform, Pulumi; version-controlled infra; reproducible environments
- **Capacity Planning** → Model growth; headroom; performance testing at scale
- **Technology Lifecycle Management** → Adopt/trial/assess/hold rings (ThoughtWorks Radar); tech debt governance
- **Cost Optimization** → FinOps; right-sizing; reserved capacity; storage tiering; showback/chargeback
##### Architecture Frameworks & Standards
- **TOGAF** → The Open Group Architecture Framework; ADM (Architecture Development Method); widely adopted
- **Zachman Framework** → 6x6 matrix of stakeholder views × abstraction levels; comprehensive but complex
- **C4 Model** → Context, Container, Component, Code diagrams; lightweight; developer-friendly
- **4+1 Views** → Logical, Development, Process, Physical + Scenarios; Kruchten's model
- **Architecture Decision Records (ADRs)** → Document context, decision, consequences; lightweight governance
- **Fitness Functions** → Automated checks for architectural characteristics; evolved architecture
##### Governance & Strategy
- **Architecture Review Board (ARB)** → Approve significant architectural decisions; risk management
- **Tech Radar** → Visualize technology adoption stages; organizational technology strategy
- **Architecture Runway** → Technical enablers ahead of feature work; avoid architectural debt
- **Evolutionary Architecture** → Incremental, guided change; fitness functions; avoid big-bang redesigns
- **Technical Debt Management** → Identify, quantify, prioritize; technical debt register; pay down deliberately
- **Build vs Buy vs Subscribe** → Strategic decision per capability; avoid commodity differentiation
##### Interview Deep-Dive Keywords
- "Bounded Context from DDD maps naturally to microservice + data ownership boundary"
- "Platform Engineering reduces developer cognitive load via golden paths and self-service IDP"
- "Architecture fitness functions provide continuous automated validation of architectural qualities"
- "Data mesh addresses centralized data lake bottleneck via domain-oriented data ownership"
- "ADRs create institutional memory; document why decisions were made, not just what"
- TOGAF ADM: iterative phases (Preliminary → A Vision → B Business → C Information Systems → D Technology → E–H Implementation); know the phases conceptually
- EA roles: Enterprise Architect (strategy), Solution Architect (project), Domain Architect (area)

---

## 66. Event-Driven Architecture (EDA)
##### Core Architectural Paradigms
- **Event-Driven Architecture (EDA)** → System behavior driven by events; producers emit, consumers react; loosely coupled
- **Message-Driven Architecture (MDA)** → Communication via messages; broker mediates; guaranteed delivery focus
- **Reactive Architecture** → Responsive, resilient, elastic, message-driven; Reactive Manifesto principles
- **Streaming Architecture** → Continuous, unbounded data processing; events processed as they arrive
- **Asynchronous Architecture** → Non-blocking; producers don't wait for consumers; higher throughput
- **CQRS** → Command (write) and Query (read) separated; often paired with Event Sourcing in EDA
- **Flow-Based Programming** → Components connected by data flows; process network of streams
##### Event Fundamentals
- **Event** → Immutable fact that something happened; past tense; e.g. `OrderPlaced`, `PaymentFailed`
- **Event Producer** → Emits events when state changes; doesn't know who consumes
- **Event Consumer** → Reacts to events; subscribes to topics; processes independently
- **Event Broker** → Intermediary storing and routing events; Kafka, RabbitMQ, EventBridge
- **Event Bus** → In-process or distributed channel for events; decouples components
- **Event Channel** → Typed conduit for specific event category; topic/queue
- **Loose Coupling** → Producer has no direct dependency on consumer; change one without affecting other
##### EDA Patterns
- **Event Notification** → Minimal event; "something happened"; consumers fetch details via API if needed
- **Event-Carried State Transfer** → Event contains all data; consumers don't need callback; higher payload
- **Event Collaboration** → Multiple services react to events, each contributing to overall workflow
- **Pub/Sub (Publish-Subscribe)** → Publisher emits to topic; all subscribers receive copy; fan-out
- **Topic-based Routing** → Route by topic name; consumers choose topics to subscribe
- **Content-based Routing** → Route by event content/attributes; more flexible; higher broker complexity
- **Event Filtering** → Consumer receives only events matching predicate; reduces processing load
- **Event Transformation** → Convert event format; enrich with additional data; adapt to consumer model
- **Event Enrichment** → Add context data to event before forwarding; lookup from external source
- **Event Correlation** → Link related events across time; correlation ID; saga tracking
- **Event Choreography** → Services react to events without central coordinator; decoupled; emergent behavior
- **Event Orchestration** → Central orchestrator commands services; explicit flow; easier to trace
##### Push vs Pull Models
- **Push Model** → Broker pushes events to consumer; low latency; consumer must keep up; backpressure challenge
- **Pull Model** → Consumer polls broker; natural backpressure; Kafka uses pull; consumer controls pace
- **Webhooks** → HTTP push; broker calls consumer's endpoint; simple integration; retry on failure
- **Long Polling** → Consumer waits for response until event available; hybrid push/pull
- **Fan-out** → One event delivered to multiple consumers; topic vs queue semantics
- **Reactive Push** → Push with backpressure signals; Reactive Streams; consumer requests(n) items
- **Push-Pull Hybrid** → Push notification + pull for data; webhooks + REST; common in low-volume systems
##### Outbox & Inbox Patterns
- **Outbox Pattern** → Write event to DB outbox table in same transaction as state change; relay to broker; solves dual-write problem
- **Inbox Pattern** → Consumer writes received event to inbox table before processing; ensures exactly-once
- **Dual-Write Problem** → Updating DB and publishing event in two steps; one can fail; Outbox solves this
- **Transactional Outbox** → Atomic: DB write + outbox row; background relay polls outbox + publishes
- **CDC-based Outbox** → Debezium reads outbox table via WAL; no polling; lower latency
##### Competing Consumers & Scaling
- **Competing Consumers** → Multiple consumer instances share work from same queue; horizontal scaling
- **Consumer Group** → Named group of consumers sharing partition assignment (Kafka); one partition → one consumer
- **Partition-based Parallelism** → Scale consumers up to partition count; design partitions for expected scale
- **Backpressure** → Consumer signals it's overwhelmed; producer slows down; Reactive Streams protocol
- **Consumer Lag** → Behind-ness of consumer vs latest offset; primary health metric; alert on growth
##### Delivery Semantics (Deep Dive)
- **At-most-once** → No retry; message lost on failure; acceptable for metrics, analytics events
- **At-least-once** → Retry on failure; consumer may see duplicates; consumer must be idempotent
- **Exactly-once** → No loss, no duplicates; hardest; Kafka: idempotent producer + transactional consumer + `read_committed`
- **Idempotent Consumer** → Processing same message twice has same effect as once; use event ID + dedup store
- **Message Deduplication** → Track processed event IDs (DB, Redis); reject already-seen IDs
- **Idempotency Key** → Unique ID per event; check before processing; store after processing
##### Message-Driven Architecture
- **Message Queue** → Point-to-point; one consumer per message; RabbitMQ queues, SQS
- **Message Broker** → Routes messages; decouples producers/consumers; handles retries, DLQ
- **Message Envelope** → Metadata wrapper: correlation ID, timestamp, type, version, source
- **Dead Letter Queue (DLQ)** → Unprocessable messages after max retries; alert on DLQ depth; manual inspection
- **Message Retry** → Automatic re-delivery on failure; exponential backoff; max retry count
- **Guaranteed Delivery** → Persistent messages; ack-based; broker stores until acknowledged
- **Message Ordering** → FIFO within partition/queue; across partitions: not guaranteed; key-based Kafka
- **Priority Queue** → Higher-priority messages processed first; RabbitMQ priority queues
##### Saga Pattern (Deep Dive)
- **Saga** → Sequence of local transactions; each service commits locally; publish event for next step
- **Orchestration Saga** → Saga Orchestrator sends commands; receives replies; central state machine
- **Choreography Saga** → Each service listens for events; reacts; no central coordinator; emergent flow
- **Compensation Transactions** → Undo completed steps on failure; must be idempotent; no true rollback
- **Saga State** → Track progress; which steps completed, which compensated; persist in DB
- **Orchestration vs Choreography** → Orchestration: easier trace, central SPOF; Choreography: decoupled, harder to trace
##### Event Streaming
- **Event Streaming** → Continuous flow of events; store + process in real-time and historically
- **Stream Processing** → Transform, aggregate, join streams in motion; stateless or stateful
- **Unbounded Data** → Data that has no end; streaming contrast to bounded batch data
- **Stateful Stream Processing** → Maintain state across events; aggregations, windowed joins; backed by RocksDB
- **Stateless Processing** → Each event processed independently; filter, map, route; trivially scalable
- **Event Time vs Processing Time** → Event time: when event occurred (in source); Processing time: when processed in system
- **Watermarks** → Estimate of event time completeness; trigger window evaluation; trade latency vs correctness
- **Windowing** → Group events into finite sets for aggregation:
  - **Tumbling Window** → Fixed, non-overlapping; e.g. sales per minute
  - **Sliding Window** → Fixed size, overlapping; e.g. 5-min window every 1 min
  - **Session Window** → Gap-based; group activity by inactivity timeout; e.g. user sessions
- **Stream Joins** → Join two streams on key + time window; stream-table join (enrich), stream-stream join (correlate)
- **Stream Aggregation** → Count, sum, avg over window; output to topic or DB
- **Late Data Handling** → Events arriving after window closed; allowed lateness; side outputs
##### Event Sourcing (Deep Dive)
- **Event Sourcing** → Never update state directly; store sequence of events; derive state by replay
- **Event Store** → Append-only, ordered log of domain events per aggregate; EventStoreDB, Kafka topic, DB table
- **Immutable Events** → Once written, never changed; basis for audit, replay, time-travel
- **Event Replay** → Rebuild aggregate state from events; enables point-in-time queries; rebuild projections
- **Snapshotting** → Periodic state snapshot; skip full replay; snapshot + events since snapshot
- **Event Versioning** → Events must evolve; upcasting: transform old events to new schema on read
- **Event Schema Evolution** → Add optional fields (backward compat); never remove/rename required fields
- **Temporal Modeling** → Model time explicitly; query state at any past point; regulatory compliance
- **Aggregate Rehydration** → Load aggregate by replaying its event stream from store
- **Write Model / Read Model** → Event Sourcing + CQRS: write model = event store; read model = projections
- **Projections** → Derived read-optimized views built from event stream; rebuild anytime
##### CQRS (Deep Dive)
- **Command** → Intent to change state; validate + apply; emits event on success; e.g. `PlaceOrderCommand`
- **Query** → Read-only; no side effects; reads from optimized read model
- **Command Model** → Validates business rules; enforces invariants; writes to event store
- **Query Model** → Denormalized; optimized for specific read patterns; updated asynchronously via projections
- **Separation Benefits** → Scale read/write independently; optimize each model separately; different DBs
- **Eventual Consistency** → Read model may lag write model; acceptable for most use cases
- **When NOT to use CQRS** → Simple CRUD apps; small teams; adds significant complexity without benefit
##### Observability in EDA
- **Distributed Tracing** → Trace event flow across services; `traceId` in event headers; OpenTelemetry
- **Correlation ID** → Unique ID per business transaction; propagate in all events; tie logs together
- **Consumer Lag Monitoring** → Alert when consumer falls behind; indicates processing bottleneck
- **Event Flow Visualization** → End-to-end event journey; Jaeger, Zipkin, Honeycomb
- **Throughput / Latency Metrics** → Events/second, end-to-end latency; Prometheus + Grafana dashboards
- **Backpressure Monitoring** → Queue depth, consumer lag; trigger auto-scaling or alerting
##### Security & Governance
- **Schema Registry** → Enforce event schema; prevent breaking changes; Confluent Schema Registry, AWS Glue
- **Schema Validation** → Validate events against registered schema before publish/consume
- **Data Contracts** → Agreed schema + semantics between producer and consumer; versioned
- **Encryption in Transit** → TLS for all broker connections; mTLS for service-to-service
- **Encryption at Rest** → Broker-level or application-level encryption; key management (KMS)
- **Authentication / Authorization** → SASL/OAuth2 for broker auth; ACLs for topic-level access control
- **Multi-Tenancy** → Topic-level isolation; separate clusters; namespace-based access control
- **Data Governance** → Data lineage via event metadata; retention policies; data classification
##### Advanced & Emerging
- **Data Mesh** → Domain-owned data products published as event streams; federated governance
- **Streaming ETL** → Replace batch ETL with real-time stream transformations; CDC + Kafka + Flink
- **Event Mesh** → Network of event brokers spanning environments; Solace; cross-cloud event routing
- **Digital Twin** → Real-time virtual replica of physical entity; event-driven state sync
- **Edge Streaming** → Process events at edge (IoT); reduce latency + bandwidth; Apache Edgent
- **AI/ML Streaming Pipelines** → Feature engineering in real-time; model inference on streams; Flink ML
- **Stateful Functions** → Serverless stateful stream processing; Apache Flink Stateful Functions
- **Serverless Streaming** → AWS EventBridge, Lambda; no infra management; event-driven functions
##### Frameworks & Tools
- **Reactive Streams** → Standard for async stream processing with backpressure; `Publisher/Subscriber/Processor`
- **Project Reactor** → Spring's reactive library; `Mono` (0-1) + `Flux` (0-N); non-blocking pipelines
- **RxJava** → ReactiveX for Java; Observable/Single/Flowable; rich operator library
- **Spring WebFlux** → Reactive web framework; Netty; handles high concurrency with few threads
- **Kafka Streams** → Library for stream processing on Kafka; KStream/KTable; stateful + windowing
- **Apache Flink** → Stateful stream processing; event time; exactly-once; complex event processing
- **Apache Spark Streaming** → Micro-batch streaming; DStream/Structured Streaming; integrates with ML
- **Apache Beam** → Unified batch + streaming model; run on Flink/Spark/Dataflow; portable pipelines
- **Akka Streams** → Actor-based reactive streams; backpressure-aware; JVM
##### Integration & API
- **REST vs Events** → REST: synchronous, request-response, tightly coupled; Events: async, decoupled, eventual
- **gRPC Streaming** → Server/client/bidirectional streaming; protobuf; lower latency than REST
- **GraphQL Subscriptions** → Real-time updates over WebSocket; client subscribes to data changes
- **Enterprise Service Bus (ESB)** → Centralized integration; heavy; SOA era; replaced by event mesh/Kafka
- **API Gateway + Events** → Gateway receives HTTP; converts to event; async backend; decouples frontend
- **Change Data Capture (CDC)** → Capture DB changes as events; Debezium; source of truth for events
##### Common Anti-Patterns
- **Event Spaghetti** → Too many event types; unclear flow; hard to trace; no schema governance
- **Fat Events** → Huge event payload; tight coupling via embedded data; break into notification + fetch
- **Chatty Events** → Too many fine-grained events for single business operation; aggregate into domain event
- **Tight Schema Coupling** → Consumer depends on every field of producer event; breaks on any change
- **No Idempotency** → Consumer processes duplicate events → wrong state; always design for at-least-once
- **Ignoring Consumer Lag** → Growing lag = data freshness SLA breach; must monitor + alert
- **Saga Without Compensation** → Business flow can fail partially with no rollback; always design compensating transactions
##### Interview Deep-Dive Keywords
- "Event-driven decouples services temporally and logically — producer doesn't know or care who consumes"
- "Outbox pattern solves dual-write: atomic DB write + event publish in single transaction"
- "Exactly-once requires coordination: idempotent producer + transactional messaging + deduplication at consumer"
- "Choreography scales better but is harder to trace; Orchestration is easier to reason about but creates central coupling"
- "Event Sourcing gives you free audit log, time-travel queries, and event replay — at the cost of operational complexity"
- "Watermarks trade latency vs completeness: tight watermark = fast results but may miss late data; loose = more complete but slower"
- Projections in Event Sourcing: can be rebuilt anytime; multiple projections from same event stream; enables schema-free evolution

---

## 67. Stream Processing
##### Core Concepts
- **Stream Processing** → Continuous computation on unbounded event sequences; process as data arrives
- **Unbounded Data** → No definite end; contrast with batch (bounded, finite dataset)
- **Bounded Data** → Finite dataset; batch processing; MapReduce, Spark batch
- **Real-Time Data Pipelines** → Source → transform → sink; sub-second latency; Kafka + Flink/Spark
- **Continuous Processing** → No sleep between batches; always running; event-by-event or micro-batch
- **Micro-batch** → Small time-window batches; Spark Streaming; simpler but higher latency than true streaming
- **True Streaming** → Record-by-record; Apache Flink; lowest latency; most complex
##### Time Semantics
- **Event Time** → Timestamp when event occurred at source; accurate for analysis; may arrive out of order
- **Processing Time** → Timestamp when event processed by system; simple but inaccurate for late data
- **Ingestion Time** → When event entered streaming system; between event and processing time
- **Out-of-order Events** → Events arrive in different order than they occurred; common in distributed sources
- **Watermarks** → Heuristic: "all events up to time T have arrived"; triggers window evaluation
- **Allowed Lateness** → Accept late events after watermark; update window result; side output for very late
- **Late Data** → Events after watermark; configurable handling: drop, update result, side output
##### Windowing (Deep Dive)
- **Tumbling Window** → Fixed size, non-overlapping; every event in exactly one window; e.g. hourly sales count
- **Sliding Window** → Fixed size, step < size; events in multiple windows; e.g. 1-hour window every 15 min
- **Session Window** → Dynamic size; bounded by inactivity gap; e.g. user sessions with 30-min timeout
- **Global Window** → All events in one window; custom trigger needed; not time-based
- **Window Trigger** → When to evaluate window: event time watermark, count, processing time, custom
- **Window Function** → Applied to window contents: `reduce`, `aggregate`, `process`
- **Early Firing** → Emit partial results before window closes; speculative results
- **Late Firing** → Update result when late data arrives; retraction semantics
##### Stateful Processing
- **State** → Aggregations, join buffers, custom accumulators stored per key
- **Keyed State** → State scoped to a key; Flink: `ValueState`, `ListState`, `MapState`, `ReducingState`
- **Operator State** → State scoped to operator instance (not key); Flink: checkpointing required
- **RocksDB State Backend** → Flink default for large state; persists to disk; spill to disk for big aggregations
- **State TTL** → Auto-expire old state; prevent unbounded state growth
- **Changelog** → State changes published to Kafka topic; enables state rebuilding + Kafka Streams KTable
##### Stream Joins
- **Stream-Stream Join** → Join two event streams on key + time window; find matching events within window
- **Stream-Table Join** → Enrich stream events with lookup data from table; e.g. enrich order with user info
- **Table-Table Join** → Join two changelogs; materialized view update; Kafka Streams
- **Interval Join** → Match events within a time interval of each other; Flink
- **Temporal Join** → Join stream with slowly-changing table; point-in-time correctness
##### Apache Flink
- **Flink** → True streaming; event time; exactly-once; scalable stateful processing
- **DataStream API** → Low-level; full control; transformations on `DataStream<T>`
- **Table API / SQL** → High-level; declarative; unified batch + streaming; Flink SQL
- **Flink Checkpointing** → Periodic consistent snapshot of state; Chandy-Lamport algorithm; O(state) time
- **Exactly-once (Flink)** → Checkpointing + Kafka transactional source/sink; 2-phase commit for sinks
- **Flink Savepoint** → Manual checkpoint; for planned maintenance, upgrades, migration
- **Task Slots** → Unit of parallelism; one slot per parallel task instance; share JVM
- **Flink Watermarks** → Generated by source or custom; `WatermarkStrategy.forBoundedOutOfOrderness(Duration)`
- **Side Outputs** → Route late or special events to separate output stream
- **CEP (Complex Event Processing)** → Detect event patterns over time; `Pattern.begin().next().within()`
##### Apache Spark Streaming
- **Structured Streaming** → DataFrame-based; micro-batch + continuous mode; exactly-once
- **DStream (Legacy)** → RDD-based; deprecated in favor of Structured Streaming
- **Trigger** → When to process: `Trigger.ProcessingTime`, `Once`, `Continuous`
- **Watermark in Spark** → `withWatermark("timestamp", "10 minutes")`; drops late data after threshold
- **Output Modes** → `Complete` (full result), `Append` (new rows only), `Update` (changed rows)
- **Checkpoint** → Recover streaming query on restart; tracks offsets + state
##### Kafka Streams
- **Kafka Streams** → Client library; no separate cluster; runs inside app; tight Kafka integration
- **KStream** → Record stream; each record independent; `filter`, `map`, `flatMap`, `join`
- **KTable** → Changelog stream; latest value per key; like materialized view; backed by compacted topic
- **GlobalKTable** → Replicated on every instance; available for non-key joins; small lookup tables
- **Topology** → DAG of processors; defined programmatically; compiled to tasks
- **State Stores** → Local RocksDB; backed by changelog topic; queryable via Interactive Queries
- **Interactive Queries** → Query local state stores directly; expose via REST API for external access
- **Repartitioning** → Shuffle data by new key; auto-triggered by key-changing operations
- **Commit Interval** → How often offsets committed; `commit.interval.ms`; affects at-least-once behavior
##### Apache Beam
- **Beam Model** → Unified programming model for batch + streaming; What/Where/When/How framework
- **Pipeline** → Directed acyclic graph of transformations; Beam program
- **PCollection** → Parallel collection; both bounded and unbounded; main data abstraction
- **PTransform** → Transformation: `ParDo`, `GroupByKey`, `Combine`, `Flatten`, `Partition`
- **Runner** → Executes Beam pipeline: Flink Runner, Spark Runner, Dataflow Runner, Direct Runner
- **Portability** → Write once, run on any runner; avoids vendor lock-in
- **Windowing in Beam** → Rich windowing: Fixed, Sliding, Session, Global; per-element timestamps
##### Reactive Streams & Backpressure
- **Reactive Streams** → JVM standard: `Publisher`, `Subscriber`, `Subscription`, `Processor`
- **Project Reactor** → `Flux<T>` (N items) + `Mono<T>` (0-1 items); operators: `map`, `flatMap`, `filter`, `zip`
- **Backpressure in Reactor** → `request(n)` signals demand; `onBackpressureBuffer/Drop/Latest`
- **RxJava** → `Observable` (no backpressure), `Flowable` (backpressure); rich operator set
- **Hot vs Cold Publisher** → Cold: starts on subscribe, replays; Hot: ongoing, subscribers join mid-stream
- **Schedulers** → `Schedulers.boundedElastic()` for I/O; `Schedulers.parallel()` for CPU; `publishOn`/`subscribeOn`
- **Error Handling** → `onErrorReturn`, `onErrorResume`, `retry`, `retryWhen` in Reactor
##### Performance Patterns
- **Parallelism** → Scale by partitioning work; more partitions = more parallelism; match to CPU cores
- **Batching** → Group small events into batches for efficiency; reduces per-event overhead
- **Compression** → Snappy/LZ4 for streaming; reduces network + disk; CPU trade-off
- **State Size Management** → Large state = GC pressure + slow checkpoints; use TTL; compact aggressively
- **Operator Chaining** → Flink chains compatible operators into single task; reduces serialization overhead
- **Async I/O** → Flink AsyncFunction; don't block event loop for DB lookups; maintain throughput
##### Common Anti-Patterns
- **Blocking in Reactive Pipeline** → Blocks event loop thread; wrap in `Schedulers.boundedElastic()`
- **Ignoring Watermarks** → Missing late data handling; incorrect window results; always configure watermark strategy
- **Unbounded State** → State grows forever; OOM; always set TTL or cleanup logic
- **Wrong Time Semantics** → Using processing time for analytics → incorrect results on replay; use event time
- **Over-partitioning** → Too many partitions → coordination overhead; checkpoint size; tune carefully
- **No Idempotent Sinks** → Exactly-once processing requires idempotent or transactional sinks
##### Interview Deep-Dive Keywords
- "Event time processing is correct; processing time is simpler but breaks on replay or delay"
- "Watermarks are a heuristic: too tight = drop data; too loose = high latency; tune per data source"
- "Flink achieves exactly-once via distributed snapshots (Chandy-Lamport) + transactional sinks"
- "Kafka Streams runs inside your app — no separate cluster; state in local RocksDB backed by Kafka topic"
- "Backpressure propagates upstream: slow consumer signals slow producer — prevents OOM and data loss"
- Session window: real-world use case = user activity analytics, fraud detection, clickstream analysis
- Flink vs Spark Streaming: Flink = true streaming, lower latency; Spark = micro-batch, better SQL ecosystem

---

## 68. Reactive Programming
##### Core Concepts
- **Reactive Programming** → Programming with asynchronous data streams; respond to events as they occur
- **Reactive Manifesto** → Four traits: Responsive (fast), Resilient (fault-tolerant), Elastic (scalable), Message-Driven
- **Responsive** → System responds in timely manner; latency guarantee; detect and handle failure
- **Resilient** → Stays responsive under failure; isolation, replication, delegation
- **Elastic** → Responsive under varying load; scale up and down; no contention points
- **Message-Driven** → Async message passing; loose coupling; backpressure; location transparency
- **Asynchronous** → Operations don't block the caller; caller continues; result delivered later
- **Non-blocking** → Thread doesn't sit idle waiting; event loop pattern; handles many concurrent connections
##### Reactive Streams Specification
- **Publisher** → Produces items; calls `onNext`, `onError`, `onComplete` on subscriber
- **Subscriber** → Consumes items; calls `subscription.request(n)` to signal demand
- **Subscription** → Link between publisher and subscriber; `request(n)` + `cancel()`
- **Processor** → Both publisher and subscriber; transformation step in pipeline
- **Backpressure Protocol** → Consumer requests(n); producer sends at most n; prevents overflow
- **Demand-driven** → Producer only produces what consumer can handle; pull-based under the hood
##### Project Reactor
- **Mono** → 0 or 1 item; `Mono<User>`, `Mono<Void>`; completes with value, empty, or error
- **Flux** → 0 to N items; `Flux<String>`; stream of items ending with complete or error
- **Cold Publisher** → Lazy; starts from beginning on each subscribe; `Flux.fromIterable()`
- **Hot Publisher** → Shared; ongoing; new subscribers join mid-stream; `Sinks`, `ConnectableFlux`
- **Operators** → `map`, `flatMap`, `filter`, `zip`, `merge`, `concat`, `switchMap`, `take`, `skip`
- **`flatMap`** → Async transform; returns inner publisher; concurrent by default; order not guaranteed
- **`concatMap`** → Sequential `flatMap`; preserves order; waits for inner to complete
- **`switchMap`** → Cancels previous inner on new item; good for typeahead / latest-wins
- **`zip`** → Combine items from multiple publishers pairwise; waits for all sources
- **`merge`** → Interleave items from multiple publishers concurrently; fastest wins
- **Error Handling** → `onErrorReturn(default)`, `onErrorResume(fallback)`, `onErrorMap(transform)`
- **Retry** → `retry(n)`, `retryWhen(companion)` for exponential backoff
- **Timeout** → `timeout(Duration)` → `TimeoutException` if no item within duration
- **Schedulers** → Control which thread executes work:
  - `Schedulers.boundedElastic()` → I/O bound; elastic thread pool; for DB calls, HTTP
  - `Schedulers.parallel()` → CPU bound; fixed thread pool = CPU cores
  - `Schedulers.single()` → Single reusable thread; for serialized work
- **`publishOn`** → Downstream runs on specified scheduler; affects operators after it
- **`subscribeOn`** → Where subscription/source runs; affects source and operators before `publishOn`
- **Context** → Reactor's equivalent of ThreadLocal; `contextWrite` + `Mono.deferContextual`
- **Sinks** → Programmatic event emission; `Sinks.many().multicast()`, `unicast()`, `replay()`
##### RxJava
- **Observable** → Push-based; no backpressure; 0-N items; use for UI events, small streams
- **Flowable** → Push + backpressure; use for large/fast data sources
- **Single** → Exactly 1 item or error; `Single<User>` for HTTP response
- **Maybe** → 0 or 1 item; `Maybe<User>` for nullable result
- **Completable** → No value; just completion or error; `Completable` for fire-and-forget
- **Subject** → Both Observable and Observer; bridge imperative → reactive; `PublishSubject`, `BehaviorSubject`
- **BehaviorSubject** → Replays last value to new subscribers; good for state management
- **CompositeDisposable** → Manage subscription lifecycle; `dispose()` to prevent memory leaks
##### Spring WebFlux
- **WebFlux** → Non-blocking web framework; Netty event loop; contrast with MVC (Servlet, blocking)
- **Router Functions** → Functional endpoint style; `RouterFunction<ServerResponse>`; no annotations
- **Annotated Controllers** → `@GetMapping` with `Mono<ResponseEntity<T>>` return type
- **WebClient** → Non-blocking HTTP client; replaces RestTemplate in reactive apps; `retrieve()` or `exchange()`
- **`ExchangeFilterFunction`** → Middleware for WebClient; logging, auth, retry
- **Reactive Security** → `ReactiveSecurityContextHolder`; `@PreAuthorize` with reactive return types
- **R2DBC** → Reactive relational DB driver; non-blocking SQL; `DatabaseClient` / `R2dbcRepository`
- **Reactive Redis** → `ReactiveRedisTemplate`; non-blocking Redis operations
- **When to use WebFlux** → High concurrency, I/O bound (many slow network calls); NOT for CPU-bound tasks
- **When to use MVC** → Team unfamiliar with reactive; CPU-bound; simpler debugging; most CRUD apps
##### Akka Streams
- **Akka Streams** → Backpressure-aware stream processing; Actor system underneath
- **Source** → Stream producer; `Source.from(List)`, `Source.tick()`
- **Sink** → Stream consumer; `Sink.foreach()`, `Sink.ignore()`
- **Flow** → Transformation step; `Flow.map()`, `Flow.filter()`
- **Graph DSL** → Complex topologies: fan-out, fan-in, cycles; `GraphDSL.create()`
- **Materialization** → Running a stream; returns materialized value (Future, count, etc.)
- **Back-pressure** → Built-in; slow sink signals slow source; no overflow
##### Common Pitfalls
- **Blocking in Reactive** → `Thread.sleep()`, JDBC, `future.get()` blocks event loop; wrap in `boundedElastic()`
- **Forgotten Subscription** → Reactor is lazy; nothing runs until `subscribe()` or return from controller
- **Memory Leaks** → Hot publisher + forgotten subscriber; always dispose; use `take()` to limit
- **Context Propagation** → Thread switches lose MDC/ThreadLocal; use Reactor Context; configure `Hooks.onEachOperator`
- **Mutable State in Pipeline** → Race conditions; streams can run on multiple threads; use atomic / immutable
- **Not Handling Errors** → Unhandled error terminates stream silently; always add `onErrorResume`
##### Interview Deep-Dive Keywords
- "Reactive programming is about async data streams + non-blocking I/O — not just about being fast"
- "`flatMap` is concurrent — use `concatMap` when order matters or inner publishers must not overlap"
- "`subscribeOn` affects the source; `publishOn` affects downstream operators — know the difference"
- "WebFlux doesn't make slow code fast — it makes I/O-bound code use fewer threads"
- "Backpressure in Reactor: `request(n)` propagates demand upstream through the operator chain"
- Cold vs Hot: most HTTP calls are cold (start fresh); use hot publishers for shared event buses or WebSocket streams
- R2DBC vs JDBC in reactive: JDBC blocks a thread per call; R2DBC uses reactive driver → truly non-blocking

---

## 69. Messaging Systems (RabbitMQ & Beyond)
##### Core Messaging Concepts
- **Message Queue** → Buffer messages between producer and consumer; decouples timing
- **Message Broker** → Intermediary: receives, stores, routes messages; RabbitMQ, ActiveMQ, SQS
- **AMQP (Advanced Message Queuing Protocol)** → Open standard for message brokers; RabbitMQ's native protocol
- **Message** → Payload + metadata (headers, routing key, content-type, correlation ID, reply-to)
- **Producer** → Publishes messages to exchange or queue
- **Consumer** → Subscribes to queue; processes messages; sends acknowledgment
- **Acknowledgment (ACK)** → Consumer confirms processing; broker removes message; `basicAck()`
- **Negative Acknowledgment (NACK)** → Consumer rejects; broker requeues or sends to DLQ; `basicNack(requeue=false)`
##### RabbitMQ Architecture
- **Exchange** → Receives messages from producers; routes to queues via bindings
- **Exchange Types** →
  - **Direct** → Route by exact routing key match; e.g. `order.placed`
  - **Topic** → Route by pattern matching; `order.*` matches `order.placed`, `order.cancelled`
  - **Fanout** → Broadcast to all bound queues; ignores routing key
  - **Headers** → Route by message header values; not routing key
- **Queue** → Buffer; stores messages; durable (survives restart) or transient
- **Binding** → Link between exchange and queue with routing key or pattern
- **Virtual Host (vhost)** → Logical namespace; isolation within one broker; separate queues, exchanges
- **Connection / Channel** → Connection = TCP; Channel = lightweight virtual connection inside TCP; use channels not connections per operation
##### Queue Properties
- **Durable Queue** → Survives broker restart; messages must also be persistent (delivery-mode=2)
- **Auto-delete** → Queue deleted when last consumer disconnects
- **Exclusive** → Only one connection can use; deleted on disconnect
- **TTL (Time to Live)** → Message or queue TTL; expired messages → DLQ or dropped
- **Max Length** → Queue size limit; overflow: drop oldest or reject new (`x-overflow`)
- **Lazy Queue** → Messages stored on disk instead of RAM; for high-volume, memory-sensitive
##### Dead Letter Exchange (DLX)
- **DLX** → Where rejected/expired/max-length-exceeded messages go; `x-dead-letter-exchange`
- **DLQ** → Queue bound to DLX; inspect unprocessable messages; re-process or alert
- **Dead-Letter Routing Key** → Override original key when dead-lettered; `x-dead-letter-routing-key`
- **Message TTL + DLQ Pattern** → Delayed retry: set TTL on retry queue → dead-letter to main queue after delay
##### Reliability Patterns
- **Persistent Messages** → `delivery-mode=2`; survives broker restart; slower (disk write)
- **Publisher Confirms** → Broker ACKs to producer; ensures message reached broker; `confirmSelect()`
- **Consumer Acknowledgment** → Manual ACK after processing; `autoAck=false`; prevent message loss on crash
- **Prefetch Count** → `basicQos(n)`; limit unacked messages per consumer; prevents consumer overwhelm
- **Retry with Dead-Letter** → NACK → DLX → retry queue (with TTL delay) → back to original queue
- **Idempotent Consumer** → Handle duplicate delivery; store processed message IDs; exactly-once behavior
##### Competing Consumers & Load Balancing
- **Competing Consumers** → Multiple consumers on same queue; round-robin distribution; horizontal scaling
- **Fair Dispatch** → `prefetch=1`; consumer gets next only after ACKing current; even load distribution
- **Consumer Cancellation** → Consumer notified when queue deleted or admin action; handle gracefully
##### RabbitMQ vs Kafka
| Aspect | RabbitMQ | Kafka |
|---|---|---|
| Model | Traditional broker; push to consumer | Distributed log; consumer pulls |
| Message Retention | Deleted after ACK (default) | Retained for configurable period |
| Ordering | Per queue | Per partition |
| Throughput | Moderate (millions/day) | Very high (billions/day) |
| Replay | No (once consumed, gone) | Yes (any consumer, any time) |
| Use Case | Task queues, RPC, routing | Event streaming, audit log, analytics |
| Complexity | Simpler to operate | More complex; needs Kafka ecosystem |
##### AWS SQS
- **SQS** → Managed queue; fully serverless; at-least-once or FIFO (exactly-once)
- **Standard Queue** → High throughput; best-effort ordering; at-least-once
- **FIFO Queue** → Strict ordering; exactly-once; lower throughput; message group ID
- **Visibility Timeout** → Message hidden after receipt; if not deleted within timeout → reappears; avoid duplicate processing
- **Long Polling** → `WaitTimeSeconds=20`; reduces empty responses; cost-efficient
- **SQS + Lambda** → Event-source mapping; Lambda triggered per batch; auto-scaling consumers
- **SQS + SNS** → SNS fan-out to multiple SQS queues; pub-sub + queue
##### Other Messaging Systems
- **Apache ActiveMQ** → JMS-compliant; enterprise features; slower than Kafka; legacy choice
- **Azure Service Bus** → Managed; AMQP + proprietary; topics/subscriptions; sessions for ordering
- **Google Pub/Sub** → Managed; global; push or pull; at-least-once; no strict ordering
- **NATS** → Ultra-fast; lightweight; fire-and-forget; at-most-once; JetStream for persistence
- **Redis Pub/Sub** → In-memory; fire-and-forget; no persistence; use Streams for durable messaging
- **Redis Streams** → Persistent log; consumer groups; ACK model; lightweight Kafka alternative
##### Spring AMQP (RabbitMQ + Spring)
- **`@RabbitListener`** → Consume from queue; `@RabbitListener(queues = "order.queue")`
- **`RabbitTemplate`** → Send messages; `convertAndSend(exchange, routingKey, message)`
- **`MessageConverter`** → JSON/Avro conversion; `Jackson2JsonMessageConverter`
- **Error Handling** → `@RabbitListener` exception → auto NACK; configure `SimpleRabbitListenerContainerFactory`
- **`@DltHandler`** → Handle messages from Dead Letter Queue in Spring
- **Retry Template** → `RetryTemplate` with backoff; configured on container factory
##### Interview Deep-Dive Keywords
- "RabbitMQ is best for task distribution and routing; Kafka for event streaming and replay"
- "Publisher Confirms + Consumer ACKs together ensure no message loss in RabbitMQ"
- "Prefetch count prevents fast producers from overwhelming slow consumers; set to 1 for fair dispatch"
- "DLX pattern enables delayed retry: TTL queue → dead-letter back to main queue after delay"
- "SQS visibility timeout must be > max processing time; otherwise message reappears and is processed twice"
- Exchange types: Direct (exact routing), Topic (pattern routing), Fanout (broadcast) — know use case for each

---

## 70. Observability & Monitoring
##### Three Pillars of Observability
- **Logs** → Discrete timestamped records; structured (JSON) preferred; queryable; event-level detail
- **Metrics** → Aggregated numerical measurements; counters, gauges, histograms; time-series
- **Traces** → End-to-end request flow across services; spans + parent-child relationships
- **Observability vs Monitoring** → Monitoring: known unknowns (predefined dashboards/alerts); Observability: unknown unknowns (explore arbitrary questions about system state)
##### Logging
- **Structured Logging** → JSON log entries; machine-parseable; include `traceId`, `spanId`, `userId`, `requestId`
- **Log Levels** → `TRACE` → `DEBUG` → `INFO` → `WARN` → `ERROR` → `FATAL`; production: INFO+; disable DEBUG in prod
- **Log Aggregation** → Centralize logs from all services; ELK stack, Splunk, Datadog Logs, AWS CloudWatch
- **ELK Stack** → Elasticsearch (store+search) + Logstash (collect+parse) + Kibana (visualize)
- **MDC (Mapped Diagnostic Context)** → Thread-local context; `MDC.put("traceId", id)`; include in all log lines
- **Correlation ID** → Unique ID per request; propagate through headers; tie all logs for one request
- **Log Retention** → Set appropriate retention (30 days hot, 1 year cold); cost vs compliance
- **Sampling** → Log only % of requests at DEBUG; 100% for errors; reduce noise + cost
##### Metrics
- **Counter** → Monotonically increasing; total requests, errors; use `rate()` in Prometheus for per-second
- **Gauge** → Current value; heap usage, queue depth, active connections; can go up and down
- **Histogram** → Distribution of values; request latency buckets; calculate P50/P95/P99
- **Summary** → Pre-computed percentiles; client-side; less flexible than histogram
- **P99 Latency** → 99th percentile; 1 in 100 requests is at or below this; tail latency matters most for UX
- **RED Method** → Rate, Errors, Duration; core metrics for every service; customer-facing focus
- **USE Method** → Utilization, Saturation, Errors; for resource monitoring (CPU, disk, network)
- **4 Golden Signals** → Latency, Traffic, Errors, Saturation; from Google SRE book
- **Cardinality** → Number of unique label combinations; high cardinality (userId as label) breaks Prometheus
##### Prometheus & Grafana
- **Prometheus** → Pull-based metrics; scrapes `/metrics` endpoints; PromQL query language; local storage
- **PromQL** → `rate(http_requests_total[5m])`, `histogram_quantile(0.99, ...)`, `sum by (service)`
- **AlertManager** → Route Prometheus alerts to PagerDuty, Slack, email; silencing, grouping, inhibition
- **Grafana** → Visualization; dashboards; multiple data sources; alerting; `rate()` + `histogram_quantile()`
- **Recording Rules** → Pre-compute expensive queries; store as new metrics; faster dashboards
- **Exporters** → Expose metrics from systems not natively instrumented: JMX exporter (JVM), node exporter (OS)
- **Micrometer** → JVM metrics facade; integrates Spring Boot with Prometheus, Datadog, CloudWatch
##### Distributed Tracing
- **Trace** → Complete journey of a request through all services; unique `traceId`
- **Span** → Unit of work within a trace; has `spanId`, `parentSpanId`, start/end timestamps, attributes
- **Context Propagation** → Pass `traceId` + `spanId` in HTTP headers (`traceparent`), Kafka headers
- **OpenTelemetry (OTel)** → Vendor-neutral standard for logs, metrics, traces; SDK + Collector
- **OTel Collector** → Receive telemetry from apps; process; export to backends (Jaeger, Datadog, Grafana Tempo)
- **Jaeger** → Open-source distributed tracing; Trace timeline view; sampling support
- **Zipkin** → Distributed tracing; similar to Jaeger; smaller ecosystem
- **Grafana Tempo** → Distributed tracing backend; integrates with Grafana; cost-effective
- **W3C Trace Context** → Standard HTTP header: `traceparent: 00-{traceId}-{spanId}-{flags}`
- **Sampling** → Head-based (decision at start) vs tail-based (decision after full trace); balance overhead vs completeness
##### SLI / SLO / SLA
- **SLI (Service Level Indicator)** → Quantitative measure; e.g. % of requests < 200ms, error rate
- **SLO (Service Level Objective)** → Target for SLI; e.g. 99.9% of requests < 200ms over 30 days
- **SLA (Service Level Agreement)** → Contract with customer; penalties for breach; usually less strict than SLO
- **Error Budget** → 1 - SLO; e.g. 99.9% SLO = 0.1% error budget = 43 min/month downtime allowed
- **Error Budget Burn Rate** → How fast error budget is consumed; alert when burning too fast
- **Alert on SLO Breach** → Better than alerting on symptoms; directly tied to user experience
- **Burn Rate Alerting** → Fast burn (1hr window) + slow burn (6hr window) alerts; multi-window multi-burn
##### Alerting Best Practices
- **Alert on Symptoms** → Alert on user impact (SLO breach, error rate high) not causes (high CPU)
- **Alert Fatigue** → Too many alerts → on-call ignores them; ruthlessly prune low-value alerts
- **Severity Levels** → P1 (wake up), P2 (business hours), P3 (ticket); route appropriately
- **Runbooks** → Link from alert to runbook; document diagnosis + remediation steps
- **Dead Man's Switch** → Alert when monitoring pipeline itself stops reporting; catch silent failures
- **PagerDuty / OpsGenie** → On-call management; escalation policies; rotation scheduling
##### Application Performance Monitoring (APM)
- **APM** → Deep application-level metrics: DB query times, external calls, JVM metrics
- **Datadog APM** → Distributed tracing + profiling + logs correlation; auto-instrumentation
- **New Relic** → APM + infrastructure + browser monitoring; NRQL for queries
- **Dynatrace** → AI-powered; auto-discovery; root cause analysis
- **Elastic APM** → Part of ELK; integrates with existing Elasticsearch
- **Continuous Profiling** → Profiling in production without overhead; Datadog, Pyroscope, Grafana Phlare
##### Health Checks
- **Liveness Probe** → Is app alive? Restart if dead; Kubernetes `livenessProbe`; `/actuator/health/liveness`
- **Readiness Probe** → Can app serve traffic? Route traffic only when ready; `/actuator/health/readiness`
- **Startup Probe** → One-time check at startup; allow slow-starting apps before liveness kicks in
- **Deep Health Check** → Check dependencies (DB, cache, external APIs); not just "is process running"
- **Spring Actuator** → `/actuator/health` with DB, Redis, Kafka indicators built-in; custom `HealthIndicator`
##### Chaos Engineering
- **Chaos Engineering** → Deliberately inject failures to verify resilience; "break things on purpose"
- **Game Day** → Planned chaos exercise; team practices incident response
- **Chaos Monkey** → Netflix; randomly terminates instances in production
- **Failure Injection** → Latency, errors, resource exhaustion, network partition
- **Hypothesis-driven** → Define expected behavior before chaos; verify or discover gaps
##### Interview Deep-Dive Keywords
- "The four golden signals cover everything: latency (slow?), traffic (load?), errors (broken?), saturation (full?)"
- "SLO-driven alerting ties engineering effort to user experience — alert on error budget burn, not CPU"
- "OpenTelemetry is the future: one SDK, multiple backends; avoid vendor lock-in for observability"
- "High cardinality labels (userId, requestId) destroy Prometheus performance; use tracing for those"
- "Liveness vs Readiness: Liveness = restart if broken; Readiness = stop sending traffic if not ready"
- P99 vs average: average hides tail latency; P99 shows what your worst 1% of users experience
- Error budget: makes reliability a product conversation — burn rate decides whether to ship or stabilize

---

*End of Complete Interview Notes — Java + DSA + OOD + Static Analysis + Principles + Patterns + System Design + DDD + Microservices + Spring + Kafka + Databases + Enterprise Architecture + EDA + Stream Processing + Reactive Programming + Messaging + Observability + Engineering Principles Master Reference + Database Master Reference + Assorted Patterns Master Reference*

---

## 72. Database Master Reference (NEW)

> **Coverage:** Every database topic from core concepts to Staff+ advanced — Core Concepts, Data Models, DB Types, SQL, Indexing, Query Optimization, Transactions, Concurrency, Consistency, Storage Engines, Sharding, Distributed DBs, Warehousing, Streaming, Security, Backup, Cloud, NoSQL, Graph, Time-Series, Anti-Patterns, and Staff+ themes. Each includes subtopics, keywords, and interview-ready notes.

---

### Core Database Concepts

- **Database** → Organized collection of structured data stored and accessed electronically. Managed by a DBMS.
- **DBMS (Database Management System)** → Software that manages databases: storage, retrieval, concurrency, security, backup. Examples: PostgreSQL, MySQL, Oracle.
- **RDBMS (Relational DBMS)** → DBMS based on relational model. Data in tables with rows/columns. SQL as query language. ACID-compliant. Examples: PostgreSQL, MySQL, Oracle, SQL Server.
- **NoSQL** → "Not Only SQL". Non-relational; schema-flexible; optimized for scale and specific data models. Examples: MongoDB, Cassandra, Redis, Neo4j.
- **Data Model** → Abstract representation of how data is organized and relationships defined. Determines query patterns and performance characteristics.
- **Schema** → Definition of database structure: table names, column types, constraints, indexes. Logical schema (what) vs physical schema (how stored).
- **Instance** → The actual data in the database at a given moment. Schema = structure; Instance = data.
- **Metadata** → Data about data. Column names, types, constraints, statistics. Stored in the data dictionary.
- **Data Dictionary / Catalog** → System repository of metadata. `information_schema` in SQL. Used by optimizer, tools, and administrators.
- **Logical vs Physical Model** → Logical: entities, relationships, attributes (ERD). Physical: actual tables, indexes, partitions, storage layout.
- **Interview Note**: "Schema vs Instance" is a classic question. Schema is the blueprint; instance is the snapshot of data at a point in time.

---

### Data Models

- **Relational Model** → Data in tables (relations). Rows = tuples, columns = attributes. Relations between tables via foreign keys. Foundation of SQL databases.
- **Hierarchical Model** → Tree structure. Parent-child relationships. Fast for known access paths; rigid. Legacy (IBM IMS). Poor for many-to-many.
- **Network Model** → Graph of records with pointers. More flexible than hierarchical; still navigational. CODASYL standard. Mostly legacy.
- **Document Model** → Semi-structured documents (JSON/BSON/XML) as the unit of storage. Schema-flexible. MongoDB, CouchDB, Firestore. Great for nested/variable data.
- **Key-Value Model** → Simplest NoSQL. Map of key → opaque value. Extremely fast lookups. Redis, DynamoDB (at core), Riak. No query on value internals.
- **Column-Family Model** → Data grouped by column families rather than rows. Optimized for wide rows and sparse data. Cassandra, HBase. Great for write-heavy time-series and analytics.
- **Graph Model** → Nodes (entities) and edges (relationships) as first-class citizens. Optimized for relationship traversal. Neo4j, Amazon Neptune. Social networks, fraud detection, knowledge graphs.
- **Time-Series Model** → Optimized for time-stamped data. High write throughput, efficient time-range queries, automatic compression. InfluxDB, TimescaleDB, Prometheus.
- **Object-Oriented Database** → Store objects directly; avoid ORM mismatch. db4o, ObjectDB. Niche use; ORM with RDBMS is far more common.
- **Interview Note**: "Which DB for which problem?" is a top system design question. Document = flexible nested data. Column-family = write-heavy analytics. Graph = relationship queries. Key-Value = caching/session. Time-Series = metrics/IoT.

---

### Database Types

- **OLTP (Online Transaction Processing)** → High-frequency short transactions. Row-store. Normalized schema. Low latency. Examples: order entry, banking, user auth. PostgreSQL, MySQL, Oracle.
- **OLAP (Online Analytical Processing)** → Complex queries over large datasets. Column-store. Denormalized. High throughput scans. Examples: reporting, BI, analytics. Redshift, Snowflake, BigQuery.
- **HTAP (Hybrid Transactional/Analytical Processing)** → Combines OLTP + OLAP in one system. Avoids ETL lag. TiDB, SingleStore, CockroachDB (partial), Google Spanner.
- **In-Memory Database** → Data lives in RAM. Extremely low latency (microseconds). Redis, VoltDB, SAP HANA. Volatile unless persisted. Used for caching, sessions, leaderboards.
- **Distributed Database** → Data spread across multiple nodes/locations. Fault-tolerant. Horizontally scalable. CockroachDB, Cassandra, Spanner, DynamoDB.
- **Embedded Database** → Runs inside application process. No server. SQLite, H2, Derby, RocksDB. Used in mobile apps, testing, desktop applications.
- **Cloud Database** → Managed database service. No infrastructure management. Multi-AZ, auto backup, auto scaling. RDS, Aurora, Cloud SQL, Cosmos DB, DynamoDB.
- **Serverless Database** → Scales to zero; pay per request. Aurora Serverless, DynamoDB on-demand, PlanetScale. Ideal for variable or unpredictable workloads.
- **Interview Note**: "Why not always use HTAP?" → Cost and complexity. OLTP and OLAP have opposing optimization strategies (row-store vs column-store). HTAP is a trade-off.

---

### Data Types

- **Numeric** → `INTEGER`, `BIGINT`, `SMALLINT`, `DECIMAL(p,s)` (exact), `FLOAT`/`DOUBLE` (approximate). Use `DECIMAL` for money — never float.
- **Character / String** → `CHAR(n)` (fixed-length, padded), `VARCHAR(n)` (variable-length), `TEXT` (unlimited). `CHAR` wastes space; `VARCHAR` is standard.
- **Boolean** → `BOOLEAN` / `BOOL`. Some DBs store as `TINYINT(1)` (MySQL) or `BIT`.
- **Date / Time / Timestamp** → `DATE` (date only), `TIME` (time only), `TIMESTAMP` (date+time, no TZ), `TIMESTAMPTZ` (with timezone). Always store in UTC.
- **Binary (BLOB)** → Binary Large Object. Store files, images, raw bytes. Better to store files in object storage (S3) and reference by URL.
- **Text (CLOB)** → Character Large Object. Long text. Search performance poor without full-text index.
- **JSON / XML** → Native JSON support in PostgreSQL (`json`, `jsonb`), MySQL 5.7+. `jsonb` = binary, indexable, faster queries. XML: `XMLTYPE` in Oracle.
- **Spatial / Geospatial** → `GEOMETRY`, `GEOGRAPHY` types. PostGIS extension for PostgreSQL. Geohash indexing. Used for location-based queries (`ST_Distance`, `ST_Within`).
- **Interview Note**: "`jsonb` vs `json` in PostgreSQL?" → `jsonb` is stored binary, supports GIN indexes, faster for queries. `json` preserves whitespace/order, faster to insert. Always prefer `jsonb`.

---

### Database Objects

- **Table** → Core storage unit. Rows (records) and columns (fields). Has a primary key, constraints, indexes.
- **Row / Record** → Single data entry in a table. Unit of DML operations (INSERT/UPDATE/DELETE).
- **Column / Field** → Named attribute with a data type. Defines the domain of values for each row.
- **View** → Named query stored in the DB. Logical table; no stored data (except materialized views). Simplifies complex queries; provides security abstraction.
- **Materialized View** → View with stored result data. Refreshed periodically or on demand. Fast reads; stale risk. Used heavily in OLAP. PostgreSQL, Oracle, Redshift support natively.
- **Index** → Data structure for fast lookups. Trades write overhead and storage for read speed. B-Tree default; Hash, GIN, GiST, BRIN for special cases.
- **Sequence** → Auto-incrementing number generator. Used for surrogate primary keys. `SERIAL` / `BIGSERIAL` in PostgreSQL; `AUTO_INCREMENT` in MySQL.
- **Trigger** → Automatic action executed on DML event (BEFORE/AFTER INSERT/UPDATE/DELETE). Use sparingly — hidden side effects, hard to debug, performance impact.
- **Stored Procedure** → Named block of SQL/procedural code stored and executed in DB. Reduces round trips; but couples business logic to DB. `CREATE PROCEDURE`.
- **Function** → Returns a value; can be used in SELECT. Deterministic functions can be indexed. `CREATE FUNCTION`.
- **Interview Note**: "Why avoid triggers?" → Hidden side effects, hard to trace, difficult to test, can cascade unexpectedly. Application logic in code is more transparent and testable.

---

### Relationships & Constraints

- **Primary Key (PK)** → Uniquely identifies each row. Implicitly `NOT NULL` + `UNIQUE`. Single column or composite. Natural key vs surrogate key (auto-increment / UUID).
- **Foreign Key (FK)** → References PK of another table. Enforces referential integrity. `ON DELETE CASCADE` / `RESTRICT` / `SET NULL` options.
- **Unique** → Ensures all values in column(s) are distinct. Allows one `NULL` (unlike PK). Automatically creates an index.
- **Not Null** → Column must have a value. Prevents missing data. Design principle: be explicit about nullability.
- **Check** → Validates column value against a condition: `CHECK (age >= 18)`. Enforced at DB level regardless of application.
- **Default** → Provides default value if none supplied on INSERT: `DEFAULT NOW()`, `DEFAULT 0`.
- **Referential Integrity** → FK constraint ensures referenced rows always exist. Prevents orphaned records. Can be deferred in PostgreSQL.
- **Cardinality** → Nature of relationship between tables: 1:1 (passport-person), 1:N (customer-orders), N:M (students-courses — requires junction table).
- **Interview Note**: "Natural key vs surrogate key?" → Natural: meaningful (email, SSN) but can change. Surrogate: system-generated (UUID, sequence), stable, no business meaning. Prefer surrogate for stability.

---

### SQL & Querying

- **SELECT** → Retrieve data. `SELECT col1, col2 FROM table WHERE condition GROUP BY col HAVING agg_condition ORDER BY col LIMIT n`.
- **INSERT / UPDATE / DELETE** → DML operations. Always use `WHERE` on UPDATE/DELETE. Batch inserts are faster than row-by-row.
- **MERGE / UPSERT** → Insert-or-update in one statement. `INSERT ... ON CONFLICT DO UPDATE` (PostgreSQL). `MERGE INTO` (ANSI SQL, Oracle, SQL Server).
- **JOIN types** → `INNER JOIN` (matching rows only). `LEFT OUTER JOIN` (all left + matched right). `RIGHT OUTER JOIN` (all right + matched left). `FULL OUTER JOIN` (all rows both sides). `CROSS JOIN` (cartesian product — use carefully).
- **Subquery** → Query nested inside another. Correlated subquery: references outer query (re-evaluated per row — often slow). Use JOIN or CTE instead where possible.
- **CTE (Common Table Expression)** → `WITH cte AS (SELECT ...) SELECT * FROM cte`. Improves readability. Recursive CTEs for hierarchical data (`WITH RECURSIVE`).
- **Window Functions** → Perform calculations across a set of rows related to current row without collapsing. `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LAG()`, `LEAD()`, `SUM() OVER (PARTITION BY ... ORDER BY ...)`.
- **Aggregation** → `SUM`, `AVG`, `COUNT`, `MIN`, `MAX`. `COUNT(*)` counts all rows; `COUNT(col)` skips NULLs. `GROUP BY` groups rows; `HAVING` filters groups (post-aggregation).
- **ORDER BY** → Sorts result. Always specify for deterministic pagination. Expensive without index on sort column.
- **Interview Note**: "Window function vs GROUP BY?" → GROUP BY collapses rows into one per group. Window functions keep all rows and add a computed column alongside each row.

---

### Indexing

- **B-Tree Index** → Default index type. Balanced tree. Supports equality (`=`), range (`<`, `>`, `BETWEEN`), ordering (`ORDER BY`), prefix matching (`LIKE 'abc%'`). O(log n) lookups.
- **Hash Index** → Hash table. Equality-only (`=`). Faster than B-Tree for equality but no range support. PostgreSQL in-memory hash joins; MySQL MEMORY engine.
- **Bitmap Index** → Bit arrays per value. Extremely fast for low-cardinality columns (gender, status, boolean) with AND/OR queries. Used heavily in OLAP. Oracle native; PostgreSQL uses internally.
- **Composite Index** → Index on multiple columns: `(last_name, first_name)`. Order matters — leftmost prefix rule: queries must use columns from left. `(A, B)` helps `WHERE A=` and `WHERE A= AND B=` but not `WHERE B=` alone.
- **Covering Index** → Index includes all columns needed by a query. Query resolved from index alone without touching the table (index-only scan). Add with `INCLUDE` clause (PostgreSQL) or by including all columns.
- **Clustered Index** → Table data physically ordered by index key. InnoDB (MySQL): PK is always clustered. PostgreSQL: `CLUSTER` command (one-time, not maintained). Fast range scans on clustered column.
- **Non-clustered Index** → Separate structure pointing to table rows. Multiple per table. Lookup requires index scan + row fetch (double lookup). PostgreSQL: all indexes are non-clustered by default (heap-based).
- **Full-Text Index** → Inverted index for text search. `tsvector` + `tsquery` in PostgreSQL. GIN index for `jsonb` and arrays. Elasticsearch for production full-text search.
- **Function-Based Index** → Index on expression: `CREATE INDEX ON users (LOWER(email))`. Query must match expression exactly: `WHERE LOWER(email) = 'x'`. Enables case-insensitive search.
- **Interview Note**: "When does an index hurt?" → High write volume (every write maintains all indexes). Index on low-cardinality column (poor selectivity). Too many indexes = slow writes. Monitor with `pg_stat_user_indexes`.

---

### Query Optimization

- **Query Plan / Execution Plan** → Step-by-step execution strategy chosen by optimizer. `EXPLAIN` (PostgreSQL/MySQL) shows plan. `EXPLAIN ANALYZE` shows actual vs estimated rows and timing.
- **Cost-Based Optimizer (CBO)** → Chooses plan with lowest estimated cost using table statistics (row counts, column distributions, histogram). PostgreSQL, Oracle, SQL Server use CBO.
- **Rule-Based Optimizer** → Uses fixed heuristic rules regardless of data. Older; less accurate. Mostly replaced by CBO.
- **Index Scan vs Full Table Scan** → Index scan: O(log n) + row fetch. Full scan: reads every row. Optimizer may prefer full scan on small tables or when selectivity is low (>15–20% of rows).
- **Predicate Pushdown** → Move filter conditions closer to the data source in the plan. Reduces rows early. Applied by optimizer automatically; critical in distributed query engines (Spark, Presto).
- **Join Optimization** → Nested Loop (small tables), Hash Join (large unsorted tables), Merge Join (large pre-sorted tables). Optimizer chooses; ensure join columns are indexed.
- **Query Rewrite** → Optimizer internally transforms query into equivalent but faster form: subquery → join, `IN` → `EXISTS`, view expansion.
- **Statistics** → `ANALYZE` (PostgreSQL) / `UPDATE STATISTICS` (SQL Server) updates column statistics. Stale stats = bad plans. Auto-analyze in PostgreSQL; manual in some DBs.
- **Interview Note**: "Query is slow — how do you debug it?" → `EXPLAIN ANALYZE` → identify Sequential Scan on large table, bad row estimates, nested loop on large sets. Add index, rewrite join, or update stats.

---

### Transactions

- **Transaction** → Unit of work that is atomic. Begins with `BEGIN`; ends with `COMMIT` (persist) or `ROLLBACK` (undo). Fundamental to data integrity.
- **ACID Properties** → Atomicity (all or nothing), Consistency (DB always valid), Isolation (concurrent transactions don't interfere), Durability (committed data survives crash via WAL).
- **Isolation Levels** → Control visibility of uncommitted changes between concurrent transactions. Trade-off: higher isolation = more locks = less concurrency.
- **Read Uncommitted** → Can read dirty (uncommitted) data. Phantom, non-repeatable, dirty reads all possible. Almost never used. MySQL only.
- **Read Committed** → Reads only committed data. Prevents dirty reads. Non-repeatable reads still possible. Default in PostgreSQL, Oracle, SQL Server.
- **Repeatable Read** → Same query returns same rows within transaction. Prevents dirty + non-repeatable reads. Phantom reads possible. Default in MySQL InnoDB (MVCC-based, phantoms prevented too).
- **Serializable** → Full isolation. Transactions appear sequential. Prevents all anomalies (dirty, non-repeatable, phantom). Highest performance cost. Predicate locking or SSI (PostgreSQL).
- **Commit / Rollback** → `COMMIT` persists; `ROLLBACK` reverts all changes in transaction. `ROLLBACK TO SAVEPOINT sp1` for partial rollback.
- **Savepoint** → Named point within transaction: `SAVEPOINT sp1`. Enables partial rollback without aborting whole transaction.
- **Interview Note**: Read phenomena to know: Dirty Read (read uncommitted data), Non-Repeatable Read (row changes between reads), Phantom Read (new rows appear between reads). Each isolation level prevents progressively more.

---

### Concurrency Control

- **Locking (Row / Page / Table)** → Row lock: fine-grained, high concurrency. Page lock: intermediate. Table lock: coarse, low concurrency. PostgreSQL: row-level by default.
- **Shared Lock (S)** → Read lock. Multiple transactions can hold simultaneously. Blocks exclusive lock.
- **Exclusive Lock (X)** → Write lock. Only one holder. Blocks all other locks (shared + exclusive).
- **Optimistic Concurrency Control** → Assume no conflict; validate at commit. Use version number or timestamp. `UPDATE ... WHERE version = ?`. Good for low-contention workloads.
- **Pessimistic Concurrency Control** → Assume conflict; lock upfront. `SELECT ... FOR UPDATE`. Prevents lost updates but reduces throughput. Good for high-contention.
- **Deadlock** → Two transactions each waiting for a lock held by the other. DB detects and kills one (the victim). Prevent by consistent lock ordering. `DEADLOCK_TIMEOUT` in PostgreSQL.
- **Livelock** → Transactions keep retrying and yielding to each other — no progress. Rarer than deadlock. Add random backoff to break symmetry.
- **MVCC (Multi-Version Concurrency Control)** → Readers don't block writers; writers don't block readers. Each transaction sees a snapshot of data at its start time. PostgreSQL, Oracle, MySQL InnoDB all use MVCC. Old row versions cleaned up by VACUUM (PostgreSQL).
- **Interview Note**: "Why is PostgreSQL read not blocked by write?" → MVCC. Readers see the version snapshot at transaction start. Writers create new versions. No read-write conflicts. VACUUM reclaims old versions.

---

### Consistency Models

- **Strong Consistency** → All reads reflect the latest committed write. Requires coordination. Single-node RDBMS or distributed CP systems (Spanner, CockroachDB). Highest safety, highest cost.
- **Eventual Consistency** → Given no new writes, all nodes will eventually converge to the same value. DynamoDB, Cassandra (tunable). High availability; temporarily stale reads.
- **Causal Consistency** → Causally related operations are seen in order by all nodes. If A causes B, everyone sees A before B. Amazon DynamoDB transactions, MongoDB sessions.
- **Read-your-writes** → After a write, you always read your own write. Sticky sessions or read from primary. Important for UX (user submits form, then sees update).
- **Monotonic Reads** → Once you read a value, you never see an older value. Prevents "going back in time". Achieved via session pinning.
- **CAP Theorem** → In presence of network partition: choose CP (consistent + partition-tolerant, may reject requests) or AP (available + partition-tolerant, may return stale). CA impossible in distributed system.
- **PACELC Theorem** → Extends CAP: when no partition (E), trade Latency (L) vs Consistency (C). DynamoDB = PA/EL. Spanner = PC/EC. Better real-world model than CAP alone.
- **Interview Note**: "Cassandra vs PostgreSQL consistency?" → Cassandra: tunable (ONE/QUORUM/ALL). Default = eventual. PostgreSQL: strong (single node) or via synchronous replication. Choose based on SLA.

---

### Storage Engine & Architecture

- **Storage Engine** → Subsystem managing how data is physically read/written. MySQL: pluggable (InnoDB default, MyISAM legacy). PostgreSQL: single engine (heap-based). RocksDB used by many NoSQL.
- **Row Store** → Rows stored contiguously. Fast for OLTP (fetch entire row). Full row read even if only one column needed. PostgreSQL, MySQL InnoDB.
- **Column Store** → Columns stored contiguously. Fast for OLAP (scan one column across millions of rows). Better compression (same type together). Redshift, Snowflake, ClickHouse, Parquet files.
- **LSM Tree (Log-Structured Merge Tree)** → Write-optimized. Writes to in-memory MemTable → flushed to immutable SSTables → compacted. Fast writes, slower reads. RocksDB, Cassandra, LevelDB, HBase.
- **Write-Ahead Log (WAL)** → Changes written to log before data pages. Enables crash recovery (replay log) and replication (stream WAL to replicas). PostgreSQL WAL, MySQL binlog.
- **SSTable (Sorted String Table)** → Immutable, sorted key-value file. Used in LSM tree storage. Compaction merges SSTables, removes tombstones.
- **Buffer Cache / Buffer Pool** → In-memory page cache. Hot pages kept in memory. `shared_buffers` in PostgreSQL; `innodb_buffer_pool_size` in MySQL. Size is critical for performance.
- **Page / Block** → Fundamental I/O unit. PostgreSQL: 8KB pages. MySQL InnoDB: 16KB pages. Data read/written at page granularity even for single row access.
- **Compression** → Column stores achieve 5–10x compression. PostgreSQL: TOAST for large values. LZ4, ZSTD, Snappy for general page compression. Reduces I/O; increases CPU.
- **Interview Note**: "Why is Cassandra write-fast?" → LSM Tree: writes go to MemTable (RAM) + CommitLog (disk sequential). No random I/O. Reads are slower — may need to check multiple SSTables + Bloom filter.

---

### Data Distribution

- **Sharding** → Horizontal partitioning across multiple nodes. Each shard holds a subset of rows. Partition key determines which shard. Enables horizontal scale-out.
- **Horizontal Partitioning** → Split rows across partitions/shards by range, hash, or list. Scales write throughput. Cross-shard queries are expensive.
- **Vertical Partitioning** → Split columns. Hot columns (frequently accessed) in one table; cold columns in another. Reduces row size; improves cache efficiency.
- **Replication** → Copy data to multiple nodes for fault tolerance and read scaling. Synchronous (strong consistency, higher latency) vs asynchronous (eventual consistency, lower latency).
- **Master-Slave / Leader-Follower** → One leader handles writes; followers replicate and serve reads. Simple but leader is single point of failure (until failover). MySQL, PostgreSQL streaming replication.
- **Multi-Master** → Multiple nodes accept writes. Conflict resolution required (last-write-wins, vector clocks, CRDTs). Cassandra, CockroachDB, DynamoDB Global Tables.
- **Consistent Hashing** → Hash ring distributes keys across nodes. Adding/removing nodes only remaps a fraction of keys (vs full rehash). Cassandra, DynamoDB use this.
- **Data Locality** → Place data close to compute. Same AZ. Partition key design ensures related data co-located. Kafka consumers on same broker AZ. Reduces network latency.
- **Interview Note**: "How do you handle hot partitions in Cassandra?" → Add random suffix to partition key (write-side fan-out), use time-bucket partition keys, or pre-split with token ranges.

---

### Distributed Databases

- **Distributed Transactions** → Transaction spans multiple nodes/databases. Requires coordination protocol. Much harder than single-node transactions. High latency cost.
- **Two-Phase Commit (2PC)** → Phase 1 (Prepare): coordinator asks all participants to vote. Phase 2 (Commit/Abort): coordinator decides based on votes. Blocking: coordinator failure = all participants stuck.
- **Three-Phase Commit (3PC)** → Adds pre-commit phase to avoid blocking. Reduces but doesn't eliminate failure scenarios. Rarely used in practice.
- **Consensus (Raft / Paxos)** → Algorithm for multiple nodes to agree on a single value. Raft (understandable, etcd, CockroachDB) vs Paxos (original, complex, Chubby). Requires majority quorum.
- **Leader Election** → Consensus used to elect single leader per shard/partition. ZooKeeper, etcd manage leader election for distributed systems.
- **Quorum** → Minimum nodes that must agree for operation to succeed. `W + R > N` for strong consistency (W=write quorum, R=read quorum, N=replicas). Cassandra: `QUORUM` = majority.
- **Gossip Protocol** → Nodes exchange state with random peers; state propagates like gossip. Decentralized, fault-tolerant. Used by Cassandra for cluster membership and failure detection.
- **Interview Note**: "Why avoid distributed transactions?" → High latency (multiple round trips), blocking on coordinator failure, complex error handling. Prefer saga pattern (choreography/orchestration) + eventual consistency + idempotent compensation.

---

### Performance & Scaling

- **Latency** → Time for a single operation. Target < 10ms for OLTP reads. Affected by: index efficiency, network hops, lock contention, buffer cache hit rate.
- **Throughput** → Operations per second. Improve via: connection pooling, batch writes, read replicas, partitioning, async processing.
- **Connection Pooling** → Reuse DB connections. DB connections are expensive (auth, memory per connection). PgBouncer (PostgreSQL), HikariCP (Java). Max connections: PostgreSQL ~200–500; use pool to multiplex.
- **Caching** → Serve repeated reads from fast cache (Redis, Memcached). Cache-aside, read-through, write-through, write-behind patterns. Cache invalidation is the hard part.
- **Read Replicas** → Route read traffic to replica nodes. Scale read throughput. Lag between primary and replica = eventual consistency. Use for reports, analytics, non-critical reads.
- **Write Scaling** → Shard by key range or hash. Reduce write contention. Batch inserts. Async writes with queues. CQRS separates write model from read model.
- **Batch Processing** → Group multiple operations: `INSERT INTO ... VALUES (...),(...),...`. JDBC batch mode. Reduce round trips; amortize overhead. 100–1000x faster than row-by-row.
- **Query Parallelism** → Parallel query execution across multiple CPU cores or nodes. `max_parallel_workers_per_gather` in PostgreSQL. ClickHouse, Presto, BigQuery designed for massive parallelism.
- **Interview Note**: "Connection pool size?" → Not "more = better". Formula: `threads = (cores * 2) + disk spindles` (Hikari recommendation). Too many connections = context switching overhead, memory exhaustion.

---

### Data Warehousing & Analytics

- **Data Warehouse** → Centralized repository for integrated, historical data from multiple sources. Optimized for query (OLAP). Redshift, Snowflake, BigQuery, Azure Synapse.
- **Data Lake** → Raw data storage in any format (structured, semi-structured, unstructured). Schema-on-read. S3 + Glue, Azure Data Lake, GCS. Flexible but can become "data swamp".
- **Data Mart** → Subset of data warehouse focused on one business area (Sales, HR). Faster queries; simpler for business users.
- **ETL / ELT** → ETL: Extract → Transform → Load (transform before loading). ELT: Extract → Load → Transform (transform in warehouse). ELT preferred in cloud (leverage warehouse compute).
- **Star Schema** → Central fact table surrounded by dimension tables. Simple join structure. Fast for OLAP queries. `sales_fact` joins to `date_dim`, `product_dim`, `customer_dim`.
- **Snowflake Schema** → Normalized star schema. Dimension tables further normalized. More joins, less storage redundancy. Named after the company (coincidence).
- **Fact Table** → Contains measurable, quantitative data (sales amount, quantity). Typically large. References dimension tables via FK.
- **Dimension Table** → Descriptive attributes (product name, category, customer name, date). Small to medium. Slowly Changing Dimensions (SCD Type 1: overwrite, Type 2: new row, Type 3: new column).
- **OLAP Cube** → Pre-aggregated multi-dimensional data. Slice, dice, drill-down, roll-up operations. SSAS, Druid. Mostly replaced by columnar warehouses.
- **Interview Note**: "Star vs Snowflake schema?" → Star: simpler queries, some redundancy, faster BI tools. Snowflake: normalized, less storage, more joins. Star preferred for query performance in BI.

---

### Streaming & Real-Time Data

- **Event Streaming** → Continuous flow of events (state changes). Kafka, Kinesis, Pulsar. Each event is immutable and persisted in the log.
- **Change Data Capture (CDC)** → Capture row-level changes (INSERT/UPDATE/DELETE) from DB transaction log. Debezium, AWS DMS, Oracle GoldenGate. Enables real-time sync, event sourcing, zero-downtime migration.
- **Log-Based Replication** → Replicate changes by reading WAL (PostgreSQL) or binlog (MySQL). Source of truth is the log. CDC is built on this.
- **Stream Processing** → Process events as they arrive. Flink, Spark Streaming, Kafka Streams. Stateful operations, windowing, joins across streams.
- **Windowing** → Group streaming events by time: Tumbling (fixed non-overlapping), Sliding (overlapping), Session (activity-based gap). Aggregate within window (sum clicks per 5-min tumbling window).
- **Interview Note**: "How do you sync two databases with zero downtime?" → CDC (Debezium) → Kafka → consumer writes to target DB. Run dual-write phase, then cut over. Validate with row count + checksum comparison.

---

### Security

- **Authentication** → Verify identity. Username/password, certificates, IAM roles (cloud). `pg_hba.conf` controls PostgreSQL auth methods.
- **Authorization** → What authenticated user can do. `GRANT SELECT ON table TO user`. `REVOKE`. Role-based.
- **RBAC (Role-Based Access Control)** → Permissions assigned to roles; users assigned to roles. `CREATE ROLE analyst; GRANT SELECT ON reports TO analyst;`.
- **ABAC (Attribute-Based Access Control)** → Permissions based on attributes (department, clearance level, time of day). More flexible than RBAC; more complex.
- **Encryption at Rest** → Encrypt data files on disk. Transparent Data Encryption (TDE) in Oracle, SQL Server. PostgreSQL: use filesystem encryption (dm-crypt, AWS EBS encryption).
- **Encryption in Transit** → TLS for all DB connections. `ssl=require` in PostgreSQL connection string. Certificates for mutual TLS (mTLS).
- **Data Masking** → Replace sensitive data with realistic but fake data. Dynamic masking (mask on query) vs static (mask in copy). Used for dev/test environments.
- **Auditing** → Log who did what when. `pgaudit` extension for PostgreSQL. AWS CloudTrail for RDS. Required for compliance (GDPR, HIPAA, SOX).
- **Row-Level Security (RLS)** → Policy-based row filtering at DB level. `CREATE POLICY on_own_data ON orders USING (user_id = current_user_id())`. Each user sees only their rows. PostgreSQL, Oracle support natively.
- **Interview Note**: "How do you secure a multi-tenant DB?" → RLS for logical isolation, separate schemas or databases for stronger isolation, encryption per tenant, audit all access.

---

### Backup & Recovery

- **Full Backup** → Complete snapshot of all data. Largest backup; longest to create. Baseline for incremental/differential.
- **Incremental Backup** → Only changes since last backup (full or incremental). Smaller, faster. Restore requires full + all incrementals in chain.
- **Differential Backup** → Changes since last full backup. Larger than incremental but simpler restore (full + latest differential only).
- **Restore** → Apply backup to recover data. Test restores regularly — untested backups are not backups. Restoration time is part of RTO planning.
- **Point-in-Time Recovery (PITR)** → Restore to any moment using base backup + WAL/binlog replay. `pg_basebackup` + WAL archiving in PostgreSQL. Recover from accidental DELETE at 2:37 PM.
- **Snapshots** → Storage-level point-in-time copy (EBS, RDS snapshots). Near-instantaneous. Consistent snapshot requires DB quiesce or crash-consistent restore.
- **Disaster Recovery (DR)** → Strategy to recover from catastrophic failure (region loss). RTO (Recovery Time Objective) = max acceptable downtime. RPO (Recovery Point Objective) = max acceptable data loss.
- **High Availability (HA)** → Minimize downtime. Multi-AZ RDS = synchronous standby, automatic failover. Aurora: 6 copies across 3 AZs. Patroni for PostgreSQL HA.
- **Interview Note**: "RTO vs RPO?" → RTO = how fast must you recover? RPO = how much data can you lose? Both drive architecture: low RPO = synchronous replication; low RTO = hot standby with automatic failover.

---

### Cloud Databases

- **Managed Database** → Cloud provider handles patching, backups, replication, failover. RDS (AWS), Cloud SQL (GCP), Azure Database. Reduces ops burden; less control.
- **Multi-AZ Deployment** → Synchronous standby in another Availability Zone. Automatic failover on primary failure. ~60 sec failover for RDS Multi-AZ.
- **Auto Scaling** → Aurora Auto Scaling adds/removes replicas based on load. DynamoDB auto-scales read/write capacity. Serverless DBs scale to zero.
- **Serverless Database** → Aurora Serverless V2: scales in fine-grained ACU increments. DynamoDB on-demand: no capacity planning. PlanetScale: MySQL-compatible serverless.
- **Global Distribution** → DynamoDB Global Tables: multi-region active-active with < 1s replication. Aurora Global: primary region + 5 secondary (read-only). CockroachDB: truly distributed multi-region.
- **Edge Databases** → DB instances at edge locations for ultra-low latency. Cloudflare D1 (SQLite at edge), PlanetScale's edge routing, Turso (libSQL distributed).
- **Interview Note**: "When to use DynamoDB vs Aurora?" → DynamoDB: key-value/document, massive scale, serverless, predictable single-digit ms. Aurora: relational, complex queries, MySQL/PostgreSQL compatible, ACID at scale.

---

### NoSQL Systems

- **Key-Value Store** → Map of key → value. O(1) lookup. Redis (in-memory + persistence), DynamoDB, Riak. Best for: sessions, caches, feature flags, leaderboards.
- **Document Store** → JSON/BSON documents. Rich query on nested fields. MongoDB, Firestore, CouchDB. Best for: catalogs, content, user profiles, variable-schema data.
- **Column Store (Column-Family)** → Wide rows. Partition key + clustering key. Cassandra, HBase. Best for: time-series, write-heavy, sparse data, multi-region.
- **Graph Database** → Nodes + edges + properties. Relationship traversal first-class. Neo4j (Cypher), Amazon Neptune (Gremlin/SPARQL). Best for: social networks, fraud detection, recommendations, knowledge graphs.
- **Schema-less** → No rigid schema enforced by DB. Flexible evolution. But: application must handle missing fields; harder to ensure data quality. Validate at application layer.
- **Denormalization** → Embed related data inside document/row to avoid joins. Faster reads; data duplication; harder to update consistently. Core NoSQL design pattern.
- **Interview Note**: "Why not use MongoDB for everything?" → No ACID multi-document transactions (added in 4.0 but with caveats), poor for complex relational queries, denormalization leads to update anomalies. Choose based on access patterns, not hype.

---

### Graph Databases

- **Nodes / Edges** → Nodes = entities (Person, Product). Edges = relationships (KNOWS, BOUGHT). Both can have properties. Edges are first-class, not foreign keys.
- **Traversal** → Navigating from node to node via edges. O(1) per hop (pointer-based, not join-based). Efficient for deep relationship queries (6 degrees of separation).
- **Cypher** → Declarative graph query language for Neo4j. `MATCH (p:Person)-[:KNOWS]->(f:Person) WHERE p.name = 'Alice' RETURN f.name`. ASCII-art syntax for patterns.
- **Gremlin** → Graph traversal language for Apache TinkerPop. Supported by Amazon Neptune, JanusGraph. Imperative style: `g.V().hasLabel('Person').out('KNOWS').values('name')`.
- **Path Queries** → Find shortest path, all paths, weighted paths. `shortestPath()` in Cypher. Classic use cases: route planning, fraud rings, supply chain tracing.
- **Interview Note**: "Why not model a social graph in PostgreSQL?" → Many-to-many self-referential queries require recursive CTEs or multiple joins. Graph DBs traverse natively in O(log n) per hop; SQL degrades exponentially with depth.

---

### Time-Series Databases

- **Time Index** → Primary index on timestamp. All queries filtered by time range. Data physically ordered by time. Enables efficient time-range scans.
- **Downsampling** → Reduce resolution over time. Keep raw data for 7 days, 1-min aggregates for 30 days, 1-hour aggregates for 1 year. Reduces storage; acceptable for old data.
- **Retention Policy** → Automatically delete data older than threshold. InfluxDB, Prometheus retention. Essential to control storage growth.
- **Compression** → Time-series data highly compressible: timestamps delta-encoded, values delta-of-delta or XOR (Gorilla compression by Meta). 10x+ compression ratios common.
- **Examples** → InfluxDB (line protocol, Flux query language), TimescaleDB (PostgreSQL extension, SQL), Prometheus (pull-based, PromQL), OpenTSDB (HBase-backed), QuestDB (SQL, columnar).
- **Interview Note**: "Why not store metrics in PostgreSQL?" → Works for small scale. Breaks at millions of writes/second. Time-series DBs have: write-optimized storage, automatic compression, retention policies, downsampling built in.

---

### Database Tools & Ecosystem

- **ETL Tools** → Apache NiFi, Talend, Informatica, AWS Glue, dbt (transformation layer). Move and transform data between systems.
- **Data Integration** → Debezium (CDC), Kafka Connect (source/sink connectors), Fivetran/Airbyte (managed connectors). Keep systems in sync.
- **Data Governance** → Policies and processes for data quality, ownership, access, compliance. Apache Atlas, Collibra, Alation.
- **Data Catalog** → Searchable inventory of data assets: what data exists, where, who owns it, lineage. AWS Glue Catalog, Apache Atlas, DataHub, Amundsen.
- **Data Lineage** → Track data from source to destination through all transformations. Audit trail for compliance. OpenLineage standard. Integrated in dbt, Marquez, DataHub.
- **Interview Note**: "How do you manage data quality in a data lake?" → Data catalog for discovery, lineage for tracing, Great Expectations or dbt tests for validation, governance policies for access and ownership.

---

### Anti-Patterns

- **N+1 Query Problem** → Fetch N rows, then make N additional queries for related data. Classic ORM trap. Fix: eager loading (JOIN), `@EntityGraph` in JPA, batch loading, DataLoader.
- **Full Table Scan Abuse** → Query missing WHERE clause or index on filtered column causes full scan. Devastating at scale. Fix: index on predicate columns, rewrite query, partition pruning.
- **Missing Index** → Frequently queried column has no index. Symptom: slow queries, high I/O. Fix: identify with `EXPLAIN`, `pg_stat_statements`, slow query log; add targeted index.
- **Over-Normalization** → So many tables and joins that query performance suffers. Correct logically but impractical for read performance. Fix: denormalize hot read paths or use materialized views.
- **Under-Normalization** → Duplicate data across tables causes update anomalies. Data inconsistency. Fix: normalize to 3NF, use denormalized views only for reads.
- **Hot Partition** → One partition/shard receives disproportionate traffic. Throughput bottleneck even though other shards are idle. Fix: better partition key design (add entropy/randomness), time-bucketing.
- **Single Point of Failure** → No redundancy: single DB instance, no replica, no backup. Fix: Multi-AZ, read replicas, backup/restore tested, HA proxy.
- **Interview Note**: "How do you solve N+1 in production?" → Identify with slow query log or APM (datadog, New Relic). Fix at ORM level (fetch join, entity graph). Batch fetching for collections. DataLoader pattern for GraphQL.

---

### Interview Power Keywords — Database Edition

| Category | Power Keywords |
|---|---|
| **Read vs Write Optimization** | Row store (OLTP reads), Column store (OLAP scans), LSM tree (write), B-tree (read), covering index |
| **Index Trade-offs** | Write overhead, selectivity, composite column order, covering index, partial index, expression index |
| **Partition Strategy** | Range vs hash vs list, hot partition avoidance, consistent hashing, cross-partition query cost |
| **Consistency vs Availability** | CAP theorem, PACELC, quorum reads/writes, tunable consistency (Cassandra ONE/QUORUM/ALL) |
| **Scaling Strategy** | Read replicas (read scale), sharding (write scale), caching (latency), connection pooling (throughput) |
| **Query Optimization** | EXPLAIN ANALYZE, index scan vs seq scan, join type, statistics staleness, predicate pushdown |

---

### Advanced / Staff+ Level Topics

- **Multi-Tenant Databases** → Strategies: shared DB + shared schema (RLS), shared DB + separate schema, separate DB per tenant. Trade-offs: isolation, cost, operational complexity.
- **Data Sovereignty** → Legal requirement to store data in specific country/region. Multi-region DB with geo-partitioning: CockroachDB, Spanner, Aurora Global with region restriction.
- **Global Replication** → Active-active across regions: DynamoDB Global Tables (last-write-wins), CockroachDB (serializable), Spanner (TrueTime). Active-passive: Aurora Global (< 1s replication lag).
- **Active-Active vs Active-Passive** → Active-Active: all regions serve reads/writes; conflict resolution required. Active-Passive: primary serves writes; passive is failover only. Active-Active = higher availability, higher complexity.
- **Data Mesh** → Decentralized data ownership. Domain teams own their data as a product. Federated governance. Contrast with centralized data warehouse.
- **Lakehouse Architecture** → Combines data lake (raw, cheap storage) with data warehouse (ACID, query performance). Delta Lake, Apache Iceberg, Apache Hudi. ACID on object storage; time travel; schema evolution.
- **HTAP Systems** → Handle OLTP and OLAP in one system. TiDB (TiKV + TiFlash), SingleStore, SAP HANA. Eliminates ETL lag for real-time analytics on operational data.
- **Cost Optimization (Storage vs Compute)** → Separate storage and compute (Snowflake, Redshift Serverless, BigQuery): pay for what you use. Tiered storage: hot (SSD), warm (HDD), cold (S3/GCS). Compress aggressively. Right-size instances.
- **Interview Note**: At Staff+ level: "How would you architect a globally distributed database for a financial system?" → Spanner/CockroachDB for strong consistency + global distribution + ACID. Geo-partitioning for data sovereignty. Synchronous replication for RPO=0. Read replicas in each region. PITR for recovery.

---

## 71. Engineering Principles Master Reference (NEW)

> **Coverage:** Every engineering principle category — Core, SOLID, Clean Code, Architectural, System Design, Security, Distributed Systems, Data & Database, Performance, Observability, DevOps, Testing, OOP Design, Design Pattern, DDD, Cloud, Anti-Principles, and Staff+ Leadership. Each includes subtopics, keywords, and interview-ready notes.

---

### Core Engineering Principles

- **Separation of Concerns (SoC)** → Split system into distinct sections, each addressing a separate concern. Foundation of all architecture. Example: MVC separates UI, logic, data.
- **Modularity** → Divide system into independent, interchangeable modules with well-defined interfaces. Enables parallel development and easier replacement.
- **Abstraction** → Expose only what callers need; hide irrelevant detail. Work at the right level of concept, not implementation.
- **Encapsulation** → Bundle data and behavior together; hide internals. Changes inside a module don't ripple outward.
- **Information Hiding** → A module should reveal as little as possible about its internal workings. Reduces coupling; enables safe refactoring.
- **Single Responsibility** → Every module, class, or function should have exactly one reason to change. Leads to high cohesion.
- **Composition over Inheritance** → Build complex behavior by combining simpler objects. More flexible than deep inheritance hierarchies; avoids fragile base class problem.
- **Program to an Interface** → Depend on abstractions, not concrete implementations. Enables swap of implementations without changing callers.
- **Least Knowledge (Law of Demeter)** → A module should only talk to its direct collaborators. Avoid chaining: `a.getB().getC().doX()` — tell, don't ask.
- **Principle of Least Astonishment (POLA)** → System behavior should match user expectations. Surprising APIs cause bugs. Consistency builds trust.
- **Interview Note**: SoC + Information Hiding + Single Responsibility are three angles on the same idea: one thing, one place, hidden from the rest.

---

### SOLID Principles

- **Single Responsibility Principle (SRP)** → A class has one reason to change. If you can't describe it in one sentence without "and", split it. Metric: cohesion (LCOM).
- **Open/Closed Principle (OCP)** → Open for extension, closed for modification. Add behavior via new code (Strategy, Decorator), never by editing stable working code.
- **Liskov Substitution Principle (LSP)** → Subtypes must be substitutable for their base type without altering correctness. Don't strengthen preconditions or weaken postconditions in subclass. Classic violation: `Square extends Rectangle`.
- **Interface Segregation Principle (ISP)** → Clients should not be forced to depend on interfaces they don't use. Split fat interfaces into focused role interfaces.
- **Dependency Inversion Principle (DIP)** → High-level modules must not depend on low-level modules. Both depend on abstractions. Abstractions must not depend on details.
- **Interview Note**: SOLID at depth = trade-off awareness. SRP → cohesion. OCP → extension model (Strategy, plugin). LSP → contract correctness. ISP → role-based APIs. DIP → inversion via DI containers.

---

### Clean Code Principles

- **DRY (Don't Repeat Yourself)** → Every piece of knowledge has exactly one representation. Duplication = two places to fix one bug. Extract shared logic; use abstraction.
- **KISS (Keep It Simple, Stupid)** → Simpler is better. Avoid clever code; optimize for readability. Complex code = hard to debug, test, and maintain.
- **YAGNI (You Aren't Gonna Need It)** → Don't build features speculatively. Build what's needed now. Defer decisions until they're forced.
- **Boy Scout Rule** → Leave code cleaner than you found it. Continuous small improvements prevent entropy accumulation.
- **Self-Documenting Code** → Code reads like prose. Meaningful names, small functions, clear intent. Comments explain *why*, not *what*.
- **Meaningful Naming** → Variable/method/class names reveal intent. `processData()` → bad. `calculateMonthlyInterest()` → good. Names are the first documentation.
- **Small Functions** → Functions do one thing. If it needs a comment header, extract it. Single level of abstraction per function.
- **Avoid Premature Optimization** → "Premature optimization is the root of all evil" — Knuth. First: make it work. Then: make it right. Then: make it fast (only if profiling shows need).
- **Interview Note**: DRY violation is often the first sign of design smell. YAGNI prevents over-engineering. Boy Scout Rule enables sustainable velocity.

---

### Architectural Principles

- **High Cohesion** → Elements within a module belong together and work toward a common purpose. Measured by LCOM (Lack of Cohesion of Methods). High cohesion → easier to understand and test.
- **Low Coupling** → Modules depend on as few other modules as possible. Changes in one don't cascade to others. Measured by afferent/efferent coupling (Ca/Ce).
- **Loose Coupling** → Dependency through abstractions (interfaces, events, queues), not concrete classes. Enables independent deployment and testing.
- **Explicit Dependencies** → Don't hide dependencies via global state or service locators. Inject them. Makes dependencies visible, testable, and replaceable.
- **Dependency Injection (DI)** → Provide dependencies from outside the class. Constructor injection preferred (immutable, testable). Spring, Guice, CDI manage this.
- **Inversion of Control (IoC)** → Framework calls your code, not the other way around. Template Method, event listeners, Spring lifecycle hooks.
- **Layered Architecture Principle** → Each layer only depends on the layer directly below. Presentation → Application → Domain → Infrastructure. Prevents cross-layer coupling.
- **Clean Architecture Principles** → Dependency rule: source code dependencies point only inward. Domain layer has zero external dependencies.
- **Hexagonal Architecture (Ports & Adapters)** → Core domain surrounded by ports (interfaces) and adapters (implementations). Swap infrastructure without touching domain.
- **Stable Dependencies Principle (SDP)** → Depend on modules that are more stable (change less) than you are. Stability = (Ce / (Ca + Ce)).
- **Stable Abstractions Principle (SAP)** → The more stable a module, the more abstract it should be. Stable concrete = rigid system.
- **Acyclic Dependencies Principle (ADP)** → No cycles in the module/package dependency graph. Break cycles with dependency inversion or a new shared module.
- **Interview Note**: Hexagonal Architecture is the answer to "how do you keep your domain testable when the DB/API changes?" Ports = interfaces, Adapters = implementations.

---

### System Design Principles

- **Scalability First Design** → Design for growth from day one. Horizontal > vertical. Stateless services scale easily; stateful services need sticky sessions or distributed state.
- **Availability over Consistency (trade-off)** → In a partition (network split), choose AP (stay available, accept stale data) or CP (reject requests to stay consistent). CAP Theorem forces this choice.
- **Fault Isolation** → Failure in one component must not cascade. Bulkhead pattern: isolate thread pools, connection pools, circuit breakers per dependency.
- **Graceful Degradation** → System partially degrades under load rather than fully failing. Return cached data, disable non-critical features, show fallback UI.
- **Backpressure Handling** → Slow consumer signals slow producer to throttle. Prevents buffer overflow and OOM. Reactive Streams spec defines this. Use bounded queues.
- **Idempotency** → Applying the same operation multiple times produces the same result as once. Critical for retries. Use idempotency keys for POST APIs. PUT is naturally idempotent.
- **Statelessness** → No server-side session state. Any instance can handle any request. Enables horizontal scaling and zero-downtime deploys.
- **Horizontal Scalability** → Add more instances to scale out. Requires stateless services, shared storage, and load balancing.
- **Data Locality** → Process data close to where it lives. Minimize network hops. Kafka consumer on same AZ as broker. Lambda near DynamoDB.
- **Eventual Consistency** → Distributed systems accept temporary inconsistency. Data converges over time. Use for high-availability, low-latency reads (DNS, shopping carts, social feeds).
- **Interview Note**: Idempotency + retry with backoff + dead letter queues = foundation of reliable distributed message processing.

---

### Security Principles

- **Principle of Least Privilege (PoLP)** → Every user, service, and process gets only the minimum access needed to do its job. Reduces blast radius of compromise.
- **Defense in Depth** → Multiple independent security layers. Breach of one layer doesn't compromise the system. WAF + Auth + Encryption + Auditing.
- **Fail Secure** → On error or uncertainty, default to deny. Never fail open (granting access on exception). Check return values; handle auth errors explicitly.
- **Zero Trust** → Never trust, always verify. Even internal services authenticate and authorize every call. Assume breach; authenticate east-west traffic.
- **Secure by Design** → Security is a first-class concern, not a bolt-on. Threat model during design. Security review as part of architecture, not just pen test at the end.
- **Secure by Default** → Insecure options require explicit opt-in. HTTPS by default. Auth required by default. No debug endpoints in prod.
- **Encryption Everywhere** → Encrypt data in transit (TLS) and at rest (AES-256). Encrypt backups and logs. Manage keys separately (KMS).
- **Input Validation** → Never trust user input. Validate at all system boundaries (API, DB, file input). Whitelist over blacklist. Parameterized queries prevent SQL injection.
- **Output Encoding** → Encode output before rendering to prevent XSS. Context-aware encoding (HTML, JS, URL). Use templating engines that auto-encode.
- **Interview Note**: Zero Trust is the answer to "how do you secure microservices?" — mTLS between services, JWT validation at every boundary, no implicit trust from network location.

---

### Distributed System Principles

- **CAP Theorem Awareness** → Consistency + Availability + Partition Tolerance: pick two when partition occurs. CP examples: ZooKeeper, etcd, PostgreSQL. AP examples: Cassandra, DynamoDB, CouchDB.
- **PACELC Trade-off** → Extends CAP: when no partition (E), trade Latency (L) vs Consistency (C). DynamoDB: PA/EL. CockroachDB: PC/EC.
- **Consensus over Coordination** → Use Raft/Paxos for agreement instead of distributed locks (which are complex and failure-prone). ZooKeeper and etcd implement Raft.
- **Immutable Data Preference** → Append-only logs; event sourcing; immutable records. Easier reasoning, replay, audit. Kafka is an immutable log.
- **Event-Driven Thinking** → Model state changes as events. Decouple producers and consumers. Enable audit, replay, and temporal decoupling.
- **Asynchronous First** → Default to async communication (queues, events). Fall back to sync only when immediate response required. Async = higher resilience.
- **Retry with Backoff** → Exponential backoff + jitter prevents thundering herd. Always cap retries (max attempts). Use dead letter queue for poison messages.
- **Circuit Breaker Principle** → Stop calling a failing service. States: Closed (normal) → Open (failing, reject fast) → Half-Open (test recovery). Hystrix, Resilience4j.
- **Bulkhead Isolation** → Isolate different consumers/services into separate thread pools, connection pools, or processes. Failure in one bulkhead doesn't drain resources of others.
- **Interview Note**: Circuit Breaker + Retry + Bulkhead + Timeout = the four resilience patterns. Every external call should have all four configured.

---

### Data & Database Principles

- **ACID Principles** → Atomicity (all or nothing), Consistency (valid state always), Isolation (concurrent transactions don't interfere), Durability (committed data survives crash). Relational DB guarantee.
- **BASE Principles** → Basically Available, Soft state, Eventually consistent. NoSQL trade-off. Accept stale reads for higher availability and scalability.
- **Schema Evolution** → Design schemas to evolve without breaking consumers. Additive changes (new nullable column) are safe. Rename/delete breaks consumers. Use versioning.
- **Data Integrity** → Enforce via constraints (FK, unique, not-null), application logic, and event validation. Never rely on a single layer alone.
- **Data Consistency Models** → Strong > Sequential > Causal > Read-your-writes > Eventual. Choose based on use case. Bank transfer = strong. Social feed = eventual.
- **Normalization vs Denormalization** → Normalize for write consistency (3NF eliminates redundancy). Denormalize for read performance (precomputed joins). OLTP = normalized; OLAP/reporting = denormalized.
- **Write Optimization vs Read Optimization** → LSM tree (RocksDB, Cassandra): fast writes, slower reads. B-tree (PostgreSQL, MySQL): balanced; faster reads. Choose per workload.
- **Data Partitioning Principle** → Horizontal (sharding by row/key) vs vertical (splitting columns). Affects query patterns, hot spots, cross-partition joins. Consistent hashing for even distribution.
- **Interview Note**: "Why Cassandra over PostgreSQL?" → Write-heavy, wide-column, multi-region. CAP: AP. BASE. Partition key design is everything — hotspot prevention is the key interview depth.

---

### Performance Principles

- **Minimize Latency** → Fewer network hops, better algorithms (O(n) → O(log n)), connection pooling, caching, co-location.
- **Maximize Throughput** → Batching (send 100 records at once), async I/O, parallelism, pipelining, zero-copy (Kafka's sendfile).
- **Caching First** → Cache at every level: CPU (array locality), in-process (Caffeine), distributed (Redis), CDN (static assets). Cache invalidation is the hardest problem.
- **Lazy Loading** → Load only when needed. Defer expensive operations. JPA `@OneToMany(fetch = LAZY)`. Initialize only on demand.
- **Batching** → Group multiple small operations into one large one. Reduce overhead per operation. JDBC batch insert, Kafka batch publish.
- **Parallelism** → Split independent work across cores/threads. Parallel streams, ForkJoinPool, CompletableFuture. Only beneficial when work is CPU-bound and data-independent.
- **Asynchronous Processing** → Offload work to background threads/queues. Return response immediately. Use for emails, notifications, reports, heavy computation.
- **Avoid Blocking** → Non-blocking I/O (NIO, Netty, Virtual Threads). Blocking wastes threads. One blocked thread = one wasted OS resource (until Virtual Threads).
- **Interview Note**: "How do you improve throughput?" → Batch, async, parallel, cache, reduce serialization overhead, reduce GC pressure, avoid lock contention.

---

### Observability Principles

- **You Can't Fix What You Can't See** → Instrument everything before going to production. Observability is not optional; it's engineering hygiene.
- **Instrument First** → Add metrics, logs, and traces as features are built. Not as an afterthought. OpenTelemetry SDK from day one.
- **Logs, Metrics, Traces Correlation** → Tie all three with a shared `traceId`. One request's log, metric spike, and trace should all be findable together.
- **High Cardinality Awareness** → Never use `userId` or `requestId` as Prometheus labels (millions of unique values = cardinality explosion). Use distributed tracing for high-cardinality dimensions.
- **Alert on Symptoms, Not Causes** → Alert on user impact: high error rate, slow P99, SLO breach. Don't alert on high CPU alone (a symptom of something, not user impact itself).
- **SLO-driven Monitoring** → Define SLIs (request success rate), set SLOs (99.9% over 30 days), track error budget. Alert on burn rate, not just threshold.
- **Interview Note**: "How do you debug a production issue?" → Traces for request flow, logs for events, metrics for trends. Start with symptoms (SLO breach), drill to cause (trace → span → log line).

---

### DevOps & Delivery Principles

- **Shift Left** → Move testing, security, and quality checks earlier in the pipeline. Cheaper to fix in code review (minutes) than in production (hours + incident cost).
- **Continuous Integration (CI)** → Every commit triggers automated build + test. Fast feedback loop. Never let `main` be broken. Trunk-based development.
- **Continuous Delivery / Deployment (CD)** → Every passing build is deployable (CD) or automatically deployed (CDP). Small, frequent, low-risk releases.
- **Infrastructure as Code (IaC)** → Version-controlled infra (Terraform, CloudFormation, Pulumi). Reproducible environments. Infra reviewed like code. No manual snowflake servers.
- **Immutable Infrastructure** → Never modify running instances. Replace with new versions. AMIs, Docker images, Kubernetes rollouts. Eliminates configuration drift.
- **Automation First** → Automate repetitive tasks. Manual processes = inconsistency + human error. If you do it twice, automate it.
- **Reproducibility** → Same input always produces same output. Reproducible builds, deterministic tests, pinned dependency versions.
- **Small Batch Releases** → Release small changes frequently. Less risk per release. Easier rollback. Faster feedback. Feature flags decouple deploy from release.
- **Interview Note**: "How do you reduce deployment risk?" → Feature flags, canary releases, blue-green deploy, automated rollback on SLO breach, small batch sizes.

---

### Testing Principles

- **Test Pyramid** → Many unit tests (fast, cheap) → fewer integration tests → few E2E tests (slow, expensive). Invert = ice cream cone = slow, brittle suite.
- **Fast Feedback** → Tests should run in seconds, not minutes. Slow tests get skipped. Unit tests: < 1ms. Integration: < 1s. E2E: acceptable to be minutes (run less often).
- **Deterministic Tests** → Same input, same output, every time. No flakiness. No dependency on external services, system time, or random without seed.
- **Isolation in Tests** → Each test sets up and tears down its own state. No shared mutable state between tests. Use `@BeforeEach` / `@AfterEach`. Test order independence.
- **Mocking vs Real Integration Balance** → Mock at unit level for speed. Use real dependencies (testcontainers) for integration. Never mock what you don't own.
- **Contract Testing First** → Before mocking a service, define its contract (Pact). Prevents consumer-provider mismatch. Critical in microservices.
- **Interview Note**: Test pyramid inversion is the most common test suite smell. "Why are your tests slow?" → Too many integration tests. "Why are they brittle?" → Too many E2E tests.

---

### Object-Oriented Design Principles

- **Favor Composition over Inheritance** → Compose behavior at runtime by combining objects. Inheritance creates tight coupling and fragile hierarchies. Strategy pattern = composition.
- **Encapsulate What Varies** → Find the parts of code that change and isolate them behind an interface. Everything else stays stable. Foundation of Strategy, State, Command patterns.
- **Open for Extension, Closed for Modification** → Add new behavior without touching existing code. Plugin architectures, Strategy swapping, event listeners.
- **Depend on Abstractions** → High-level code depends on interfaces, not concrete classes. Enables testability (mock the interface) and flexibility (swap implementation).
- **Tell, Don't Ask** → Tell objects what to do; don't query their state to make decisions outside them. Avoids `if (obj.getStatus() == ACTIVE) obj.process()` — push logic into the object.
- **Hollywood Principle ("Don't call us, we'll call you")** → Framework controls the flow; calls your registered hooks. IoC containers, event listeners, callback registration.
- **Interview Note**: "Tell, Don't Ask" is the OOP answer to procedural thinking. If you're calling getters to make decisions, move the decision into the class.

---

### Design Pattern Principles

- **Encapsulate Behavior** → Wrap varying behavior in objects (Command, Strategy). Pass behavior around, compose, swap at runtime.
- **Separate Construction from Representation** → How an object is built (Builder, Factory) is separate from what it is. Enables different representations from same construction process.
- **Delegate Responsibility** → One object hands work to another specialized object. Decorator delegates to wrapped object, Proxy delegates to real subject.
- **Promote Reusability** → Patterns are reusable solutions to recurring problems. Name them in code and design conversations for shared vocabulary.
- **Decouple Sender and Receiver** → Command, Observer, Mediator: the entity initiating action doesn't know who handles it. Enables extensibility without modification.
- **Interview Note**: Patterns are vocabulary, not recipes. "We used Observer here" tells your team the decoupling model instantly. Pattern names reduce cognitive overhead.

---

### Domain-Driven Design (DDD) Principles

- **Ubiquitous Language** → Business and engineering share the same vocabulary. Terms in code match terms in domain conversations. Reduces translation errors and misunderstandings.
- **Bounded Context** → Clear boundary where a domain model applies. Each bounded context owns its data and schema. `Order` means different things in Sales vs Fulfillment.
- **Aggregate Root Consistency** → Transactional consistency is enforced only within an aggregate. Cross-aggregate changes use eventual consistency via domain events.
- **Domain Events** → Capture state changes as events (`OrderPlaced`, `PaymentFailed`). Decouple bounded contexts. Enable event sourcing, audit logs, projections.
- **Explicit Context Mapping** → Define how bounded contexts relate: Shared Kernel, Customer-Supplier, Conformist, Anti-Corruption Layer, Open Host, Published Language.
- **Anti-Corruption Layer** → Translate external model to your internal domain model. Protect domain integrity from messy third-party or legacy APIs.
- **Interview Note**: "How do you integrate with a legacy system without polluting your domain?" → Anti-Corruption Layer. Wrap the legacy API, translate to your Ubiquitous Language.

---

### Cloud & Scalability Principles

- **Design for Failure** → Assume every component will fail. Build redundancy, retries, circuit breakers, fallbacks. Chaos engineering validates this.
- **Elasticity** → Scale up automatically when load increases, scale down when it decreases. Auto-scaling groups, Kubernetes HPA, serverless functions.
- **Pay-as-you-go** → Provision only what you need, when you need it. Serverless (Lambda, Cloud Run) takes this to the extreme: pay per invocation.
- **Multi-region Redundancy** → Deploy across regions for disaster recovery. Active-active (serve traffic from both) vs active-passive (failover). RTO/RPO requirements drive the choice.
- **Decouple Compute & Storage** → Stateless compute + separate persistent storage. Enables independent scaling of each. S3 + Lambda, RDS + ECS.
- **Auto-scaling First** → Build auto-scaling in from the start. Manual capacity planning at cloud scale = either over-provisioning (cost) or under-provisioning (incidents).
- **Interview Note**: "How would you handle a 10x traffic spike?" → Horizontal scaling + auto-scaling + caching + async offloading + CDN for static + graceful degradation for non-critical paths.

---

### Anti-Principles (What to Avoid)

- **Over-engineering** → Building solutions far more complex than the problem demands. Today's "flexible architecture" is tomorrow's maintenance burden. YAGNI prevents this.
- **Premature Optimization** → Optimizing before profiling proves a bottleneck. Makes code complex, hard to read, and often wrong. Measure first; optimize the 3% that matters.
- **Tight Coupling** → Module A depends directly on concrete class B. Change B = change A. Hard to test, deploy, or replace independently. The root cause of most design debt.
- **Big Ball of Mud** → No discernible architecture. Everything depends on everything. Changes ripple unpredictably. Characterized by fear of touching anything.
- **Golden Hammer** → Using one tool/pattern/technology for every problem regardless of fit. Microservices for a 2-person team. Kafka for 100 events/day. Kubernetes for a hobby project.
- **Reinventing the Wheel** → Building from scratch what already exists as a battle-tested library. Use standard solutions; invest creativity in your actual problem domain.
- **Interview Note**: "Golden Hammer" and "Over-engineering" are the most common anti-patterns at senior+ level. The discipline to *not* use a pattern is as valuable as knowing when to use one.

---

### Leadership & Engineering Principles (Staff+)

- **Think in Systems** → See the whole, not just parts. Understand feedback loops, emergent behavior, and second-order effects. Local optimization can degrade global system performance.
- **Optimize for Outcomes, Not Output** → Shipping features is output. User adoption, reduced latency, zero incidents = outcomes. Measure what actually matters.
- **Bias for Action** → Make reversible decisions quickly; take more time on irreversible ones. Paralysis is more dangerous than imperfect action in most engineering contexts.
- **Ownership** → Act as if you built it, you maintain it, and you are on call for it. End-to-end accountability from design to production health.
- **Long-term Thinking** → Every shortcut has a carrying cost. Technical debt is real interest. Make trade-offs explicitly and document them. Don't let urgency override architecture.
- **Trade-off Transparency** → Surface trade-offs explicitly in design docs and reviews. "We chose X over Y because of Z constraint." Hiding trade-offs creates surprises later.
- **Simplicity at Scale** → The hardest engineering skill is making complex systems simple. The best systems are the ones that can be understood, debugged, and extended by anyone on the team.
- **Build for Operability** → Every system should be easy to deploy, monitor, debug, and roll back. Operability is a feature. Runbooks, dashboards, alerts are first-class deliverables.
- **Measure What Matters** → Instrument based on what drives user value and business outcomes. Vanity metrics (requests/sec in isolation) vs meaningful metrics (P99 latency, error budget burn).
- **Interview Note**: At Staff+ level, the question shifts from "how do you build this?" to "how do you decide *what* to build, *when* to build it, and *how* to align the team around it?"

---

### Interview Power Keywords — Principles Edition

| Category | Power Keywords |
|---|---|
| **Trade-offs** | CAP theorem, ACID vs BASE, normalization vs denormalization, sync vs async, consistency vs availability |
| **Constraints-driven design** | SLO → architecture decisions, budget → infra choices, team size → module boundaries |
| **Evolutionary Architecture** | Fitness functions, architecture decision records (ADRs), incremental migration, strangler fig pattern |
| **Backward Compatibility** | Additive schema changes, API versioning, consumer-driven contracts, deprecation cycles |
| **Incremental Delivery** | Feature flags, canary deploys, dark launches, trunk-based development, experiment infrastructure |
| **Cost vs Performance Balance** | Right-size infra, spot instances, tiered storage, caching to reduce DB load, batch over real-time |
| **Risk Mitigation** | Defense in depth, circuit breakers, chaos engineering, runbooks, blameless post-mortems |
---

## 73. Assorted Patterns Master Reference (NEW)

> **Coverage:** 160+ patterns across Creational, Structural, Behavioral, Concurrency, Architectural, Enterprise, Microservices, Functional, UI/Presentation, Data Access, Testing, and Game/Systems categories. Each pattern includes intent, structure, use case, and interview note.

---

### Creational Patterns

- **Abstract Factory** → Creates families of related objects without specifying concrete classes. `GUIFactory` produces `Button` + `Checkbox` — Windows vs Mac variants. Use when system must be independent of how its objects are created. *Interview*: "Factory Method makes one product; Abstract Factory makes a family."
- **Builder** → Separates construction of a complex object from its representation. Step-by-step: `new Builder().setHost().setPort().build()`. Handles optional parameters cleanly. *Interview*: "Builder vs telescoping constructors — Builder wins when >3 optional params."
- **Factory** → Generic term for any method that returns an object without exposing creation logic. Encapsulates `new`. Static factory methods (`Optional.of()`, `List.of()`).
- **Factory Kit** → A configurable factory using a map of builders. Register creators at startup; retrieve by key. Avoids subclassing for each variant. *Interview*: "Plugin-style factory — open/closed without changing core."
- **Factory Method** → Define interface for creating object; let subclasses decide which class to instantiate. `Creator.createProduct()` deferred to `ConcreteCreator`. Promotes extension without modification.
- **Multiton** → Controlled instances per key: `getInstance(key)`. Registry of named singletons. Thread pools per queue name, logger per class. *Interview*: "Multiton = parameterized Singleton."
- **Monostate** → All instances share the same state via static fields. Looks like distinct objects; behaves like singleton. Hard to test — use sparingly.
- **Object Pool** → Reuse expensive objects (DB connections, threads, parsers). `pool.acquire()` → use → `pool.release()`. HikariCP for JDBC. *Interview*: "Pool avoids GC pressure and initialization overhead."
- **Prototype** → Clone existing object instead of creating from scratch. `Object.clone()` or copy constructor. Useful when creation is expensive. Shallow vs deep copy distinction matters.
- **Singleton** → One instance per JVM. Enum-based is simplest and safest (thread-safe, serialization-safe). Double-checked locking needs `volatile`. *Interview*: "Why enum Singleton? — JVM guarantees single instance; immune to reflection attacks and serialization."
- **Step Builder** → Builder that enforces creation order at compile time via interfaces. Each step returns next step's interface. Prevents partial construction. *Interview*: "Fluent API with compile-time state enforcement."
- **Registry** → Centralized store for looking up objects by name/key. `ServiceRegistry.lookup("userService")`. Spring `ApplicationContext` is a registry.

---

### Structural Patterns

- **Adapter** → Convert interface of a class into interface clients expect. Wraps incompatible object. Object adapter (composition — preferred) vs class adapter (inheritance). *Interview*: "Adapter = translator between two incompatible interfaces."
- **Bridge** → Decouple abstraction from implementation so both can vary independently. `Shape` (abstraction) + `Renderer` (implementation). Avoids Cartesian product of subclasses. *Interview*: "Bridge = composition over inheritance for two orthogonal dimensions."
- **Composite** → Treat individual objects and compositions uniformly. Tree structure: `Component` implemented by `Leaf` and `Composite`. File system, UI component trees. *Interview*: "Composite lets clients ignore difference between single and group."
- **Composite Entity** → Coarse-grained entity enclosing multiple fine-grained objects. J2EE pattern. Reduces remote calls by grouping related data into one entity bean.
- **Composite View** → Assemble view from multiple sub-views. Template includes header, footer, content fragments. JSP include, Thymeleaf fragments, React component composition.
- **Decorator** → Wrap object to add behavior without modifying it. `BufferedInputStream(new FileInputStream(...))`. Stacks infinitely. Implements same interface as wrapped object. *Interview*: "Decorator adds responsibility at runtime; subclassing adds at compile time."
- **Delegation** → Object hands work to a helper object rather than inheriting it. Kotlin `by` keyword. Composition-based behavior sharing. More flexible than inheritance.
- **Dynamic Proxy** → Create proxy at runtime implementing given interfaces. Java `java.lang.reflect.Proxy`. Used by Spring AOP, Hibernate lazy loading, mock frameworks. *Interview*: "Dynamic proxy = runtime-generated Decorator for cross-cutting concerns."
- **Extension Objects** → Add new behaviors to an object without changing its class. `obj.getExtension(Printable.class)`. Eclipse plugin model. Open/Closed at object level.
- **Facade** → Unified interface to a complex subsystem. `OrderFacade.placeOrder()` hides inventory, payment, shipping services. Simplifies client code. *Interview*: "Facade reduces dependencies; Adapter makes incompatible interfaces work together."
- **Filterer** → Functional pattern for type-safe filtering on subtypes in a collection. Returns correctly typed filtered result. Avoids unchecked casts on heterogeneous collections.
- **Flyweight** → Share common state (intrinsic) between many fine-grained objects; extrinsic state passed by caller. String pool, glyph objects in text editor. `Integer.valueOf(-128 to 127)`. *Interview*: "Flyweight = cache of immutable shared objects to reduce memory."
- **Marker Interface** → Empty interface used as tag. `Serializable`, `Cloneable`. JVM/framework checks `instanceof`. Better replaced by annotations in modern Java. *Interview*: "Prefer annotations over marker interfaces — more flexible, no inheritance pollution."
- **Private Class Data** → Restrict access to class state by moving it to a separate immutable data class. Encapsulate what should not change after construction. Similar to making fields final.
- **Proxy** → Surrogate that controls access to another object. Virtual proxy (lazy init), Remote proxy (RMI/stub), Protection proxy (auth check), Caching proxy (memoize). *Interview*: "Proxy controls access; Decorator adds behavior."
- **Twin** → Simulate multiple inheritance in languages that do not support it. Two tightly coupled classes acting as one. Rarely needed in Java with interfaces + default methods.
- **Virtual Proxy** → Delays expensive object creation until first use. Image loaded only when drawn. ORM lazy-loaded collections. `LazyInitializer` in Hibernate.

---

### Behavioral Patterns

- **Acyclic Visitor** → Visitor variant using overloaded visit methods only on types that need visiting. Breaks cyclic dependency between Visitor and Element hierarchies. More flexible than classic Visitor.
- **Chain of Responsibility** → Pass request along chain of handlers until one handles it. `Handler.setNext(handler)`. Logging levels, middleware pipeline, Servlet filters. *Interview*: "Decouples sender from receiver; handler decides to process or pass on."
- **Command** → Encapsulate request as object. Supports undo/redo, queuing, logging. `execute()` / `undo()`. Remote controls, transaction logs, macro recording. *Interview*: "Command = action as object — enables queuing, logging, reversibility."
- **Commander** → Manages distributed transactions and failover using commands. Pairs with Command for reliable distributed execution with retry and recovery semantics.
- **Collecting Parameter** → Pass a collection into a method to accumulate results instead of returning them. Avoids creating intermediate lists. Useful when multiple methods build one result.
- **Context Object** → Encapsulate context/state shared across a pipeline or request scope. Avoid passing many parameters; use context carrier object. `HttpServletRequest` is an example.
- **Curiously Recurring Template Pattern (CRTP)** → `class Derived extends Base<Derived>`. Simulates static polymorphism. Common in C++; rare in Java but used for fluent builder hierarchies.
- **Double Dispatch** → Method behavior depends on runtime type of two objects. Visitor pattern is the canonical implementation. Workaround for Java single dispatch.
- **Execute Around** → Pair of actions wrapping arbitrary code: setup -> execute -> teardown. Try-with-resources, `TransactionTemplate.execute()`, `JdbcTemplate`. *Interview*: "Execute Around = template for resource lifecycle."
- **Interpreter** → Define grammar + interpreter for a language. AST nodes implement `interpret()`. SQL parsers, regex engines, expression evaluators. *Interview*: "Interpreter pattern = DSL in code. Expensive for complex grammars — use parser generators instead."
- **Iterator** → Sequential access to elements without exposing underlying structure. Java `Iterator<T>` / `Iterable<T>` / enhanced for-loop. External (caller controls) vs internal (collection controls).
- **Mediator** → Central hub coordinating interactions between objects. Objects do not reference each other directly. Chat room, air traffic control, event bus. *Interview*: "Mediator reduces N x N coupling to N x 1."
- **Memento** → Capture and externalize object state without violating encapsulation. Originator creates memento; Caretaker stores it. Undo/redo, game save states. *Interview*: "Memento = snapshot of object state, opaque to caretaker."
- **Null Object** → Default object with do-nothing behavior. Eliminates null checks. `NullLogger`, `NullIterator`. Return `Optional.empty()` or Null Object — never return raw null from API. *Interview*: "Null Object = remove conditional null checks; replace with polymorphism."
- **Observer** → One-to-many dependency: when subject changes state, all dependents notified. `EventListener`, `ReactiveStreams`, `@EventListener` in Spring. *Interview*: "Observer = pub-sub in process. Beware: memory leaks if listeners not deregistered."
- **Parameter Object** → Group related method parameters into a single object. Reduces parameter list length. `SearchCriteria` instead of 6 separate args. Improves readability and extensibility.
- **Property** → Store dynamic attributes on an object at runtime. `Map<String, Object>` of named properties. JavaScript-like flexibility in Java. Useful when schema is not fixed.
- **Role Object** → Attach role-specific behavior to an object without subclassing. `customer.getRole(VIPCustomer.class)`. Better than fat base class. Context-sensitive behavior.
- **Servant** → Class providing common functionality to a group of classes. Stateless helper passed objects to operate on. Avoids repeating methods across unrelated classes.
- **Specification** → Encapsulate business rule as predicate object. Composable: `spec1.and(spec2).not()`. `Predicate<T>` in Java 8 is the functional equivalent. *Interview*: "Specification = business rule as first-class object. Compose complex rules from simple ones."
- **State** → Object changes behavior when internal state changes. Appears to change class. Vending machine, TCP connection states, workflow engines. *Interview*: "State = replace conditional logic (if/switch) with polymorphism. Each state is a class."
- **Strategy** → Define family of algorithms; make them interchangeable. `Sorter` with `BubbleSortStrategy` / `QuickSortStrategy`. *Interview*: "Strategy = inject behavior. Change algorithm without changing context."
- **Template Method** → Skeleton algorithm in base class; subclasses fill in steps. `AbstractList`, `HttpServlet.doGet()`. Inversion of control at class level. *Interview*: "Template Method = Hollywood Principle in abstract class."
- **Type Object** → Represent categories of objects as objects rather than subclasses. `MonsterType` instead of `TrollClass`, `DragonClass`. Enables runtime type definition.
- **Visitor** → Add operations to object structure without modifying it. Visitor defines `visit(ConcreteElement)`. Element calls `visitor.visit(this)`. Requires knowing all element types. *Interview*: "Visitor = Open/Closed for new operations, Closed for new elements."

---

### Concurrency Patterns

- **Active Object** → Decouples method execution from invocation. Method calls enqueued; executed in separate thread. Returns `Future`. Combines Command + Scheduler + Proxy.
- **Actor Model** → Actors = lightweight concurrent entities. Communicate via immutable messages. No shared state. Akka (Java/Scala), Erlang. *Interview*: "Actor model eliminates shared-state concurrency bugs. Each actor processes one message at a time."
- **Async Method Invocation** → Non-blocking method call; result retrieved later via callback or Future. `CompletableFuture`, `@Async` in Spring. Improves throughput for I/O-bound work.
- **Balking** → If object is not in appropriate state, ignore/reject the request instead of waiting. `if (!initialized) return;`. Light switch already on — do nothing. Avoids blocking.
- **Double-Checked Locking** → Reduce locking overhead by checking condition twice: once without lock, once with. Field must be `volatile` to prevent instruction reordering. *Interview*: "Without `volatile`, double-checked locking is broken due to JMM reordering."
- **Event-Based Asynchronous** → Components communicate via events; caller does not block. `CompletableFuture`, RxJava, Spring Events. Decouples producer from consumer in time.
- **Guarded Suspension** → Thread waits until condition is true before proceeding. `while (!condition) wait();`. Blocking queue producer/consumer. Pair with Balking.
- **Half-Sync/Half-Async** → Synchronous layer handles I/O; async layer handles processing. Netty event loop (async) hands off to business thread pool (sync). Best of both worlds.
- **Leader Election** → Elect one node as coordinator among distributed peers. ZooKeeper, etcd (Raft). Avoids split-brain. Kafka controller, Elasticsearch master.
- **Leader-Followers** → Thread pool where one thread is leader, accepts I/O, then promotes a follower. High-performance server pattern. Reduces context switching vs thread-per-connection.
- **Lockable Object** → Explicit locking controlled by the object itself. `lock()` / `unlock()`. More flexible than `synchronized`. `ReentrantLock`, `StampedLock`.
- **Monitor** → Combines lock + condition variable. Java `synchronized` + `wait()/notify()`. Ensures mutual exclusion + cooperation. `java.util.concurrent.locks.Condition` is the explicit version.
- **Poison Pill** → Sentinel message signaling consumer to stop. `queue.put(POISON_PILL)`. Clean shutdown of producer-consumer pipelines. *Interview*: "Poison Pill = graceful termination signal through the queue."
- **Producer-Consumer** → Decouple producers from consumers via shared buffer/queue. `BlockingQueue` bridges rates. Backpressure when queue full. *Interview*: "Producer-Consumer = temporal decoupling. Queue absorbs burst; consumer processes at its rate."
- **Promise** → Represents result of async computation available in future. `CompletableFuture<T>` in Java. Chain with `thenApply`, `thenCompose`, `exceptionally`. Avoid blocking on `get()`.
- **Reactor** → Event-driven: single thread dispatches events to handlers. Netty, NIO Selector. High throughput with minimal threads. *Interview*: "Reactor = event loop. One thread handles many connections via non-blocking I/O."
- **Thread-Pool Executor** → Pool of reusable threads for task execution. `Executors.newFixedThreadPool(n)` / `ThreadPoolExecutor(core, max, keepAlive, queue)`. *Interview*: "Size: CPU-bound = cores+1; IO-bound = cores x (1 + wait/compute ratio)."

---

### Architectural Patterns

- **Clean Architecture** → Concentric rings: Entities -> Use Cases -> Interface Adapters -> Frameworks. Dependency rule: always points inward. Domain has zero external dependencies. *Interview*: "Clean Architecture = Dependency Inversion applied at architecture level."
- **CQRS (Command Query Responsibility Segregation)** → Separate write model (Commands) from read model (Queries). Different DBs, schemas, or services. Write: normalized; Read: denormalized/projected. *Interview*: "CQRS shines when read/write load or model differ significantly. Adds complexity — justify with scale."
- **Event Sourcing** → Store state as sequence of events, not current snapshot. Replay to rebuild state. Audit trail built-in. Kafka as event log. *Interview*: "Event Sourcing = immutable log as source of truth. Temporal queries and full audit are free."
- **Event-Driven Architecture** → Producers emit events; consumers react asynchronously. Kafka, RabbitMQ. Loose coupling across services. *Interview*: "EDA enables choreography (no central orchestrator) vs orchestration (Saga with central coordinator)."
- **Hexagonal Architecture (Ports & Adapters)** → Core domain surrounded by ports (interfaces) and adapters (implementations: REST, DB, MQ). Swap infrastructure without touching domain. *Interview*: "Hexagonal = testable domain. Test business logic without DB or HTTP."
- **Layered Architecture** → Horizontal layers: Presentation -> Business -> Persistence -> Database. Each layer only calls the one below. Violation: presentation calling persistence directly. *Interview*: "Layered = most common starting point. Risk: anemic domain if business logic leaks to service layer."
- **Microservices Aggregator** → Aggregator service calls multiple downstream microservices and combines results into one response. Reduces client chattiness. BFF (Backend for Frontend) is a specialized aggregator.
- **Microservices API Gateway** → Single entry point for all clients. Routes, aggregates, authenticates, rate-limits. Kong, AWS API Gateway, Spring Cloud Gateway. *Interview*: "API Gateway = reverse proxy + cross-cutting concerns. Avoid putting business logic here."
- **Microservices Client-Side UI Composition** → Frontend composes UI fragments from multiple microservices. Micro-frontends. Each team owns full stack including UI fragment.
- **Microservices Distributed Tracing** → Propagate `traceId` across service calls. Jaeger, Zipkin, OpenTelemetry. Reconstruct full request journey across services. *Interview*: "Without distributed tracing, debugging a 500ms latency spike across 10 services is impossible."
- **Microservices Idempotent Consumer** → Message consumer designed to safely process duplicate messages. Deduplicate via idempotency key stored in DB. Critical for at-least-once delivery. *Interview*: "Kafka at-least-once + idempotent consumer = effectively exactly-once processing."
- **Microservices Log Aggregation** → Centralize logs from all services. ELK, Datadog, Splunk. Correlate by `traceId`. Structured JSON logging required. *Interview*: "Log aggregation + distributed tracing + metrics = full observability triangle."
- **Microservices Self-Registration** → Service registers itself with discovery server on startup; deregisters on shutdown. Eureka, Consul. vs external registration (Kubernetes does this for you).
- **Monolithic Architecture** → Single deployable unit. Simpler to develop/test/deploy initially. Risk: tight coupling, scaling bottleneck, long build times. *Interview*: "Start monolith, extract microservices at pain points — not upfront."
- **Saga** → Distributed transaction via sequence of local transactions + compensating transactions on failure. Choreography (event-driven, decentralized) vs Orchestration (central Saga coordinator). *Interview*: "Saga = alternative to 2PC. Each step publishes event; failure triggers compensation."
- **Strangler** → Incrementally replace legacy system. New functionality in new system; legacy gradually strangled. Route traffic via facade. *Interview*: "Strangler Fig = safe migration. Never big-bang rewrite. Strangler facade hides which system handles request."

---

### Enterprise & Integration Patterns

- **Ambassador** → Helper service co-deployed with client to offload connectivity concerns: retry, circuit breaking, logging, auth. Sidecar for outbound calls. Envoy, Linkerd.
- **Anti-Corruption Layer** → Translate external model to internal domain model. Protect domain from legacy or third-party API pollution. Adapter + Facade at domain boundary.
- **Business Delegate** → Hides complexity of business service lookup and invocation from presentation layer. J2EE pattern. Decouples web tier from business tier.
- **Circuit Breaker** → Stop calling failing service. States: Closed (normal) -> Open (failing, fast-fail) -> Half-Open (probe recovery). Resilience4j, Hystrix. *Interview*: "Circuit Breaker = fail fast + recover gracefully. Prevents cascade failures."
- **Data Bus** → Shared communication channel for data exchange between components. Components publish/subscribe to typed data. Decouples producers from consumers.
- **Data Mapper** → Transfers data between objects and database while keeping them independent. ORM layer: Hibernate `SessionFactory`, JPA `EntityManager`. *Interview*: "Data Mapper = no active record coupling; domain objects do not know about DB."
- **Data Transfer Object (DTO)** → Plain object for transferring data between layers/services. No business logic. Avoid leaking domain/entity objects to API layer. *Interview*: "DTO = boundary object. Decouple API contract from domain model."
- **Domain Model** → Rich object model embodying behavior and data. Entities, Value Objects, Aggregates, Domain Services. Opposite of Anemic Domain Model (logic in services, not objects).
- **Event Aggregator** → Subscribe to many event sources; republish under unified stream. Reduces subscriber coupling. `EventBus` (Guava), Spring `ApplicationEventPublisher`.
- **Event Queue** → Decouple event producers from handlers via a queue. Async event dispatch. Game loop processes one event per frame. Bounded queue prevents memory overflow.
- **Feature Toggle** → Enable/disable features at runtime without redeployment. LaunchDarkly, Unleash, `@ConditionalOnProperty`. *Interview*: "Feature flags decouple deploy from release. Canary rollout, A/B testing, kill switch."
- **Gateway** → Encapsulate access to external system or resource. Single point of integration. Different from API Gateway: this is internal service-to-external boundary.
- **Identity Map** → Cache loaded objects by ID; return cached instance if already loaded. Prevents loading same DB row twice in a unit of work. Hibernate `SessionCache`.
- **Intercepting Filter** → Pre/post processing of requests in a chain. Servlet `Filter`, Spring `HandlerInterceptor`, gRPC interceptors. Logging, auth, rate limiting, compression.
- **Metadata Mapping** → Map metadata to object attributes. ORM annotations (`@Column`, `@Table`). Reflection-based mapping framework. Configuration-driven column mapping.
- **Naked Objects** → Domain objects directly exposed as UI. UI auto-generated from domain model. Rapid prototyping, admin interfaces.
- **Notification** → Collect multiple validation errors and return together rather than throwing on first error. `ValidationResult` with list of errors. *Interview*: "Notification pattern vs throwing exceptions — return all errors at once for better UX."
- **Page Controller** → One controller per page/URL. Handles HTTP request, coordinates model update, selects view. Servlet per page. Simple MVC variant.
- **Page Object** → Represent UI page as object in tests. `LoginPage.enterCredentials().submit()`. Selenium WebDriver pattern. Encapsulates UI selectors from test logic.
- **Partial Response** → Return only requested fields. `?fields=id,name,email`. GraphQL does this natively. Reduces payload size for mobile/low-bandwidth.
- **Repository** → Abstraction over data store. `UserRepository.findByEmail()`. Collection-like interface for domain objects. Spring Data `JpaRepository`. *Interview*: "Repository = domain-focused data access. DAO is more DB-focused. Repository deals with Aggregates."
- **Separated Interface** → Place interface in different package/module from its implementation. Dependency points to abstraction layer. Plugin architecture, Clean Architecture dependency rule.
- **Serialized Entity** → Persist entity by serializing object graph. Java serialization, JSON/XML. Tightly couples serialized format to class structure — version carefully.
- **Serialized LOB** → Store a complex object graph in a single DB column as serialized blob (JSON/XML/binary). Simple to implement; hard to query. *Interview*: "Use sparingly — querying inside blob is painful. Good for opaque config/preferences."
- **Service Layer** → Defines application boundary with set of available operations. Coordinates domain objects, transactions, security. `@Service` in Spring. *Interview*: "Service Layer = use cases. Thin orchestrator; business logic belongs in domain model."
- **Service Locator** → Central registry for locating services. `ServiceLocator.getService(OrderService.class)`. Anti-pattern for most cases — hides dependencies; prefer Dependency Injection.
- **Service Stub** → Fake implementation of external service for testing. `WireMock`, `MockServer`. Enables testing without real external dependency. *Interview*: "Service Stub = test double at network boundary."
- **Service to Worker** → Front Controller dispatches to Worker (controller) which uses Helpers, then selects View. Structural MVC pattern for server-side web.
- **Session Facade** → Remote facade providing coarse-grained API over fine-grained domain objects. J2EE EJB pattern. Reduces remote call chattiness. Similar to Facade but specifically for remote boundary.
- **Single Table Inheritance** → All subclass data in one table with discriminator column. Simple queries; nullable columns for subclass-specific data. JPA `@Inheritance(strategy=SINGLE_TABLE)`.
- **Table Inheritance** → General term for mapping class hierarchy to DB tables. Three strategies: Single Table, Joined Table, Table per Class. Each has query complexity vs storage trade-off.
- **Table Module** → One class per DB table handling all business logic for that table rows. Between Transaction Script and Domain Model complexity. Like a DAO with behavior.
- **Template View** → View is a template with placeholders filled at render time. JSP, Thymeleaf, Freemarker. Server-side rendering.
- **Transaction Script** → Organize business logic as sequential procedure scripts per use case. Simple CRUD apps. Becomes unmanageable as complexity grows. *Interview*: "Transaction Script -> Domain Model as complexity grows. Know when to make the transition."
- **Unit of Work** → Tracks objects changed in a business transaction; commits all changes at once. Hibernate `Session`, JPA `EntityManager`. Batches DB operations. *Interview*: "Unit of Work = commit once at end. Prevents partial updates and reduces DB round trips."
- **Value Object** → Immutable object defined by its attributes, not identity. `Money(100, USD) == Money(100, USD)`. No `id`. Records in Java 16+. *Interview*: "Value Object = equality by value. Entity = equality by identity (id)."
- **Version Number** → Optimistic locking via version column. `@Version` in JPA. Increment on update; reject stale update if version mismatch. *Interview*: "Version Number = optimistic concurrency without pessimistic locks."
- **View Helper** → Helper class used by view to format/process data for display. Avoids logic in templates. `DateFormatter`, `CurrencyHelper`. Keeps views clean.

---

### Data Access Patterns

- **DAO Factory** → Factory producing DAO implementations per data store type. `DAOFactory.getDAO(DAOFactory.MYSQL)`. Enables switching persistence technology without changing business logic.
- **Data Access Object (DAO)** → Abstract and encapsulate all access to data source. `UserDAO.findById()`, `UserDAO.save()`. Works with any persistence technology. More generic than Repository. *Interview*: "DAO = data-layer interface. Repository = domain-layer interface over aggregates."
- **Optimistic Offline Lock** → Handle concurrent edits by detecting conflicts at commit time. Version column checked; reject if changed. Used in long-running business transactions spanning multiple requests.
- **Dirty Flag** → Track whether object has been modified since last save. Hibernate dirty checking. Only save changed objects — avoids unnecessary DB writes.
- **Lazy Loading** → Defer loading of related data until first access. JPA `@OneToMany(fetch=LAZY)`. Virtual Proxy, Value Holder, Ghost implementations. *Interview*: "Lazy loading causes N+1 if not planned. Use `JOIN FETCH` or `@EntityGraph` for bulk loads."
- **MapReduce** → Split large dataset computation into Map (transform per record) + Reduce (aggregate). Hadoop, Spark. Parallelized across nodes. *Interview*: "MapReduce = embarrassingly parallel bulk data processing. Not for OLTP."

---

### Functional Patterns

- **Callback** → Pass function to be called on completion. `CompletableFuture.thenApply()`, `onClick(handler)`. Inversion of control for async notification.
- **Collection Pipeline** → Chain of transformations on collections. `list.stream().filter().map().collect()`. Declarative, readable, lazy. *Interview*: "Pipeline = functional composition on sequences."
- **Combinator** → Higher-order function that combines functions or structures without external variables. `Predicate.and()`, `Function.compose()`. Functional design pattern.
- **Currying** → Transform function of N args into chain of N single-arg functions. `f(a,b,c)` -> `f(a)(b)(c)`. Partial application. Java: simulate via lambda returning lambda.
- **Fluent Interface** → Method chaining for readable DSL. `builder.setName().setAge().build()`. `Stream`, `Optional`, jOOQ. Return `this` or next step.
- **Function Composition** → Combine two functions into one: `g(f(x))`. `Function.andThen()`, `Function.compose()`. Build complex transformations from simple ones.
- **Monad** → Design pattern for chaining operations on wrapped values while handling effects (null, error, async). `Optional` (null monad), `CompletableFuture` (async monad), `Stream` (list monad). `flatMap` is the monadic bind. *Interview*: "Optional is a monad — `flatMap` chains nullable operations without explicit null checks."
- **Pipeline** → Series of processing stages where output of one is input of next. `Stream`, Unix pipes, Kafka Streams topology. Each stage is independent and composable.
- **Trampoline** → Technique to implement tail-recursive algorithms iteratively. Return function instead of calling it; loop calls returned functions. Prevents stack overflow for deep recursion.

---

### Resilience & Scalability Patterns

- **Backpressure** → Mechanism for slow consumer to signal slow producer. Reactive Streams `Subscription.request(n)`. Prevents buffer overflow and OOM. *Interview*: "Backpressure = flow control across async boundary. Pull-based model gives consumer control."
- **Caching** → Store results of expensive operations for reuse. L1 (in-process: Caffeine), L2 (distributed: Redis), L3 (CDN). Cache-aside vs read-through vs write-behind. *Interview*: "Cache invalidation is hardest. TTL + event-driven invalidation. Never cache unbounded data."
- **Fan-Out/Fan-In** → Fan-Out: split work across parallel tasks. Fan-In: aggregate results. `CompletableFuture.allOf()`. `StructuredTaskScope` (Java 21). Parallel aggregation pattern.
- **Health Check** → Endpoint reporting service liveness and readiness. `/actuator/health`. Kubernetes `livenessProbe`/`readinessProbe`. Deep health checks DB, cache, external APIs.
- **Queue-Based Load Leveling** → Queue absorbs traffic spikes; consumer processes at steady rate. Decouples burst producers from capacity-limited consumers. SQS, RabbitMQ, Kafka.
- **Rate Limiting** → Control request rate to protect service. Token bucket (bursty allowed), Leaky bucket (smooth), Fixed window, Sliding window. Redis + Lua script for distributed rate limiting. *Interview*: "Token bucket = bursts allowed up to bucket size. Leaky bucket = steady output rate regardless of input."
- **Retry** → Re-attempt failed operations. Exponential backoff + jitter prevents thundering herd. Max retries + dead letter queue for poison messages. Resilience4j `Retry`. *Interview*: "Retry must be idempotent. Non-idempotent retries = duplicate side effects."
- **Sharding** → Horizontal partition of data across nodes. Consistent hashing for even distribution. Each shard handles subset of keys. *Interview*: "Shard key design is everything — avoid hotspots, enable range queries where needed."
- **Throttling** → Limit resource consumption per client/tenant. Request throttling (rate limit) vs resource throttling (CPU, memory). 429 Too Many Requests. Token bucket per API key.

---

### UI & Presentation Patterns

- **Bloc** → Business Logic Component. Flutter pattern. Stream-based: events in, states out. UI rebuilds on state change. Separates UI from business logic.
- **Flux** → Unidirectional data flow. Action -> Dispatcher -> Store -> View -> Action. React ecosystem. Redux is the most popular Flux implementation.
- **Front Controller** → Single controller handles all requests; delegates to specific handlers. `DispatcherServlet` in Spring MVC. Centralizes cross-cutting concerns (auth, logging).
- **Model-View-Controller (MVC)** → Separate Model (data), View (UI), Controller (input handling). Spring MVC. Classic web pattern. Risk: fat controller or fat model antipatterns.
- **Model-View-Intent (MVI)** → Unidirectional: Intent (user action) -> Model (state) -> View (render). Popular in Android, Kotlin. Predictable state management.
- **Model-View-Presenter (MVP)** → Presenter mediates between View (passive) and Model. View has no logic. Presenter testable without UI. Android pre-MVVM.
- **Model-View-ViewModel (MVVM)** → ViewModel exposes observable state; View binds and reacts. Data binding. Angular, WPF, SwiftUI, Jetpack Compose. *Interview*: "MVVM = two-way binding. ViewModel survives config changes; survives View recreation."
- **Presentation Model** → ViewModel for view-specific state. Abstracts view state from domain model. Pre-cursor to MVVM.

---

### Testing Patterns

- **Arrange/Act/Assert (AAA)** → Structure unit tests in three phases: Arrange (setup), Act (invoke), Assert (verify). Improves readability. *Interview*: "AAA = standard test structure. Given/When/Then (BDD) maps directly to Arrange/Act/Assert."
- **Object Mother** → Factory for creating test fixtures. `UserMother.validUser()`, `OrderMother.pendingOrder()`. Centralizes test data creation. Reduces duplication across tests.
- **Service Stub** → Replace real service with controlled fake for isolation. WireMock, MockServer. Enables testing without real external dependency.
- **Page Object** → Encapsulate UI selectors in test objects. `LoginPage.enterCredentials().submit()`. Separates test logic from UI structure.

---

### Game & Systems Patterns

- **Bytecode** → Encode behavior as instructions for a virtual machine. Scripting in game engines. Custom bytecode interpreter for modding/sandboxing. Alternative to complex interpreter trees.
- **Data Locality** → Arrange data in memory for cache efficiency. Arrays of Structs (AoS) vs Structs of Arrays (SoA). Cache-friendly access patterns. Entity-Component-System (ECS) uses SoA.
- **Double Buffer** → Two buffers: one being rendered/read, one being updated/written. Swap atomically. Prevents tearing artifacts. Graphics rendering, audio output.
- **Game Loop** → Core loop: `processInput()` -> `update()` -> `render()`. Fixed timestep vs variable timestep. Foundation of all real-time interactive applications.
- **Spatial Partition** → Organize objects in space for efficient querying: Quadtree (2D), Octree (3D), BSP tree, Grid. Collision detection, rendering frustum culling, proximity queries.
- **Subclass Sandbox** → Base class provides set of protected operations; subclasses implement behavior using only those operations. Limits subclass coupling to rest of codebase.
- **Update Method** → Each game object has `update(deltaTime)` called each frame. Objects self-contained. Separation of simulation from rendering loop.

---

### Miscellaneous Patterns

- **Abstract Document** → Dynamic property management with type safety. Objects implement `Document` interface; properties stored in map. Flexible schema without fixed class hierarchy.
- **Client Session** → Session state stored entirely client-side (JWT, cookie). Server stateless. Scales horizontally. Revocation is hard. *Interview*: "Client session = stateless server. JWT carries claims. Revocation requires token blacklist or short TTL."
- **Converter** → Bidirectional transformation between domain model and DTO/view model. `UserConverter.toDTO(user)` / `toEntity(dto)`. MapStruct generates at compile time.
- **Dependency Injection** → Provide dependencies from outside the class. Constructor injection preferred (immutable, testable). Framework (Spring, Guice) manages wiring. *Interview*: "DI = explicit dependencies. Makes classes testable in isolation — inject mocks."
- **Money** → Value object for monetary amounts. Pair of `(amount: BigDecimal, currency: Currency)`. Never use `double` for money. JSR-354 `MonetaryAmount`. *Interview*: "Money pattern prevents float precision bugs. Always BigDecimal + Currency."
- **Mute Idiom** → Suppress checked exceptions that can never actually occur, wrapping in `RuntimeException`. Use when API forces checked exception you cannot handle. `try { ... } catch (Exception e) { throw new RuntimeException(e); }`
- **Object Mother** → (see Testing) Centralized test fixture factory.
- **Publish-Subscribe** → Publishers emit events to topic; all subscribers receive. Decouples by topic. Kafka topics, JMS topics, Spring `@EventListener`. vs Observer (direct reference) vs Message Queue (point-to-point). *Interview*: "Pub-Sub = topic-based broadcast. Observer = direct object notification. Queue = point-to-point."
- **RAII (Resource Acquisition Is Initialization)** → Resources acquired in constructor, released in destructor. C++ idiom. Java equivalent: try-with-resources (`AutoCloseable`). *Interview*: "Java try-with-resources is RAII — `close()` guaranteed even on exception."
- **Server Session** → Session state held server-side. Sticky sessions or distributed session store (Redis). Stateful; harder to scale horizontally than client sessions.
- **Tolerant Reader** → Consumer ignores unknown fields in messages/responses. Enables backward-compatible schema evolution. JSON consumers should ignore extra fields. *Interview*: "Tolerant Reader = forward-compatible integration. Do not fail on unknown fields."

---

### Pattern Groupings Quick Reference

| Category | Key Patterns |
|---|---|
| **Creational** | Singleton, Factory Method, Abstract Factory, Builder, Prototype, Object Pool, Registry, Step Builder |
| **Structural** | Adapter, Decorator, Proxy, Facade, Composite, Bridge, Flyweight, Delegation, Dynamic Proxy |
| **Behavioral** | Strategy, Observer, Command, State, Template Method, Iterator, Chain of Responsibility, Visitor, Mediator, Memento, Null Object, Specification |
| **Concurrency** | Actor Model, Producer-Consumer, Thread Pool, Circuit Breaker, Reactor, Saga, Monitor, Active Object, Promise, Poison Pill |
| **Architectural** | Layered, Hexagonal, Clean Architecture, CQRS, Event Sourcing, Monolith, Microservices, Saga, Strangler |
| **Data Access** | Repository, DAO, Unit of Work, Identity Map, Data Mapper, Lazy Loading, Dirty Flag, Version Number |
| **Enterprise** | Service Layer, Facade, Gateway, Ambassador, Anti-Corruption Layer, Strangler, Feature Toggle, Session Facade |
| **Functional** | Monad, Pipeline, Combinator, Currying, Function Composition, Fluent Interface, Trampoline, Callback |
| **Resilience** | Circuit Breaker, Retry, Bulkhead, Backpressure, Rate Limiting, Queue-Based Load Leveling, Throttling |
| **UI** | MVC, MVVM, MVP, MVI, Flux, Front Controller, Bloc |
| **Testing** | AAA, Object Mother, Page Object, Service Stub |
| **Game/Systems** | Game Loop, Update Method, Double Buffer, Spatial Partition, Data Locality, Bytecode, Subclass Sandbox |

---

### Interview Power Keywords — Patterns Edition

| Context | Answer |
|---|---|
| **Strategy vs State** | Strategy: interchangeable algorithms chosen by client. State: behavior changes as internal state changes — object drives the switch. |
| **Decorator vs Proxy** | Decorator adds behavior (same interface). Proxy controls access (same interface). Intent differs — behavior vs access control. |
| **Repository vs DAO** | Repository: domain-centric, works with Aggregates, collection-like. DAO: DB-centric, table-per-DAO, more generic. |
| **Saga vs 2PC** | 2PC: synchronous, blocking, strong consistency. Saga: async, eventual consistency, compensating transactions on failure. |
| **Event Sourcing vs CRUD** | CRUD: current state only. Event Sourcing: full history as events, state derived by replay. Audit trail and temporal queries are free. |
| **Singleton pitfalls** | Global state = hard to test. Classloader scope in app servers. Use enum form. Consider DI container singletons instead of hand-rolled. |
| **Command pattern benefits** | Decouples invoker from receiver. Supports undo/redo, queuing, logging, macro recording. |
| **CQRS trade-off** | Separate read/write models = eventual consistency between them. Justifiable when read/write loads or models differ significantly. Adds operational complexity. |
| **Observer memory leak** | Listener registered but never deregistered. Listener holds reference to dead object. Fix: weak references or explicit deregister on shutdown. |
| **Facade vs Mediator** | Facade: simplifies external access to subsystem (unidirectional). Mediator: coordinates communication between peers (bidirectional). |
