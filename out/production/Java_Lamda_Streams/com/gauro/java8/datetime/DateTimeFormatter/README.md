# DateTimeFormatter class inside Joda Date and Time API

**Formatting & Parsing Date-Time Objects**
- `java.time.format` **package**
  - Introduced to handle formatting and parsing of all date & time objects in Java.
  - Replaces the older, non–thread-safe `java.text.DateFormat`.

- **Thread-safe Formatters**
  - All `DateTimeFormatter` instances are **immutable and thread-safe.**
  - This allows using **singleton** formatters like predefined constants (`ISO_LOCAL_DATE`, `BASIC_ISO_DATE`, etc.) across multiple threads safely.

- **Custom Patterns & Locales**
  - You can specify:
    - custom patterns → `DateTimeFormatter.ofPattern("dd/MMM/yyyy")`
    - specific locale → `DateTimeFormatter.ofPattern("d. MMMM yyyy", Locale.GERMAN)`
  - Useful for internationalization and displaying dates in different human-readable formats.

## Coding Example: DateTimeFormatterExample
### LocalDate object
```java
LocalDate date = LocalDate.of(2008, 6, 16);
```

**Explanation:** 
- Creates a `LocalDate` object representing **16 June 2008.**

---

### Built-in ISO Formatters
```java
String baseISO = date.format(DateTimeFormatter.BASIC_ISO_DATE);
System.out.println(baseISO); // 20080616
```

**Explanation:**
- `BASIC_ISO_DATE` prints a date without hyphens → `YYYYMMDD`.
- Useful when storing compact date strings or using machine-readable formats.

```java
String localISO = date.format(DateTimeFormatter.ISO_LOCAL_DATE);
System.out.println(localISO); // 2008-06-16
```

**Explanation:**
- Standard ISO format with hyphens → `YYYY-MM-DD`.
- Most common international date representation.

---

### Parsing Strings into LocalDate
```java
LocalDate baseISODate = LocalDate.parse("20080616", DateTimeFormatter.BASIC_ISO_DATE);
System.out.println(baseISODate); //2008-06-16
```

**Explanation:**
- Parses a compact ISO date string into a `LocalDate` object.
- Java automatically interprets the format based on the formatter.

```java
LocalDate localISODate = LocalDate.parse("2008-06-16", DateTimeFormatter.ISO_LOCAL_DATE);
System.out.println(localISODate); //2008-06-16
```

**Explanation:**
- Parses a standard ISO formatted date.
- Very common when reading dates from APIs, JSON, or databases.

---

### Using Custom Pattern
```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MMM/yyyy");
LocalDate localDate = LocalDate.of(2008, 6, 18);

String formattedDate = localDate.format(formatter);
System.out.println(formattedDate); // 18/Jun/2008
```

**Explanation:**
- `dd` → day (2 digits)
- `MMM` → short month name (Jun)
- `yyyy` → full year
- Custom formats help when displaying dates to users in specific formats (reports, UI).

---

### Using Custom Pattern + Locale
```java
DateTimeFormatter germanFormatter = DateTimeFormatter.ofPattern("d. MMMM yyyy", Locale.GERMAN);
LocalDate date1 = LocalDate.of(2008, 6, 16);

String formattedDateGer = date1.format(germanFormatter); // 16. Juni 2008
System.out.println(formattedDateGer); // 16. Juni 2008
```

**Explanation:**
- `MMMM` → full month name (“June”)
- Because Locale is German → “Juni” instead of “June”.
- Useful for applications supporting multiple languages.

---

**Final Summary**

- **DateTimeFormatter** is the modern Java class for formatting & parsing date/time.
- It is **thread-safe**, making it reliable and safe for enterprise applications.
- Supports **built-in ISO formats** and **custom patterns.**
- Allows **Locale-based formatting**, useful for internationalized output.
- Works with all Java date/time types: `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`, etc.
- Parsing and formatting are consistent, predictable, and less error-prone compared to legacy `DateFormat`.

---