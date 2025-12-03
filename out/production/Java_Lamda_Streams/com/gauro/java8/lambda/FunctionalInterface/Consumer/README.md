# Consumer Functional Interface

Consumer interface will consume/accept the given input for
processing but not return anything to the invocation method.

It is defined in:
```java
java.util.function.Consumer<T>
```

### Consumer API Overview
#### Type Parameter
- `<T>` → Input type

#### Single Abstract Method (SAM)
- `void accept(T t)`
- runs the action

#### Chaining Methods
- `andThen()`
- lets you chain multiple Consumers

No static methods are available in Consumer functional interface

---

## Coding example: ConsumerExample
### Basic Example
```java
public static void main(String[] args) {

    // Creating a Consumer
    Consumer<String> convertAndDisplay = input -> System.out.println("Converted value is: "+input.toUpperCase());

    // invoking accept method inside the Consumer
    convertAndDisplay.accept("Eazy Bytes");
```
just prints the input and **does not return anything**

**Output**
```java
Converted value is: EAZY BYTES
```

### Chaining Consumers
```java
// Creating a Consumer
Consumer<String> appendInput = input -> System.out.println("New value after appending is: "+"HELLO "+input);

// invoking accept method inside the Consumer
appendInput.andThen(convertAndDisplay).accept("Java 8");
```
**Explanation** 
- Runs appendInput first
  - This prints `New value after appending is: HELLO Java 8`
- Then runs convertAndDisplay
  - This prints `Converted value is: JAVA 8`

**Output**
```java
New value after appending is: HELLO Java 8
Converted value is: JAVA 8
```
appendInput.andThen(convertAndDisplay).accept("Java 8");

---