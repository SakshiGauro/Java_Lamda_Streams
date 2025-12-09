# Time Zones and Calendars inside Joda Date and Time API

Java 8 introduced a modern timezone API inside the `java.time` package. These classes are far more accurate, intuitive, and DST-aware compared to old Java date/time classes.

**Key Classes**
1. `ZoneId`
   - Replacement for `java.util.TimeZone`
   - Represents a geographic region such as `Asia/Kolkata` or `Europe/Paris`
   - Contains full DST rules

2. `ZoneOffset` 
   - Represents a fixed offset such as `+05:30` or `-02:00`
   - Does **NOT** handle Daylight Saving Time (DST)
   - Useful when you want only the numeric offset, not the full timezone rules

3. `ZonedDateTime`
   - Represents **date + time + full timezone information**
   - Example: `2007-12-03T10:15:30+01:00[Europe/Paris]`
   - **DST-aware** → recommended for displaying date/time to users

4. `OffsetDateTime`
   - Represents **date + time + fixed offset** 
   - No geographic region included
   - Example: `2007-12-03T10:15:30+01:00`
   - **Preferred for storing timestamps in databases**
  
       (because offset is fixed and unambiguous)

## Coding Example: TimeZoneExample
### Printing All Zone IDs
```java
printAllZones();
```

**Explanation:** 
- This prints all available time-zone IDs.

**Output**
```java
Pacific/Pago_Pago (-11:00) 
Pacific/Samoa (-11:00) 
Pacific/Niue (-11:00) 
US/Samoa (-11:00)
...
```

---

### Working with ZoneId and ZonedDateTime
#### Time in India
```java
ZoneId india = ZoneId.of("Asia/Kolkata");
ZonedDateTime indiaDateTime = ZonedDateTime.now(india);
System.out.println("Time in India now : " + indiaDateTime);
```

**Explanation:**
- `ZoneId.of("Asia/Kolkata")` loads the full timezone definition for India.
- `ZonedDateTime.now(india)` gives the exact current time with offset + DST details

**Output**
```java
Time in India now : 2025-12-09T05:39:04.384004400+05:30[Asia/Kolkata]
```

---

#### Convert India time → Paris time (DST-aware)
```java
ZonedDateTime parisZonedDateTime = indiaDateTime.withZoneSameInstant(ZoneId.of("Europe/Paris"));
System.out.println("Time in Paris now : " + parisZonedDateTime);
```

**Explanation:**
- `withZoneSameInstant()` keeps the _same moment in time_
- but converts it according to Paris timezone rules (including DST).

**Output**
```java
Time in Paris now : 2025-12-09T01:09:04.384004400+01:00[Europe/Paris]
```

---

### Using ZoneOffset and OffsetDateTime
#### Fixed offset (+05:30) time
```java
ZoneOffset zoneOffSet = ZoneOffset.of("+05:30");
OffsetDateTime offsetDateTime = OffsetDateTime.now(zoneOffSet);
System.out.println("Time in India now using offset : " + offsetDateTime);
```

**Explanation:**
- This does NOT consider DST.
- It simply applies a fixed `+05:30` offset.

**Output**
```java
Time in India now using offset : 2025-12-09T05:39:04.387005+05:30
```

---

#### Convert +05:30 → +01:00 offset
```java
OffsetDateTime targetOffsetDateTime = offsetDateTime.withOffsetSameInstant(ZoneOffset.of("+01:00"));
System.out.println("Time in Paris now using offset : " + targetOffsetDateTime);
```

**Explanation:**
- Converts time by keeping the same instant but using a different numeric offset.

**Output**
```java
Time in Paris now using offset : 2025-12-09T01:09:04.387005+01:00
```

---

### Comparing `ZonedDateTime` vs `OffsetDateTime`
```java
ZonedDateTime dateTime1 = ZonedDateTime.now(ZoneId.of("America/New_York"));
OffsetDateTime dateTime2 = OffsetDateTime.now(ZoneOffset.of("-05:00"));
System.out.println(dateTime1);
System.out.println(dateTime2);
System.out.println(dateTime2.toEpochSecond() - dateTime1.toEpochSecond());
```

**Explanation:**
- `dateTime1`: Uses full DST rules for New York
- `dateTime2`: Uses fixed `-05:00` offset
- If they represent the same moment, epoch seconds difference = 0

**Output**
```java
2025-12-08T19:09:04.387005-05:00[America/New_York]
2025-12-08T19:09:04.387005-05:00
0
```

---

### Adding Months — DST Effect
```java
ZonedDateTime dateTimePlus1 = dateTime1.plusMonths(6);
OffsetDateTime dateTimePlus2 = dateTime2.plusMonths(6);
System.out.println(dateTimePlus1);
System.out.println(dateTimePlus2);
System.out.println(dateTimePlus2.toEpochSecond() - dateTimePlus1.toEpochSecond());
```

**Explanation:**
- New York timezone enters Daylight Saving Time (DST) → changes from `-05:00` to `-04:00`
- OffsetDateTime stays fixed at `-05:00`
- The difference becomes **1 hour (3600 seconds).**

**Output**
```java
2026-06-08T19:09:04.387005-04:00[America/New_York]
2026-06-08T19:09:04.387005-05:00
3600
```

---

### Converting LocalDateTime → ZonedDateTime
```java
LocalDateTime ldt = LocalDateTime.of(2000, 6, 16, 12, 30, 0);
ZonedDateTime parisDateTime = ldt.atZone(ZoneId.of("Europe/Paris"));
System.out.println("Depart : " + parisDateTime);
```

**Explanation:**
- `atZone()` attaches a timezone to a _timezone-less_ `LocalDateTime`.

**Output**
```java
Depart : 2000-06-16T12:30+02:00[Europe/Paris]
```

---

### Creating OffsetDateTime from LocalDateTime
```java
ZoneOffset asiaKolkata = ZoneOffset.of("+05:30");
LocalDateTime dateTime = LocalDateTime.of(2014, Month.MARCH, 18, 13, 45);
OffsetDateTime dateTimeInKolkata = OffsetDateTime.of(dateTime, asiaKolkata);
System.out.println("Given time in Kolkata : " + dateTimeInKolkata);
```

**Explanation:**
- Combines LocalDateTime with a fixed offset into a complete timestamp.

**Output**
```java
Given time in Kolkata : 2014-03-18T13:45+05:30
```

---

### Alternative Calendar Systems (ISO + 4 others)

Java supports 5 calendar systems:
- ISO (default)
- Hijrah (Islamic)
- Japanese
- Thai Buddhist
- Minguo (Taiwan)

```java
HijrahDate todayIslamic = HijrahDate.now();
System.out.println("Islamic date for today : " + todayIslamic);
```

**Explanation:**
- Represents today's date in the Islamic lunar calendar.

**Output**
```java
Islamic date for today : Hijrah-umalqura AH 1447-06-17
```

---
