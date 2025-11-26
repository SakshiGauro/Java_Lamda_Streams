# Binary Literals

A binary literal is a number that is represented in 0s and 1s (binary digits). Java allows you to
express integral types (byte, short, int, and long) in a binary number system especially when
we are dealing with the bit-wise operators.
• To handle the scenarios where we need to express an long/integer/short/byte in binary
number system, Java 7 added a new feature called ‘Binary Literal’. We just need to add a prefix
of either 0b/0B Infront of the binary digit representation, then java will take care of converting
into a decimal representation value of it.
int num = 0B111;
System.out.println(“The number value is = "+ num); // This will print 7 on the console

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

Output
```java
The value of byte number is : 7
The value of short number is : 1
The value of int number is : 5
The value of long number is : 1891
Is Decimal and Binary value is same ? : true
The value of long after multiplication is: 3782
```