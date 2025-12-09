# LocalDate Class in Java 8 (`java.time` package)

- `LocalDate` represents an **immutable date object without time or timezone.**
- Useful when you only care about the date (year, month, day) but not the time of day.
- You can create a `LocalDate` using `now()`, `of()`, or `parse()` methods.
- Provides utility methods to get information like **day of month, day of week, month length, leap year check,** etc.

## Coding Example: LocalDateExample
### Creating a LocalDate with of()

```java
LocalDate date = LocalDate.of(1989, 6, 16);
System.out.println("Given Date is: "+date);
```

**Explanation:**
- `LocalDate.of(year, month, day)` creates a specific date (June 16, 1989).
- The object `date` now holds this date in an immutable form.

**Output**
```java
Given Date is: 1989-06-16
```

---

### Extracting Year, Month, and Day

```java
int year = date.getYear();
System.out.println("Given Year is: "+year);

Month month = date.getMonth();
System.out.println("Given Month is: "+month);

int day = date.getDayOfMonth();
System.out.println("Given Day is: "+day);
```

**Explanation:**
- `getYear()` returns the year (1989).
- `getMonth()` returns the enum `Month.JUNE`.
- `getDayOfMonth()` returns the day of the month (16).

**Output**
```java
Given Year is: 1989
Given Month is: JUNE
Given Day is: 16
```

---

### Day of Week, Month Length, and Leap Year Check

```java
DayOfWeek dow = date.getDayOfWeek();
System.out.println("Given day of the week is: "+dow);

int len = date.lengthOfMonth();
System.out.println("Given length of month is: "+len);

boolean leap = date.isLeapYear();
System.out.println("Is a leap year: "+leap);
```

**Explanation:**
- `getDayOfWeek()` returns the day of the week (e.g., FRIDAY).
- `lengthOfMonth()` returns the total number of days in that month (30 for June).
- `isLeapYear()` checks if the year is a leap year (false for 1989).

**Output**
```java
Given day of the week is: FRIDAY
Given length of month is: 30
Is a leap year: false
```

---

### Using `ChronoField` to Access Date Components

```java
int year1 = date.get(ChronoField.YEAR);
System.out.println("Given year is: "+year1);

int month1 = date.get(ChronoField.MONTH_OF_YEAR);
System.out.println("Given month is: "+month1);

int day1 = date.get(ChronoField.DAY_OF_MONTH);
System.out.println("Given day is: "+day1);
```

**Explanation:**
- `ChronoField` provides a generic way to access date components.
- Functions like `get(ChronoField.YEAR)` return the corresponding integer values.

**Output**
```java
Given year is: 1989
Given month is: 6
Given day is: 16
```

---

### Parsing a Date from a String

```java
LocalDate parseDate = LocalDate.parse("2000-06-16");
System.out.println("Parse Date is: "+parseDate);
```

**Explanation:**
- `LocalDate.parse(String)` converts a string in `YYYY-MM-DD` format to a `LocalDate`.
- Useful for reading dates from text sources.

**Output**
```java
Parse Date is: 2000-06-16
```

---

### Getting the Current Date

```java
LocalDate today = LocalDate.now();
System.out.println("Today's date is: "+ today);
```

**Explanation:**
- `LocalDate.now()` returns the current system date. 
- This is often used for comparison, validation, or logging.

**Output**
```java
Today's date is: 2025-12-07
```

---