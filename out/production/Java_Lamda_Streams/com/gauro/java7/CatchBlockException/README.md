# Catching Multiple Exceptions using a single CATCH block

Before Java 7, if the same action needed to be performed for multiple exceptions (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`), you were forced to write **multiple catch blocks**, causing repetitive code.

## Before Java 7 (Multiple Catch Blocks Needed)

```java
public static void beforeJava7() {
    int arr[] = { 1, 2, 3 };
    try {
        for (int i = 0; i < arr.length + 1; i++) {
            System.out.println(arr[i]);
        }
    } catch (NullPointerException nex) {
        LOGGER.log(Level.SEVERE, nex.toString());
    } catch (ArrayIndexOutOfBoundsException aioex) {
        LOGGER.log(Level.SEVERE, aioex.toString());
    }
}
```

### Drawback
- Code duplication
- Repeated catch blocks with identical logic

### Output 
```java
1
2
3
SEVERE: java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
```

---

## After JAVA7 (One Catch handles Multiple Exceptions)

Java 7 introduced **multi-catch**, allowing you to catch multiple exception types in **one catch block** when the handling logic is the same.

```java
public static void withJava7() {
    int arr[] = { 1, 2, 3 };
    try {
        for (int i = 0; i < arr.length + 1; i++) {
            System.out.println(arr[i]);
        }
    } catch (NullPointerException | ArrayIndexOutOfBoundsException | ClassCastException ex) {
        LOGGER.log(Level.SEVERE, ex.toString());
    }
}
```

### Benefits
- Cleaner and shorter code
- Avoids duplicated catch logic
- Multiple exceptions separated by `|`
- write exceptions separated by |.

> **Important Rule**
> 
> In a multi-catch block, the exception variable (ex) is implicitly final
→ You cannot assign a new value to it inside the catch block.

### Output

```java
1
2
3
SEVERE: java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
```
---