# Lambda Expression

Java was originally designed as a purely **object-oriented** language in the 1990s. As software trends shifted toward **concurrent**, **event-driven**, and **reactive** systems, functional programming concepts grew in importance.
Java 8 introduced lambda expressions to blend functional programming into Java's Object-Oriented ecosystem.

### What Is a Lambda Expression?

A **lambda expression** is:
- A block of code you can **pass around** (like a function in Python/Ruby).
- An anonymous function → no name, no return type, no access modifier.
- A way to treat behavior as data, allowing you to pass methods as arguments.
- Enabled by Functional Interfaces (interfaces with exactly one abstract method).

### Functional Interfaces

A functional interface must contain exactly **one abstract method**, but can have any number of:
- `default` methods
- `static` methods

**Example**
```java
@FunctionalInterface
public interface Printer {
    void print();
}
```

This single abstract method is what the lambda expression represents.

---

## Lambda Syntax Simplification
|Traditional Method	| Lambda Version        |
|--------	|-----------------------|
|`public void hello() { System.out.println("Hello"); }`	| `() -> System.out.println("Hello")`|
|`public void print(String s)`	| `s -> System.out.println(s)`|
|`public int sum(int a, int b)`	| `(a, b) -> a + b`|
	
### Rules
- Curly braces `{}` optional if the body is a single line.
- Parentheses `()` around parameters optional if there is exactly one parameter.
- `return` is optional for single-expression bodies.

---

## Example 1: No Parameter, No Return Type

### Functional Interface: VoidMethodWithNoParams

```java
@FunctionalInterface
public interface VoidMethodWithNoParams {
	public void printHello();
}
```

### Example Usage Class: 
```java
private static void voidMethodWithNoParams() {

    VoidMethodWithNoParams method = () -> {
        System.out.println("Method with no return and input params");
    };

    VoidMethodWithNoParams method1 = () -> System.out.println("Ignoring {} since we have only 1 line");

    method.printHello();
    method1.printHello();
}
```
- `method` -> assigning a lambda function to the interface reference method
- `method.printHello()` executes the code **inside the lambda**

**Output**
```java
Method with no return and input params
Ignoring {} since we have only 1 line
```

## Example Two: One Parameter, No Return

### Functional Interface: VoidMethodWithOneParam

```java
@FunctionalInterface
public interface VoidMethodWithOneParam {

	public void printInput(String input);
	
}
```

One input param with the datatype _String_

### Example Usage Class:

```java
private static void voidMethodWithOneParam() {
    VoidMethodWithOneParam method = (input) -> {
        System.out.println(input);
    };

    VoidMethodWithOneParam method1 = (input) -> System.out.println(input.toLowerCase());

    VoidMethodWithOneParam method2 = input -> System.out.println(input.toUpperCase());

    method.printInput("Hello");
    method1.printInput("Eazy Bytes");
    method2.printInput("Welcome");

}
```
- `toUpperCase` `toLowerCase`-> changes the case of the input

#### Lambda Expression
|Traditional Method	| Lambda Version                          |
|--------	|-----------------------------------------|
|`public void printInput(String input) { System.out.println(input); }`	| `input ->  System.out.println(input); ` |

**Output**
```java
Hello
eazy bytes
WELCOME
```

## Example 3: Two Parameters, No Return

### Functional Interface: VoidMethodWithTwoParams

```java
@FunctionalInterface
public interface VoidMethodWithTwoParams {

	public void calculateAndPrint(int a, int b);
	
}
```

### Example Usage Class:

```java
private static void voidMethodWithTwoParams() {
    VoidMethodWithTwoParams addition = (a, b) -> {
        System.out.println(a + b);
    };

    VoidMethodWithTwoParams multiplication = (a, b) -> System.out.println(a * b);

    addition.calculateAndPrint(5, 2);
    multiplication.calculateAndPrint(5, 2);

}
```
> **Note:** The compiler can detect the input parameters data type based on the abstract method. But you can still mention them inside your lambda code and these are optional in nature.

**Output**
```java
7
10
```

## Example 4: Two Parameters, With Return Type

### Functional Interface: ReturnMethodWithTwoParams
```java
@FunctionalInterface
public interface ReturnMethodWithTwoParams {

	public int calculateAndReturn(int a, int b);
	
}
```

### Example Usage
```java
private static void returnMethodWithTwoParams() {
    ReturnMethodWithTwoParams addition = (a, b) -> {
        return (a + b);
    };

    System.out.println(addition.calculateAndReturn(5, 2));

    ReturnMethodWithTwoParams multiply = (a, b) -> {
        return (a * b);
    };

    System.out.println(multiply.calculateAndReturn(5, 2));

    ReturnMethodWithTwoParams division = (a, b) -> a / b;

    System.out.println(division.calculateAndReturn(100, 5));

}
```
> **Note:** If we have a single line of code inside our lambda method then `return` keyword is optional.
We can remove it and compiler can interpret that the outcome of the statement should be return.

**Output**
```java
7
10
20
```
---

## Lambda Complex Example 

Lambda expressions are used extensively in Java’s Collections and Streams APIs (introduced in Java 8). Understanding how they work is essential for writing modern, clean, and concise Java code.

**Lambda Syntax**
```java
(argument-list) -> {body}
```

### Benefits of Lambda Expressions

- Reduce boilerplate code.
- Improve readability.
- Replace anonymous inner classes with clean, concise syntax.
- Can be passed as method arguments or stored as variables.
- Require a **Functional Interface**, i.e., an interface with exactly one abstract method.

#### Variable Capture in Lambdas

Lambda expressions can access variables from their surrounding scope. These include:
- Static variables
- Instance variables
- Local variables (but only if they are _final_ or _effectively final_)

**Why Local Variables Must Be Final/Effectively Final?**

Local variables live on the **stack**, while lambdas may execute later on the **heap**.

To ensure thread safety and consistency, Java forbids mutating local variables inside lambda expressions.

**Key Rules**
- Lambdas **cannot modify** local variables outside their block.
- Lambdas **can modify** instance variables and static variables.
- This is allowed because instance/static variables live on the heap.


### Coding Example: AnanymousVsLambda

```java
int sum = 0;
public void sum() {
    int tempSum = 0;
    ArithmeticOperation sumOperation = (a,b)-> {
        int sum = 0;
        // tempSum = 0; //Compilation error
        this.sum = a+b;
        System.out.println("The value of sum inside lambda is: "+sum);
        return this.sum;
    };
    System.out.println("The sum of given 2 numbers is: "+sumOperation.
            performOperation(10, 20));
}
```
**Why `this` Is Needed Here?**

`this.sum` refers to the **instance variable** of the class.
The local variable `sum` inside the lambda shadows the class variable, so `this` clarifies which one you're using.

**Output**
```java
The value of sum inside lambda is: 0
The sum of given 2 numbers is: 30
```
---