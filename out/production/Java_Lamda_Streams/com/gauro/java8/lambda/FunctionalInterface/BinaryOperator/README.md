# BinaryOperator Functional Interface

`BinaryOperator<T>` is a **child** of `BiFunction<T,U,R>` .We will use this in the scenarios where the: 
- Both input parameters are of the **same type.**
- The return value is also of the **same type.**

So essentially: it takes **two values of type T** and returns **one value of type T.**

It is defined in:
```java
java.util.function.BinaryOperator<T>
```

### BinaryOperator API Overview
#### Type Parameter
- `<T>` → Type of both input arguments and the return value.

#### Inherits all methods from BiFunction<T, U, R>:
- `apply(T t1, T t2)` → executes logic using the two inputs and returns a result.
- `andThen()` → can chain another function that accepts the output.

#### Static Methods
- `BinaryOperator<T> maxBy(Comparator<? super T> comparator)` → returns the larger of two elements.
- `BinaryOperator<T> minBy(Comparator<? super T> comparator)` → returns the smaller of two elements.

---

## Coding Example: BinaryOperatorExample
### Appending Strings

```java
// Creating a BinaryOperator
BinaryOperator<String> appendAndConvert = (word1, word2) -> (word1 + word2).toUpperCase();

// Calling BinaryOperator method
System.out.println("The updated value after appending and converting is : "
+ appendAndConvert.apply("Hello ", "Eazy Bytes Students"));
```
**Explanation:**
Takes two strings, concatenates them, and converts to uppercase. Input and output types are the **same** (`String`).

**Output**
```java
The updated value after appending and converting is : HELLO EAZY BYTES STUDENTS
```

### Using maxBy and minBy
```java
BinaryOperator<Integer> maxOperation = BinaryOperator.maxBy((a, b) -> (a > b) ? 1 : ((a == b) ? 0 : -1));
System.out.println("The largest number is: "+maxOperation.apply(16, 30));

BinaryOperator<Integer> minOperation = BinaryOperator.minBy((a, b) -> (a > b) ? 1 : ((a == b) ? 0 : -1));
System.out.println("The smallest number is: "+minOperation.apply(16, 30));
```

**Explanation:**
- `maxBy()` uses a comparator to pick the **larger value.**
- `minBy()` uses a comparator to pick the **smaller value.**
- Both inputs and the result are of the same type (`Integer`).

```java
The largest number is: 30
The smallest number is: 16
```

---
