# CLOSE METHOD INSIDE URLCLASSLOADER

`java.net.URLClassLoader` is used to load classes and resources from a search path of URLs referring to both JAR files and directories.

```java
URL[] urls = {new URL("file:junit-4.11.jar"),
new URL("file:commons-io-2.8.0.jar")};
URLClassLoader loader = new URLClassLoader(urls);
Class<?> junitClass = loader.loadClass("org.junit.runner.JUnitCore");
```

## Problem Before Java 7

Before Java 7, `URLClassLoader` did not have a `close()` method, which often caused **resource leaks** (open file handles on JARs).

## Java 7 Solution – `close()` Method

Java 7 added a `close()` method to `URLClassLoader` by making it implement `AutoCloseable`.

This allows it to be used safely inside a **try-with-resources** block:

```java
try (URLClassLoader loader = new URLClassLoader(urls)) {
    Class<?> junitClass = loader.loadClass("org.junit.runner.JUnitCore");
}
```
---