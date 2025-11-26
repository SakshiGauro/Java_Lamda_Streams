# Using Underscore In Numeric Values

Java 7 introduced the ability to use **underscores (`_`) inside numeric literals** to improve readability, especially for large numbers, similar to how we would use a punctuation
mark like a comma (,) in mathematics.

The JVM ignores underscores — they are **only for human readability.**

**Example:** 

```java
int num = 1_00_00_000;
```

---

### Rules & Restrictions

Underscores **cannot** be placed:
- At the beginning or end of a number

  `int x = _10; // ❌`
- Next to a decimal point

  `float f = 3._14; // ❌`
- Before a type suffix (L, F, etc.)

    `long l = 100_L; // ❌`
- Where digits are strictly expected

    `int x = 0B_0101; // ❌`

---

## Code Example: `UnderScoreInNumerics`

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

### Output
```java
Integer value using underscore is :10000456
Long value using underscore is :10000456
Float value using underscore is :3.141325
Double value using underscore is :64565.5793123
Decimal value of Binary representation using underscore is :1891
```

---