# Default Method in Interfaces (Java 8)

When Java team decided to provided lot of features that supports lambda, functional
programming by updating the collections framework, they got a problem. If they add new
abstract methods inside the interfaces/abstract classes all the classes implementing them has
to updated as per the requirements and this will effect all the teams using Java.
• To overcome this and provide backward compatibility even after adding new features inside
Interfaces, Java team allowed concrete method implementations inside Interfaces which are
called as default methods.
• Default methods are also known as defender methods or virtual extension methods.
• Just like regular interface methods, default methods are also implicitly public.
• Unlike regular interface methods, default methods will be declared with default keyword at the
beginning of the method signature along with the implementation code.

Sample default method inside an Interface,
public interface ArithmeticOperation {
default void method1() {
System.out.println("This is a sample default method inside
Interface");
}
}
• Interface default methods are by-default available to all the implementation classes. Based on
requirement, implementation class can use these default methods with default behavior or can
override them.
• We can’t override the methods present inside the Object class as default methods inside a
interface. The compiler will throw errors if we do so.
• We can’t write default methods inside a class. Even in the scenarios where we are overriding
the default keyword should not be used inside the class methods.

The most typical use of default methods in interfaces is to incrementally provide additional
features/enhancements to a given type without breaking down the implementing classes.
• What happens when a class implements multiple Interfaces which has similar default methods
defined inside them?
public interface A {
default void m1() { // }
}
public interface B {
default void m1() { // }
}
public class C implements A,B {
??????
}
✓ This will create ambiguity to the compiler and it will
throw an error. We also call it as Diamond problem.
✓ To solve it we must provide implementation of method
m1() inside your class either with your own logic or by
invoking one of the interface default method.
@Override
public void m1() {
// Custom implementation OR
// A.super.m1() OR
// B.super.m1() OR
}

To remove ambiguioty -> A(interface), 

INTERFACE WITH D EFAULT METHOD S Vs AB STRACT CLASS

Interface with default

Interfaces with default methods can’t have a
constructor, state and behavior
There is no chance for creating instance variables
Static and instance blocks are not allowed
They can be used to write lambda expressions if
they have only abstract method inside them
Inside them we can’t override Object class
methods

ABSTRACT CLASS

Abstract classes can have a constructor, state and
behavior
Instance variables can be created inside abstract
classes
Static and instance blocks are allowed
Can’t be leveraged to write lambda expressions
Inside them we can override Object class methods

Coding example
```java
public default void autoPilot() {
System.out.println("I will help in driving with out manual support");
}
```
implicitly public
followed by default. 
After implementing this new feature, the class can do two things: 
- ignore the default method and continue to use this default method
- override this default methjod with their own logic 
This provides backward compatibility while also giving time to roll off new features without affecting the subclasses

```java
@Override
public void autoPilot() {
    System.out.println("Honda Auto pilot applied");
}
```
overrides the default method
