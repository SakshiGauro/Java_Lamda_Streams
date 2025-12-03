# BI FUNCTIONAL INTERFACES

As of now we have see the functional interfaces which will accept only 1 parameter as input
but what if we have a need to send 2 input parameters. To address the same Java has Bi
Functional interfaces.
• java.util.function.BiPredicate<T, U> – Similar to Predicate but it can accept 2 input
parameters and return a boolean value
• @param `<T>` the type of the first argument to the predicate
• @param `<U>` the type of the second argument the predicate
• java.util.function.BiFunction<T, U, R> – Similar to Function but it can accept 2 input
parameters and return a output as per the data type mentioned.
• @param `<T>` the type of the first argument to the function
• @param `<U>` the type of the second argument to the function
• @param `<R>` the type of the result of the function

java.util.function.BiConsumer`<T, U>` – Similar to Consumer but it can accept 2 input
parameters and no return value same as Consumer
• @param <T> the type of the first argument to the operation
• @param <U> the type of the second argument to the operation
• There is no BiSupplier for Supplier functional interface as it will not accept any input
parameters.

## B INARY OPERATOR F UNCTIONAL INTERFACE

java.util.function.BinaryOperator<T>
• BinaryOperator<T> is a child of BiFunction<T,U,R> .We will use this in the scenarios where the
2 input parameters and 1 return parameter data types is same.
• @param <T> the type of the operands and result of the operator
• In other words we can say that BinaryOperator takes two arguments of the same type and
returns a result of the same type of its arguments.
• In addition to the methods that it inherits from BiFunction<T,U,R>, it also has 2 utility static
methods inside it. They both will be used to identify the minimum or maximum of 2 elements
based on the comparator logic that we pass,
• static <T> BinaryOperator<T> minBy(Comparator<? super T> comparator)
• static <T> BinaryOperator<T> maxBy(Comparator<? super T> comparator)

# Coding Example: BinaryOperatorExample

```java
// Creating a BinaryOperator
BinaryOperator<String> appendAndConvert = (word1, word2) -> (word1 + word2).toUpperCase();

// Calling BinaryOperator method
System.out.println("The updated value after appending and converting is : "
+ appendAndConvert.apply("Hello ", "Eazy Bytes Students"));
```
two inputs and return type of the same datatype String


Two Static methods in BinaryOperator: maxBy and minBy. Both accpe4t Comparator


```java
BinaryOperator<Integer> maxOperation = BinaryOperator.maxBy((a, b) -> (a > b) ? 1 : ((a == b) ? 0 : -1));
System.out.println("The largest number is: "+maxOperation.apply(16, 30));

BinaryOperator<Integer> minOperation = BinaryOperator.minBy((a, b) -> (a > b) ? 1 : ((a == b) ? 0 : -1));
System.out.println("The smallest number is: "+minOperation.apply(16, 30));

```

---

# PRIMITIVE TYPE F UNCTIONAL INTERFACES

All the functional interfaces like Predicate, Function, Consumer that we discussed previously
accepts or returns only Object type values like Integer, Double, Float, Long etc.
• There is a performance problem with this. If we pass any primitive input values like int, long,
double, float Java will auto box them in order to convert them into corresponding wrapper
objects. Similarly once the logic is being executed Java has to convert them into primitive
types using unboxing.
• Since there is lot of auto boxing and unboxing happening it may impact performance for
larger values/inputs. To overcome such scenarios Java has primitive type functional interfaces
as well.

![img.png](img.png)

