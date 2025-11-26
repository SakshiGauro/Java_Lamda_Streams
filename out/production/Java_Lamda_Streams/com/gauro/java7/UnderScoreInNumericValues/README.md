# Using Underscore In Numeric Values

From Java 7, we can use the underscore(_) inside the numeric values to improve readability of
the code. However the compiler will remove them internally while processing the numeric
values.
• For example if our code contains numbers with many digits, we can use an underscore
character to separate digits in groups of three, similar to how we would use a punctuation
mark like a comma in mathematics.
int num = 1_00_00_000;
• But please note that below restrictions while using the underscore inside your numeric values,
✓ It is not allowed at the beginning or end of a number
✓ It is not allowed adjacent to a decimal point
✓ It is not allowed prior to an L or F suffix that we use to indicate long/float numbers
✓ It is not allowed where a string of digits is expected.
int num = _6, 6_, 6._0, 6_.0,6_54_00_L, 6_54_00_F, 0B_0101

```java
int inum = 10_000_456;
System.out.println("Integer value using underscore is :" + inum);
long lnum = 10_000_456;
System.out.println("Long value using underscore is :" + lnum);
float fnum = 3.14_13_25F;
System.out.println("Float value using underscore is :" + fnum);
double dnum = 64_565.579_31_23;
System.out.println("Double value using underscore is :" + dnum);
long longBinary = 0b0_000_011_101_100_011;
System.out.println("Decimal value of Binary representation using underscore is :" + longBinary);
```

Output
```java

```