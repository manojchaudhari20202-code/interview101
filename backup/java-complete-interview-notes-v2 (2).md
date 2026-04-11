# Java Complete Interview Reference — Full Edition

> **All topics merged:** Original source file (Java Concurrency · Java Collections · Java IO/NIO) + all remaining Java topics
> Every section includes subtopics, keywords, and interview notes.

---

## TABLE OF CONTENTS
- 1. Java OOP
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
- 13. Java Version Features (Java 8-24)
- 14. Java Records
- 15. Java Sealed Classes
- 16. Java Pattern Matching
- 17. Java Switch Expressions
- 18. Java var & Type Inference
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
- 32. Java Internals & Advanced
- 33. Java Interview Master Keywords

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

## 13. Java Version Features (Java 8–24)

### Java 8 (LTS) — Foundation of Modern Java
Lambda, Stream API, Optional, default/static interface methods, method references, `java.util.function`, `java.time`, `CompletableFuture`, Base64 API, parallel array sort.

### Java 9
JPMS modules, JShell REPL, `List/Set/Map.of()` immutable factories, private interface methods, Flow API (Reactive Streams), `Stream.takeWhile/dropWhile/iterate`, `Optional.stream/ifPresentOrElse`, HTTP/2 client incubator, G1 default GC.

### Java 10
`var` local type inference, `toUnmodifiableList/Set/Map()`, `List/Set/Map.copyOf()`.

### Java 11 (LTS)
`var` in lambda params, String `isBlank/strip/lines/repeat`, `Files.readString/writeString`, HTTP Client stable, launch single-file `java Hello.java`, `Optional.isEmpty()`, ZGC+Epsilon experimental, Java EE/CORBA modules removed.

### Java 12–13
Switch expressions preview (arrow syntax, no fall-through), `String.indent/transform`, Text Blocks preview.

### Java 14
Records preview, `instanceof` pattern matching preview, Helpful NullPointerException messages, Switch expressions stable.

### Java 15
Text Blocks stable, Sealed Classes preview, Hidden Classes, ZGC+Shenandoah production-ready.

### Java 16
Records stable, `instanceof` pattern matching stable, `Stream.toList()`, Unix-domain sockets.

### Java 17 (LTS)
Sealed Classes stable, Pattern matching for switch preview, Strong JDK encapsulation enforced, Enhanced RandomGenerator API, Foreign Function & Memory API incubator.

### Java 18
UTF-8 default charset, `jwebserver` simple web server, `@snippet` in Javadoc, `finalize()` deprecated for removal.

### Java 19–20
Virtual Threads preview, Structured Concurrency preview, Record Patterns preview, FFM API preview.

### Java 21 (LTS) — Major Milestone
- **Virtual Threads stable** → `Thread.ofVirtual().start(...)`.
- **Sequenced Collections** → `SequencedCollection/Set/Map`: `getFirst/getLast/addFirst/addLast/reversed()`.
- **Pattern matching for switch stable** → `case Integer i when i > 0 ->`.
- **Record Patterns stable** → `case Point(int x, int y) ->` deconstruct in patterns.
- Structured Concurrency preview, Scoped Values preview, String Templates preview.
- **Keywords**: Virtual threads = paradigm shift for IO-heavy apps; millions of threads possible.

### Java 22–24
- `_` unnamed variables/patterns stable (Java 22): `catch (Exception _)`, `for (var _ : list)`.
- Foreign Function & Memory API stable (Java 22).
- Stream Gatherers preview→stable (Java 24): `Stream.gather(Gatherer)` for custom intermediate ops.
- Class-File API stable (Java 24): parse/generate/transform `.class` files (standard ASM replacement).
- Unnamed classes + instance main preview: `void main() { ... }` without class declaration.
- **Keywords**: Java 25 = next LTS (2025); Valhalla (value types) and Amber (language features) ongoing.

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

*End of DSA Interview Notes — covers all topics from Core Concepts through Real-World Mapping*
