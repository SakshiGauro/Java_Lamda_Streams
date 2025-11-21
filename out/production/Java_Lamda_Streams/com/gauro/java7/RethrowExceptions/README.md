# Rethrowing Exceptions with more inclusive type checking

Java 7 introduced **more precise rethrow analysis**, allowing developers to rethrow exceptions while specifying **more specific exception types** in the method’s `throws` clause.

Before Java 7, rethrowing an exception inside a `catch (Exception e)` block forced the method to declare only the **general** exception type (`Exception`), even if only specific exceptions were possible.

---

## Before Java 7 (Forced to Declare a General Exception)

```java
static class FirstException extends Exception { }

static class SecondException extends Exception { }

public static void beforeJava7(String exceptionName) throws Exception {
    try {
        if (exceptionName.equals("First")) {
            throw new FirstException();
        } else {
            throw new SecondException();
        }
    } catch (Exception e) {
        throw e;
    }
}
```

### Why this happens
- The catch parameter `e` is of type `Exception`.
- When rethrowing `e`, the compiler cannot determine which specific subclass was thrown.
- Therefore, the method **must** declare the generic `Exception`.

### Output

```java
Exception in thread "main" com.gauro.java7.RethrowExceptions.RethrowExceptions$FirstException
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.beforeJava7(RethrowExceptions.java:31)
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.main(RethrowExceptions.java:18)
```

--- 

## Java 7 (More Precise Rethrow Analysis)

Java 7's compiler analyzes the **actual exceptions thrown in the try block**, even when caught as a general type (`Exception`).
So, if only `FirstException` or `SecondException` can originate from the try block, the compiler allows them to be declared explicitly.

```java
static class FirstException extends Exception { }

static class SecondException extends Exception { }

public static void withJava7(String exceptionName) throws FirstException, SecondException {
    try {
        if (exceptionName.equals("First")) {
            throw new FirstException();
        } else {
            throw new SecondException();
        }
    } catch (Exception e) {
        throw e;
    }
}
```

### Why this works
- The compiler analyzes the `try` block and sees that only FirstException and SecondException are ever thrown.
- Even though `e` is caught as `Exception`, the compiler guarantees that:
  - `e instanceof FirstException || e instanceof SecondException`
- Thus, the rethrow is type-safe.

### Output

```java
Exception in thread "main" com.gauro.java7.RethrowExceptions.RethrowExceptions$FirstException
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.withJava7(RethrowExceptions.java:49)
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.main(RethrowExceptions.java:19)
```
---