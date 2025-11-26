# Using String in Switch Statements

Before Java 7, switch statements allows only Enum and int types.
• From Java 7, Java allows to use String objects in the expression of switch statement.
• String value is case sensitive and null objects are not allowed. In case if you use null value, java
will throw an NullPointerException.
• It must be only String object and normal Object is not allowed
switch (input)
{
case (“Monday”):
System.out.println(“Today is Monday");
break;
default:
System.out.println(“Today is not a Monday");
}

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

Output
```java
Today is Wednesday
```

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
use the case logic together to reduce redundant code

```java
Today is Weekend
```