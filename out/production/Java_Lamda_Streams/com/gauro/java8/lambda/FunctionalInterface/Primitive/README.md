# PRIMITIVE TYPE FUNCTIONAL INTERFACES

In Java, the functional interfaces we learned earlier (`Predicate`, `Function`, `Consumer`, etc.) work with **Object types** such as:
- `Integer`
- `Double`
- `Float`
- `Long`
- `Boolean`

But this creates a **performance issue.**

Why? Because when we pass primitive values (`int`, `double`, `long`, etc.), Java must:

1. **Autobox** → convert primitive → wrapper object
2. **Unbox** → convert wrapper object → primitive
3. **Re-box** → convert primitive → wrapper for return value

![img.png](img.png)

This constant boxing and unboxing can slow down performance, especially with large data or loops.

To fix this, Java created **Primitive Functional Interfaces** (e.g., `IntPredicate`, `DoubleFunction`, `IntSupplier`, etc.) that **work directly on primitives**, no boxing/unboxing needed.

---

### Primitive Vs. Wrapper
#### Wrapper Classes
- Objects stored on the heap
- Can be `null`
- Heavier (object overhead)
- Required for collections
- Support autoboxing/unboxing

**Examples:** `Integer`, `Double`, `Float`, `Long`, `Character`, `Boolean`

#### Summary: Primitive vs Wrapper

|**Feature**	|**Primitive**	| **Wrapper**          |
|--------|------|-------------------------------|
|Type|	Not an object| 	Object                       |
|Stored in|	Stack| 	Heap                         |
|Can be null|	 No| 	 Yes                         |
|Performance|	Faster	| Slower (memory + GC overhead) |
|Use in Collections|	 No| 	Yes                          |
|Autoboxing	|Not needed	| Needed                        |

---

## Primitive Functional Interfaces

Below is a grouped, organized list of the most important primitive functional interfaces in Java.

> Note: 
> 
> All interfaces live in the `java.util.function` package.

