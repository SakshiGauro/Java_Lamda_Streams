# Coding Exercise: Using `Path` and `Paths`

This exercise demonstrates the key APIs introduced in Java 7 under `java.nio.file` for working with file and directory paths.

### Code Example: PathsInJava7

```java
private static void buildPath() throws IOException {
    Path path = Paths.get(HOME_DIR, "java7", "Test.txt");
    Path fileName = path.getFileName();
    System.out.println("File name is : "+fileName.toString());
    System.out.println("File system is : "+path.getFileSystem().toString());
    System.out.println("File system separator is : "+path.getFileSystem().getSeparator());
    for(int i=0;i<path.getNameCount();i++) {
    Path subPath = path.getName(i);
    System.out.println("Path location at index : "+(i+1)+" is "+subPath.toString());
    }
    System.out.println("Sub path is "+path.subpath(0,2));
    System.out.println("Root path is "+path.getRoot());
    System.out.println("Parent path is "+path.getParent());

    Path redundantPath = Paths.get(HOME_DIR, "java7", ".","Test.txt");
    System.out.println("Redundant path is "+redundantPath.toString());
    Path cleanPath = redundantPath.normalize();
    System.out.println("Clean path is "+cleanPath.toString());
    URI uri = cleanPath.toUri();
    System.out.println("URI path is "+uri.toString());
    System.out.println("Absolute path is "+cleanPath.toAbsolutePath().toString());
    
    Path partialPath = Paths.get(HOME_DIR, "java7");
    Path combinedPath = partialPath.resolve("Test.txt");
    System.out.println("Combined path is "+combinedPath.toString());
    
    if(!partialPath.equals(combinedPath)) {
        System.out.println("Paths are not equal");
    }
}
```

## Breakdown of Important Methods

`Paths.get(HOME_DIR, "java7", "Test.txt");`

- Utility method used to construct a `Path`.
- Accepts root + any number of directories + filename. 
- Automatically uses the system-specific file separator.
- Another `get()` method accepts a **URI (Uniform Resource Identifier)**.

`getFileName();`

Returns only the file name (`Test.txt`).

`getFileSystem()`

Returns the underlying file system (Windows, Linux, macOS).

`getSeparator()`

Returns the OS-specific separator (\ for Windows, / for Unix).

---

## Iterating Through Subpaths

```java
for(int i=0;i<path.getNameCount();i++) {
    Path subPath = path.getName(i);
    System.out.println("Path location at index : "+(i+1)+" is "+subPath.toString());
}
```

- Retrieves individual components **excluding the root**.
- Essentially treats the path like an array.

### Other path Operations

`getRoot()`

Returns the root directory (e.g., C:\).

`getParent()`

Returns the parent path (e.g., C:\java7).

---

## Normalizing Redundant Paths
```java
Path redundantPath = Paths.get(HOME_DIR, "java7", ".","Test.txt");
Path cleanPath = redundantPath.normalize();
```

- `.` represents the current directory.
- `normalize()` removes unnecessary components.

---

## Converting to URI

`cleanPath.toUri()`

Converts the path to a URI representation.

---

## Absolute Path

`toAbsolutePath()`

Returns the complete path starting from the system root.

---

## Combining Paths

```java
Path combinedPath = partialPath.resolve("Test.txt");
```
- Appends a file/directory to an existing path.
- Useful for dynamic path building.

---
