# `@SafeVarargs` Annotation

The `@SafeVarargs` annotation was introduced in **Java 7** to suppress warnings related to unsafe operations with varargs, especially when used with generics.

**Purpose**
- Suppresses compiler warnings about **heap pollution**.
- Indicates that a method using varargs is **safe** and will not cause heap corruption.

**Where It Can Be Used**

`@SafeVarargs` can be applied only to:
- final methods
- static methods
- constructors
- private instance methods (added in Java 9)

---
## Example: Safe Varargs Method

```java
private static void sum(int... nums) {
    System.out.println(Arrays.toString(nums));
    int sum = 0;
    for (int num : nums) {
        sum = sum + num;
    }
    System.out.println("The total sum for the given input is : " + sum);
}
```

`int... nums` allows the method to accept any number of `int` arguments, avoiding multiple overloaded methods.

## Output 
```java
[1]
The total sum for the given input is : 1
[1, 2]
The total sum for the given input is : 3
[1, 2, 3]
The total sum for the given input is : 6
```

--- 

### Heap pollution Explanation
Heap pollution occurs when a variable of a parameterized type refers to an object that is not of that type.
Example: mixing `List<String>` and `List<Integer>` inside a varargs array can eventually cause a **ClassCastException**.

**Example Using `@SafeVarargs`**
```java
@SafeVarargs
public final void print(List<String>... messages) {
    String firstElement = messages[0].get(0); 
    System.out.println(firstElement); 
}
```

## Output
```java
Eazy
```