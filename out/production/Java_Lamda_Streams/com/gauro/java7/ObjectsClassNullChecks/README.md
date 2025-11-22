# Objects Class and Null Checks

**Cleaner, Safer, and More Readable Null Handling with `java.util.Objects`**

Java 7 introduced a new utility class:

`java.util.Objects`

This class provides several helpful static utility methods for working with objects, including:
- Null checks
- Hash code computation
- Equality comparison
- Safe string conversion

The most significant additions for defensive programming are:
- `Objects.requireNonNull(T obj)`
- `Objects.requireNonNull(T obj, String message)`

### Why Use `Objects.requireNonNull`?

Developers might ask:

> “Why use `requireNonNull()` if referencing a null object throws a NullPointerException anyway?”

### Here’s why:

- ✔ Predictable behavior — always throws a NullPointerException, even before referencing
- ✔ Customized error messages — makes debugging easier
- ✔ More readable and intentional code
- ✔ Fail-fast behavior — the error occurs exactly where the issue lies

### Example Usage
```java
private static void processPersonDetails(Person person) {
    Objects.requireNonNull(person, "Person object can't be null");
    System.out.println(person.getFirstName());
    System.out.println(person.getLastName());
}
```

**Why this is better**

- The null check is explicit
- The error message is clear
- The failure happens _immediately_ instead of somewhere deeper in the code

### Output

When person is null, the method throws:

```java
Exception in thread "main" java.lang.NullPointerException: Person object can't be null
	at java.base/java.util.Objects.requireNonNull(Objects.java:259)
	at com.gauro.java7.ObjectsClassNullChecks.RequireNonNull.processPersonDetails(RequireNonNull.java:23)
	at com.gauro.java7.ObjectsClassNullChecks.RequireNonNull.main(RequireNonNull.java:19)
```

---