### Predicate Versions (return boolean, accept primitive)
|Interface	| Input Type	                               | Method                       |
|-----|-------------------------------------------|------------------------------|
|`IntPredicate`	| int                                       | 	`boolean test(int value)`   |
|`DoublePredicate`| 	doub`le                                  | 	`boolean test(double` value)` |
|`LongPredicate`| 	long                                     | 	`boolean test(long value) ` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void predicatePrimitiveFunctions() {
    IntPredicate checkInt = a -> a % 2 == 0;
    System.out.println("Output from IntPredicate is : " + checkInt.test(10));

    DoublePredicate checkDouble = a -> a % 2 == 0;
    System.out.println("Output from DoublePredicate is : " + checkDouble.test(10.0));

    LongPredicate checkLong = a -> a % 2 == 0;
    System.out.println("Output from LongPredicate is : " + checkLong.test(1034497756));

}
```

### Function Versions (primitive input, object output)

|Interface| 	Input Type |	Output	| Method                |
|-------|-------------|-----------|-----------------------|
|`IntFunction<R>`	| int         |	R| `R apply(int value)`    |
|`DoubleFunction<R>`	| double      |	R	| `R apply(double value)` |
|`LongFunction<R>`| 	long       | 	R	         |`R apply(long value)`|

#### Coding Example: PrimitiveFunctionsExample
```java
IntFunction<String> applyInt = a -> Integer.toString(a);
System.out.println("Output from IntFunction is : " + applyInt.apply(10));

DoubleFunction<String> applyDouble = a -> Double.toString(a);
System.out.println("Output from DoubleFunction is : " + applyDouble.apply(10.0));

LongFunction<String> applyLong = a -> Long.toString(a);
System.out.println("Output from LongFunction is : " + applyLong.apply(1034497756));
```

### ToX Functions (object input → primitive output)

|Interface| 	Input Type |	Output	| Method                |
|-------|-------------|-----------|-----------------------|
|`ToIntFunction<T>`	| any         |	int| `int applyAsInt(T value)`    |
|`ToDoubleFunction<T>`	| any      |	double	| `double applyAsDouble(T value)` |
|`ToLongFunction<T>`| 	any       | 	long	         |`long applyAsLong(T value)`|

#### Coding Example: PrimitiveFunctionsExample
```java
ToIntFunction<String> toInt = a -> Integer.parseInt(a);
System.out.println("Output from ToIntFunction is : " + toInt.applyAsInt("10"));

ToDoubleFunction<String> toDouble = a -> Double.parseDouble(a);
System.out.println("Output from ToDoubleFunction is : " + toDouble.applyAsDouble("10.0"));

ToLongFunction<String> toLong = a -> Long.parseLong(a);
System.out.println("Output from ToLongFunction is : " + toLong.applyAsLong("1034497756"));
```
### Primitive-to-Primitive Converters

| Interface              | Input → Output | Method                |
| ---------------------- | -------------- | --------------------- |
| `IntToLongFunction`    | int → long     | `applyAsLong(int)`    |
| `IntToDoubleFunction`  | int → double   | `applyAsDouble(int)`  |
| `LongToIntFunction`    | long → int     | `applyAsInt(long)`    |
| `LongToDoubleFunction` | long → double  | `applyAsDouble(long)` |
| `DoubleToIntFunction`  | double → int   | `applyAsInt(double)`  |
| `DoubleToLongFunction` | double → long  | `applyAsLong(double)` |

#### Coding Example: PrimitiveFunctionsExample
```java
IntToLongFunction intToLong = a -> (long) a;
System.out.println("Output from IntToLongFunction is : " + intToLong.applyAsLong(10));

IntToDoubleFunction intToDouble = a -> (double) a;
System.out.println("Output from IntToDoubleFunction is : " + intToDouble.applyAsDouble(10));

LongToIntFunction longToInt = a -> (int) a;
System.out.println("Output from LongToIntFunction is : " + longToInt.applyAsInt(10344));

LongToDoubleFunction longToDouble = a -> (double) a;
System.out.println("Output from LongToDoubleFunction is : " + longToDouble.applyAsDouble(10344));

DoubleToIntFunction doubleToInt = a -> (int) a;
System.out.println("Output from DoubleToIntFunction is : " + doubleToInt.applyAsInt(10.0));

DoubleToLongFunction doubleToLong = a -> (long) a;
System.out.println("Output from DoubleToLongFunction is : " + doubleToLong.applyAsLong(10344.0));
```

---

### Bi-Functions (2 inputs → primitive output)

| Interface                  | Inputs | Output | Method                    |
| -------------------------- | ------ | ------ | ------------------------- |
| `ToIntBiFunction<T, U>`    | T, U   | int    | `applyAsInt(T t, U u)`    |
| `ToLongBiFunction<T, U>`   | T, U   | long   | `applyAsLong(T t, U u)`   |
| `ToDoubleBiFunction<T, U>` | T, U   | double | `applyAsDouble(T t, U u)` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void biFunctionPrimitiveFunctions() {
    ToIntBiFunction<String, String> toIntBiFunc = (input1, input2) -> {
    return (Integer.parseInt(input1) + Integer.parseInt(input2));
    };
    System.out.println("Output from ToIntBiFunction is : " + toIntBiFunc.applyAsInt("10", "20"));

    ToLongBiFunction<String, String> toLongBiFunc = (input1, input2) -> {
    return (Long.parseLong(input1) + Long.parseLong(input2));
    };
    System.out.println("Output from ToLongBiFunction is : " + toLongBiFunc.applyAsLong("1045556", "2065767"));

    ToDoubleBiFunction<String, String> toDoubleBiFunc = (input1, input2) -> {
    return (Double.parseDouble(input1) + Double.parseDouble(input2));
    };
    System.out.println("Output from ToDoubleBiFunction is : " + toDoubleBiFunc.applyAsDouble("10.0", "2.0"));
}
```

---

### Consumers (accept primitive input, no output)

| Interface              | Input     | Method                           |
| ---------------------- | --------- | -------------------------------- |
| `IntConsumer`          | int       | `void accept(int value)`         |
| `LongConsumer`         | long      | `void accept(long value)`        |
| `DoubleConsumer`       | double    | `void accept(double value)`      |
| `ObjIntConsumer<T>`    | T, int    | `void accept(T t, int value)`    |
| `ObjLongConsumer<T>`   | T, long   | `void accept(T t, long value)`   |
| `ObjDoubleConsumer<T>` | T, double | `void accept(T t, double value)` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void consumerPrimitiveFunctions() {
    IntConsumer intCons = a -> System.out.println("Output from IntConsumer:"+ a);
    intCons.accept(10);

    LongConsumer longCons = a -> System.out.println("Output from LongConsumer:"+ a);
    longCons.accept(1004345);

    DoubleConsumer doubleCons = a -> System.out.println("Output from DoubleConsumer:"+ a);
    doubleCons.accept(10.0);

    ObjIntConsumer<String> objInt = (input,a) -> System.out.println("Output from ObjIntConsumer:"+ input+a);
    objInt.accept("Ten", 10);

    ObjLongConsumer<String> objLong = (input,a) -> System.out.println("Output from ObjLongConsumer:"+ input+a);
    objLong.accept("Thousand", 1000);

    ObjDoubleConsumer<String> objDouble = (input,a) -> System.out.println("Output from ObjDoubleConsumer:"+ input+a);
    objDouble.accept("Ten", 10.0);
}
```

---

### Suppliers (no input → primitive output)

| Interface         | Output  | Method           |
| ----------------- | ------- | ---------------- |
| `IntSupplier`     | int     | `getAsInt()`     |
| `LongSupplier`    | long    | `getAsLong()`    |
| `DoubleSupplier`  | double  | `getAsDouble()`  |
| `BooleanSupplier` | boolean | `getAsBoolean()` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void supplierPrimitiveFunctions() {
    IntSupplier intSupp = () -> {
    Random rand = new Random();
    return rand.nextInt(1000);
    };
    System.out.println("Output from IntSupplier is : " + intSupp.getAsInt());

    LongSupplier longSupp = () -> {
    Random rand = new Random();
    return rand.nextLong();
    };
    System.out.println("Output from LongSupplier is : " + longSupp.getAsLong());

    DoubleSupplier doubleSupp = () -> {
    Random rand = new Random();
    return rand.nextDouble();
    };
    System.out.println("Output from DoubleSupplier is : " + doubleSupp.getAsDouble());

    BooleanSupplier booleanSupp = () -> LocalDate.now().isLeapYear();
    System.out.println("Output from BooleanSupplier is : " + booleanSupp.getAsBoolean());
}
```

---

### Unary Operators (primitive → same primitive)

| Interface             | Input/Output    | Method                  |
| --------------------- | --------------- | ----------------------- |
| `IntUnaryOperator`    | int → int       | `applyAsInt(int)`       |
| `LongUnaryOperator`   | long → long     | `applyAsLong(long)`     |
| `DoubleUnaryOperator` | double → double | `applyAsDouble(double)` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void unaryPrimitiveFunctions() {
    IntUnaryOperator intUnary = a -> a*2;
    System.out.println("Output from IntUnaryOperator is : " + intUnary.applyAsInt(24));
    
    LongUnaryOperator longUnary = a -> a*2;
    System.out.println("Output from LongUnaryOperator is : " + longUnary.applyAsLong(456767));
    
    DoubleUnaryOperator doubleUnary = a -> a*2;
    System.out.println("Output from DoubleUnaryOperator is : " + doubleUnary.applyAsDouble(4.5));
}
```

---

### Binary Operators (two primitives → same primitive)

| Interface              | Inputs         | Output | Method                       |
| ---------------------- | -------------- | ------ | ---------------------------- |
| `IntBinaryOperator`    | int, int       | int    | `applyAsInt(left, right)`    |
| `LongBinaryOperator`   | long, long     | long   | `applyAsLong(left, right)`   |
| `DoubleBinaryOperator` | double, double | double | `applyAsDouble(left, right)` |

#### Coding Example: PrimitiveFunctionsExample
```java
private static void binaryPrimitiveFunctions() {
    IntBinaryOperator intBinary = (a,b) -> a+b;
    System.out.println("Output from IntBinaryOperator is : " + intBinary.applyAsInt(24,26));

    LongBinaryOperator longBinary = (a,b) -> a+b;
    System.out.println("Output from LongBinaryOperator is : " + longBinary.applyAsLong(456767,5768787));

    DoubleBinaryOperator doubleBinary = (a,b) -> a+b;
    System.out.println("Output from DoubleBinaryOperator is : " + doubleBinary.applyAsDouble(4.5,45.45));
}
```

---

## Coding example: PrimitiveFunctionsExample
### Boxing Problem
```java
private static void problemWithNormalFunctionalInterfaces() {

    // Creating a Function
    // 1) First the input value provided will be converted to Integer using
    // AutoBoxing
    // 2) Second the input value provided to the method body will be converted to
    // int
    // using Auto UnBoxing during business logic
    // 3) Finally after business logic the return value has to be converted to
    // Integer
    // using AutoBoxing
    Function<Integer, Integer> doubleTheValue = input -> input * 2;
    
    int[] iparray = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int[] oparray = new int[iparray.length];
    
    for (int i = 0; i < iparray.length; i++) {
        oparray[i] = doubleTheValue.apply(iparray[i]);
    }
    System.out.println("The output array is: " + Arrays.toString(iparray));
    System.out.println("The output array is: " + Arrays.toString(oparray));
}
```
#### Why is this slow?
Because every loop iteration does `boxing` + `unboxing` + `reboxing`.

---