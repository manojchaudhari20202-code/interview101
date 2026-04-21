
# Java Best Practices — Quick Reference

---

## 1. Code Style & Naming Conventions

- **Classes**: PascalCase (`CustomerOrder`, `PaymentService`)
- **Methods/Variables**: camelCase (`calculateTotal`, `orderCount`)
- **Constants**: UPPER_SNAKE_CASE (`MAX_RETRY_COUNT`)
- **Packages**: lowercase, reverse domain (`com.company.module`)
- Keep methods short — single responsibility, ideally < 30 lines
- One class per file; class name must match filename

---

## 2. OOP Principles

- **SOLID**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- Favor **composition over inheritance**
- Program to **interfaces**, not implementations
- Use **encapsulation** — keep fields private, expose via getters/setters only when needed
- Avoid deep inheritance hierarchies (> 2–3 levels is a warning sign)

---

## 3. Clean Code Practices

- **Fail fast** — validate inputs early
- Avoid magic numbers/strings → use named constants or enums
- **DRY** (Don't Repeat Yourself) — extract common logic
- **YAGNI** — don't add functionality until needed
- Avoid `null` returns → use `Optional<T>` (Java 8+)
- Prefer **immutable objects** where possible (`final` fields, no setters)

---

## 4. Exception Handling

- Use **checked exceptions** for recoverable conditions, **unchecked** for programming errors
- Never swallow exceptions silently (`catch (Exception e) {}`)
- Always log the exception with context
- Clean up resources with **try-with-resources** (implements `AutoCloseable`)
- Don't use exceptions for flow control
- Create custom exceptions for domain-specific errors

```java
// Good
try (InputStream is = new FileInputStream(file)) {
    // use stream
} catch (IOException e) {
    log.error("Failed to read file: {}", file.getName(), e);
    throw new FileProcessingException("Cannot process file", e);
}
```

---

## 5. Collections & Generics

### Core Guidelines
- Use **generics** to ensure type safety — avoid raw types
- Prefer `List`, `Set`, `Map` interfaces over concrete types in declarations
- Use `Collections.unmodifiableList()` / `List.of()` for immutable collections
- Use `EnumSet`/`EnumMap` when keys are enums
- Choose the right collection: `ArrayList` (random access), `LinkedList` (frequent insert/delete), `HashMap` (fast lookup), `TreeMap` (sorted)
- Use `isEmpty()` not `size() == 0`

### List Implementations
| Implementation | When to Use | Time Complexity |
|---|---|---|
| `ArrayList` | Random access, frequent reads | O(1) get, O(n) add/remove |
| `LinkedList` | Frequent insert/delete at ends | O(n) get, O(1) add/remove ends |
| `Vector` | Legacy thread-safe (avoid) | Similar to ArrayList + sync |
| `CopyOnWriteArrayList` | Read-heavy, rare writes | O(n) write, snapshot reads |

### Set Implementations
| Implementation | When to Use | Ordering | Null Allowed |
|---|---|---|---|
| `HashSet` | Fast unique elements, no order needed | Unordered | One null |
| `LinkedHashSet` | Unique + insertion order | Insertion order | One null |
| `TreeSet` | Unique + sorted order | Natural/Comparator | No null |
| `EnumSet` | Enum constants only | Declaration order | No null |

### Map Implementations
| Implementation | When to Use | Ordering | Thread-Safe |
|---|---|---|---|
| `HashMap` | General purpose, fast lookup | Unordered | No |
| `LinkedHashMap` | Insertion order + LRU cache | Insertion order | No |
| `TreeMap` | Sorted keys, range queries | Sorted | No |
| `ConcurrentHashMap` | High concurrency | Unordered | Yes |
| `EnumMap` | Enum keys | Declaration order | No |
| `WeakHashMap` | Cache with GC-friendly keys | Unordered | No |

### Queue & Deque Implementations
| Implementation | When to Use | Bounded | Thread-Safe |
|---|---|---|---|
| `ArrayDeque` | Stack/queue, fast ends | No | No |
| `LinkedList` | Queue operations needed | No | No |
| `PriorityQueue` | Priority ordering, heap | No | No |
| `ArrayBlockingQueue` | Bounded producer-consumer | Yes | Yes |
| `LinkedBlockingQueue` | Unbounded producer-consumer | Optional | Yes |
| `ConcurrentLinkedQueue` | Non-blocking concurrent | No | Yes |

### Collection Performance Tips
- **ArrayList**: Pre-size with `new ArrayList<>(expectedSize)` to avoid resizing
- **HashMap**: Use initial capacity `= (int) (expectedSize / 0.75f) + 1` to avoid rehashing
- **StringBuilder**: Use for string concatenation in loops, not `+`
- **Arrays vs Lists**: Use `Arrays.asList()` for fixed-size views, `new ArrayList<>(Arrays.asList())` for modifiable
- **Iteration**: Enhanced for-loop or streams preferred over `Iterator` unless removing elements

### Collection Utility Methods
```java
// Immutable collections (Java 9+)
List<String> immutable = List.of("a", "b", "c");
Set<Integer> immutableSet = Set.of(1, 2, 3);
Map<String, Integer> immutableMap = Map.of("key1", 1, "key2", 2);

// Collections class utilities
Collections.emptyList() / singletonList(item) / unmodifiableList(list)
Collections.emptySet() / singleton(item) / unmodifiableSet(set)
Collections.emptyMap() / singletonMap(k, v) / unmodifiableMap(map)

// Common operations
Collections.sort(list) / reverse(list) / shuffle(list)
Collections.binarySearch(list, key) // requires sorted list
Collections.max(collection) / min(collection)
Collections.frequency(collection, element)
Collections.disjoint(c1, c2) // true if no common elements
```

### Generics Best Practices
- Use diamond operator: `Map<String, List<Integer>> map = new HashMap<>()`
- Use bounded type parameters: `<T extends Comparable<T>>`
- PECS principle: Producer Extends, Consumer Super
- Avoid raw types: `List list = new ArrayList()` → `List<String> list = new ArrayList<>()`
- Use `? extends T` for read-only, `? super T` for write-only parameters
- Consider `Collections.checkedList()` for runtime type safety in critical code

---

## 6. Concurrency

- Prefer **`java.util.concurrent`** classes over raw `synchronized`
- Use `ExecutorService` / `ThreadPoolExecutor` instead of creating raw threads
- Prefer **`ConcurrentHashMap`** over `HashMap` in multithreaded code
- Use **`volatile`** for visibility; use **`AtomicInteger`** etc. for atomic ops
- Avoid shared mutable state — prefer immutability or thread-local storage
- Use `CompletableFuture` for async pipelines (Java 8+)
- Always shut down `ExecutorService` in `finally` or use try-with-resources

---

## 7. Java 8+ Modern Idioms

- Use **Streams API** for collection processing (filter/map/reduce)
- Use **lambdas** and **method references** to reduce boilerplate
- Use **`Optional`** to make nullability explicit in APIs
- Use **`LocalDate`/`LocalDateTime`** (not `Date`/`Calendar`)
- Use **`var`** (Java 10+) for local type inference when type is obvious
- Prefer **records** (Java 16+) for simple data carriers over POJOs
- Use **sealed classes** (Java 17+) for closed type hierarchies

---

## 8. Performance

- Avoid unnecessary object creation in loops
- Use **`StringBuilder`** for string concatenation in loops, not `+`
- Cache expensive computations — don't recompute in loops
- Use primitive types (`int`, `long`) over boxed types (`Integer`, `Long`) in hot paths
- Be careful with **autoboxing/unboxing** in performance-sensitive code
- Use **lazy initialization** where appropriate
- Profile before optimizing — don't guess bottlenecks

---

## 9. Security

- Never log sensitive data (passwords, tokens, PII)
- Use **`PreparedStatement`** — never concatenate SQL strings (SQL Injection)
- Validate and sanitize all external inputs
- Use `SecureRandom` not `Random` for security-sensitive randomness
- Avoid deserializing untrusted data (Java deserialization vulnerabilities)
- Use HTTPS; don't disable SSL certificate validation
- Store passwords with strong hashing (`bcrypt`, `PBKDF2`) not `MD5`/`SHA1`

---

## 10. Testing

- Follow **AAA**: Arrange → Act → Assert
- Write **unit tests** (JUnit 5), **integration tests**, and **contract tests**
- Aim for meaningful coverage — test behavior, not implementation
- Use **Mockito** for mocking dependencies
- Test edge cases: null inputs, empty collections, boundary values
- Keep tests **independent** — no shared mutable state between tests
- Use **`@ParameterizedTest`** for data-driven tests

---

## 11. Dependency Management & Build

- Use **Maven** or **Gradle**; never commit JAR dependencies to source control
- Pin dependency versions; use a BOM (Bill of Materials) for related libs
- Keep dependencies minimal — every dependency is a liability
- Regularly update dependencies (security patches)
- Use **multi-module** builds for large projects

---

## 12. Static Code Analysis Tools

### Checkstyle
- Enforces **coding style** and formatting rules
- Catches: naming violations, missing Javadoc, line length, import order
- Config: `checkstyle.xml` (Google/Sun style guides available)
- IDE plugins available for real-time feedback

### PMD
- Detects **code defects and bad practices**
- Catches: unused variables, empty catch blocks, unnecessary object creation, God classes, dead code
- Rules organized in rulesets (Best Practices, Code Style, Design, Error Prone, Performance)

### SpotBugs (successor to FindBugs)
- Detects **bug patterns** via bytecode analysis
- Catches: null dereferences, infinite loops, incorrect `equals()`/`hashCode()`, resource leaks, thread safety issues
- More powerful than PMD for actual bugs (works on bytecode)

### SonarQube / SonarLint
- Comprehensive **quality gate** tool (bugs, vulnerabilities, code smells, coverage, duplications)
- SonarLint: IDE plugin for real-time analysis
- SonarQube: CI/CD server with dashboards and history
- Tracks **technical debt** and enforces quality gates on PRs
- Covers OWASP Top 10 security rules

### Error Prone (Google)
- Compile-time **bug detection** integrated into `javac`
- Catches: common mistakes that compile fine but are logically wrong
- Examples: `@Nullable` misuse, incorrect `equals` calls, misused `assertEquals` arg order

### NullAway
- Detects **NullPointerException** risks at compile time
- Works with `@Nullable`/`@NonNull` annotations
- Lighter weight than full type systems like Checker Framework

### Checker Framework
- Pluggable **type-checking** system at compile time
- Supports: Nullness, Tainting, Regex, Units, Lock checkers
- More thorough than NullAway but heavier to set up

### ArchUnit
- Tests **architectural constraints** as unit tests
- Examples: "controllers must not access repositories directly", "no circular dependencies"
- Integrates with JUnit 5

---

## 13. Static Analysis in CI/CD Pipeline

```
Code Push
  → Compile (Error Prone / NullAway)
  → Unit Tests
  → Checkstyle (style gate)
  → PMD + SpotBugs (defect gate)
  → SonarQube (quality gate — coverage, smells, security)
  → Integration Tests
  → Deploy
```

**Recommended minimal setup:**
| Tool | Purpose | When |
|---|---|---|
| Checkstyle | Style consistency | Pre-commit / CI |
| SpotBugs | Bug patterns | CI |
| SonarLint | Real-time feedback | IDE |
| SonarQube | Full quality gate | CI/CD server |

---

## 14. Common Anti-Patterns to Avoid

| Anti-Pattern | Problem |
|---|---|
| God Class | Does too much — hard to test/maintain |
| Anemic Domain Model | Domain objects with no behavior (just getters/setters) |
| Service Locator | Hides dependencies — prefer DI |
| Double-Checked Locking (old-style) | Broken without `volatile` before Java 5 |
| Catching `Throwable`/`Error` | Swallows JVM errors (`OutOfMemoryError`) |
| `finalize()` method | Deprecated, unpredictable GC behavior |
| `static` mutable state | Makes testing and concurrency hard |
| Returning `null` from collections | Return empty collection instead |

---

## 15. Logging Best Practices

- Use **SLF4J** with Logback or Log4j2 (never `System.out.println`)
- Use **parameterized messages** — `log.debug("User {} logged in", userId)` (not string concat)
- Log at appropriate levels: `ERROR` (failures), `WARN` (unexpected but handled), `INFO` (key events), `DEBUG` (development detail)
- Never log passwords, tokens, or PII
- Include correlation IDs for distributed tracing (MDC)

---

## 16. Code Review Checklist

- [ ] No raw types or unchecked casts
- [ ] Resources closed properly (try-with-resources)
- [ ] No NPE risk (`Optional`, null checks, `@NonNull`)
- [ ] Thread safety considered for shared state
- [ ] No hardcoded credentials or sensitive data
- [ ] Adequate test coverage for new logic
- [ ] No unused imports/variables (static analysis clean)
- [ ] Exception handling is meaningful, not swallowed
- [ ] SQL uses parameterized queries
- [ ] Equals/hashCode consistent and overridden together

---

## 17. Java Type System & Primitives

### Primitives vs Wrappers
| Primitive | Wrapper | Size |
|---|---|---|
| `byte` | `Byte` | 8-bit |
| `short` | `Short` | 16-bit |
| `int` | `Integer` | 32-bit |
| `long` | `Long` | 64-bit |
| `float` | `Float` | 32-bit IEEE 754 |
| `double` | `Double` | 64-bit IEEE 754 |
| `char` | `Character` | 16-bit Unicode |
| `boolean` | `Boolean` | true/false |

- Integer cache: `Integer.valueOf(-128 to 127)` returns cached instances — `==` works in that range, use `.equals()` always
- `float`/`double` are imprecise — use `BigDecimal` for money/financial calculations
- Widening: `byte → short → int → long → float → double` (automatic)
- Narrowing: requires explicit cast; may lose data

### Strings
- `String` is **immutable** and interned — string literals share pool
- `==` compares references; `.equals()` compares content
- `String.intern()` forces pool lookup — rarely needed
- `StringBuilder` (non-thread-safe) vs `StringBuffer` (thread-safe, slower)
- Key methods: `charAt`, `substring`, `indexOf`, `split`, `trim`, `strip` (Unicode-aware, Java 11+), `isBlank` (Java 11+), `repeat` (Java 11+), `formatted` (Java 15+)
- `String.format()` / `formatted()` for templating; `String.join()` for joining collections

```java
String result = String.join(", ", List.of("a", "b", "c")); // "a, b, c"
String s = "Hello %s".formatted("World");
```

---

## 18. java.lang — Core Classes

### Object (root of all classes)
- `equals(Object o)` — logical equality; always override with `hashCode`
- `hashCode()` — must be equal when `equals` is true; consistent within a run
- `toString()` — override for meaningful debug output
- `clone()` — prefer copy constructors over `Cloneable`
- `getClass()` — runtime class; `instanceof` for type check (Java 16+: pattern matching)
- `wait()` / `notify()` / `notifyAll()` — low-level monitor ops (prefer `java.util.concurrent`)

### Math
```java
Math.abs(-5)          // 5
Math.max(3, 7)        // 7
Math.pow(2, 10)       // 1024.0
Math.sqrt(16)         // 4.0
Math.floor / ceil / round
Math.random()         // [0.0, 1.0) — use Random/SecureRandom instead
Math.PI, Math.E
```

### System
```java
System.currentTimeMillis()   // epoch ms — use Instant.now() instead
System.nanoTime()            // relative nanoseconds (for timing only)
System.arraycopy(src, si, dst, di, len)  // fast array copy
System.exit(0)               // terminate JVM — avoid in libraries
System.getenv("PATH")        // environment variables
System.getProperty("user.home")  // JVM system properties
```

### Autoboxing / Unboxing Pitfalls
```java
Integer a = null;
int b = a;  // NullPointerException — unboxing null
Long sum = 0L;
for (int i = 0; i < 1000; i++) sum += i;  // 1000 autobox operations — use long
```

---

## 19. Collections Framework (java.util)

### Hierarchy
```
Iterable
  └── Collection
        ├── List       → ArrayList, LinkedList, Vector, Stack, CopyOnWriteArrayList
        ├── Set        → HashSet, LinkedHashSet, TreeSet, CopyOnWriteArraySet
        │    └── SortedSet → NavigableSet → TreeSet
        └── Queue      → LinkedList, PriorityQueue, ArrayDeque
              └── Deque → ArrayDeque, LinkedList
Map (separate hierarchy)
  → HashMap, LinkedHashMap, TreeMap, Hashtable, ConcurrentHashMap, EnumMap, WeakHashMap
```

### Choosing the Right Collection
| Need | Use |
|---|---|
| Ordered, index access | `ArrayList` |
| Frequent head/tail insert | `ArrayDeque` |
| Unique elements, fast lookup | `HashSet` |
| Unique + insertion order | `LinkedHashSet` |
| Unique + sorted | `TreeSet` (implements `NavigableSet`) |
| Key-value, fast lookup | `HashMap` |
| Key-value + insertion order | `LinkedHashMap` |
| Key-value + sorted keys | `TreeMap` |
| Priority ordering | `PriorityQueue` (min-heap by default) |
| Thread-safe map | `ConcurrentHashMap` |
| Enum keys | `EnumMap` |

### Key Utility Methods (`Collections` class)
```java
Collections.sort(list)             // natural order (Comparable)
Collections.sort(list, comparator) // custom order
Collections.reverse(list)
Collections.shuffle(list)
Collections.min(coll) / max(coll)
Collections.frequency(coll, obj)
Collections.unmodifiableList(list) // read-only view
Collections.singletonList(item)    // immutable single-element list
Collections.nCopies(5, "x")        // [x, x, x, x, x]
Collections.disjoint(c1, c2)       // true if no common elements
```

### Arrays Utility
```java
Arrays.sort(arr)
Arrays.binarySearch(arr, key)      // array must be sorted
Arrays.fill(arr, value)
Arrays.copyOf(arr, newLength)
Arrays.copyOfRange(arr, from, to)
Arrays.equals(a, b)                // deep: Arrays.deepEquals
Arrays.asList(1, 2, 3)             // fixed-size List backed by array
Arrays.stream(arr)                 // convert to Stream
```

---

## 20. Streams API (java.util.stream)

### Pipeline: Source → Intermediate Ops → Terminal Op
```java
list.stream()
    .filter(x -> x > 0)          // intermediate (lazy)
    .map(x -> x * 2)             // intermediate
    .sorted()                    // intermediate
    .limit(10)                   // intermediate
    .collect(Collectors.toList()) // terminal (eager, triggers execution)
```

### Intermediate Operations
| Op | Description |
|---|---|
| `filter(Predicate)` | Keep matching elements |
| `map(Function)` | Transform each element |
| `flatMap(Function)` | Flatten nested streams |
| `distinct()` | Remove duplicates |
| `sorted()` / `sorted(Comparator)` | Sort elements |
| `peek(Consumer)` | Debug/side-effect without changing stream |
| `limit(n)` | Take first n |
| `skip(n)` | Skip first n |
| `takeWhile(Predicate)` | Java 9+ — take while true |
| `dropWhile(Predicate)` | Java 9+ — drop while true |

### Terminal Operations
| Op | Returns |
|---|---|
| `collect(Collector)` | Collection/Map/String |
| `forEach(Consumer)` | void |
| `count()` | `long` |
| `findFirst()` / `findAny()` | `Optional<T>` |
| `anyMatch` / `allMatch` / `noneMatch` | `boolean` |
| `min(Comparator)` / `max(Comparator)` | `Optional<T>` |
| `reduce(identity, BinaryOp)` | single value |
| `toArray()` | `Object[]` |

### Key Collectors
```java
Collectors.toList()
Collectors.toSet()
Collectors.toUnmodifiableList()          // Java 10+
Collectors.toMap(keyFn, valueFn)
Collectors.groupingBy(classifier)        // Map<K, List<V>>
Collectors.partitioningBy(predicate)     // Map<Boolean, List<V>>
Collectors.joining(", ", "[", "]")       // string concatenation
Collectors.counting()
Collectors.summingInt(fn)
Collectors.averagingInt(fn)
Collectors.toUnmodifiableMap(k, v)
```

### Parallel Streams
```java
list.parallelStream().filter(...).collect(...);
// Good for: CPU-bound, large datasets, stateless ops
// Bad for: I/O-bound, small datasets, ordered/stateful ops, shared mutable state
```

---

## 21. Functional Interfaces (java.util.function)

| Interface | Method | Use |
|---|---|---|
| `Predicate<T>` | `test(T) → boolean` | Filter/condition |
| `Function<T,R>` | `apply(T) → R` | Transform |
| `BiFunction<T,U,R>` | `apply(T,U) → R` | Two-arg transform |
| `Consumer<T>` | `accept(T) → void` | Side effect |
| `BiConsumer<T,U>` | `accept(T,U) → void` | Two-arg side effect |
| `Supplier<T>` | `get() → T` | Factory/lazy value |
| `UnaryOperator<T>` | `apply(T) → T` | Same-type transform |
| `BinaryOperator<T>` | `apply(T,T) → T` | Combine two same-type |
| `Comparator<T>` | `compare(T,T) → int` | Ordering |

### Composing Functions
```java
Predicate<String> notEmpty = s -> !s.isEmpty();
Predicate<String> notNull  = Objects::nonNull;
Predicate<String> valid    = notNull.and(notEmpty);
Predicate<String> either   = notNull.or(notEmpty);
Predicate<String> isEmpty  = notEmpty.negate();

Function<Integer, Integer> times2 = x -> x * 2;
Function<Integer, Integer> plus3  = x -> x + 3;
Function<Integer, Integer> both   = times2.andThen(plus3); // (x*2)+3
Function<Integer, Integer> bothR  = times2.compose(plus3); // (x+3)*2
```

---

## 22. Optional (java.util.Optional)

```java
Optional<String> opt = Optional.of("hello");         // throws NPE if null
Optional<String> safe = Optional.ofNullable(maybeNull); // safe
Optional<String> empty = Optional.empty();

opt.isPresent()                    // true
opt.isEmpty()                      // Java 11+
opt.get()                          // throws NoSuchElementException if empty — avoid
opt.orElse("default")              // value or default
opt.orElseGet(() -> compute())     // lazy default
opt.orElseThrow(IllegalStateEx::new)
opt.ifPresent(System.out::println)
opt.map(String::toUpperCase)       // transform if present
opt.flatMap(s -> findByName(s))    // avoids Optional<Optional<T>>
opt.filter(s -> s.length() > 3)
opt.ifPresentOrElse(v -> use(v), () -> handleEmpty()); // Java 9+
opt.or(() -> Optional.of("fallback"))  // Java 9+
```

- Never use `Optional` as method parameter or field — only as return type
- Never wrap collections in `Optional` — return empty collection instead

---

## 23. Date & Time API (java.time — Java 8+)

### Key Classes
| Class | Represents |
|---|---|
| `LocalDate` | Date only (no time, no zone) — `2024-01-15` |
| `LocalTime` | Time only — `10:30:00` |
| `LocalDateTime` | Date + time, no zone |
| `ZonedDateTime` | Date + time + zone — use for cross-timezone |
| `Instant` | Machine timestamp (UTC epoch) — use for storage/logging |
| `Duration` | Amount of time in seconds/nanos |
| `Period` | Amount of time in years/months/days |
| `ZoneId` | Timezone identifier (`"America/New_York"`) |
| `DateTimeFormatter` | Formatting/parsing |

### Common Operations
```java
LocalDate today = LocalDate.now();
LocalDate birthday = LocalDate.of(1990, Month.JUNE, 15);
LocalDate nextWeek = today.plusWeeks(1);
long daysBetween = ChronoUnit.DAYS.between(birthday, today);
boolean isLeap = today.isLeapYear();

ZonedDateTime now = ZonedDateTime.now(ZoneId.of("UTC"));
Instant timestamp = Instant.now();

DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = today.format(fmt);
LocalDate parsed = LocalDate.parse("15-06-1990", fmt);

// Convert legacy Date ↔ Instant
Date legacyDate = Date.from(instant);
Instant fromLegacy = legacyDate.toInstant();
```

---

## 24. I/O & NIO.2 (java.io / java.nio)

### Classic java.io
```java
// Reading text
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) { ... }
}

// Writing text
try (PrintWriter pw = new PrintWriter(new FileWriter("out.txt"))) {
    pw.println("Hello");
}

// Binary streams: FileInputStream / FileOutputStream + BufferedInputStream/BufferedOutputStream
// Always buffer! Raw streams are slow
```

### Modern java.nio.file (NIO.2 — Java 7+)
```java
Path path = Path.of("data/file.txt");         // Java 11+; Paths.get() older

// Read/write entire file
String content = Files.readString(path);           // Java 11+
List<String> lines = Files.readAllLines(path);
Files.writeString(path, "content");               // Java 11+
Files.write(path, bytes);

// Copy / Move / Delete
Files.copy(src, dst, StandardCopyOption.REPLACE_EXISTING);
Files.move(src, dst, StandardCopyOption.ATOMIC_MOVE);
Files.delete(path);                               // throws if missing
Files.deleteIfExists(path);

// Directory operations
Files.createDirectories(path);
Files.exists(path) / Files.isDirectory(path) / Files.isRegularFile(path)

// Walk directory tree
Files.walk(startPath)
     .filter(Files::isRegularFile)
     .filter(p -> p.toString().endsWith(".java"))
     .forEach(System.out::println);

// Streaming lines (memory-efficient for large files)
try (Stream<String> lines = Files.lines(path)) {
    lines.filter(l -> l.contains("ERROR")).forEach(log::error);
}
```

### Serialization
- Implement `Serializable` (marker interface) to enable default serialization
- Define `serialVersionUID` to control version compatibility
- Use `transient` for fields to exclude from serialization
- Prefer JSON/Protocol Buffers/Avro over Java serialization for external data — native serialization has security risks

---

## 25. Reflection (java.lang.reflect)

```java
Class<?> clazz = Class.forName("com.example.MyClass");
Class<?> clazz2 = obj.getClass();
Class<?> clazz3 = MyClass.class;        // preferred — compile-time safe

// Inspect
clazz.getDeclaredFields()               // all fields (including private)
clazz.getMethods()                      // public methods (including inherited)
clazz.getDeclaredMethods()              // all methods declared in this class
clazz.getConstructors()

// Invoke
Method m = clazz.getDeclaredMethod("myMethod", String.class);
m.setAccessible(true);                  // bypass access checks
Object result = m.invoke(instance, "arg");

// Create instance
Constructor<?> ctor = clazz.getDeclaredConstructor();
Object obj = ctor.newInstance();
```

- Reflection breaks encapsulation — use only when necessary (frameworks, DI, serialization)
- Slow compared to direct calls — avoid in hot paths
- Modules (Java 9+): deep reflection requires `--add-opens` or `opens` in `module-info.java`

---

## 26. Generics Deep Dive

### Wildcards
```java
List<? extends Number> upper = new ArrayList<Integer>(); // read-only (PECS Producer)
List<? super Integer>  lower = new ArrayList<Number>();  // write-only (PECS Consumer)

// PECS: Producer Extends, Consumer Super
public <T> void copy(List<? extends T> src, List<? super T> dst) { ... }
```

### Type Erasure
- Generic type info is erased at runtime — `List<String>` becomes `List` at bytecode level
- Cannot do `new T()`, `T[]`, or `instanceof List<String>` — use `Class<T>` token instead
- `@SuppressWarnings("unchecked")` suppresses erasure warnings — document why

### Bounded Type Parameters
```java
<T extends Comparable<T>>          // T must implement Comparable
<T extends Serializable & Cloneable> // multiple bounds (class first, then interfaces)
```

---

## 27. Enums (java.lang.Enum)

```java
public enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS  (4.869e+24, 6.0518e6);

    private final double mass;
    private final double radius;

    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    public double surfaceGravity() {
        return G * mass / (radius * radius);
    }
}

Planet.MERCURY.name()       // "MERCURY"
Planet.MERCURY.ordinal()    // 0
Planet.valueOf("VENUS")     // Planet.VENUS
Planet.values()             // all values
EnumSet.allOf(Planet.class) // efficient set of all enum constants
EnumMap<Planet, String> map = new EnumMap<>(Planet.class);
```

- Enums are singleton instances — safe for `==` comparison
- Can implement interfaces but cannot extend classes (already extends `Enum`)
- Use `switch` expressions (Java 14+) with enums for exhaustive pattern matching

---

## 28. Nested & Inner Classes

| Type | Declaration | Has outer `this`? | When to use |
|---|---|---|---|
| Static nested class | `static class Foo` inside outer | No | Logically grouped, no outer access needed |
| Inner class | `class Foo` inside outer | Yes | Tightly coupled to outer instance |
| Local class | class inside a method | Yes | Rare — one-time use in a method |
| Anonymous class | `new Interface() {...}` | Yes | Short one-off implementations (prefer lambdas) |

- Static nested classes are preferred — no hidden reference to outer instance (avoids memory leaks)
- Inner class instances hold implicit reference to outer — be careful with long-lived inner objects

---

## 29. Interfaces & Abstract Classes

### Interface (Java 8+)
```java
interface Shape {
    double area();                           // abstract (implicit public abstract)
    default String describe() {              // default — can override
        return "Shape with area " + area();
    }
    static Shape circle(double r) {          // static factory method
        return () -> Math.PI * r * r;
    }
    private double helper() { ... }         // Java 9+ private helper
}
```

- All fields are `public static final` (constants)
- A class can implement multiple interfaces
- Use interfaces to define contracts; default methods for optional behavior

### Abstract Class vs Interface
| | Abstract Class | Interface |
|---|---|---|
| Constructor | Yes | No |
| State (fields) | Yes (any access) | Only `public static final` |
| Multiple inheritance | No | Yes (multiple) |
| Use when | Shared state/code | Contract/capability |

---

## 30. Lambda & Method References

### Method Reference Types
```java
// Static method
Function<String, Integer> parse = Integer::parseInt;

// Instance method of a particular object
Runnable r = System.out::println;       // bound — specific instance

// Instance method of an arbitrary object of the type
Function<String, String> upper = String::toUpperCase; // unbound

// Constructor
Supplier<ArrayList<String>> factory = ArrayList::new;
```

### Effectively Final
- Lambdas can only capture **effectively final** local variables (value never changes after init)
- Lambdas capture `this` (outer instance) implicitly — be aware in serialization/memory

---

## 31. Concurrency Deep Dive (java.util.concurrent)

### Executors
```java
ExecutorService pool = Executors.newFixedThreadPool(4);
ExecutorService cached = Executors.newCachedThreadPool();       // unbounded — careful
ScheduledExecutorService sched = Executors.newScheduledThreadPool(2);

// Preferred: configure ThreadPoolExecutor directly
ExecutorService tpe = new ThreadPoolExecutor(
    4, 8,                            // core, max pool size
    60L, TimeUnit.SECONDS,           // keep-alive for idle threads
    new LinkedBlockingQueue<>(100),  // bounded task queue
    new ThreadPoolExecutor.CallerRunsPolicy() // rejection policy
);
```

### Future & CompletableFuture
```java
Future<Integer> f = pool.submit(() -> compute());
Integer result = f.get(5, TimeUnit.SECONDS);  // blocking with timeout

// CompletableFuture — non-blocking composition
CompletableFuture.supplyAsync(() -> fetchData(), pool)
    .thenApply(data -> transform(data))
    .thenCompose(data -> saveAsync(data))      // flatMap for async
    .thenAccept(result -> log(result))
    .exceptionally(ex -> handleError(ex))
    .whenComplete((res, ex) -> cleanup());

CompletableFuture.allOf(f1, f2, f3).join();   // wait for all
CompletableFuture.anyOf(f1, f2, f3).join();   // wait for first
```

### Synchronization Primitives
```java
ReentrantLock lock = new ReentrantLock();
lock.lock();
try { /* critical section */ } finally { lock.unlock(); }

// ReadWriteLock — multiple readers OR one writer
ReadWriteLock rwLock = new ReentrantReadWriteLock();
rwLock.readLock().lock() / rwLock.writeLock().lock();

// Semaphore — limit concurrent access
Semaphore sem = new Semaphore(3);   // 3 permits
sem.acquire(); try { ... } finally { sem.release(); }

// CountDownLatch — wait for N events
CountDownLatch latch = new CountDownLatch(3);
latch.countDown();     // in each worker
latch.await();         // blocks until count = 0

// CyclicBarrier — all threads rendezvous at a point
CyclicBarrier barrier = new CyclicBarrier(3, () -> log("All arrived"));
barrier.await();       // each thread waits; action runs when all arrive

// Phaser — flexible multi-phase barrier (Java 7+)
```

### Atomic Classes
```java
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet()
counter.compareAndSet(expected, update)  // CAS — basis of lock-free algorithms
AtomicReference<T>, AtomicLong, AtomicBoolean
LongAdder  // better than AtomicLong under high contention (Java 8+)
```

### Thread-Safe Collections
```java
ConcurrentHashMap<K,V>           // segmented locking — high concurrency
CopyOnWriteArrayList<E>          // read-heavy, rare writes
CopyOnWriteArraySet<E>
BlockingQueue<E>                 // producer-consumer: LinkedBlockingQueue, ArrayBlockingQueue
ConcurrentLinkedQueue<E>         // non-blocking FIFO
```

---

## 32. JVM Memory Model & Garbage Collection

### Memory Areas
- **Heap**: all object instances; divided into Young (Eden + Survivor) and Old (Tenured) generations
- **Stack**: per-thread; holds stack frames (local variables, operand stack)
- **Metaspace** (Java 8+): class metadata (replaced PermGen)
- **Code Cache**: JIT-compiled native code

### GC Algorithms
| GC | Use Case |
|---|---|
| **Serial GC** | Single-threaded, small heaps |
| **Parallel GC** | Throughput-focused, multi-core |
| **G1 GC** (default Java 9+) | Balanced latency/throughput, large heaps |
| **ZGC** (Java 15+ prod) | Ultra-low pause < 1ms, very large heaps |
| **Shenandoah** | Low-pause, similar to ZGC |

### GC Tuning Flags
```bash
-Xms512m -Xmx4g            # initial / max heap
-XX:+UseG1GC               # use G1
-XX:MaxGCPauseMillis=200    # G1 pause target
-XX:+UseZGC                # use ZGC (Java 15+)
-verbose:gc                 # GC logging
-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/dump.hprof
```

### Common Memory Leaks
- Static collections holding object references
- Unclosed streams/connections
- Inner class instances holding outer class reference
- Listeners/callbacks not deregistered
- `ThreadLocal` values not removed after use

---

## 33. Java Module System (JPMS — Java 9+)

```java
// module-info.java
module com.company.myapp {
    requires java.sql;                      // compile + runtime dependency
    requires transitive java.logging;       // re-exported to consumers
    requires static some.optional.lib;      // compile-only

    exports com.company.myapp.api;          // what others can use
    exports com.company.myapp.internal to com.company.other;  // restricted

    opens com.company.myapp.model;          // allows reflection (DI frameworks)
    opens com.company.myapp.model to jackson.databind; // selective

    provides com.spi.Service with com.company.impl.ServiceImpl;
    uses com.spi.Service;                   // ServiceLoader
}
```

- Modules enforce strong encapsulation at JVM level (not just `public`/`private`)
- `--add-opens` / `--add-exports` flags break encapsulation at runtime (legacy libs)
- Unnamed module: classpath code — can access named module exports but not opens

---

## 34. Design Patterns — Java Implementations

### Creational
```java
// Singleton (thread-safe — initialization-on-demand holder)
class Singleton {
    private static class Holder { static final Singleton INSTANCE = new Singleton(); }
    public static Singleton getInstance() { return Holder.INSTANCE; }
}

// Builder
User user = User.builder().name("Alice").age(30).email("a@b.com").build();

// Factory Method
Shape shape = ShapeFactory.create("CIRCLE");  // returns Circle instance

// Abstract Factory — creates families of related objects

// Prototype — clone() or copy constructor
```

### Structural
```java
// Decorator
InputStream is = new GZIPInputStream(new BufferedInputStream(new FileInputStream(f)));

// Proxy — JDK dynamic proxy or CGLIB
Object proxy = Proxy.newProxyInstance(loader, interfaces, handler);

// Adapter — wraps incompatible interface

// Composite — tree structures (UI components, file systems)

// Facade — simplify complex subsystem
```

### Behavioral
```java
// Strategy
sorter.sort(list, Comparator.comparing(Person::getAge));

// Observer / Listener
button.addActionListener(e -> handleClick());

// Command — encapsulate action as object (undo/redo)

// Template Method — abstract class defines skeleton, subclasses fill steps

// Chain of Responsibility — filter chains, middleware

// Iterator — for-each loop uses Iterator under the hood

// State — objects change behavior based on internal state
```

---

## 35. String Handling Deep Dive

```java
// String pool
String a = "hello";                // pool
String b = new String("hello");    // heap, NOT pool
a == b          // false
a.equals(b)     // true
b.intern() == a // true

// Comparison
"abc".compareTo("abd")             // negative (a < b lexicographically)
"abc".compareToIgnoreCase("ABC")   // 0
String.CASE_INSENSITIVE_ORDER      // Comparator for sorting

// Regex
"hello world".matches("hello.*")
"a1b2c3".replaceAll("[0-9]", "#")
String[] parts = "a,b,,c".split(",", -1);  // -1 keeps trailing empty strings
Pattern p = Pattern.compile("\\d+");       // compile once, reuse
Matcher m = p.matcher("abc123def456");
while (m.find()) { System.out.println(m.group()); }

// Java 15+ Text Blocks
String json = """
              {
                "name": "Alice",
                "age": 30
              }
              """;
```

---

## 36. Records, Sealed Classes & Pattern Matching (Java 16–21)

### Records (Java 16+)
```java
record Point(int x, int y) {}          // immutable data carrier
// auto-generates: constructor, accessors, equals, hashCode, toString

record Range(int lo, int hi) {
    Range {                            // compact canonical constructor
        if (lo > hi) throw new IllegalArgumentException();
    }
    int length() { return hi - lo; }  // custom method
}
```

### Sealed Classes (Java 17+)
```java
sealed interface Shape permits Circle, Rectangle, Triangle {}
record Circle(double radius) implements Shape {}
record Rectangle(double w, double h) implements Shape {}
final class Triangle implements Shape { ... }
```

### Pattern Matching
```java
// instanceof (Java 16+)
if (obj instanceof String s && s.length() > 5) { ... }

// switch expressions (Java 14+)
int result = switch (day) {
    case MONDAY, FRIDAY -> 6;
    case TUESDAY         -> 7;
    default              -> 8;
};

// switch with patterns (Java 21+)
String describe = switch (shape) {
    case Circle c    -> "Circle r=" + c.radius();
    case Rectangle r -> "Rect " + r.w() + "x" + r.h();
    case Triangle t  -> "Triangle";
};
```

---

## 37. Virtual Threads (Java 21 — Project Loom)

```java
// Create virtual thread
Thread vt = Thread.ofVirtual().start(() -> handleRequest());

// ExecutorService with virtual threads
try (ExecutorService ex = Executors.newVirtualThreadPerTaskExecutor()) {
    ex.submit(() -> processRequest());
}
```

- **Virtual threads** are lightweight (JVM-managed), not OS threads — can create millions
- Block on I/O without blocking OS thread — carrier thread is released and reused
- Ideal for **I/O-bound** workloads (HTTP, DB, file) — not for CPU-bound
- Do NOT pool virtual threads — create per task
- `synchronized` blocks pin virtual thread to carrier — prefer `ReentrantLock`
- Compatible with existing `java.util.concurrent` APIs

---

## 38. Networking (java.net)

```java
// HTTP Client (Java 11+) — replaces HttpURLConnection
HttpClient client = HttpClient.newBuilder()
    .connectTimeout(Duration.ofSeconds(10))
    .build();

HttpRequest req = HttpRequest.newBuilder()
    .uri(URI.create("https://api.example.com/data"))
    .header("Accept", "application/json")
    .GET()
    .build();

// Synchronous
HttpResponse<String> resp = client.send(req, BodyHandlers.ofString());
int status = resp.statusCode();
String body = resp.body();

// Asynchronous
client.sendAsync(req, BodyHandlers.ofString())
      .thenApply(HttpResponse::body)
      .thenAccept(System.out::println);

// POST with body
HttpRequest post = HttpRequest.newBuilder()
    .uri(uri)
    .header("Content-Type", "application/json")
    .POST(BodyPublishers.ofString(jsonBody))
    .build();
```

---

## 39. JDBC (java.sql)

```java
// Connection pool (e.g., HikariCP) — never create raw connections per request
DataSource ds = new HikariDataSource(config);

try (Connection con = ds.getConnection();
     PreparedStatement ps = con.prepareStatement(
         "SELECT * FROM users WHERE email = ? AND active = ?")) {

    ps.setString(1, email);
    ps.setBoolean(2, true);

    try (ResultSet rs = ps.executeQuery()) {
        while (rs.next()) {
            String name = rs.getString("name");
            int age = rs.getInt("age");
        }
    }
}

// Transactions
con.setAutoCommit(false);
try {
    // multiple statements
    con.commit();
} catch (SQLException e) {
    con.rollback();
    throw e;
}
```

- Always use **connection pools** (HikariCP, c3p0) — never `DriverManager.getConnection` in prod
- Close `Connection`, `Statement`, `ResultSet` in reverse order (or try-with-resources)
- Use `executeBatch()` for bulk inserts/updates

---

## 40. Java Memory & Reference Types

| Reference Type | Class | GC Behavior |
|---|---|---|
| Strong | Normal variable | Never collected while reachable |
| Soft | `SoftReference<T>` | Collected only when JVM needs memory — good for caches |
| Weak | `WeakReference<T>` | Collected at next GC — canonical maps (`WeakHashMap`) |
| Phantom | `PhantomReference<T>` | Post-finalization cleanup; always returns `null` on `get()` |

```java
WeakHashMap<Key, Value> cache = new WeakHashMap<>(); // entries GC'd when key unreachable
SoftReference<byte[]> buffer = new SoftReference<>(new byte[1024 * 1024]);
byte[] data = buffer.get(); // may be null if GC'd
if (data == null) data = loadData();
```

---

## 41. Collections & Data Structures — Best Practices

### Declaration: Always Use Interface Types
```java
// Good — program to the interface
List<String>   list = new ArrayList<>();
Set<String>    set  = new HashSet<>();
Map<String, Integer> map = new HashMap<>();
Deque<String>  deque = new ArrayDeque<>();

// Bad — locks you into implementation
ArrayList<String> list = new ArrayList<>();
```

---

### Choosing the Right List
| Scenario | Use | Reason |
|---|---|---|
| Random access by index | `ArrayList` | O(1) get |
| Frequent add/remove at head/tail | `ArrayDeque` | O(1) both ends; faster than LinkedList |
| Frequent insert/delete in middle | `LinkedList` | O(1) insert with iterator, but poor cache locality |
| Thread-safe, read-heavy | `CopyOnWriteArrayList` | Lock-free reads; full copy on write |
| Sorted, unique | `TreeSet` (not a List) | Maintained order, O(log n) ops |
| Fixed-size from array | `Arrays.asList()` | No add/remove; backed by array |
| True immutable | `List.of()` (Java 9+) | Throws on any mutation |

> **Prefer `ArrayDeque` over `LinkedList`** for stack/queue — better memory locality, no node overhead.

---

### Choosing the Right Map
| Scenario | Use | Note |
|---|---|---|
| General key-value | `HashMap` | O(1) avg; unordered |
| Preserve insertion order | `LinkedHashMap` | O(1); iteration order = insert order |
| Sorted by key | `TreeMap` | O(log n); implements `NavigableMap` |
| Enum keys | `EnumMap` | Array-backed; most efficient |
| Concurrent access | `ConcurrentHashMap` | Segment locking; never `Hashtable` |
| Count occurrences | `HashMap` + `merge` | See idiom below |
| Bidirectional lookup | Guava `BiMap` | Or maintain two maps manually |
| LRU cache | `LinkedHashMap` (access-order) | Override `removeEldestEntry` |

```java
// Count word frequency
Map<String, Integer> freq = new HashMap<>();
for (String word : words) {
    freq.merge(word, 1, Integer::sum);    // cleaner than getOrDefault
}

// LRU Cache using LinkedHashMap
Map<K, V> lru = new LinkedHashMap<>(capacity, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry<K,V> e) {
        return size() > capacity;
    }
};
```

---

### Choosing the Right Set
| Scenario | Use |
|---|---|
| Fast membership test | `HashSet` — O(1) |
| Maintain insertion order | `LinkedHashSet` |
| Sorted unique elements | `TreeSet` — O(log n), implements `NavigableSet` |
| Enum values | `EnumSet` — bitfield, ultra-fast |
| Thread-safe | `CopyOnWriteArraySet` (read-heavy) or `Collections.synchronizedSet` |

```java
// EnumSet — prefer over HashSet for enums
EnumSet<DayOfWeek> weekend = EnumSet.of(DayOfWeek.SATURDAY, DayOfWeek.SUNDAY);
EnumSet<DayOfWeek> weekdays = EnumSet.complementOf(weekend);
```

---

### Queue & Deque

```java
// Use ArrayDeque as Stack (not java.util.Stack which extends Vector)
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);          // addFirst
stack.pop();            // removeFirst
stack.peek();           // peekFirst

// Use ArrayDeque as Queue (not LinkedList)
Queue<String> queue = new ArrayDeque<>();
queue.offer("a");       // addLast
queue.poll();           // removeFirst — returns null if empty (vs remove() throws)
queue.peek();           // peekFirst

// PriorityQueue — min-heap by default
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
minHeap.offer(5); minHeap.offer(1); minHeap.offer(3);
minHeap.poll();   // 1 — always smallest

// Priority by custom field
PriorityQueue<Task> pq = new PriorityQueue<>(Comparator.comparingInt(Task::getPriority));
```

---

### Immutable & Unmodifiable Collections

```java
// Java 9+ — truly immutable (no nulls, no duplicates in Set)
List<String>        immList = List.of("a", "b", "c");
Set<String>         immSet  = Set.of("x", "y");
Map<String, Integer> immMap = Map.of("one", 1, "two", 2);
Map<String, Integer> immMap2 = Map.ofEntries(
    Map.entry("one", 1), Map.entry("two", 2)
);
List<String> copy = List.copyOf(existingList);  // defensive copy, immutable

// Unmodifiable view (wraps mutable — original can still change)
List<String> view = Collections.unmodifiableList(mutableList);

// Defensive copy pattern — expose immutable view of internal state
public List<String> getItems() {
    return List.copyOf(this.items);   // not Collections.unmodifiableList — that's a view
}
```

---

### Sorting & Ordering

```java
// Comparable — natural ordering (implement in the class)
class Employee implements Comparable<Employee> {
    public int compareTo(Employee o) {
        return Integer.compare(this.id, o.id);  // use Integer.compare, not subtraction
    }
}

// Comparator — external, multiple orderings
Comparator<Employee> byName   = Comparator.comparing(Employee::getName);
Comparator<Employee> byAge    = Comparator.comparingInt(Employee::getAge);
Comparator<Employee> combined = byName.thenComparingInt(Employee::getAge);
Comparator<Employee> reversed = byName.reversed();
Comparator<Employee> nullSafe = Comparator.nullsFirst(byName);

list.sort(combined);
list.sort(Comparator.comparing(Employee::getName, String.CASE_INSENSITIVE_ORDER));

// NEVER use subtraction in comparators — integer overflow bug
// Bad:  (a, b) -> a.age - b.age
// Good: Comparator.comparingInt(Employee::getAge)
```

---

### Map Iteration & Manipulation

```java
Map<String, Integer> map = new HashMap<>();

// Iterate entries
for (Map.Entry<String, Integer> e : map.entrySet()) {
    System.out.println(e.getKey() + "=" + e.getValue());
}
map.forEach((k, v) -> System.out.println(k + "=" + v));  // Java 8+

// Safe get with default
int val = map.getOrDefault("key", 0);

// Compute patterns (Java 8+)
map.putIfAbsent("key", 0);
map.computeIfAbsent("key", k -> new ArrayList<>());      // great for Map<K, List<V>>
map.computeIfPresent("key", (k, v) -> v + 1);
map.compute("key", (k, v) -> v == null ? 1 : v + 1);
map.merge("key", 1, Integer::sum);                       // most concise for counting
map.replaceAll((k, v) -> v * 2);

// Group into Map<K, List<V>>
Map<String, List<Employee>> byDept =
    employees.stream().collect(Collectors.groupingBy(Employee::getDepartment));
```

---

### Collection Operations & Algorithms

```java
// Set operations (non-destructive)
Set<String> union = new HashSet<>(setA);
union.addAll(setB);

Set<String> intersection = new HashSet<>(setA);
intersection.retainAll(setB);

Set<String> difference = new HashSet<>(setA);
difference.removeAll(setB);

// Bulk collection ops
list.removeIf(s -> s.isEmpty());            // in-place filter (Java 8+)
list.replaceAll(String::toUpperCase);       // in-place transform (Java 8+)

// Binary search (list must be sorted)
int idx = Collections.binarySearch(sortedList, target);
int idx2 = Collections.binarySearch(list, target, comparator);

// Frequency & disjoint
int count = Collections.frequency(list, "value");
boolean noCommon = Collections.disjoint(listA, listB);

// Min/Max
Optional<String> max = list.stream().max(Comparator.naturalOrder());
String min = Collections.min(list);
```

---

### equals() & hashCode() Contract

Critical for correct behavior in `HashMap`, `HashSet`, `Hashtable`:

1. If `a.equals(b)` → `a.hashCode() == b.hashCode()` (mandatory)
2. If `a.hashCode() == b.hashCode()` → `a.equals(b)` may be false (collision OK)
3. `hashCode()` must be **consistent** within a single run
4. `equals()` must be **reflexive, symmetric, transitive, consistent**, and handle `null`

```java
// Records auto-generate correct equals/hashCode based on all components
record Point(int x, int y) {}

// Manual (using Objects utility)
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof Employee e)) return false;
    return id == e.id && Objects.equals(name, e.name);
}

@Override
public int hashCode() {
    return Objects.hash(id, name);   // varargs — handles nulls
}
```

> Never use **mutable fields** in `hashCode` for objects stored in a `HashSet`/`HashMap` — mutating the key corrupts the bucket lookup.

---

### Common Collection Pitfalls

| Pitfall | Problem | Fix |
|---|---|---|
| `Arrays.asList()` then `add()`  | `UnsupportedOperationException` — fixed size | Use `new ArrayList<>(Arrays.asList(...))` |
| `List.of()` then `add()` | `UnsupportedOperationException` | It's immutable by design |
| Modifying list during for-each | `ConcurrentModificationException` | Use `removeIf()` or `Iterator.remove()` |
| `HashMap` in concurrent code | Data corruption / infinite loop (Java 7) | Use `ConcurrentHashMap` |
| `==` on Integer > 127 | `false` due to cache boundary | Always use `.equals()` |
| `LinkedList` random access | O(n) per get — slow | Use `ArrayList` or `ArrayDeque` |
| Subtraction in Comparator | Integer overflow | Use `Integer.compare()` |
| Null key in `TreeMap` | `NullPointerException` on compare | Use `HashMap` or null-safe Comparator |
| Storing mutable key in `HashSet` | Lost entry after mutation | Use immutable keys |
| Large `initial capacity` in `HashMap` | Wastes memory | Default 16 is fine unless size is known |

---

### Time & Space Complexity Reference

| Collection | get | add | remove | contains | Ordered |
|---|---|---|---|---|---|
| `ArrayList` | O(1) | O(1) amort. | O(n) | O(n) | Insertion |
| `LinkedList` | O(n) | O(1) ends | O(1) w/iter | O(n) | Insertion |
| `ArrayDeque` | O(1) ends | O(1) amort. | O(1) ends | O(n) | Insertion |
| `HashSet` | — | O(1) avg | O(1) avg | O(1) avg | No |
| `LinkedHashSet` | — | O(1) avg | O(1) avg | O(1) avg | Insertion |
| `TreeSet` | — | O(log n) | O(log n) | O(log n) | Sorted |
| `HashMap` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | No |
| `LinkedHashMap` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | Insertion |
| `TreeMap` | O(log n) | O(log n) | O(log n) | O(log n) | Sorted |
| `PriorityQueue` | O(n) | O(log n) | O(log n) | O(n) | Heap order |
