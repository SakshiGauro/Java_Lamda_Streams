# @SafeVarargs Annotation

Java 5 introduced the concept of varargs, or a method parameter of variable length, as well
as parameterized types. @SafeVarargs annotation is introduced in JDK 7 which is used to
suppress the unsafe operation warnings at the compile time.
• @SafeVarargs annotation is used to indicate that methods will not cause heap pollution.
These methods are considered to be safe.
• @SafeVarargs can only be applied on
✓ Final methods
✓ Static methods
✓ Constructors
• From Java 9, it can also be used with private instance methods.

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

int... nums means that sum method can take any number of parameters as long as they're all ints. 

- saves a lot of method duplicates.

Heap pollution 
Heap has strings and integhers, which is a mix which will eventuallly create a class cast excetion. This will cause heap pollution .

```java
@SafeVarargs
public final void print(List<String>... messages) {
    String firstElement = messages[0].get(0); 
    System.out.println(firstElement); 
}
```