# Primitive data vs Wrapper object
In Java, primitive data types and wrapper classes serve to store values, but they differ fundamentally in their nature and capabilities.
Primitive Data Types:
Primitive data types are fundamental building blocks in Java, representing basic values directly. They are not objects and are stored directly in memory, typically on the stack.
Examples: byte, short, int, long, float, double, char, boolean.
Characteristics:
Directly store values.
Cannot be null.
More memory-efficient and performant than objects.
Cannot be used in Java Collections Framework (like ArrayList, HashMap) directly, as these frameworks require objects.
Wrapper Classes:
Wrapper classes provide object representations for primitive data types. Each primitive type has a corresponding wrapper class. They are objects and are stored on the heap.
Examples: Byte, Short, Integer, Long, Float, Double, Character, Boolean.
Characteristics:
Encapsulate a primitive value within an object.
Can be null, as they are objects.
Consume more memory due to object overhead.
Can be used with Java Collections Framework and other object-oriented features.
Provide utility methods for converting between primitive types and strings, and for performing other operations.
Support Autoboxing (automatic conversion from primitive to wrapper object) and Unboxing (automatic conversion from wrapper object to primitive).
Key Differences Summarized:
Feature
Primitive Type
Wrapper Class
Type
Not an object
Object
Storage
Stack
Heap
Null Value
Cannot be null
Can be null
Memory/Performance
More efficient
Less efficient
Collections
Cannot use directly
Can use directly

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.IntPredicate – Always accepts int as input
boolean test(int value);
✓ java.util.function.DoublePredicate – Always accepts double as input
boolean test(double value);
✓ java.util.function.LongPredicate – Always accepts long as input
boolean test(long value);
✓ java.util.function.IntFunction<R> - Always accepts int as input and return any type as output
R apply(int value);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.DoubleFunction<R> - Always accepts double as input and return any type as output
R apply(double value);
✓ java.util.function.LongFunction<R> - Always accepts long as input and return any type as output
R apply(long value);
✓ java.util.function.ToIntFunction<T> - Always return int value but accepts any type as input
int applyAsInt(T value);
✓ java.util.function.ToDoubleFunction<T> - Always return double value but accepts any type as input
double applyAsDouble(T value);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.ToLongFunction<T> - Always return long value but accepts any type as input
long applyAsLong(T value);
✓ java.util.function.IntToLongFunction - Always takes int type as input and return long as return type
long applyAsLong(int value);
✓ java.util.function.IntToDoubleFunction - Always takes int type as input and return double as return type
double applyAsDouble(int value);
✓ java.util.function.LongToIntFunction - Always takes long type as input and return int as return type
int applyAsInt(long value);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.LongToDoubleFunction - Always takes long type as input and return double as return
type
double applyAsDouble(long value);
✓ java.util.function.DoubleToIntFunction - Always takes double as input and return int as return type
int applyAsInt(double value);
✓ java.util.function.DoubleToLongFunction - Always takes double type as input and return long as return
type
long applyAsLong(double value);
✓ java.util.function.ToIntBiFunction - Always takes 2 input parameters of any type and return int as
return type
int applyAsInt(T t, U u);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.ToLongBiFunction - Always takes 2 input parameters of any type and return long as
return type
long applyAsLong(T t, U u);
✓ java.util.function.ToDoubleBiFunction - Always takes 2 input parameters of any type and return double
as return type
double applyAsDouble(T t, U u);
✓ java.util.function.IntConsumer - Always accepts int value as input
void accept(int value);
✓ java.util.function.LongConsumer - Always accepts long value as input
void accept(long value);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.DoubleConsumer - Always accepts double value as input
void accept(double value);
✓ java.util.function.ObjIntConsumer<T> - Always accepts 2 inputs of type int and any data type
void accept(T t, int value);
✓ java.util.function.ObjLongConsumer<T> - Always accepts 2 inputs of type long and any data type
void accept(T t, long value);
✓ java.util.function.ObjDoubleConsumer<T> - Always accepts 2 inputs of type double and any data type
void accept(T t, double value);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.IntSupplier - Always return int value as output
int getAsInt();
✓ java.util.function.LongSupplier - Always return long value as output
long getAsLong();
✓ java.util.function.DoubleSupplier - Always return double value as output
double getAsDouble();
✓ java.util.function.BooleanSupplier - Always return boolean value as output
boolean getAsBoolean();

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.IntUnaryOperator - Always accept and return int values
int applyAsInt(int operand);
✓ java.util.function.LongUnaryOperator - Always accept and return long values
long applyAsLong(long operand);
✓ java.util.function.DoubleUnaryOperator - Always accept and return double values
double applyAsDouble(double operand);

Below are the most important primitive functional interfaces provided by the Java team,
✓ java.util.function.IntBinaryOperator - Always accept 2 input parameters and return in int values
int applyAsInt(int left, int right);
✓ java.util.function.LongBinaryOperator - Always accept 2 input parameters and return in long values
long applyAsLong(long left, long right);
✓ java.util.function.DoubleBinaryOperator - Always accept 2 input parameters and return in double
values
double applyAsDouble(double left, double right);

# Coding example: PrimitiveFunctionsExample

```java
private static void problemWithNormalFunctionalInterfaces() {

    // Creating a Function
    // 1) First the input value provided will be converted to Integer using
    // AutoBoxing
    // 2) Second the input value provided to the method body will be converted to
    // int
    // using Auto UnBoxing during business logic
    // 3) Finally after business logic the return value has to be converted to
    // Integer
    // using AutoBoxing
    Function<Integer, Integer> doubleTheValue = input -> input * 2;
    
    int[] iparray = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int[] oparray = new int[iparray.length];
    
    for (int i = 0; i < iparray.length; i++) {
        oparray[i] = doubleTheValue.apply(iparray[i]);
    }
    System.out.println("The output array is: " + Arrays.toString(iparray));
    System.out.println("The output array is: " + Arrays.toString(oparray));
}
```
use boxing, unboxing and unvoxing. Performance is degraded with larger data

