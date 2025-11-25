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

