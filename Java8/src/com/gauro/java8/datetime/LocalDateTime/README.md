# LocalDateTime Class in Java 8 (java.time package)

- `LocalDateTime` combines **both date and time** without a timezone.
- Useful when you need **complete timestamp info**, but not concerned with time zones.
- Can be created directly using `of()` or by combining a `LocalDate` and `LocalTime`.

## Coding Example: LocalDateTimeExample
### Creating LocalDate and LocalTime
```java
LocalDate date = LocalDate.of(1989, 6, 16);
LocalTime time = LocalTime.of(12, 30, 10);
```

**Explanation:**
- `date` represents 16 June 1989. 
- `time` represents 12:30:10.

---

### Creating LocalDateTime directly
```java
LocalDateTime dateTime = LocalDateTime.of(1989, Month.JUNE, 16, 12, 30, 10);
System.out.println("The given Date and Time is: "+dateTime);
```

**Explanation:**
- Combines date and time in one object.

**Output**
```java
The given Date and Time is: 1989-06-16T12:30:10
```

---

### Creating LocalDateTime from LocalDate and LocalTime
```java
LocalDateTime dateTimeVal = LocalDateTime.of(date, time);
```

**Explanation:**
- Combines previously created `LocalDate` and `LocalTime` into a `LocalDateTime`.

---

### Accessing Date and Time Components
```java
System.out.println(dateTimeVal.getYear());
System.out.println(dateTimeVal.getMonth());
System.out.println(dateTimeVal.getDayOfMonth());
System.out.println(dateTimeVal.getDayOfWeek());
System.out.println(dateTimeVal.getDayOfYear());
System.out.println(dateTimeVal.getHour());
System.out.println(dateTimeVal.getMinute());
System.out.println(dateTimeVal.getSecond());
System.out.println(dateTimeVal.getNano());
```

**Explanation:**
- Extracts specific year, month, day, hour, minute, second, nanosecond, etc.
- Provides easy access to all components without parsing strings.

**Output**
```java
1989
JUNE
16
FRIDAY
167
12
30
10
0
```

---

### Comparing LocalDateTime Objects
```java
System.out.println(dateTimeVal.isAfter(dateTime));
System.out.println(dateTimeVal.isBefore(dateTime));
System.out.println(dateTimeVal.isEqual(dateTime));
```

**Explanation:**
- `isAfter()`, `isBefore()`, `isEqual()` are used to compare two `LocalDateTime` objects.

**Output**
```java
false
false
true
```

---

### Adding Time to LocalDateTime
```java
System.out.println(dateTimeVal.plusYears(1));
System.out.println(dateTimeVal.plusWeeks(3));
System.out.println(dateTimeVal.plusDays(2));
System.out.println(dateTimeVal.plusHours(4));
System.out.println(dateTimeVal.plusMinutes(40));
System.out.println(dateTimeVal.plusSeconds(20));
```

**Explanation:**
- `plusYears()`, `plusWeeks()`, `plusDays()`, `plusHours()`, `plusMinutes()`, `plusSeconds()` create new `LocalDateTime` objects with added time.
- Original `dateTimeVal` remains **immutable**.

**Output**
```java
1990-06-16T12:30:10
1989-07-07T12:30:10
1989-06-18T12:30:10
1989-06-16T16:30:10
1989-06-16T13:10:10
1989-06-16T12:30:30
```

---

### Subtracting Time from LocalDateTime
```java
System.out.println(dateTimeVal.minusYears(1));
System.out.println(dateTimeVal.minusWeeks(3));
System.out.println(dateTimeVal.minusDays(2));
System.out.println(dateTimeVal.minusHours(4));
System.out.println(dateTimeVal.minusMinutes(40));
System.out.println(dateTimeVal.minusSeconds(20));
```

**Explanation:**
- `minusYears()`, `minusWeeks()`, `minusDays()`, etc., create new objects with **reduced time**.

**Output**
```java
1988-06-16T12:30:10
1989-05-26T12:30:10
1989-06-14T12:30:10
1989-06-16T08:30:10
1989-06-16T11:50:10
1989-06-16T12:29:50
```

---

### Extracting Only Date or Time
```java
LocalDate dateLocal = dateTimeVal.toLocalDate();
System.out.println("The given time value is: "+dateLocal);

LocalTime timeLocal = dateTimeVal.toLocalTime();
System.out.println("The given date value is: "+timeLocal);
```

**Explanation:**
- `toLocalDate()` returns **only the date** part.
- `toLocalTime()` returns **only the time** part.

**Output**
```java
The given time value is: 1989-06-16
The given date value is: 12:30:10
```

---

### Getting Current Date and Time
```java
LocalDateTime dateTimeNow = LocalDateTime.now();
System.out.println("The current date & time value is: "+dateTimeNow);
```

**Explanation:**
- `LocalDateTime.now()` returns the **current system date and time**.

**Output**
```java
The current date & time value is: 2025-12-07T18:05:14.805190900
```

---