```java
private static void predicatePrimitiveFunctions() {
    IntPredicate checkInt = a -> a % 2 == 0;
    System.out.println("Output from IntPredicate is : " + checkInt.test(10));

    DoublePredicate checkDouble = a -> a % 2 == 0;
    System.out.println("Output from DoublePredicate is : " + checkDouble.test(10.0));

    LongPredicate checkLong = a -> a % 2 == 0;
    System.out.println("Output from LongPredicate is : " + checkLong.test(1034497756));

}
```

# METHOD REFERENCES

Sometimes, there is already a method that carries out exactly the action that you’d like to pass
on inside lambda code. In such cases it would be nicer to pass on the method instead of
duplicating the code again.
• This problem is solved using method references in Java 8. Method references are a special
type of lambda expressions which are often used to create simple lambda expressions by
referencing existing methods.
• There are 4 types of method references introduced in Java 8,
✓ Static Method Reference (Class::staticMethod)
✓ Reference to instance method from instance (objRef::instanceMethod)
✓ Reference to instance method from class type (Class::instanceMethod)
✓ Constructor Reference (Class::new)
• As you might have observed, Java has introduced a new operator :: (double colon) called as
Method Reference Delimiter.. In general, one don’t have to pass arguments to method
references.

Static Method Reference (Class::staticMethod)
✓ As you can see first we have written a
lambda expression code for the Functional
interface ‘ArithmeticOperation’ to
calculate the sum of given 2 integers.
✓ Later since we have same logic of code
present inside a static method we used
static method reference as highlighted.
✓ This way we can leverage the existing
static methods code to pass the behavior,
instead of writing lambda code again.
✓ Using method references is mostly advised
if you already have code written inside a
method or if your code inside lambda is
large(we can put in separate method).

```java
public static void staticMethodReference() {
    ArithmeticOperation operation = (a, b) -> {
        int sum = a + b;
        System.out.println("The sum of given input values using lambda is: " + sum);
        return sum;
    };
    operation.performOperation(2, 3);

    ArithmeticOperation methodRef = MethodReference::performAddition;
    methodRef.performOperation(2, 3);
}

public static int performAddition(int a, int b) {
    int sum = a + b;
    System.out.println("The sum of given input values using static method reference is: " + sum);
    return sum;
}
```

Reference to instance method from instance (objRef::instanceMethod)
✓ As you can see first we have written a
lambda expression code for the Functional
interface ‘ArithmeticOperation’ to
calculate the sum of given 2 integers.
✓ Later since we have same logic of code
present inside a method we used instance
method reference as highlighted using an
object of the class.
✓ This way we can leverage the existing
instance methods code to pass the
behavior, instead of writing lambda code
again.

```java
public static void instanceMethodObjReference() {
    ArithmeticOperation operation = (a, b) -> {
        int sum = a + b;
        System.out.println("The sum of given input values " + "using lambda is: " + sum);
        return sum;
    };
    operation.performOperation(2, 3);
    MethodReference methodRef = new MethodReference();
    ArithmeticOperation instanceMethod = methodRef::performInstanceAddition;
    instanceMethod.performOperation(2, 3);
}

public int performInstanceAddition(int a, int b) {
    int sum = a + b;
    System.out.println("The sum of given input values using instance " + "method reference is: " + sum);
    return sum;
}
```

Reference to instance method from class type (Class::instanceMethod)
✓ This type of method reference is similar to
the previous example, but without having
to create a custom object
✓ As you can see first we have written a
lambda expression code inside forEach
method to print all the list elements.
✓ Later since we have same logic of code
present inside a method of System.out, we
used instance method reference as
highlighted using class type itself.
✓ This way we can leverage the existing
methods code to pass the behavior,
instead of writing lambda code again.

```java
public static void instanceMethodWithClassName() {
    List<String> departmentList = new ArrayList<>();
    departmentList.add("Supply");
    departmentList.add("HR");
    departmentList.add("Sales");
    departmentList.add("Marketing");
    departmentList.forEach(s -> System.out.println(s));

    departmentList.forEach(System.out::println);
}
```

Constructor Reference (Class::new)
✓ Constructor references are just like
method references, except that the name
of the method is new. For example,
Product::new is a reference to a Product
constructor.
✓ As you can see we have used constructor
reference in the place of lambda code to
create a new product details using
functional interface ‘ProductInterface’.
✓ Few other examples of Constructor
reference are,
• String::new;
• Integer::new;
• ArrayList::new;
• UserDetail::new;

```java
public static void constructorReference() {
    ProductInterface productUsingLambda = (name, price) -> new Product(name, price);
    Product prodSamsung = productUsingLambda.getProduct("Samsung Galaxy", 1000);
    System.out.println(prodSamsung.toString());

    ProductInterface productUsingRef = Product::new;
    Product prodApple = productUsingRef.getProduct("Apple IPhone", 1500);
    System.out.println(prodApple.toString());
}
```
lamda expression using method reference will be initialized reagrless of using them. 
However, lamda expressionw ill not be initialized and will only stay as a behavior and definition unless used. 


