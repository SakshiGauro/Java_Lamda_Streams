# Lambda Expression

Java was designed in the 1990s as an object-oriented programming language, when objectoriented programming was the principal paradigm for software development. Recently,
functional programming has risen in importance because it is well suited for concurrent and
event-driven (or “reactive”) programming. That doesn’t mean that objects are bad. Instead, the
winning strategy is to blend object-oriented and functional programming.
• The main objective of Lambda Expression which is introduced in Java 8 is to bring benefits of
functional programming into Java.
• A “lambda expression” is a block of code that you can pass around so it can be executed later,
once or multiple times. It is an anonymous (nameless) function. That means the function which
doesn’t have the name, return type and access modifiers.
• It enable to treat functionality as a method argument, or code as data.
• Lambda has been part of Java competitive languages like Python, Ruby already

@FunctionalInterface
interfaces with only one abstract method. but any number of static and defauylt methods

# Examples of Lambda programming
✓ public void printHello() { () -> {
System.out.println(“Hello”); =====➔ System.out.println(“Hello”);
} }
✓ public void printHello() {
System.out.println(“Hello”); =====➔ () -> System.out.println(“Hello”);
}
Note: When we have a single line of code inside your lambda method, we can remove the {}
surrounding it to make it more simple.

lambda -> anonymous methods with no names, access modifiers and data parameters. This is possible due to FunctionalInterface. 

```java
public void printHello();
```
public method with void return type and no parameters

Once the interface is implemented, we can overide the method using the lambda function 

removing curly brackets {} is ok as long as the code is in a single line

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
object refernce of the interface
VoidMethodWithNoParams method holds the behavior of what i deifne which is a print statement System.out.println("Method with no return and input params");
can write any number of business logic using a single funtional interface abstract method aka method1. 

**Output**
```java
Method with no return and input params
Ignoring {} since we have only 1 line
```

Example Two: single input param and return type

```java
@FunctionalInterface
public interface VoidMethodWithOneParam {

	public void printInput(String input);
	
}
```
has one inoput param with the datatype akak String

Examples of Lambda programming
✓ public void printInput(String input) { (input) -> {
System.out.println(input); =====➔ System.out.println(input);
} }
✓ public void printInput(String input) {
System.out.println(input); =====➔ input -> System.out.println(input);
}
Note: When we have a single input parameter inside your lambda method, we can remove the ()
surrounding it to make it more simple.

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
toLowerCase and toUpperCase change the case of the input

Output
```java
Hello
eazy bytes
WELCOME
```

More than one  input param

```java
@FunctionalInterface
public interface VoidMethodWithTwoParams {

	public void calculateAndPrint(int a, int b);
	
}
```

Examples of Lambda programming
✓ public void add(int a, int b) { (int a, int b) -> {
int res = a+b; int res = a+b;
System.out.println(res); =====➔ System.out.println(res);
} }
✓ public void add(int a, int b) { (a, b) -> {
int res = a+b; int res = a+b;
System.out.println(res); =====➔ System.out.println(res);
} }
Note: The compiler can detect the input parameters data type based on the abstract method. But
you can still mention them inside your lambda code and these are optional in nature.

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

Output
```java
7
10
```

return statements

```java
@FunctionalInterface
public interface ReturnMethodWithTwoParams {

	public int calculateAndReturn(int a, int b);
	
}
```
Examples of Lambda programming
✓ public int add(int a, int b) {
int res = a+b;
return res; =====➔ (a, b) -> return a+b;
}
✓ public int add(int a, int b) {
int res = a+b;
return res; =====➔ (a, b) -> a+b;
}
Note: If we have a single line of code inside your lambda method then return keyword is optional.
We can remove it and compiler can interpret that the outcome of the statement should be return.

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

Output
```java
7
10
20
```

Lambda expressions are used heavily inside the Collections, Streams libraries from Java 8. So it
is very important to understand them.
• Java Lambda Expression Syntax,
(argument-list) -> {body}
• With the help of Lambda expressions we can reduce length of the code, readability will be
improved and the complexity of anonymous inner classes can be avoided.
• We can provide Lambda expressions in the place of object and method arguments.
• In order to write lambda expressions or code we need Functional interfaces.

Lambda expressions can use variables defined in an outer scope. They can capture static
variables, instance variables, and local variables, but only local variables must be final or
effectively final.
• A variable is final or effectively final when it's initialized once and is never mutated in its owner
class; we can't initialize it in loops or inner classes.
✓ Inside lambda code or blocks, we can’t modify the local
variables present outside the lambda blocks.
✓ There is a reason for this restriction. Mutating variables
in a lambda expression is not thread safe.
✓ But we can update the static or member variables
present inside the class. Because they stored on the
heap, but local variables are on the stack. Because
we're dealing with heap memory, the compiler can
guarantee that the lambda will have access to the
latest value always.

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
using `this` statement to differentiate variables in classes and lambda expersiions
 
Output
```java
The value of sum inside lambda is: 0
The sum of given 2 numbers is: 30
```

Anonymous Class

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

create an object of an interface using new operator, passing a behavior without initializing a class

output



