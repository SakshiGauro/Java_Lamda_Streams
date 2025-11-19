# Try-With-Resources (Java 7)

## Overview
Java 7 introduced **Try-With-Resources** to make life easier for developers and improve code quality. Before Java 7, resources such as files, streams, or network connections had to be manually closed in a `finally` block, which often led to resource leaks or verbose code.

The new syntax allows developers to initialize resources inside the `try()` parentheses. When the try block completes, Java automatically calls the resource’s `close()` method.

## What Is Try-With-Resources?

A simple try-with-resources statement:

```java
try (BufferedReader br = ...) {
    // work with br
}
```
When the try block finishes, the JVM automatically calls:

```br.close();```

This behavior is enabled by the new interface introduced in Java 7:
`java.lang.AutoCloseable`. Any class implementing `AutoCloseable` can be used inside a try-with-resources block.

## Before Java 7 — Manual Resource Handling
Method: `beforeJava7()`

Before Java 7, resources needed to be closed manually inside a `finally` block:

```java
public static void beforeJava7() throws IOException {
    BufferedReader br = null;
    try {
        br = new BufferedReader(new FileReader("E:/jobHunt/javaLamda/Java_Lamda_Streams/Java7/test.txt"));
        String sCurrentLine;
        while ((sCurrentLine = br.readLine()) != null) {
            System.out.println(sCurrentLine);
        }
    } finally {
        br.close();
    }
}
```

### Important Behaviors

- If you remove the `finally` block, Java throws:
`try without catch, finally, or resource declarations`
- The `finally` block ensures resource cleanup even if an exception occurs.
- Forgetting `br.close()` leads to resource leaks.

---

## After Java 7 — Automatic Cleanup with Try-With-Resources
Method: `withJava7()`

After Java 7, resources **do not** need to be closed manually inside a `finally` block:

```java
public static void withJava7() throws FileNotFoundException, IOException {
    try(BufferedReader br = new BufferedReader(new FileReader("E:/jobHunt/javaLamda/Java_Lamda_Streams/Java7/test.txt"));) {
        String sCurrentLine;
        while ((sCurrentLine = br.readLine()) != null) {
            System.out.println(sCurrentLine);
        }
    }
}
```

### Important Behaviors

- No `finally` block required.
- The JVM automatically calls `br.close()`.
- Reassigning the resource variable inside the block is not allowed:
```Cannot assign a value to final variable 'br'```
- Resource variables inside `try()` must be **final**. 
- Try-with-resources can still have `catch` or `finally` blocks if needed.

---

## Using Custom Resources with AutoCloseable

You can define your own resource by implementing `AutoCloseable`.

```java
public class CustomResource implements AutoCloseable {

	@Override
	public void close() throws Exception {
		System.out.println(" From close method inside the CustomResource class");

	}

	public void readFromResource() {
		System.out.println(" Reading data... ");
	}

}
```

### Output
```java
 Reading data... 
 From close method inside the CustomResource class
```
This shows that Java automatically calls `cr.close()`.

---
