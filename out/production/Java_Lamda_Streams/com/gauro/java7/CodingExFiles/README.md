# Coding Example: Working With Files (Java 7 NIO)

This example demonstrates how to use the enhanced Java 7 `java.nio.file.Files` APIs for reading, writing, copying, creating, and deleting files.

## Code Example: FilesInJava7
```java
private static void workingWithFiles() throws IOException {
    Path path = Paths.get(HOME_DIR, "java7", "Test.txt");
    byte[] bytes = Files.readAllBytes(path);
    String content = new String(bytes, StandardCharsets.UTF_8);
    System.out.println("Content of the file is: " + content);
    
    List<String> lines = Files.readAllLines(path, StandardCharsets.UTF_8);
    for(String line : lines) {
        System.out.println("Content of the line is: " + line);
    }
    
    String newLine = " How are you?";
    Files.write(path,newLine.getBytes() , StandardOpenOption.APPEND);
    
    Path newPath = Paths.get(HOME_DIR, "java8");
    Files.createDirectory(newPath);
    Path filePath = Paths.get(HOME_DIR, "java8","Hello.txt");
    Files.createFile(filePath);
    
    Path newFilePath = Paths.get(HOME_DIR, "java8","Test.txt");
    InputStream in = Files.newInputStream(path);
    Files.copy(in, newFilePath);
    
    Files.copy(path, filePath, StandardCopyOption.REPLACE_EXISTING,
            StandardCopyOption.COPY_ATTRIBUTES);
    
    Files.delete(newFilePath);
    boolean deleted = Files.deleteIfExists(newFilePath);
    System.out.println(deleted);
    
}
```

## Breakdown of Operations

**1. Reading a File as Bytes**
```java
byte[] bytes = Files.readAllBytes(path);
```

- Reads the entire file into a byte array.
- Useful when working with binary content

**2. Reading File Line-by-Line**
```java
List<String> lines = Files.readAllLines(path, StandardCharsets.UTF_8);
```

- Returns a `List<String>` of all lines.
- More convenient for text files compared to raw bytes.

**3. Writing to a File**
```java
Files.write(path,newLine.getBytes() , StandardOpenOption.APPEND);
```

- Appends text to the existing file.
- Other supported modes: `CREATE`, `WRITE`, etc.

**4. Creating Directories and Files**
```java
Path newPath = Paths.get(HOME_DIR, "java8");
Files.createDirectory(newPath);
Path filePath = Paths.get(HOME_DIR, "java8","Hello.txt");
Files.createFile(filePath);
```

- `createDirectory()` → creates a new folder.
- `createFile()` → creates an empty file inside it.

**5. Copy Using InputStream**
```java
Path newFilePath = Paths.get(HOME_DIR, "java8","Test.txt");
InputStream in = Files.newInputStream(path);
Files.copy(in, newFilePath);
```

- Copies file content from one path to another.

**6. Copy with Options**
```java
Files.copy(path, filePath, StandardCopyOption.REPLACE_EXISTING, StandardCopyOption.COPY_ATTRIBUTES);
```

- `REPLACE_EXISTING` → overwrites target
- `COPY_ATTRIBUTES` → preserves metadata

**7. Deleting Files**
```java
Files.delete(newFilePath);
boolean deleted = Files.deleteIfExists(newFilePath);
```

- `delete()` → throws exception if file doesn't exist.
- `deleteIfExists()` → returns `true` if deletion succeeded; `false` otherwise.

---
