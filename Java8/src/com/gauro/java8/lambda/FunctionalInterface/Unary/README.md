# Unary Operator Functional Interface

Unary Operator Functional Interface is a child of Function interface. We use this operator where both the input and output parameters data type is same i.e. `T`. 

It is defined in:
```java
java.util.function.UnaryOperator<T>
```

### Unary API Overview
#### Type Parameter
- `<T>` → Input and Output type

> Since it is a `Function<T,T>`, all the methods `apply()`, `compose()`, `andThen()` are available inside the UnaryOperator interface.

---

## Coding example : UnaryOperatorExample

### Basic Example
```java
// Creating a Function
Function<String, String> convertStr = input -> input.toUpperCase();

// Calling Function method
System.out.println("The uppercase value of given input is : " + convertStr.apply("Eazy Bytes"));

// Creating a Function
UnaryOperator<String> convertStrWithUnary = input -> input.toUpperCase();
```

- Both take a String.
- Both return a String.
- Both convert it to uppercase.
- UnaryOperator just describes that more clearly.

Output
```java
The uppercase value of given input is : EAZY BYTES
The uppercase value of given input with Unary operator is : EAZY BYTES
```

### identity()
```java
UnaryOperator<String> sameValue = UnaryOperator.identity();

// Calling Function method
System.out.println("The value of given input is : " + sameValue.apply("Eazy Bytes"));
```
- returns its input argument as its output

**Output**
```java
The value of given input is : Eazy Bytes
```

### Mixing Function and UnaryOperator 
You can chain them together using `andThen()` or `compose()`
as long as:

- both take the same type (e.g., Integer → Integer)

#### andThen() example
```java
Function<Integer, Integer> multiplyOperation = a -> {
    System.out.println("Multiply by 2 Operation");
    return a * 2;
};

UnaryOperator<Integer> tripleOperation = a -> {
    System.out.println("Multiply by 3 Operation");
    return a * 3;
};

// Chaining the function methods using andThen()
multiplyOperation = multiplyOperation.andThen(tripleOperation);

System.out.println(multiplyOperation.apply(5));
```
- First function: multiply by 2
  - 5 × 2 = 10
- `andThen()` second function: multiply by 3
  - 10 × 3 = 30
- Final Output = 30

**Output**
```java
Multiply by 2 Operation
Multiply by 3 Operation
30
```

#### compose() example
```java
// Chaining the function methods using andThen()
multiplyOperation = multiplyOperation.compose(tripleOperation);

System.out.println(multiplyOperation.apply(5));
```
- First `compose()`: triple operation (multiply by 3)
  - 5 × 3 = 15
- Second: multiply-by-2 operation
  - 15 × 2 = 30
- Third `andThen()`:  multiply-by-3 operation
  - 30 x 3 = 90
- Final Output = 90

**Output**
```java
Multiply by 3 Operation
Multiply by 2 Operation
Multiply by 3 Operation
90
```

---

### Summary

|Interface	|Input	|Output	|Purpose|
|---|-----|--------|--------|
|`Function<T, R>`	|`T`	|`R`	|Takes something, returns something (any type)|
|`UnaryOperator<T>`	|`T`	|`T`|	Same thing as Function, but both types must match|

---