# Coding Ex Files

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
- byte[] bytes = Files.readAllBytes(path);
- gets the conetct of the files in an array of bytes. 

```java
List<String> lines = Files.readAllLines(path, StandardCharsets.UTF_8);
for(String line : lines) {
    System.out.println("Content of the line is: " + line);
}
```
- instead of converting all the data into bytes, it will give you a list of lines inside the files. 

```java
String newLine = " How are you?";
Files.write(path,newLine.getBytes() , StandardOpenOption.APPEND);
```
- adding a new line to the path. param. We can also append, create a new file, and many more

```java
Path newPath = Paths.get(HOME_DIR, "java8");
Files.createDirectory(newPath);
Path filePath = Paths.get(HOME_DIR, "java8","Hello.txt");
Files.createFile(filePath);
```
- create a new folder `java8` using createDirectory with file `Hello.txt` using createFile

```java
Path newFilePath = Paths.get(HOME_DIR, "java8","Test.txt");
InputStream in = Files.newInputStream(path);
Files.copy(in, newFilePath);
```
- copy the content from java7/test.txt to java8/test.txt

```java
Files.copy(path, filePath, StandardCopyOption.REPLACE_EXISTING,
StandardCopyOption.COPY_ATTRIBUTES);
```

- replace an existing file

```java
Files.delete(newFilePath);
boolean deleted = Files.deleteIfExists(newFilePath);
System.out.println(deleted);
```
- delete - deletes the file
- deleteIfExists: returns a true if the file has been deleted. For this case it returns false since the file has been previously deleted

