# Static Method in Interfaces

From Java 8, just like we can write default methods inside interfaces, we can also write static
methods inside them to define any utility functionality.
• Since static methods don't belong to a particular object, they are not available to the classes
implementing the interface, and they have to be called by using the interface name preceding
the method name.
• Defining a static method within an interface is similar to defining one in a class.
• Static methods in interfaces make possible to group related utility methods, without having
to create artificial utility classes that are simply placeholders for static methods.
• Since interface static methods by default not available to the implementation class,
overriding concept is not applicable.
• Based on our requirement we can define exactly same method in the implementation class,
it’s valid but not overriding.

public interface A {
public static void sayHello() {
System.out.println("Hi, This is a static method inside Interfaces");
}
}
public class B implements A {
private static void sayHello() {
System.out.println("Hi, This is a static method inside class");
}
public static void main(String[] args) {
B b = new B();
b.sayHello();
B.sayHello();
A.sayHello();
}
}
✓ Since static methods are allowed from Java 8, we
can write a main method inside an interface and
execute it as well.

If i want to use the static method inside the interface, i have to call it using the interface name aka A.sayHello();

code Example

```java
public static void sayHello() {
    System.out.println("Hi, This is your favourite car");
}
```

in honda, same method name and signature
```java
private static void sayHello() {
    System.out.println("Hi, This is your favourite honda car");
}
```

Vehicle.sayHello(); -> 
coming from interface 
Hi, This is your favourite car

Honda.sayHello();
coming from class
Hi, This is your favourite honda car

