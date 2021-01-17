# exceptions

You’ve probably noticed in the course of writing your own programs, that
problems occurring in compilation or execution of your code are called
exceptions. The use of exceptions allows Java to deal with runtime problems in
a flexible manner. You can handle each type of exception in a different way,
and allow your application to continue without crashing. 

Exceptions in Java come in two forms: “checked and unchecked.” The term
“checked” means that the compiler will look for and catch the error, and you
will not be able to run your application until it’s fixed. An unchecked
exception will slip through, and crop up in the middle of execution,
potentially killing your application if not handled. 

  - `Throwable` (Checked)
    - `Error` (**Unchecked**)
    - `Exception` (Checked)
      - `IOException` (Checked)
      - `ClassNotFoundException` (Checked)
      - `RuntimeException` (**Unchecked**)
        - `ArithmeticException` (**Unchecked**)
        - `ClassCastException` (**Unchecked**)
        - `IndexOutOfBoundsException` (**Unchecked**)

Looking at the inheritance tree for the Exception class, we see at the top of
the tree is the Throwable class. It has two subclasses, Error and Exception.
Errors are things that have nothing to do with your Java program. They are rare
occurrences like the JVM running out of memory. 

The Exception class has over a hundred subclasses for which only three are
shown here. These subclasses are usually associated with being unable to locate
or connect to a resource such as a file, a database, another server, etc. 

The RuntimeException class represents the dividing line between checked and
unchecked exceptions. It too has over a hundred direct subclasses for which
only three of the more common ones are shown. Runtime exceptions are associated
with logic problems in your code such as accessing a non-existent array element
or division by zero or casting to something outside the inheritance tree. 

```java
public class ExceptionTest {
  public static void main(String[] args) {
    try {
      System.out.println("1 / 0 = " + (1 / 0));
    } catch (ArithmeticException e) {
      System.out.println("Caught an arithmetic exception!");
      // print the stack trace programtically
      e.printStackTrace();
    } finally {
      System.out.println("This is the optional \"finally\" block.");
    }
    System.out.println("The code has continued on, like normal!");
  }
}
```

Exceptions are handled in Java with a try/catch/finally block as shown here.
The try block contains code or method invocations which can throw exceptions.
The catch block grabs the thrown exception and executes the enclosed code. You
can have multiple catch blocks to handle different types of exceptions
differently. 

The finally block executes regardless of the outcome, even if there is a return
statement in the try block. Note that unchecked or runtime exceptions can also
be caught if desired. 

Here, we have deliberately created a program that makes a mathematical error.
It divides a number by zero. When we run this we get the ArithmeticException
which is a runtime exception. To handle this, we have placed a try/catch block
around the problematic print statement. The catch block will print the
exception’s stack trace, so we can see what went wrong, but because the
exception was caught, program execution can continue after printing the
stacktrace. 

The finally block would normally have code to properly close resources like
FileStreamReaders or connections to a database. Because we don’t have any of
that to do, we’ll just have our finally block print a statement. In this
example, program execution would continue immediately after the finally block
regardless if an exception is caught. When we run this program we get the
exception’s stack trace printed out programmatically, and we execute whatever
is in the finally block as shown. We can then see that statements occurring
after the try/catch block execute as expected, proving that the bug did not
crash the program like it might have otherwise. 

When catching multiple exceptions in Java, each catch statement will be
evaluated in order to determine if it applies to the exception being thrown,
and only the first applicable one will actually catch the exception. This can
cause unexpected results, if we catch an exception earlier than expected. 

Remember the inheritance tree for exceptions? Well, the principle of
polymorphism means that every ArithmeticException is also a RuntimeException,
which is also an Exception. Consider what happens if we catch a generic
Exception before catching the ArithmeticException. Now not only will the print
statement in the second catch block NOT execute for ArithmeticExceptions, it
won’t execute for any exceptions! This is because any exception will always be
caught by the catch block that handles the more generic Exception first. 

In Java a method does not need to handle an exception at all! Instead, you can
simply re-throw it to the calling code thereby getting rid of the problem. This
re-throwing can continue all the way back to the main method where throwing the
exception to the JVM may in fact crash the program. You should always be
careful to properly handle exceptions somewhere, if not where they immediately
occur. 

```java
import java.io.FileInputStream;

public class CheckedExceptionExample {
  public static void openFile() throws FileNotFoundException {
    new FileInputStream("C:\\DoesNotExist.txt");
  }
  public static void main(String[] args) {
    try {
      openFile();
    } catch (FileNotFoundException e) {
      e.printStackTrace();
    }
  }
}
```

Here we have created a program to demonstrate the policy regarding checked
exceptions. The main method calls a static method openFile. The FileInputStream
class has a constructor that accepts a filename. If the file is not found, the
constructor throws a FileNotFoundException. Since we have made the OpenFile
method throw the exception back to the calling code with the “throws” clause,
the compiler is now happy with the openFile method. However, we now need to
catch the exception in our main method. 

Exceptions are an elegant way to handle crashes, but there may be situations
where handling an exception is actually less preferable than letting an
application crash. This is typically the case when performance is so important
that you can’t waste processing time on handling exceptions, or when your
application is communicating remotely with another application, and you need to
keep the information exchanged between the two synchronized. For most
applications though, this isn’t the case, and handling exceptions can offer a
lot of protection. 

# lecture notes

Exceptions come in two forms: checked and unchecked. 

Checked exceptions are tested by the compiler. You need to handle these with code or you'll not be able to run your program.

Unchecked exceptions are not tested by the compiler. 

## Throwable Hierarchy

The Throwable classis the parent of all exceptions.

Error is a subclass of Throwable that represents conditions that are typically irrecoverable from; an example is the JVM running out of memory. 

Exception is also a subclass of Throwable. 

RuntimeException is a class that represents unchecked exceptions. This type of exception typically deals with logic errors in your program, such as division by zero or accessing an array index outside of its boundaries.

## Handling Exceptions

Use a try/catch/finally block to handle an exception. 

```java
try {
  //code that may throw exception
} catch (Exception e){
  //code to execute if exception is caught
} finally {
  //code to execute at the end if an exception is thrown or not 
}
```

A try block is used to contain code that can potentially throw an exception. 

A catch block is used to catch any exceptions that may be thrown from code in the try block. Afterwards, it will execute any code within its block.

A finally block is used to execute code regardless of if an exception is thrown (even if a return statement is in the try block)

NOTE: You can also catch RuntimeException or a subclass if you wanted.

## Multiple Catch Blocks

You can catch multiple exceptions by specifying multiple catch clauses.Ordermatters when writing multiple catch blocks. The least specific Exception class should be placed last (because it will catch any subclasses due to polymorphism)

## Re-throwing Exceptions

You can also re-throw an exception instead of using a try/catch block. To throw an Exception you'll use the throws keyword on the method that uses code that throws exceptions:

```java
public void methodName() throws Exception { 
  ...
}
```
