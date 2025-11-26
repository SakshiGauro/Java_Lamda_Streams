# WatchService

Java 7 introduces a new interface called ‘java.nio.file.WatchService’ that watches registered
objects for changes and events. For example a file manager may use a watch service to
monitor a directory for changes so that it can update its display of the list of files when files
are created or deleted.
• It is very common for many application to track on files such as configuration so that we can
refresh the value inside the memory on every change. We used to handle using a Thread that
periodically poll for file change before Java 7. But this made easy using ‘WatchService’.
• A Watchable object is registered with a watch service by invoking its register method,
returning a WatchKey to represent the registration. When an event for an object is detected
the key is signaled, and if not currently signaled, it is queued to the watch service so that it can
be retrieved by consumers that invoke the poll or take methods to retrieve keys and process
events. Once the events have been processed the consumer invokes the key's reset method to
reset the key which allows the key to be signaled and re-queued with further events.
- also use this in places where all events happen in a queue. After we are done processing the queue, call reset method to reset processed events.


Important methods and classes related to WatchService

![methodsWatchService.png](img.png)

Code

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

Code explain 

```java
WatchService watchService = FileSystems.getDefault().newWatchService();
```

get watch serrvice from the file system 

```java
Path path = Paths.get("C:\\WatchService");
```
path of the watchserice. It is a watchable object (extends Watchable)

```java
path.register(watchService, StandardWatchEventKinds.ENTRY_CREATE, StandardWatchEventKinds.ENTRY_MODIFY,
            StandardWatchEventKinds.ENTRY_DELETE);
```
param: the watchserive, events to register/watch for changes. For this case, I want to see if a file has been creates, miodified or deleted


```java
 WatchKey key = watchService.take();
```
returns the watch key after the watch service registers the watchable object 

```java
while (poll) {
    for (WatchEvent<?> event : key.pollEvents()) {
        System.out.println("Event kind : " + event.kind() + " - for the file : " + event.context());
    }
    poll = key.reset();
}
```
using the watch keeo, I am polling for events that are happening insde the path. If there are any changes, I get the event and prionts it on console

Output
```java
Event kind : ENTRY_CREATE - for the file : New Text Document.txt
Event kind : ENTRY_DELETE - for the file : New Text Document.txt
Event kind : ENTRY_CREATE - for the file : Watchserice.txt
Event kind : ENTRY_MODIFY - for the file : Watchserice.txt
Event kind : ENTRY_DELETE - for the file : Watchserice.txt
```