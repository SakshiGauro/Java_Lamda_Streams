# Static Method in Interfaces

Starting from **Java 8**, interfaces can contain **static methods** in addition to abstract and default methods. This addition allows interfaces to provide related utility functionality without relying on external helper classes.

### Key Points
#### Static Methods Allowed in Interfaces

Java 8 introduced static methods inside interfaces just like those in classes. They are useful for grouping utility logic related to the interface.

#### Static Methods Are Not Inherited by Implementing Classes

Static methods **do not belong to an instance**, so they are **not inherited** by the implementing class.
To call a static method in an interface, use the **interface name:**

```java
A.sayHello();
```

#### Same Name in Class ≠ Overriding

Static methods **cannot be overridden.**
If a class has a static method with the same name and signature, it is simply another method—not an override.

**Example:**

_Vehicle Interface:_
```java
public interface Vehicle {
    public static void sayHello() {
        System.out.println("Hi, This is your favourite car");
    }
}
```

_Honda Class:_

```java
public class Honda implements Vehicle {
    private static void sayHello() {
        System.out.println("Hi, This is your favourite honda car");
    }
}
```

_Using them:_

```java
Vehicle.sayHello(); // calls interface method
Honda.sayHello();   // calls class method
```

#### Main Method Inside Interfaces

Since interfaces can now have static methods, you can also write a **main method** inside an interface and execute it directly:

```java
public static void main(String[] args) {
    System.out.println("Running from static method inside interface");
}
```

---
