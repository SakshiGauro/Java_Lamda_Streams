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

### Important Behaviors

- No `finally` block required.
- The JVM automatically calls `br.close()`.
- Reassigning the resource variable inside the block is not allowed:
  ```Cannot assign a value to final variable 'br'```
- Resource variables inside `try()` must be **final**.
- Try-with-resources can still have `catch` or `finally` blocks if needed.



---

To make Developer life easy and improve the quality of the code, a new feature called ‘TRYWITH-RESOURCES statements’ are introduced.
• Using this we don’t have to explicitly close the resource. We just have to initialize the
resources details inside the () immediately next to try keyword. In its simplest form, the trywith-resources statement can be written as,
try (BufferedReader br = ...) {
//work with br
}
• When try block execution completes the br.close() method will be automatically called by JVM.
For this a new interface is created in Java 7 which is ‘java.lang.AutoCloseable’

We have three methods: 

1. In the code public static void beforeJava7() throws IOException" shows how we used to handle resources before JAVA 7. Before JAva7, we had to close it explicitly using the `finally` block. 
. removing "finally **{**
br.close();
}" throws an error "java: 'try' without 'catch', 'finally' or resource declarations" 
This is a finally block ensures that certain code, typically for resource cleanup (like closing files or network connections), is executed regardless of whether an exception occurred in the try block or not. This is crucial for preventing resource leaks.

2. In "public static void withJava7() throws FileNotFoundException, IOException {" method, it shows that the `finally` block is not required to close the resource as it automatically closes it and JVM (insert full name) takes care of it.
   IF you try to create a new resource txt file with the same variable ("br"). It throws the  "Cannot assign a value to final variable 'br'".

Before ‘java.lang.AutoCloseable’ introduced in Java 7, we have an interface ‘java.io.Closeable’
which restricts the type of exception thrown to only IOException.
• But the new Interface(AutoCloseable) can be used in more general contexts, where the
exception thrown during closing is not necessarily an IOException.
• Since Closeable meets the requirements for AutoCloseable, it is implementing AutoCloseable
when the latter was introduced.
• A try-with-resources statement can itself have catch and finally clauses for other requirements
inside the application.
• You can specify multiple resources as well inside the try-with-resources statement.

Sample implementation of try-with-resources statement,
• All resource reference variables should be final or effective final. So we can’t perform reassignment with
in the try block.
• Till Java 1.6, try block should be followed by either catch or finally block but from Java 7 we can have
only try with resource block with out catch & finally blocks.

3. In "public static void withJava7() throws FileNotFoundException, IOException {" We have a new interface called AutoCloseable. This is because the closeable interface will restrict the close method to throw only IOExcpetion. However, we might wanna throw different errors such as fileNotFound expection and many more. 
