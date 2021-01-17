# Exceptions?

Exceptions are events that occur during the execution of programs that disrupt
the normal flow of instructions (e.g. divide by zero, array access out of
bound, etc.). 

In Java, an exception is an object that wraps an error event that occurred
within a method and contains: 

    - Information about the error including its type 
    - The state of the program when the error occurred 
    - Optionally, other custom information 

## Categories of Exceptions : 

    - Checked Exceptions
    - Unchecked Exceptions
    - Errors

## Checked Exceptions

Checked exceptions are those that : 

    - The compiler enforces that you handle them explicitly. 
    - Methods that generate checked exceptions must declare that they throw
      them. 
    - Methods that invoke other methods that throw checked exceptions must
      either handle them (they can be reasonably expected to recover) or let
      them propagate by declaring that they throw them. 

## Example

If you use FileReader class in your program to read data from a file, if the
file specified in its constructor doesn't exist, then a FileNotFoundException
occurs, and the compiler prompts the programmer to handle the exception. 

```java
import java.io.File;
import java.io.FileReader;

public class FilenotFoundDemo {

   public static void main(String args[]) {    
      // If the file does not exist an exception is thrown.
      // That exception is called as FileNotFoundException
      File file = new File("E://file.txt");
      FileReader fr = new FileReader(file); 
   }

}
```

## Unchecked Exceptions

    - Errors and RuntimeExceptions are unchecked — that is, the compiler does
      not enforce (check) that you handle them explicitly. 
    - Methods do not have to declare that they throw them (in the method
      signatures). 
    - It is assumed that the application cannot do anything to recover from
      these exceptions (at runtime). 

## Example

If you have declared an array of size 5 in your program, and trying to call the
6th element of the array then an ArrayIndexOutOfBoundsException occurs. 

```java
public class Unchecked_Demo {

   public static void main(String args[]) {
      int num[] = {1, 2, 3, 4};
      System.out.println(num[5]);
   }
}
```

## Errors

These are not exceptions at all, but problems that arise beyond the control of
the user or the programmer. Errors are typically ignored in your code because
you can rarely do anything about an error. For example, if a stack overflow
occurs, an error will arise. They are also ignored at the time of compilation. 

## Exception Hierarchy

 All exception classes are subtypes of the java.lang.Exception class. The
 exception class is a subclass of the Throwable class. Other than the exception
 class there is another subclass called Error which is derived from the
 Throwable class. 
 
## Catching Exceptions

A method catches an exception using a combination of the try and catch
keywords. A try/catch block is placed around the code that might generate an
exception. Code within a try/catch block is referred to as protected code, and
the syntax for using try/catch looks like the following 

```java
try {
   // Protected code
} catch (ExceptionName e1) {
   // Catch block
}
```

The code which is prone to exceptions is placed in the try block. When an
exception occurs, that exception occurred is handled by catch block associated
with it. Every try block should be immediately followed either by a catch block
or finally block.

A catch statement involves declaring the type of exception you are trying to
catch. If an exception occurs in protected code, the catch block (or blocks)
that follows the try is checked. If the type of exception that occurred is
listed in a catch block, the exception is passed to the catch block much as an
argument is passed into a method parameter.

## Example

The following is an array declared with 2 elements. Then the code tries to
access the 3rd element of the array which throws an exception. 

```java
// File Name : ExcepTest.java
import java.io.*;

public class ExcepTest {
   public static void main(String args[]) {
      try {
         int a[] = new int[2]; // Size 2
         System.out.println("Access element three :" + a[3]); // Accessing 3rd element
      } catch (ArrayIndexOutOfBoundsException e) {
         System.out.println("Exception thrown  :" + e);
      }
      System.out.println("Out of the block");
   }
}
```

## The Throw/Throws Keyword

    - If a method does not handle a checked exception, the method must declare
      it using the throws keyword. The throws keyword appears at the end of a
      method's signature. 
    - One can throw an exception, either a newly instantiated one or an
      exception that you just caught, by using the throw keyword. 
    - Understand the difference between throws and throw keywords, throws is
      used to postpone the handling of a checked exception and throw is used to
      invoke an exception explicitly. 

## Example

```java
import java.io.*;

public class className {
   public void deposit(double amount) throws RemoteException {
      // Method implementation
      throw new RemoteException();
   }
   // Remainder of class definition
}
```

## Finally Block

The finally block follows a try block or a catch block. A finally block of code
always executes, irrespective of occurrence of an Exception.

Using a finally block allows you to run any cleanup-type statements that you
want to execute, no matter what happens in the protected code.

A finally block appears at the end of the catch blocks and has the following
syntax 

```java
try {
   // Protected code
} catch (ExceptionType1 e1) {
   // Catch block
} catch (ExceptionType2 e2) {
   // Catch block
} catch (ExceptionType3 e3) {
   // Catch block
}finally {
   // The finally block always executes.
}
```

## Example

```java
public class ExcepTest {
   public static void main(String args[]) {
      int a[] = new int[2]; // Size 2
      try {
         System.out.println("Access element three :" + a[3]); // Accessing 3rd element
      } catch (ArrayIndexOutOfBoundsException e) {
         System.out.println("Exception thrown  :" + e);
      }finally { // Always executed no matter what!
         a[0] = 6;
         System.out.println("First element value: " + a[0]);
         System.out.println("The finally statement is executed");
      }
   }
}
```

Output : 

```
Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
First element value: 6
The finally statement is executed
```

