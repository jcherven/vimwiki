# Classes and Objects
## Object

Any entity that has state and behavior is known as an object. For example a
chair, pen, table, keyboard, bike, etc. It can be physical or logical.

An Object can be defined as an instance of a class. An object contains an
address and takes up some space in memory. Objects can communicate without
knowing the details of each other's data or code. The only necessary thing is
the type of message accepted and the type of response returned by the objects.

Example: A dog is an object because it has states like color, name, breed, etc.
as well as behaviors like wagging the tail, barking, eating, etc. 

## Class

A class, in the context of Java, are templates that are used to create objects,
and to define object data types and methods. Core properties include the data
types and methods that may be used by the object 

A class can also be defined as a blueprint from which you can create an
individual object. Class doesn't consume any space.

## Advantages of OOPs over Procedure Oriented Programming

    -OOPs makes development and maintenance easier whereas in a
    procedure-oriented programming language it is not easy to manage if code
    grows as project size increases.  -OOPs provides data hiding whereas in a
    procedure-oriented programming language a global data can be accessed from
    anywhere. 

```java
public class Dog {
   String breed;
   int age;
   String color;

   void barking() {}

   void hungry() {}

   void sleeping() {}

}
```

A class is a blueprint from which individual objects are created.

The code above is a sample of a class Dog with attributes and behavior. 

NEXT: [Constructors](Constructors)
< [OOP Study Guide](OOP-Study-Guide)
< [Index](Index)
