# Using String in Switch Statements

Before Java 7, the `switch` statement only supported:
- `int`
- `Enum`
- `char`
- `byte`
- `short`

Starting from **Java 7**, developers can use **String objects** inside `switch` expressions.

**Key Points**
- You can now use **String** in `switch` statements.
- **Case-sensitive** comparisons.
- **Null values are NOT allowed** — using a `null` String will cause a `NullPointerException`.
- Only **String type** is allowed. You cannot use a plain `Object`.

---

## Code Example: SwitchWithString
### Example 1: Basic String Switch

```java
private static void displayTodayDetails() {
    String input = "Wednesday";
    switch (input) {
    case "Monday":
        System.out.println("Today is Monday");
        break;
    case "Tuesday":
        System.out.println("Today is Tuesday");
        break;
    case "Wednesday":
        System.out.println("Today is Wednesday");
        break;
    case "Thursday":
        System.out.println("Today is Thursday");
        break;
    case "Friday":
        System.out.println("Today is Friday");
        break;
    case "Saturday":
        System.out.println("Today is Saturday");
        break;
    default:
        System.out.println("Today is Sunday");
    }
}
```

### Output
```java
Today is Wednesday
```

### Example 2: Combining Multiple Case Labels

You can combine case labels to reduce redundant code:

```java
private static void displayWeekDetails() {
    String input = "Saturday";
    switch (input) {
    case "Monday": case "Tuesday": case "Wednesday": case "Thursday": case "Friday":
        System.out.println("Today is Weekday");
        break;
    case "Saturday": case "Sunday":
        System.out.println("Today is Weekend");
        break;
    default:
        System.out.println("Today is Holiday");
    }
}
```

### Output

```java
Today is Weekend
```

---