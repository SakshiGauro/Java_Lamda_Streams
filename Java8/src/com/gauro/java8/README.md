

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


