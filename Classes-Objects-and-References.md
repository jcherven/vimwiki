# Classes, Objects, and References

< [TOP](OOP-Concepts) | [Inheritance](Inheritance) >

Object Oriented Programming means breaking normally procedural code into
structures called Objects, where possible. Different programming languages go
about this in different ways, but there are some universal terms that are
important to understand.

Specifically, it's important to understand the difference between a **Class**,
an **Object**, and a **Reference Variable**.

A **class** is a template used to instantiate objects. It's also called a
**type** in some circumstances, such as when used with a reference variable. A
class used to instantiate an object determines what states and behaviors an
object will possess - as a template, the object will possess individual copies
of the states and behaviors defined in the class. A class used as the type for
a reference variable determines what behaviors of the referenced object can be
invoked.

An **object** is an instance of a class in memory. In most OOP languages, you
never interact with objects in memory directly. Instead, you interact with them
through their *reference*, which is the memory address used by the JVM to find
a particular object. Other OOP languages do allow you to manipulate objects
directly, but even these still use references most of the time.

A **reference variable** is a variable that stores the *reference* to an object
in memory. Just like the type of a primitive variable determines the range of
values that a primitive variable can store, the **type** of a reference
variable determines what **types** of objects a reference variable can store a
reference to. When a **class** is used as the **type** of a **reference
variable**, that reference can only be used to invoke behaviors of the object
that are declared in the **class/type**.

Example: 
```java
Animal someVar = new Animal();
  1      2            3
```
    1. The class/type of the reference variable
    2. The name of the reference variable
    3. The instantiation of a new object using the "`new`" keyword to invoke a
       constructor

    - The someVar reference variable does not contain an Animal object, it
      contains a reference that points to it in memory
    - The Animal type means that someVar can only store a reference to an
      object that is an instance of the Animal class (directly or through
      inheritance)
    - The Animal type means that someVar can only be used to invoke methods or
      access public variables present in the Animal class (whether defined in
      Animal or inherited from a superclass)
    - The "new Animal()" expression creates an object, it is not the object
      itself. You can never access the object directly. 

Understanding these concepts and their implications is key to properly
understanding OOP languages and concepts.

< [TOP](OOP-Concepts) | [Inheritance](Inheritance) >

Back to [OOP Concepts](OOP-Concepts)
