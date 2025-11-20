# Suppressed Exceptions in Java (Java 7+)
Suppressed exceptions are exceptions that occur but are ignored because another exception takes precedence.
A common case is when an exception occurs in a `try` block, and another occurs in `finally` (or during resource closing), causing the original one to be lost.

Java 7 introduced **suppressed exception handling** to prevent this loss.

--- 

## New Methods Added in Java 7

Java 7 added support in the `Throwable` class:
```java
Throwable.addSuppressed(Throwable exception);
Throwable[] getSuppressed();
```
1. `addSuppressed()`: Adds additional exception details without losing the original exception.
2. `getSuppressed()`: Returns all suppressed exceptions, useful for debugging and logging.

---

## CustomeDirtyResource Class

```java
public class CustomDirtyResource implements AutoCloseable {

	@Override
	public void close() throws Exception {
		throw new NullPointerException("OOOPs. It is very bad to have a NullPointerExceptions !!");

	}

	public void readFromResource() {
		throw new RuntimeException("I am sorry. I don't have data available right now due to network issue !!!");
	}

}
```
This simulates a scenario with:
- Exception in `readFromResource()` → RuntimeException
- Exception in `close()` → NullPointerException

---

## Before java7 (loss of original exception)

```java
public static void beforeJava7() throws Exception {
    CustomDirtyResource cr = null;
    try {
        cr = new CustomDirtyResource();
        cr.readFromResource();
    } finally {
        cr.close();
    }
}
```
After the two exceptions occur. Since there is no `catch` block, the exceptions are thrown back to the `main` method. 

```java
catch (Exception ex) {
    LOGGER.log(Level.SEVERE, ex.getMessage());
}
```

**Problem**

This logs the recent exception that occurred and loses track of the original exception. The **second** exception (`NullPointerException` from `close()`) overwrites the original `RuntimeException`.

**Logged Output**
```java
SEVERE: OOOPs. It is very bad to have a NullPointerExceptions !!
```

The original exception is **lost**. This issue is solved in Java7. 

--- 

## After java7 

```java
public static void withJava7() throws Exception {
    try (CustomDirtyResource cr = new CustomDirtyResource();) {
        cr.readFromResource();
    }
}
```

### How it works

When multiple exceptions occur:
- The main exception is thrown (RuntimeException).
- Any others (NullPointerException from `close()`) are automatically added to `getSuppressed()`.

### Catch Block

```java
  catch (Exception ex) {
    LOGGER.log(Level.SEVERE, ex.getMessage());
    final Throwable[] suppressedExceptions = ex.getSuppressed();
    final int numSuppressed = suppressedExceptions.length;
    if (numSuppressed > 0) {
        for (final Throwable exception : suppressedExceptions) {
            LOGGER.log(Level.SEVERE, exception.getMessage());
        }
    }
```

The exception object holds the original expedition (instead of recent one). All the following exceptions will be stored in `getSuppressed()` method. The developer can later debug all the issues. 

**Output**
```java
SEVERE: I am sorry. I don't have data available right now due to network issue !!!
SEVERE: OOOPs. It is very bad to have a NullPointerExceptions !!
```

### How are we adding without the addsupressed method?

```java
public final synchronized Throwable[] getSuppressed() {
    if (suppressedExceptions == SUPPRESSED_SENTINEL ||
        suppressedExceptions == null)
        return EMPTY_THROWABLE_ARRAY;
    else
        return suppressedExceptions.toArray(EMPTY_THROWABLE_ARRAY);
}
```

In try-with-resources, the JVM internally calls:
- The primary exception becomes the main thrown exception.
- Any exceptions thrown during `close()` are added using `addSuppressed()`.

If no suppressed exceptions exist, `getSuppressed()` returns an **empty** array.

---

