# Rethrowing Exceptions with more inclusive type checking

The Java SE 7 compiler performs more precise analysis of rethrown exceptions than earlier
releases of Java SE. This enables you to specify more specific exception types in the throws
clause of a method declaration.
• Consider the below example,

```java
static class FirstException extends Exception { }

static class SecondException extends Exception { }

public static void beforeJava7(String exceptionName) throws Exception {
    try {
        if (exceptionName.equals("First")) {
            throw new FirstException();
        } else {
            throw new SecondException();
        }
    } catch (Exception e) {
        throw e;
    }
}
```
This examples' try block could throw either FirstException or SecondException. Suppose you
want to specify these exception types in the throws clause of the beforeJava7 method
declaration. In releases prior to Java SE 7, you cannot do so. Because the exception parameter
of the catch clause, e, is type Exception, and the catch block rethrows the exception parameter
e, you can only specify the exception type Exception in the throws clause of the beforeJava7
method declaration.
• However, in Java SE 7, you can specify the exception types FirstException and SecondException
in the throws clause in the rethrowException method declaration. The Java SE 7 compiler can
determine that the exception thrown by the statement throw e must have come from the try
block, and the only exceptions thrown by the try block can be FirstException and
SecondException. Even though the exception parameter of the catch clause, e, is type
Exception, the compiler can determine that it is an instance of either FirstException or
SecondException.

OutPut
```java
Exception in thread "main" com.gauro.java7.RethrowExceptions.RethrowExceptions$FirstException
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.beforeJava7(RethrowExceptions.java:31)
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.main(RethrowExceptions.java:18)
```
--- 

Code snipper with Java 7 new feature,

```java
static class FirstException extends Exception { }

static class SecondException extends Exception { }

public static void withJava7(String exceptionName) throws FirstException, SecondException {
    try {
        if (exceptionName.equals("First")) {
            throw new FirstException();
        } else {
            throw new SecondException();
        }
    } catch (Exception e) {
        throw e;
    }
}
```
- makes the methods more readable

Output

```java
Exception in thread "main" com.gauro.java7.RethrowExceptions.RethrowExceptions$FirstException
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.withJava7(RethrowExceptions.java:49)
	at com.gauro.java7.RethrowExceptions.RethrowExceptions.main(RethrowExceptions.java:19)
```
