# Default Method in Interfaces (Java 8)

### Why Default Methods Were Introduced

Before Java 8:
- Interfaces could only contain **abstract methods.**
- Adding a new abstract method to an interface would break **all** implementing classes.
- This was a big problem when updating the Collections API to support **lambda expressions** and **streams**.

Java 8 solved this with **default methods**, which allow concrete method implementations **inside interfaces.**

---

### What Are Default Methods?

- Methods in an interface that have a **default implementation.**
- Declared using the `default` keyword.
- Also called:
  - _Defender methods_
  - _Virtual extension methods_
- They provide **backward compatibility** without forcing all implementing classes to change.

---

### Syntax

Sample default method inside an Interface

```java
public interface ArithmeticOperation {
    default void method1() {
        System.out.println("This is a sample default method inside Interface");
    }
}
```

- Default methods are implicitly `public`.
- Implementing classes can:
  - Inherit them as-is
  - Override them

---

### Rules & Restrictions

#### Allowed
- Default methods **inside interfaces**
- Implementing classes may override default methods.

#### Not Allowed
- You **cannot** write a default method inside a class.
- You **cannot** override `Object` class methods (like `toString()`) as default methods.
- Interfaces still **cannot have instance variables.**
- They cannot have constructors or instance initialization blocks.

The most typical use of default methods in interfaces is to incrementally provide additional features/enhancements to a given type without breaking down the implementing classes.

---

### Multiple Inheritance and the Diamond Problem

What happens if two interfaces define the same default method?

```java
public interface A {
    default void m1() { // }
}
public interface B {
    default void m1() { // }
}
public class C implements A,B {
    // ERROR: m1() is ambiguous
}
```

#### How to Fix

You MUST override the method in your class:

```java
@Override
public void m1() {
    // Option 1: custom logic
    System.out.println("Custom implementation");

    // Option 2: choose a specific interface
    A.super.m1();
    // or
    B.super.m1();
}
```

### Default Methods vs Abstract Classes

|Feature |	Interface with Default Methods |	Abstract Class|
| --------| ------------------|------------|
| Constructors | Not allowed | Allowed |
| Instance variables|	Not allowed| Allowed|
|Static/Instance blocks| Not allowed| Allowed|
|Multiple inheritance	|Allowed| Not allowed|
|Can override Object methods| No|	Yes|
|Use in lambdas| Only if single abstract method|Cannot be used|

### Coding example: Honda, Vehicle
#### Vehicle Interface
```java
public interface Vehicle {

    int getSpeed();

    void applyBreak();

    default void autoPilot() {
        System.out.println("I will help in driving without manual support");
    }

    public static void sayHello() {
        System.out.println("Hi, This is your favourite car");
    }

    public static void main(String[] args) {
        System.out.println("Running from static method inside interface");
    }
}
```

#### Class Implementing the Interface: Honda
```java
/**
 * 
 */
package com.gauro.java8.DefaultMethodInterfaces;

/**
 * @author EazyBytes
 *
 */
public class Honda implements Vehicle {

	@Override
	public int getSpeed() {
		return 100;
	}

	@Override
	public void applyBreak() {
		System.out.println("Breaks applied");
	}
	
	@Override
	public void autoPilot() {
		System.out.println("Honda Auto pilot applied");
	}

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		Honda honda = new Honda();
		honda.applyBreak();
		honda.autoPilot();
		Vehicle.sayHello();
		Honda.sayHello();
	}
	
	private static void sayHello() {
		System.out.println("Hi, This is your favourite honda car");
	}
}

```
When the `Vehicle` interface introduces the new `autoPilot` feature as a default method, the `Honda` class has **two options:**
- Use the **default implementation** without making any changes.
- **Override the default method** and provide its own custom behavior.

This approach preserves **backward compatibility**, allowing existing classes to continue working as is while still enabling new features to be added to interfaces without breaking existing implementations.

---