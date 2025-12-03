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

# Anonymous Inner Class vs Lambda Expression
This example demonstrates how the same behavior can be implemented using:
1. Anonymous Inner Class (pre–Java 8 style)
2. Lambda Expression (Java 8+ functional style)

---

### Functional Interface: ArithmeticOperation
```java
@FunctionalInterface
public interface ArithmeticOperation {

	public int performOperation(int a, int b);
	
	public default void performAdd(int a, int b) {
		System.out.println(a + b);
	}

	public static void printTheInput(int res) {
		System.out.println(res);
	}

}
```

### Usage Example

```java
public static void main(String[] args) {
    int firstInt = 10, secondInt = 6;

    ArithmeticOperation oldsum = new ArithmeticOperation() {
        @Override
        public int performOperation(int a, int b) {
            return a + b;
        }
    };
    System.out.println(
            "The sum of two input integers with out lambda is : " + oldsum.performOperation(firstInt, secondInt));

    ArithmeticOperation sum = (a, b) -> a + b;
    ArithmeticOperation multi = (a, b) -> a * b;
    ArithmeticOperation sub = (a, b) -> a - b;
    
    System.out.println("The sum of two input integers is : " + sum.performOperation(firstInt, secondInt));
    System.out.println(
            "The multiplication of two input integers is : " + multi.performOperation(firstInt, secondInt));
    System.out.println("The subtraction of two input integers is : " + sub.performOperation(firstInt, secondInt));

}
```

**Output**

```java
The sum of two input integers with out lambda is : 16
The sum of two input integers is : 16
The multiplication of two input integers is : 60
The subtraction of two input integers is : 4
```

### Explanation
**Anonymous Inner Class**

You create an object of an interface using the `new` keyword and **provide the method implementation inline**, _without creating a separate class._

**Lambda Expression**

You pass **behavior directly**, without creating a class or using the `new` keyword.
A lambda is essentially a **shorter, cleaner way** to implement the single abstract method of a functional interface.

---

Anonymous Inner Class vs Lambda Expression

|Feature | 	Anonymous Inner Class                                                                                     | 	Lambda Expression                                                   | 
| -------|------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
|What it is	| A class without a name                                                                                     | 	A method without a name (anonymous function)                        |
|Interfaces supported	| Can implement interfaces with multiple abstract methods	                                                   | Works only with Functional Interfaces (one abstract method)          |
|Can extend classes?	| Yes — can extend both abstract and concrete classes                                                        | 	No — lambdas cannot extend any class                                |
|Variable support| 	Can declare instance variables                                                                            | 	Only local variables allowed inside lambda body                     |
|Meaning of this| 	Refers to the anonymous inner class object	                                                               | Refers to the outer/enclosing class                                  |
|Memory allocation	| Object created on heap each time                                                                           | 	Stored in Method Area (as a single instance), more memory-efficient |
|Verbosity	| Verbose and boilerplate-heavy                                                                              | 	Short, clean, and readable                                          |
|Use case| When multiple methods or state is needed| 	When implementing a single abstract method (Functional Interface)   |

---

