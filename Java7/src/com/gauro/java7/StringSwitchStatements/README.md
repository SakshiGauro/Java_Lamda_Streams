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
