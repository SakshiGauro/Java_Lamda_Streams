# Method References

Sometimes a method already exists that performs exactly the logic you want to express in a lambda. Instead of rewriting the same logic, Java 8 allows you to reference existing methods directly using **method references**, which are essentially shorthand for simple lambda expressions.

Method references use the `::` **(double colon / Method Reference Delimiter)** operator.

They are essentially _lambda expressions pointing to existing methods_, without needing to pass arguments manually.

### Types of Method References
| Type                                 | Syntax                   | When to Use                                                                                |
| ------------------------------------ | ------------------------ | ------------------------------------------------------------------------------------------ |
| **Static Method Reference**          | `Class::staticMethod`    | When the logic is already in a static method.                                              |
| **Instance Method (via object)**     | `objRef::instanceMethod` | When you have an object instance whose method you want to reuse.                           |
| **Instance Method (via class type)** | `Class::instanceMethod`  | When the method will be called on the **object passed as argument** (common with streams). |
| **Constructor Reference**            | `Class::new`             | When your lambda simply creates a new object.                                              |

---

## Static Method Reference (Class::staticMethod)
### Coding Example: MethodReference

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

**Explanation**
- First we use a lambda to implement the addition logic. 
- Since the same logic exists in a static method `performAddition()`, we replace the lambda with a static method reference (`MethodReference::performAddition`)
- This avoids duplicate code and reuses existing logic.
- Static method references are recommended when a method already has the exact logic you want, or when the lambda becomes large and should be moved into its own reusable method.

**Output**
```java
The sum of given input values using lambda is: 5
The sum of given input values using static method reference is: 5
```

---

## Instance Method Reference Using Object (objRef::instanceMethod)
### Coding Example: MethodReference

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

**Explanation**
- A lambda is first used for addition.
- Since the same logic exists in an instance method, we reference it using an object (`methodRef::performInstanceAddition`).
- This reuses the object’s behavior without rewriting the lambda.

**Output**
```java
The sum of given input values using lambda is: 5
The sum of given input values using instance method reference is: 5
```

---

## Instance Method Reference Using Class Type (Class::instanceMethod)
### Coding Example: MethodReference

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

**Explanation**
- First we print list elements using a lambda.
- Since `println()` already performs the same action, we replace the lambda with a method reference that does the same thing  without having
  to create a custom object.
- This makes the code cleaner and avoids extra lambda syntax.

**Output**
```java
Supply
HR
Sales
Marketing
Supply
HR
Sales
Marketing
```

---

## Constructor Reference (Class::new)
### Coding Example: MethodReference

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

**Explanation**
- A lambda is first used to create a new Product object.
- Since the lambda only calls the constructor, we replace it with a constructor reference (`Product::new`).
- This makes the code more readable and directly reuses the class constructor.
- Few other examples of Constructor reference are:
  - `String::new;`
  - `Integer::new;`
  - `ArrayList::new;`
  - `UserDetail::new;`

**Output**
```java
Product [name=Samsung Galaxy, price=1000]
Product [name=Apple IPhone, price=1500]
```

---

## Important Concept: Lambda vs Method Reference Initialization

### Method reference → Object / method binding happens immediately

**Example:**
```java
ArithmeticOperation op = MethodReference::performAddition;
```

As soon as this line executes:
- The method reference is resolved (linked to the target method).
- But the method itself is **not executed** until you call `op.performOperation()`.

### Lambda expression → Not initialized until invoked

**Example:**
```java
ArithmeticOperation op = (a, b) -> a + b;
```

A lambda:
- **Does not bind to any method until execution**
- Remains a behavior definition
- Nothing inside lambda runs or resolves until `op.performOperation()` is called

### Summary Table

| Aspect           | Lambda Expression       | Method Reference                       |
| ---------------- | ----------------------- | -------------------------------------- |
| When resolved?   | At runtime when invoked | Immediately bound to target method     |
| When executed?   | Only when invoked       | Only when invoked                      |
| Behavior stored? | Behavior defined inline | Behavior forwarded to existing method  |
| Performance      | Slightly more overhead  | Slightly faster (method already known) |

---
