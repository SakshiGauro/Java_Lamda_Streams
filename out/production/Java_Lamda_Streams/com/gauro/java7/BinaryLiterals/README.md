# Binary Literals in Java7

Java 7 introduced **Binary Literals**, allowing developers to represent numbers using **binary (0s and 1s)** directly in code. This is especially useful when working with **bitwise operators**, masks, and low-level programming.

Binary literals can be used with all **integral types**:
- byte
- short
- int
- long

To use a binary literal, prefix it with:

```java
0b   or   0B
```

Java automatically converts the binary digits into their decimal value.

**Example**
```java
int num = 0B111;
System.out.println("The number value is = "+ num); 
// This will print 7 on the console
```

---

## Code Example: BinaryLiterals

```java
public static void main(String[] args) {

    byte byteBinary = 0b111;
    short shortBinary = 0B001;
    int intBinary = 0B101;
    long longBinary = 0b0000011101100011;

    System.out.println("The value of byte number is : " + byteBinary);
    System.out.println("The value of short number is : " + shortBinary);
    System.out.println("The value of int number is : " + intBinary);
    System.out.println("The value of long number is : " + longBinary);

    int num = 5;
    System.out.println("Is Decimal and Binary value is same ? : " + (intBinary == num));
    System.out.println("The value of long after multiplication is: " + (longBinary * 2));
}
```

**Output**
```java
The value of byte number is : 7
The value of short number is : 1
The value of int number is : 5
The value of long number is : 1891
Is Decimal and Binary value is same ? : true
The value of long after multiplication is: 3782
```

---