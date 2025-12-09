# Introduction to Joda Date and time API

Before Java 8, working with dates and times in Java had multiple design issues:

- `java.util.Date` and **SimpleDateFormat** are **not thread-safe.**
- The `Date` class does not represent a human-readable date but an instant in time with millisecond precision.
- Years start from 1900, and months are **0-indexed**, which is unintuitive.

**Example:**
```java
Date date = new Date(117, 8, 21); // Represents 21 Sep 2017
```

Java attempted to fix this with `java.util.Calendar`, but it also has design flaws and is error-prone. The presence of both **Date** and **Calendar** creates confusion about which to use.

**DateFormat** is also problematic: it’s not thread-safe and only works with Date objects.

**Why Joda-Time?**

Due to these limitations, developers started using **third-party libraries**, such as **Joda-Time**, for better date/time handling. Many features of Joda-Time were later integrated into **Java 8** in the **`java.time` package.**

### Java 8 `java.time` Package

The new package provides robust and intuitive classes for handling dates and times:

- `LocalDate` – Represents a date without time (e.g., 2025-12-07)
- `LocalDateTime` – Represents date and time without timezone
- `Instant` – Represents a moment on the timeline in UTC
- `Duration` – Measures time-based amount in seconds/nanoseconds
- `Period` – Measures date-based amount in years, months, days

These classes are **immutable, thread-safe**, and provide **clear, human-readable APIs** for date/time manipulation.

---
