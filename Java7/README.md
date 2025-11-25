# Summary of Java7 new features 

THE TRY-WITH-RESOURCES STATEMENT
JVM handles closing the resources opened in the code
automatically after the try block by calling close().
01
SUPPRESSED EXCEPTIONS
Handles the scenarios where we get multiple exceptions
by holding all the subsequent exceptions inside an
array.
02
CATCHING MULTIPLE EXCEPTIONS
A single catch block can handle multiple exceptions
using a | operator if we have similar action need to be
taken.
03
RETHROWING EXCEPTIONS WITH TYPE CHECKING
Enables to specify more specific exception types in the
throws clause of a method declaration.
04
EASIER EXCEPTION HANDLING FOR REFLECTIONS
Introduces a single exception that replace multiple exceptions
that need to be handles when we are invoking methods using
reflections.

OBJECTS CLASS & NULL CHECKS
requireNonNull methods inside Objects class can be
used to check null values of an Object
06
CLOSE METHOD INSIDE URLCLASSLOADER
Provided a new close method inside the URLClassLoader
which will be invoked by JVM to avoid memory leaks.
07
ENHANCEMENTS TO FILES & DIRECTORIES
New interfaces, classes like Path, Paths, Files introduced
to make the operations on files and directories easy.
08
WATCHSERVICE
Provides easier approach to track any directory/ files
changes instead of using Threads.
09
BINARY LITERALS & STRING IN SWITCH STATEMENT
Binary representation of numbers can be easily transferred
/assigned to decimal representation using a prefix 0b/0B. And
Strings are allowed inside the Switch statements

TYPE INFERENCE/DIAMOND OPERATOR
11 Simplifies the use of generics when creating an object
USING UNDERSCORE IN NUMERIC LITERALS
Improves the readability of the long numbers as it
allows ‘_’
inside the numeric values.
12
JDBC IMPROVEMENTS
JDBC library is optimized to use the try-with-resources
features and added new approaches to create RowSet
classes.
13
GARBAGE-FIRST COLLECTOR
A new garbage framework is build to handle
applications that have large heap sizes.
14
FORK & JOIN FRAMEWORK
A new framework that will process huge tasks parallelly by
levering all the CPU cores available.

