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

