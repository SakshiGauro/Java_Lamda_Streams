# Optional in Java 8 — A Better Way to Handle Nulls

Handling `NullPointerException` is one of the most common (and annoying) tasks in Java development. Before Java 8, developers relied on deep nested `if (obj != null)` checks to avoid crashes.

Java 8 introduced `java.util.Optional<T>` to help avoid NullPointerExceptions, reduce boilerplate code, and create cleaner, more expressive APIs.

### Why Optional?
**The Problem (Before Java 8)**

You often had to do multiple nested null checks:

```java
if (user != null) {
    Order order = user.getOrder();
    if (order != null) {
        Item item = order.getItem();
        if (item != null) {
            return item.getName();
            }
        }
    }
return "Not Available";
```

This leads to:
- verbose code
- hard-to-read logic
- frequent NullPointerExceptions

### What Optional Solves
#### Clearly communicates “this value might be absent.”

Instead of:
```java
Order order
```

you explicitly express the possibility of no value with:
```java
Optional<Order> order
```

This **signals in the method signature itself** that the value may or may not exist.

#### Helps prevent NullPointerException.

`Optional.empty()` is a **safe object**, not a null reference. So operations on it are safe and predictable.

#### Reduces repetitive null-checking code.
`Optional` encourages cleaner, more expressive handling of missing values instead of scattered `if (x != null)` checks.

---

### Creating Optional Objects

```java
Optional<Product> empty = Optional.empty(); 
// Creates an empty Optional

Optional<Product> p1 = Optional.of(product);
// Only use of() when you're sure product is not null

Optional<Product> p2 = Optional.ofNullable(product);
// Safely handles null by returning Optional.empty()

```

### Advantages of Optional

- No explicit null checks
- No accidental NullPointerExceptions
- Cleaner method signatures
- Self-documenting API behavior
- Reduces boilerplate code

### Important methods provided by Optional in Java 8

| Method	       | Description                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------|
| `empty()`       | Creates an empty Optional instance                                                                |
| `isPresent()`   | 	Returns true if value exists                                                                     |
| `ifPresent()`   | 	Runs code only if value exists                                                                   |
| `get()`         | 	Returns value (NoSuchElementException if empty)                                                  |
| `map()`         | 	Transforms the value if present                                                                  |
| `flatMap()`	    | Flattens nested Optionals                                                                         |
| `filter()`      | 	Returns Optional if value is present and the predicate matches. Otherwise, returns the empty one | 
| `orElse()`      | 	Returns the value if present; otherwise, returns the given default value                         | 
| `orElseGet()`   | 	Returns the value if present; otherwise, returns the one provided by the given Supplier          |
| `orElseThrow()` | 	Returns the value if present; otherwise, throws the exception     |

---

## Coding Exercise

### Before Java 8 — NullPointerException

```java
public static void beforeJava8() {
		String[] str = new String[10];
		String lowercaseString = str[5].toLowerCase(); //NullPointExecption
		System.out.print(lowercaseString);
	}
```

---

### With Optional (Java 8)

```java
public static void withJava8() {
    String[] str = new String[10];
    str[5] = "Eazy Bytes";

    Optional<String> empty = Optional.empty();
    System.out.println(empty);

    Optional<String> value = Optional.of(str[5]);
    System.out.println(value.get());
    // We should of() when we are sure that value will present, otherwise go for
    // ofNullable()
    Optional<String> nullValue = Optional.ofNullable(str[4]);
    nullValue.ifPresent(System.out::println);
    System.out.println(nullValue.orElse("No Value"));

    Optional<String> nonEmptyString = Optional.of("Eazy Bytes");
    Optional<String> emptyString = Optional.empty();

    System.out.println("Non-Empty Optional: " + nonEmptyString.map(String::toUpperCase));
    System.out.println("Empty Optional: " + emptyString.map(String::toUpperCase));

    Optional<Optional<String>> nonEmptyOptionalInput = Optional.of(Optional.of("Eazy Bytes"));
    System.out.println("Optional value: " + nonEmptyOptionalInput);
    System.out.println("Optional.map: " + nonEmptyOptionalInput.map(input -> input.map(String::toUpperCase)));
    System.out
            .println("Optional.flatMap: " + nonEmptyOptionalInput.flatMap(input -> input.map(String::toUpperCase)));

    Optional<String> country = Optional.of("INDIA");
    Optional<String> emptyCountry = Optional.empty();

    // Filter on Optional
    System.out.println(country.filter(g -> g.equals("india"))); // Optional.empty
    System.out.println(country.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional[MALE]
    System.out.println(emptyCountry.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional.empty

    if (country.isPresent()) {
        System.out.println("Value available");
    }

    country.ifPresent(c -> System.out.println("In Country Option, value available is:" + c));

    // condition failed, no output will be printed
    emptyCountry.ifPresent(c -> System.out.println("In Country Option, value available is:" + c));

    System.out.println(country.orElse("No Country data available"));
    System.out.println(emptyCountry.orElse("No Country data available"));
    System.out.println(emptyCountry.orElseGet(()->"No Country data available"));
    System.out.println(emptyCountry.orElseThrow(NoSuchElementException::new));
    
    /*
     * country.ifPresentOrElse(value -> System.out.println("Value is present, its: "
     * + value), () -> { System.out.println("Value is empty"); });
     */
}
```

