# Completable Feature

Java 8 introduces `java.util.concurrent.CompletableFuture` for **asynchronous, non-blocking programming.**

Unlike normal Future, it supports:
- Callbacks (`thenApply`, `thenAccept`, `thenRun`)
- Chaining
- Combining multiple async tasks

Runs tasks on a **separate thread**, freeing the main thread and execute other tasks in parallel.

**Main Methods**

- `runAsync()` → runs in background, returns **nothing**
- `supplyAsync()` → runs in background, returns a **value**
- `get()` → blocks until future is complete
- `thenApply()` → transforms output
- `thenAccept()` → consumes output without returning anything

---

## Coding example: CompletableFutureExample
### runAsync() Example

```java
private static void runAsync() throws InterruptedException, ExecutionException {
    CompletableFuture<Void> async = CompletableFuture.runAsync(() -> {
        try {
            TimeUnit.SECONDS.sleep(1);
            System.out.println("Running in a separate thread than the main thread.");
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
    });
    System.out.println("runAsync Blocking 1");
    async.get();
    System.out.println("runAsync Blocking 2");
}
```

**Explanation:**
- `runAsync()` runs a task without returning a value (Void)
- It launches a new background thread that sleeps for 1 sec.
- During that waiting time, the main thread prints `"runAsync Blocking 1"`
- `async.get()` **pauses the main thread** until async task finishes. Async thread prints `"Running in a separate thread than the main thread."`
- Finally, the main thread resumes and prints `runAsync Blocking 2`
- Useful for **fire-and-wait** tasks where no return value is needed.

**Output**
```java
runAsync Blocking 1
Running in a separate thread than the main thread.
runAsync Blocking 2
```

---

### supplyAsync() Example

```java
private static void supplyAsync() throws InterruptedException, ExecutionException {
    CompletableFuture<String> async = CompletableFuture.supplyAsync(() -> {
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
        return "Eazy Bytes";
    });
    System.out.println("supplyAsync Blocking 1");
    String result = async.get();
    System.out.println(result);
    System.out.println("supplyAsync Blocking 2");
}
```

**Explanation:**
- `supplyAsync()` is like `runAsync()` but returns a value.
- It launches a new background thread that sleeps for 1 sec.
- During that waiting time, the main thread prints `"supplyAsync Blocking 1"`
- `async.get()` **pauses the main thread** until async task finishes. Async thread returns `"Eazy Bytes"`. 
- Finally, the main thread resumes and prints the returned value and `"supplyAsync Blocking 2"`
- Good for offloading expensive computations to another thread.

**Output**
```java
supplyAsync Blocking 1
Eazy Bytes
supplyAsync Blocking 2
```

---

### thenApply() Example

```java
private static void thenApply() throws InterruptedException, ExecutionException {
    CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
        return "Eazy";
    });

    System.out.println("thenApply middle block");

    CompletableFuture<String> finalFuture = future.thenApply(name -> {
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
        return name + " Bytes";
    });

    System.out.println("thenApply before final block");
    System.out.println(finalFuture.get());
    System.out.println("thenApply Blocking");
}
```

**Explanation:**
- `thenApply()` transforms the result of the previous stage. It has a **callback mechanism.** 
- It launches a new background thread (`future`) that sleeps for 1 sec and returns `"Eazy"`
- During that waiting time, the main thread resumes and prints `"thenApply middle block"`. 
- It then launches another new background thread (`finalFuture`) that takes in a returned value from `future`. It **sleeps for 1 sec** and **concatenates** the two strings and **returns** the value. 
- Back in the main thread, it prints `"thenApply before final block"`, the returned value from `finalFuture` and `"thenApply Blocking"`.

**Output**
```java
thenApply middle block
thenApply before final block
Eazy Bytes
thenApply Blocking
```

---

### thenAccept() Example

```java
private static void thenAccept() throws InterruptedException, ExecutionException {
    CompletableFuture<Void> future = CompletableFuture.supplyAsync(() -> {
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
        return "Accept";
    }).thenAccept(result -> {
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            throw new IllegalStateException(e);
        }
        System.out.println("Received the value " + result);
    });
    System.out.println("thenAccept non-blocking");
    future.get();
}
```

**Explanation:**
- `thenAccept()` consumes the result but returns no new value.
- The main thread launches an async task that sleeps for 1 sec and returns `"Accept"`
- While the background thread is running, the main thread resumes and prints `"thenAccept non-blocking"`.
- When `future.get()` runs, the main thread **blocks** until:
  - the async thread returns `"Accept"` 
  - the `thenAccept()` consumer runs (also sleeping 1 sec), and prints`"Received the value Accept"`

**Output**
```java
thenAccept non-blocking
Received the value Accept
```

---