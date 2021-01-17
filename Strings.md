# Java Basics

## Strings

The package java.lang is a special package in Java – it’s the default
one,which means it’s implicitly imported into all Java classes. Therefore, it
requires no package declaration. Many useful classes come from this package
including System and String. The String class is special in Java for several
reasons:For one, it can be instantiated in two different ways unlike all other
classes. But most importantly, string objects are often recycled by the JVM
instead of creating new ones every time. This is called the string pool. This
is important, because the String class is immutable in Java,which means String
objects cannot be changed once they are created.

`one = "Hello"`
`two = "Hello"`
| Reference Variables | Heap Memory        |
|---------------------|--------------------|
| String one          | String0x1: "Hello" |
| String two          | String0x1: "Hello" |
--------------------------------------------

Here’s an illustration of how this works. On the left, we have our reference
variables. Remember that a reference variable in Java is not an object in its
own right,it’s a link to an instance of an object in memory. On the right, we
have a crude representation of the JVM’s heap memory, where objects are stored.
When we create a String object , either in the “primitive” style or as a new
object,a String object is created in memory that holds the value we assign it
Strings are immutable,so if we try to change the value of the String in our
reference variable,the JVM actually creates a new String object, and redirects
our reference.

The orphaned String object will be cleaned up by the garbage collection process
later,to free up the memory it’s using. 

If I have a String variable here, and I initialize it to “Hello”,what happens
when I create a second String with the value “Hello”?Well, because Strings are
immutable,the JVM decides that it should be safe for these two variables to
share the same instance,and so they will both be directed to the same object in
memory. This helps save memory where you might have hundreds of Strings with
the same value in a very large applications. 

`one = "Hello"`
`two = new String ("Hello");`
| Reference Variables | Heap Memory        |
|---------------------|--------------------|
| String one          | String0x1: "Hello" |
| String two          | String0x2: "Hello" |
--------------------------------------------

There is a way to override this though – if we use the new keyword to force a
new String object to be instantiated,we can force the JVM to have duplicate
Strings in memory. 

Here in eclipse we will be investigating the creation of a string object using
the two different ways we just learned. 

```java
package examples;

public class StringTest {
  public static void main(String[] args) {
    String stringA = "Hello";
    String stringB = new String("Hello");
    
    System.out.println("String A: " + stringA);
    System.out.println("String B: " + stringB);
    
    if (stringA == stringB)
      System.out.println("stringA and stringB point to the same object");
    else
      System.out.println("stringA and stringB do NOT point to the same object");
  }
}
```

Recall this behavior is unique to the String class. Nowhere else in Java can
you create an object of a class without using the “new” operator. Using the
“primitive” approach we have the following line of code:Its Looks simple enough
but it is quite profound since string is an object NOT a primitive. Java
magically creates the “Hello” object in memory using a simple assignment. What
makes more sense to the student of Object Oriented Programming is the “object”
approach to string creation given in this line of code:

```java
String stringA = "Hello";
```

Here we have passed the desired string as a constructor argument. If we print
them both, we’ll see that they both have the same value, but they are not the
same object.

```output
String A: Hello
String B: Hello
stringA and stringB do NOT point to the same object
```

There are a number of useful methods in the string class, and you should become
very familiar with them. Many common interview questions test knowledge of how
Strings in Java work,and the best ways to manipulate them.  You can find links
to the documentation in the reference section.

Let’s look at some of the most commonly used String methods. Here in eclipse,
we have created a few strings to work with.

```java
String string1 = "hello";
String string2 = new String("Hello");

String.length() -> 5
String.toUpperCase() -> HELLO
String.toLowerCase() -> hello
String.indexOf('e') -> 1
String.lastIndexOf('l') -> 3
String.charAt(4) -> o
String1.equals(String2) -> false
String1.equalsIgnoreCase(string2) -> true
```

For the first string,that is string1, we have used several of the methods in
the String API – which is short for “application programming interface. ”An API
is just a library of functions you can use to interact with a program or
component.

For the second string, that is string2,we perform a comparison using the .
equals method and string1. The results of running this code appear on the
console at the bottom. 

Most of the string methods are self explanatory. 

- Length returns the number of characters in the string. 
- toUppercase converts all characters to uppercase, and tolowerCase converts
  all characters to lowercase. 
- indexOf returns the index of the first occurrence of a specific character. If
  no occurrence is found a -1 is returned.  Bear in mind, that the first
  element has an index of zero. 
- lastIndexOf returns the index of the last occurrence of a specific character. 
- charAt returns a character for a given index and throws an exception if the
  index is larger than possible for the given string. 

For the string comparisons, notice the first attempt with . equals fails
because of the capital letter in String 1,However, use of the equalsIgnoreCase
method results in a “true. ”

The String class is a very special class in Java. It comes from the java. lang
package and has a rich API. Because it is an immutable class, care must be
taken not to continually redefine string references which results in wasted
memory. 