### Understanding Key Concepts

#### empty()

```java
Optional<String> empty = Optional.empty();
```
Represents no value, but an empty optional representation of a given object.

#### of() vs ofNullable()

```java
Optional<String> value = Optional.of(str[5]); // throws NullPointerException if Null
Optional<String> nullValue = Optional.ofNullable(str[4]); // safe, returns empty Optional
```
Use `of` when we are sure that a value is present. 
Use `ofNullable` when we are not sure if the value is present. `nullValue` holds an empty representation of it. 

#### ifPresent()
```java
nullValue.ifPresent(System.out::println);
```
prints the value only if value exists.

#### orElse()
```java
System.out.println(nullValue.orElse("No Value"));
```
- if a value is not present, print "No value" 
- `::` -> method reference 

#### map()
```java
Optional<String> nonEmptyString = Optional.of("Eazy Bytes");
Optional<String> emptyString = Optional.empty();

System.out.println("Non-Empty Optional: " + nonEmptyString.map(String::toUpperCase));
System.out.println("Empty Optional: " + emptyString.map(String::toUpperCase));
```
Transforms the value inside Optional if value is present. If empty, it does nothing.

**Output** 
```java
Non-Empty Optional: Optional[EAZY BYTES]
Empty Optional: Optional.empty
```

#### flatMap()

```java
Optional<Optional<String>> nonEmptyOptionalInput = Optional.of(Optional.of("Eazy Bytes"));
System.out.println("Optional value: " + nonEmptyOptionalInput);
System.out.println("Optional.map: " + nonEmptyOptionalInput.map(input -> input.map(String::toUpperCase)));
System.out.println("Optional.flatMap: " + nonEmptyOptionalInput.flatMap(input -> input.map(String::toUpperCase)));
```
Flattens nested Optionals:

`Optional<Optional<String>> -> Optional<String>`

**Output**
```java
Optional value: Optional[Optional[Eazy Bytes]]
Optional.map: Optional[Optional[EAZY BYTES]]
Optional.flatMap: Optional[EAZY BYTES]
```

### filter()

```java
Optional<String> country = Optional.of("INDIA");
Optional<String> emptyCountry = Optional.empty();

// Filter on Optional
System.out.println(country.filter(g -> g.equals("india"))); // Optional.empty
System.out.println(country.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional[MALE]
System.out.println(emptyCountry.filter(g -> g.equalsIgnoreCase("INDIA"))); // Optional.empty
```
- prints the value if the value matches the content. Otherwise, prints `Optional.empty`
- `equalsIgnoreCase` -> ignores the case

**Output**
```java
Optional.empty
Optional[INDIA]
Optional.empty
```

### isPresent()

```java
if (country.isPresent()) {
    System.out.println("Value available");
}

country.ifPresent(c -> System.out.println("In Country Option, value available is:" + c));

// condition failed, no output will be printed
emptyCountry.ifPresent(c -> System.out.println("In Country Option, value available is:" + c));
```
- `isPresent` returns a boolean if a country is not empty
- `ifPresent` will execute the given method if the value is present. For emptyCountry, it will not run the method as the value is not present. 

**Output**
```java
Value available
In Country Option, value available is:INDIA
```

### orElse(), orElseGet(), orElseThrow()
```java
System.out.println(country.orElse("No Country data available"));
System.out.println(emptyCountry.orElse("No Country data available"));
System.out.println(emptyCountry.orElseGet(()->"No Country data available"));
System.out.println(emptyCountry.orElseThrow(NoSuchElementException::new));
```
- Since `country` has some value in it, it will print the country i.e.  `INDIA`
- Since `emptyCountry` has no value, it will print `No Country data available`
- `()->"No Country data available")` lambda expression to call another method 
- `orElseThrow` throws an exception if no value is present

```java
INDIA
No Country data available
No Country data available
Exception in thread "main" java.util.NoSuchElementException
	at java.base/java.util.Optional.orElseThrow(Optional.java:403)
	at com.gauro.java8.optional.OptionalExample.withJava8(OptionalExample.java:65)
	at com.gauro.java8.optional.OptionalExample.main(OptionalExample.java:9)
```

---
