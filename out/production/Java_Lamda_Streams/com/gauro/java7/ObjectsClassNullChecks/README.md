# Objects Class and Null Checks

Java 7 introduced a new class “java.util.Objects” consists of utility static methods for operating
on objects. This methods include null checks, computing hash code, comparing two objects,
returning a string for an object.
• Importantly the Objects class has the below 2 methods to null-check the object. Both of them
will throw NullPointerException if the given object is null and the custom message also can be
passed to display on the NullPointerException details.
✓ requireNonNull(T obj)
✓ requireNonNull(T obj, String message)
• It may look for the developers why I should use these methods as if the object is null anyways
the NullPointerException will be thrown by the code. But these methods provides controlled
behavior, easier debugging.

```java
private static void processPersonDetails(Person person) {
    Objects.requireNonNull(person, "Person object can't be null");
    System.out.println(person.getFirstName());
    System.out.println(person.getLastName());
}
```

Better readability
