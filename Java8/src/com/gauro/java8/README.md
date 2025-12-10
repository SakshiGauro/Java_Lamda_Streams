# Java 8 – Feature Summary

Java 8 introduced major enhancements that significantly improved the language's flexibility, performance, and functional capabilities.
Below is a concise, structured summary of the core features.

### 01. Default Methods in Interfaces

Interfaces can now contain **concrete implemented methods** using the `default` keyword.
This enables evolving interfaces without breaking old implementations.

### 02. Static Methods in Interfaces

Interfaces can also contain **static utility methods**, allowing reusable logic directly inside the interface.

### 03. Optional – Handling Nulls Safely

`Optional<T>` helps avoid `NullPointerException` by providing:
- Explicit null handling
- Methods such as `isPresent()`, `orElse()`, `orElseGet()`, `orElseThrow()`

### 04. Lambda Expressions (Λ)

Java 8 introduced **lambda syntax**, enabling functional-style programming:
- Cleaner code
- Compact inline implementations
- Core part of Streams and functional interfaces

### 05. Functional Interfaces

A **Functional Interface** has exactly one abstract method.

Examples: `Runnable`, `Comparator`, `Supplier`, `Function`, etc.
They enable lambda expressions and method references.

### 06. Method References

Shortcut syntax for lambdas that refer to:
- Static methods (`Class::method`)
- Instance methods (`obj::method`)
- Constructors (`Class::new`)

### 07. Constructor References

Creates new objects using `Class::new` instead of verbose lambda object creation.

### 08. Streams API

`java.util.stream` allows:
- Functional-style data processing
- Declarative operations (`map`, `filter`, `reduce`, etc.)
- Easy parallel processing

### 09. New Date & Time API (Joda-like)

`java.time` package introduced:

- Immutable date/time objects
- Classes like `LocalDate`, `LocalTime`, `Instant`, `Duration`, `Period`
- Thread-safe `DateTimeFormatter`

This was designed to replace flawed `java.util.Date` and `Calendar`.

### 10. CompletableFuture – Async & Non-blocking Programming

Introduced powerful abstractions for:
- Asynchronous tasks
- Non-blocking pipelines
- Functional-style callbacks (`thenApply`, `thenAccept`, `thenRun`)

### 11. Map Enhancements

New default methods inside `Map`:
- `forEach()`
- `getOrDefault()`
- `compute()`, `computeIfAbsent()`, `computeIfPresent()`
- `replace()`, `replaceAll()`
- Sorting helpers like `Entry.comparingByKey()`

### 12. Other Miscellaneous Updates

Several APIs received useful new methods:

**Collections**
- `List.replaceAll()`, `List.sort()`
- `Iterable.forEach()`, `Iterable.spliterator()`
- `Collection.removeIf()`
- Stream support: `stream()` & `parallelStream()`

**Comparator**
- `reversed()`, `thenComparing()`
- `naturalOrder()`, `reverseOrder()`
- `nullsFirst()`, `nullsLast()`

**Arrays**
- `setAll()`, `parallelSort()`, `parallelPrefix()`

**String**
- `String.join()`

**Math**
- Overflow-safe methods:

    `addExact()`, `subtractExact()`, `multiplyExact()`, `incrementExact()`, `decrementExact()`, `negateExact()`

**Number (Integer, Long, etc.)**
- `sum()`, `min()`, `max()`

**Boolean**
- `logicalAnd()`, `logicalOr()`, `logicalXor()`

**Objects**
- `isNull()`, `nonNull()`

---