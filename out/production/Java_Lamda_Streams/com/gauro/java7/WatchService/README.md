# WatchService (Java 7)

Java 7 introduced the `java.nio.file.WatchService` API, allowing applications to monitor directories for changes such as file creation, modification, or deletion.

Before Java 7, developers typically used background threads to repeatedly poll directories for changes. This was inefficient and error-prone. The `WatchService` API provides a cleaner, event-driven way to react to file system changes.

## How WatchService Works

- A **WatchService** monitors registered directories for events.
- A **Watchable** object (e.g., a `Path`) registers with the WatchService using the `register()` method.
- Registration returns a **WatchKey**, which represents the subscription.
- When events occur, the **WatchKey is signaled** and placed in the event queue.
- The application retrieves events by calling:
  - `poll()` – non-blocking
  - `take()` – blocking (waits for events)
- After processing events, the key must be reset using `key.reset()` to continue receiving future events.

This event-driven model is useful wherever operations need to react to real-time file system changes.

|Component| Purpose |
|------------|---------|
|`WatchService`|Core interface for watching file changes|
|`WatchKey`|Represents a registration of a watchable object|
|`WatchEvent`|Represents individual events (create, delete, modify)|
|`StandardWatchEventKinds`|Predefined event kinds (ENTRY_CREATE, ENTRY_MODIFY, ENTRY_DELETE)|
|`register()`|Registers a `Path` to listen for specific events|

## Important methods and classes related to WatchService

![methodsWatchService.png](img.png)

## Code Example - WatchServiceInJava7

```java
public static void directoryWatchService() throws Exception {
    WatchService watchService = FileSystems.getDefault().newWatchService();
    Path path = Paths.get("C:\\WatchService");
    path.register(watchService, StandardWatchEventKinds.ENTRY_CREATE, StandardWatchEventKinds.ENTRY_MODIFY,
            StandardWatchEventKinds.ENTRY_DELETE);
    boolean poll = true;
    WatchKey key = watchService.take();
    while (poll) {
        for (WatchEvent<?> event : key.pollEvents()) {
            System.out.println("Event kind : " + event.kind() + " - for the file : " + event.context());
        }
        poll = key.reset();
    }
    
}
```

## Code explaination 

**1. Creating a WatchService**
```java
WatchService watchService = FileSystems.getDefault().newWatchService();
```

- Retrieves a WatchService from the default file system.

**2. Creating the path to monitor**
```java
Path path = Paths.get("C:\\WatchService");
```
- The directory to observe (a Watchable object).

**3. Registering Events**
```java
path.register(watchService, StandardWatchEventKinds.ENTRY_CREATE, StandardWatchEventKinds.ENTRY_MODIFY,
            StandardWatchEventKinds.ENTRY_DELETE);
```
This tells the WatchService to notify us when:
- A file is created
- A file is modified
- A file is deleted

**4. Waiting for Events**
```java
 WatchKey key = watchService.take();
```
- Blocks until an event is available.
- Returns a WatchKey representing the directory’s event queue.

**5. Processing Events**
```java
while (poll) {
    for (WatchEvent<?> event : key.pollEvents()) {
        System.out.println("Event kind : " + event.kind() + " - for the file : " + event.context());
    }
}
```
- Retrieves all events associated with the key.
- `event.context()` returns the file name inside the directory.

**6. Resetting the Key**
```java
poll = key.reset();
```
- Allows the key to receive more events.
- If it returns **false**, the directory is no longer accessible.

### Sample Output
```java
Event kind : ENTRY_CREATE - for the file : New Text Document.txt
Event kind : ENTRY_DELETE - for the file : New Text Document.txt
Event kind : ENTRY_CREATE - for the file : Watchserice.txt
Event kind : ENTRY_MODIFY - for the file : Watchserice.txt
Event kind : ENTRY_DELETE - for the file : Watchserice.txt
```

---