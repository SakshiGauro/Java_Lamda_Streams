# Instant, Duration, Period classes (java.time package)

- **Instant:** Represents a specific moment on the timeline since the Unix epoch **(1970-01-01T00:00:00Z)** in UTC.
- **Duration:** Represents the amount of time between two **time-based objects** (`Instant`, `LocalTime`, `LocalDateTime`) in **seconds, minutes, hours, or nanoseconds.**
- **Period:** Represents the difference between two **date-based objects** (`LocalDate`) in **years, months, days.**

## Coding example: InstantExample
### Working with `Instant`
```java
Instant instant = Instant.ofEpochSecond(6);
System.out.println(instant);
```

**Explanation:**
- Creates an `Instant` 6 seconds after Unix epoch.

**Output**
```java
1970-01-01T00:00:06Z
```

---

```java
System.out.println(Instant.ofEpochSecond(4, 1_000));
System.out.println(Instant.ofEpochSecond(4, -1_000));
```

**Explanation:**
- `Instant.ofEpochSecond(seconds, nanos)` allows **adding or subtracting nanoseconds.**

**Output**
```java
1970-01-01T00:00:04.000001Z
1970-01-01T00:00:03.999999Z
```

---

```java
Instant instantNow = Instant.now();
System.out.println(instantNow);
```

**Explanation:**
- Returns the **current timestamp in UTC.**

**Output**
```java
2025-12-07T23:20:08.778115300Z
```

---

### Duration Between Instants
```java
Duration instantDuration = Duration.between(instant,instantNow);
System.out.println(instantDuration);
```

**Explanation:**
- Calculates **duration between two instants.**

**Output**
```java
PT490319H20M2.7781153S
```

---

### Duration Between LocalTime Objects
```java
LocalTime time = LocalTime.of(12, 30, 10);
LocalTime time1 = LocalTime.of(16, 30, 10);
Duration timeDuration = Duration.between(time,time1);
System.out.println(timeDuration);
```

**Explanation:**
- Duration between `12:30:10` and `16:30:10` = **4 hours.**

**Output**
```java
PT4H
```

---

### Duration Between LocalDateTime Objects
```java
LocalDateTime dateTime = LocalDateTime.of(1989, Month.JUNE, 16, 12, 30, 10);
LocalDateTime dateTime1 = LocalDateTime.of(2000, Month.JUNE, 16, 16, 30, 10);
Duration dateTimeDuration = Duration.between(dateTime,dateTime1);
System.out.println(dateTimeDuration);
```

**Explanation:**
- Duration between **1989-06-16T12:30:10** and **2000-06-16T16:30:10.**
- Duration counts **exact time in seconds**, ignoring calendar differences.

**Output**
```java
PT96436H
```

---

### Period Between LocalDate Objects
```java
LocalDate date = LocalDate.of(1989, 6, 16);
LocalDate date1 = LocalDate.of(1989, 6, 26);
Period localDatePeriod = Period.between(date,date1);
System.out.println(localDatePeriod);

```

**Explanation:**
- Period calculates **difference in years, months, and days** between two dates.

**Output**
```java
P10D
```

---
