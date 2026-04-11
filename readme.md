## TOPICS
- [Java Collection](java.collection.md)
- [Java Streams](java.streams.md)
- [Java Concurrency](java.concrrency.md)
- [Java IO NIO](java.ionio.md)
- [Java DSA](java.dsa.md)
- [Java OOMD](java.oomd.md)
- [Java Patterns](java.patterns.md)
- [Java Principles](java.principles.md)


| Implementation | When to Use | Ordering | Thread-Safe |
|---|---|---|---|
| `HashMap` | General purpose, fast lookup | Unordered | No |
| `LinkedHashMap` | Insertion order + LRU cache | Insertion order | No |
| `TreeMap` | Sorted keys, range queries | Sorted | No |
| `ConcurrentHashMap` | High concurrency | Unordered | Yes |
| `EnumMap` | Enum keys | Declaration order | No |
| `WeakHashMap` | Cache with GC-friendly keys | Unordered | No |