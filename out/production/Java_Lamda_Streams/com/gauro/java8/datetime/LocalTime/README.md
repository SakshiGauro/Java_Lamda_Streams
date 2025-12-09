# LocalTime Class in Java 8 (java.time package)

- `LocalTime` represents an **immutable object for the time of day without any date or timezone.**
- Useful when you care **only about hours, minutes, seconds.**
- You can create a `LocalTime` using `now()`, `of()`, or `parse()`.
- Provides utility methods to access **hour, minute, second, nanosecond.**

## Coding Example: LocalTimeExample
### Creating a LocalTime with of()

```java
LocalTime time = LocalTime.of(12, 30, 10);
```

**Explanation:**
- `LocalTime.of(hour, minute, second)` creates a time representing 12:30:10.
- The object `time` is immutable and stores only time components.

---

### Extracting Hour, Minute, and Second

```java
int hour = time.getHour();
System.out.println("Given Houre is: " + hour);

int minute = time.getMinute();
System.out.println("Given minute is: " + minute);

int second = time.getSecond();
System.out.println("Given second is: " + second);
```

**Explanation:**
- `getHour()` returns the hour component (12).
- `getMinute()` returns the minute component (30).
- `getSecond()` returns the second component (10).

**Output**
```java
Given Houre is: 12
Given minute is: 30
Given second is: 10
```

---

### Parsing a Time from a String

```java
LocalTime parseTime = LocalTime.parse("12:30:10");
System.out.println("Given parse time is: " + parseTime);
```

**Explanation:**
- `LocalTime.parse(String)` converts a string in `HH:mm:ss` format into a `LocalTime` object.

**Output**
```java
Given parse time is: 12:30:10
```

---

### Getting the Current Time

```java
LocalTime currentTime = LocalTime.now();
System.out.println("Given current time is: " + currentTime);
```

**Explanation:**
- `LocalTime.now()` returns the current system time at runtime. 
- This is useful for logging or time-based comparisons

**Output**
```java
Given current time is: 17:54:58.504793
```

---
