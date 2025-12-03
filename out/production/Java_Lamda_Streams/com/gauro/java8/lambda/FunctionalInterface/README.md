# Functional Interface

A Functional Interface is an interface that contains exactly one abstract method.
Because it has only one unimplemented method, it can be used as the target for lambda expressions or method references.

### Rules for Functional Interfaces

- Only one abstract method is allowed
- Also called a SAM (Single Abstract Method) interface
- Can contain any number of default methods
- Can contain any number of static methods
- Can contain any number of private methods
- Can be used with lambda expressions because the compiler already knows which method must be implemented

> **Why only one abstract method?**
> 
> With only one abstract method, the compiler knows:
> - which method the lambda is implementing
> - the method name
> - parameter types
> - return type
> 
> **No ambiguity.**

### @FunctionalInterface Annotation

Java 8 introduced `@FunctionalInterface` to explicitly mark an interface as functional.

**Benefits:**
- The compiler throws an error if someone adds a second abstract method.
- Makes the design intention clear.

### Functional Interfaces Existing Before Java 8!

Even before lambdas, Java already had interfaces that fit the SAM pattern:

| Interface  | 	Single Abstract Method | 
|------------|-------------------------|
| Runnable	  | `run()`                   |
| Comparable |	`compareTo()`|

### Examples
**Valid Functional Interface**
```java
@FunctionalInterface
public interface ArithmeticOperation {
    public int performOperation(int a, int b);   // SAM
}
```

**Invalid — Two Abstract Methods**
```java
@FunctionalInterface
public interface ArithmeticOperation {
    public int performOperation(int a, int b);
    public int performOperation(int c);    // second abstract method → invalid
}
```

**Invalid — No Abstract Method**
```java
@FunctionalInterface
public interface ArithmeticOperation {
    // No abstract method → invalid functional interface
}
```

---

## Inheritance in Functional Interfaces
1. **Valid – Inherits a Single Abstract Method**
```java
@FunctionalInterface
   public interface ArithmeticOperation {
   int performOperation(int a, int b);
}

@FunctionalInterface
public interface SimpleOperation extends ArithmeticOperation {
}
```

`SimpleOperation` is valid because it **inherits the single abstract method.**

2. **Valid – Override With Same Signature**
```java
@FunctionalInterface
   public interface SameOperation extends ArithmeticOperation {
       int performOperation(int a, int b);  // same method signature
   }
```

Still valid because it **does not add a new abstract method.**

3. **Invalid – Adds Another Abstract Method**
```java
@FunctionalInterface
public interface InvalidOperation extends ArithmeticOperation {
    int performAnotherOperation(int a, int b); // adds a new method
}
```

Invalid because it **produces 2 abstract methods.**

4. **No Annotation → No Restriction**
```java
public interface NormalOperation extends ArithmeticOperation {
   int normalOperation(int a, int b); // allowed
}
```
Since it is not marked with `@FunctionalInterface`, multiple abstract methods are fine.

---

## Predefined Functional Interfaces (java.util.function)

Java 8 introduced many commonly used functional interfaces inside:
```java
java.util.function
```

**Most Important Ones**

|Interface|	Purpose|
|-------|-----------|
|`Predicate<T>`|Takes T → returns boolean|
|`Function<T,R>`|	Takes T → returns R|
|`Consumer<T>`	|Takes T → returns nothing|
|`Supplier<T>`	|Takes nothing → returns T|
|`BiPredicate<T,U>`|	Takes T & U → returns boolean|
|`BiFunction<T,U,R>`|	Takes T & U → returns R|
|`BiConsumer<T,U>`|	Takes T & U → returns nothing|
|`UnaryOperator<T>`	|T → T|
|`BinaryOperator<T>`	|(T, T) → T|
|Primitive variants|	For int, long, double types|

### Example: Predicate with Optional (OptionalExample)

```java
System.out.println(country.filter(g -> g.equals("india"))); // Optional.empty
System.out.println(country.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional[MALE]
System.out.println(emptyCountry.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional.empty
```
`filter` accepts a **`Predicate<T>`.**

**When to use Predicate?**

Use `Predicate<T>` when:
- You take an input of any type **T**
- And you return a **boolean**

---