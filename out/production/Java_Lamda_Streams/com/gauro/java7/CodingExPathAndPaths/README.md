# Coding Exercise: Using `Path` and `Paths`

This exercise demonstrates the key APIs introduced in Java 7 under `java.nio.file` for working with file and directory paths.

### Code Example: PathsInJava7

```java
private static void buildPath() throws IOException {
    Path path = Paths.get(HOME_DIR, "java7", "Test.txt");
    Path fileName = path.getFileName();
    System.out.println("File name is : "+fileName.toString());
    System.out.println("Fiel system is : "+path.getFileSystem().toString());
    System.out.println("Fiel system separator is : "+path.getFileSystem().getSeparator());
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

```java
Path path = Paths.get(HOME_DIR, "java7", "Test.txt");
```

- Utility method used to construct a `Path`.
- Accepts root + any number of directories + filename. 
- Automatically uses the system-specific file separator.
- Another `get()` method accepts a **URI (Uniform Resource Identifier)**.

```java
Path fileName = path.getFileName();
```
Returns only the file name (`Test.txt`).

```java
System.out.println("File system is : "+path.getFileSystem().toString());
```
Returns only the file name (`Test.txt`).

```java
Path fileName = path.getFileName();
```
Returns only the file name (`Test.txt`).

```java
Path fileName = path.getFileName();
```
Returns only the file name (`Test.txt`).
- getFileName - gets the file name. 
- getFileSystem - gets the file system eg: Linux, Mac or Windows. 
- getSeparator() - gets the file separator
- 
```java
for(int i=0;i<path.getNameCount();i++) {
Path subPath = path.getName(i);
System.out.println("Path location at index : "+(i+1)+" is "+subPath.toString());
}
```

- gets the subpath excluding the root. Convert the path into an array and get the subpaths
- path.getRoot(): get's the root 

```java
Path redundantPath = Paths.get(HOME_DIR, "java7", ".","Test.txt");
System.out.println("Redundant path is "+redundantPath.toString());
Path cleanPath = redundantPath.normalize();
System.out.println("Clean path is "+cleanPath.toString());
```

- We can get rid of redundants values wsuch as "." using the normalize

```java
URI uri = cleanPath.toUri();
System.out.println("URI path is "+uri.toString());

```

- convert the path to a URI 
```java
System.out.println("Absolute path is "+cleanPath.toAbsolutePath().toString());
```

- What is an absoulte path? since this is an absoulte path, it displays the same path but. 

```java
Path partialPath = Paths.get(HOME_DIR, "java7");
Path combinedPath = partialPath.resolve("Test.txt");
System.out.println("Combined path is "+combinedPath.toString());
```
- combines two paths together
- 


