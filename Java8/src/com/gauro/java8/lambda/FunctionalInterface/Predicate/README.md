# Predicate Functional Interface

The Predicate functional interface is used when you accept one input argument and return a boolean result after evaluating a condition.

It is defined in:
```java
java.util.function.Predicate<T>
```

### Predicate API Overview
#### Type Parameter

- `<T>` — the type of the input argument.

#### Single Abstract Method (SAM)
- `boolean test(T t)`

  Evaluates the condition and returns `true` or `false`.
  Single abstract method available. 

#### Static Method
- `static <T> Predicate<T> isEqual(Object targetRef)`

    Returns a predicate that tests whether two objects are equal.

#### Default Methods for Predicate Chaining

Predicates can be combined using logical operators:

|Method	| Description     |
|----------|-----------------|
|`default Predicate<T> and(Predicate<? super T> other)`	| Logical **AND**     |
|`default Predicate<T> or(Predicate<? super T> other)`	| Logical **OR**      |
|`default Predicate<T> negate()`	| Logical **NOT** | 

#### isEqual()

Used to compare object equality by returning a new predicate.
Equivalent to:
```java
x -> x.equals(targetRef)
```

---

## Coding Example: PredicateExample

### Basic Predicate
```java
// Creating a predicate
Predicate<Integer> isEven = i -> i % 2 == 0;

// Calling predicate method
System.out.println("Is the number 61 is even? : " + isEven.test(61));
```
- Creates a test called `isEven`.
- `i -> i % 2 == 0` is a lambda function to check if `i` is even. 
- `.test(61)` runs the predicate using **61**.
- Since **61** is odd → result is `false`.

**Output**
```java
Is the number 61 is even? : false
```

### Predicate Chaining
#### AND
```java
// Creating a predicate
Predicate<Integer> isGreaterThan50 = i -> i > 50;

// Predicate AND Chaining
System.out.println("Is the number 61 is even & greater than 50 ? : " + isGreaterThan50.and(isEven).test(61));
```

#### OR
```java
// Predicate OR Chaining
System.out.println(
"Is the number 61 is either even or greater than 50 ? : " + isGreaterThan50.or(isEven).test(61));
```

#### NEGATE (NOT)
```java
// Predicate negate Chaining
System.out.println("Is the number 61 is odd? : " + isEven.negate().test(61));
```
**Meaning:**
- `and`: **both** must be true
- `or`: **at least one** must be true
- `negate`: **flips** the result (NOT operator)

**Output**
```java
Is the number 61 is even & greater than 50 ? : false
Is the number 61 is either even or greater than 50 ? : true
Is the number 61 is odd? : true
```

---

### Predicate in Streams (more details coming soon)

```java
// Usage of Predicate inside Collections & Streams
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> collect = list.stream().filter(isEven).collect(Collectors.toList());

System.out.println("List of even numbers from the given list: "+collect); // [2, 4, 6, 8, 10]
```

**Explanation:**
The stream takes one element at a time and applies the `isEven` predicate.
Only elements returning `true` are collected.

**Output**
```java
List of even numbers from the given list: [2, 4, 6, 8, 10]
```

---

### Using Predicate.isEqual()

```java
Predicate<String> checkEquality  = Predicate.isEqual("Eazy Bytes");
System.out.println("Is the input string is equal ? : " + checkEquality.test("Eazy Bytes"));
```

This returns a predicate that checks if the input equals `Eazy Bytes`.

**Output**
```java
Is the input string is equal ? : true
```
---