# Summary of Java7 new features 

### 1. Try-With-Resources Statement
- JVM automatically closes resources after the `try` block by calling `close()`.
- Removes the need for manual `finally` blocks.

### 2. Suppressed Exceptions
- When multiple exceptions occur (e.g., in try-with-resources), secondary exceptions are stored in a suppressed list instead of being lost.

### 3. Catching Multiple Exceptions
- A single `catch` block can handle multiple exceptions using the `|` operator.

```java
catch (IOException | SQLException e) { ... }
```


### 4. Rethrowing Exceptions with Type Checking

- Java 7 enables more specific exception types to be declared in the `throws` clause when rethrowing exceptions.

### 5. Easier Exception Handling for Reflections

- Multiple reflection-related exceptions are replaced with a **single** common exception type, simplifying error handling.

### 6. Objects Class & Null Checks

- New `Objects` utility class.
- `Objects.requireNonNull()` helps validate null values clearly and safely.

### 7. URLClassLoader.close()

- A new `close()` method allows proper cleanup of resources to avoid memory leaks.

### 8. File & Directory Enhancements (NIO.2)

Introduced powerful new APIs:
- `Path`
- `Paths` 
- `Files`

These simplify file I/O, directory traversal, and metadata operations.

### 9. WatchService API

- A modern way to monitor directory/file changes.
- Eliminates need for custom thread-based watchers.

### 10. Binary Literals & String in Switch

- Binary literals using `0b` or `0B` prefix.
- Strings can now be used in switch statements.

### 11. Type Inference / Diamond Operator

- Simplifies generics by removing the need to repeat type parameters.

```java
Map<String, Integer> map = new HashMap<>();
```

### 12. Underscore in Numeric Literals

- Improves readability of large numbers.
```java
int num = 1_000_000;
```

### 13. JDBC Improvements

- JDBC 4.1 supports try-with-resources for automatic closing of:
  - `Connection`
  - `Statement`
  - `ResultSet`
- Added `RowSetProvider` and `RowSetFactory` to create different RowSet types easily.

### 14. G1 (Garbage-First) Collector

- A new garbage collector designed for large heap applications.
- Provides predictable pause times and better performance.

### 15. Fork & Join Framework

- Enables parallel processing by splitting tasks into smaller subtasks.
- Uses a _work-stealing algorithm_ for efficient CPU utilization.
- Forms the basis of Java 8’s parallel streams.

---