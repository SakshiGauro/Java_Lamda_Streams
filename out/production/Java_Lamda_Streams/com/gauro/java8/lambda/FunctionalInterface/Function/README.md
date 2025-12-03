# Function Functional Interface

The Function interface represents a function that:
- takes **one input** of type `T`
- returns **one output** of type `R`
- can return **any datatype**, not just boolean

This makes it more flexible than **Predicate**, which only returns a boolean.

It is defined in:
```java
java.util.function.Function<T, R>
```

### Function API Overview
#### Type Parameter
- `<T>` → Input type
- `<R>` → Output type

#### Single Abstract Method (SAM)
- `R apply(T t)`

Runs the function using the given input and returns a result.

#### Static Method
- `static <T> Function<T, T> identity()`
- Returns a function that gives the same value back as the input.
- Example:
`Function.identity().apply("Hello") → "Hello"`

#### Chaining Methods

You can chain functions using:
- `andThen()` → first run _this_ function, then run the next one.
- `compose()` → first run the **given function**, then run _this_ function.

**The Difference**

|Method	|Execution Order|
|------|----------|
|`andThen()`|	First current function → then the next one|
|`compose()`|	First the given function → then current function|

---

## Coding example: FunctionExample

### Basic Function
```java
// Creating a Function
Function<String, String> convertStr = input -> input.toUpperCase();

// Calling Function method
System.out.println("The uppercase value of given input is : " + convertStr.apply("Eazy Bytes"));
```
- Takes a String
- Returns a String
- Converts the string to uppercase

### identity()
```java
Function<String, String> sameValue = Function.identity();// Calling Function method
System.out.println("The value of given input is : " + sameValue.apply("Eazy Bytes"));
```
- returns its input argument as its output

**Output**
```java
The value of given input is : Eazy Bytes
```

### Chaining
#### andThen()
```java
Function<Integer, Integer> multiplyOperation = a -> {
    System.out.println("Double Operation");
    return a * 2;
};

// Chaining the function methods using andThen()
multiplyOperation = multiplyOperation.andThen(a -> {
System.out.println("Triple Operation");
return 3 * a;
});

System.out.println(multiplyOperation.apply(5));
```

**Explanation:**
- First function: multiply input by **2**
  - For input `5` → `5 * 2 = 10`
- `andThen()` adds another function: multiply by **3**
  - Takes the result of the first function → `10 * 3 = 30`

**Output**
```java
Double Operation
        Triple Operation
        30
```

#### compose()
```java
Function<Integer, Integer> divOperation = a -> {
    System.out.println("Division by 2 Operation");
    return a / 2;
};

// Chaining the function methods using compose()
divOperation = divOperation.compose(a -> {
    System.out.println("Division by 3 Operation");
    return a / 3;
});

System.out.println(divOperation.apply(30));
```
**Explanation**
- `compose()` runs the added function first
- First: division by **3**, `30 → 30 / 3 = 10`
- Then: division by **2**, `10 / 2 = 5`

**Output**
```java
Division by 3 Operation
Division by 2 Operation
5
```

---

## Predicate vs Function

|**Feature**| 	**Predicate**      |	**Function**|
|------|-----------------|-------------|
|Purpose	|Check a condition	|Perform business logic and return a value|
|Return Type	|**boolean** only	|Any datatype|
|SAM Name	|`test()`	|`apply()`|
|Type Parameters	|1 (`T`)	|2 (`T`, `R`)|
|Static Method	|`isEqual()`	|`identity()`|
|Chaining Methods	|`and()`, `or()`, `negate()`	|`andThen()`, `compose()`|

> **In simple terms:**
> 
> Predicate → “Is this true or false?”
> Function → “Take this input, do something, and give me the result.”

---