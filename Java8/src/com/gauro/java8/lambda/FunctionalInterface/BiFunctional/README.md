# Bi-Functional Interfaces

Up until now, you’ve seen **Predicate, Function, Consumer**, etc.—but they only take **ONE** input.

But sometimes you need **TWO inputs.**

Example:
- Add two numbers
- Compare two strings
- Check if one number is bigger than another
- Print both firstname and lastname together

To handle this, Java provides **Bi-Functional Interfaces**, which are simply the “two-input” versions of the existing ones.

---

## BiPredicate<T, U>
It is defined in:
```java
java.util.function.BiPredicate<T, U> 
//Similar to Predicate but it can accept 2 inputs and return a boolean
```

### Type Parameter
- `<T>` → First Input type
- `<U>` → Second Input type

### Single Abstract Method (SAM)
- `boolean test(T t, U u)`
  
    Executes the predicate using the two inputs and returns a boolean result.

### Coding Example: BiFunctionalExamples
```java
// Creating a BiPredicate
BiPredicate<Integer, Integer> isEven = (a, b) -> (a + b) % 2 == 0;

// Calling BiPredicate method
System.out.println("Is the sum of given numbers is even? : " + isEven.test(4, 9));
```

**Output**
```java
Is the sum of given numbers is even? : false
```

---

## BiFunction<T, U, R>
It is defined in:
```java
java.util.function.BiFunction<T, U, R>
//Similar to Function but it can accept 2 inputs and return a result, R
```

### Type Parameter
- `<T>` → First Input type
- `<U>` → Second Input type
- `<R>` → Result type

### Single Abstract Method (SAM)
- `R apply(T t, U u)`

  Executes the function with both inputs and returns the computed output.

### Coding Example: BiFunctionalExamples
```java
// Creating a BiFunction
BiFunction<Integer, Integer, Double> power = (a1, a2) -> Math.pow(a1, a2);

// Calling BiFunction method
        System.out.println("The power of given numbers is : " + power.apply(4, 9));
```

**Output**
```java
The power of given numbers is : 262144.0
```

---

## BiConsumer<T, U>
It is defined in:
```java
java.util.function.BiConsumer<T, U>
//Similar to Consumer but it can accept 2 inputs and no return value
```

### Type Parameter
- `<T>` → First Input type
- `<U>` → Second Input type

### Single Abstract Method (SAM)
- `void accept(T t, U u)`

  Performs an action using the two provided values.

### Coding Example: BiFunctionalExamples
```java
// Creating a Consumer
BiConsumer<String, String> appendAndConvert = (word1, word2) -> System.out
        .println("Converted value is: " + (word1+word2).toUpperCase());

// invoking accept method inside the Consumer
        appendAndConvert.accept("Hello ","Eazy Bytes!");
```

**Output**
```java
Converted value is: HELLO EAZY BYTES!
```

---

## Why There Is No BiSupplier?

A Supplier **never accepts inputs**, it only returns a value.
Therefore, a “BiSupplier” doesn’t make sense because the Supplier concept does not involve parameters at all.

---
        