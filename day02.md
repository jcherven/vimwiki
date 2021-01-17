# Week 01 day 02 copied from Geo

## Review:

* Creating a project
* Creating a Class
* Writing main method (reason for having a class: methods must belong to a class, main method must exist as entry way into app)
* What is Java? Features?
   * What is a statically typed language?
   * What is a compiled language?
* JDK -> JRE -> JVM
   * JVM: Translates/Converts bytecode into machine code (DON’T SAY COMPILE)
   * What are each? Usage?
   * Don’t need JDK to run Java apps, only for creating it
* Primitives
* Control Flow Statements
   * For
      * forEach (for arrays)
   * While
   * Do while
   * If / if else
   * Switch
   * Possibly also try/catch

## Class Notes:

### Java Syntax Typing:
* Class: Titlecase (ApplesAndFruit)
* Methods & Variables: Camelcase (applesAndFruit)
* Packages: lowercase (applesandfruit)

### What is a Java Array?
* Fixed, ordered set of data w/ same datatype, in allocation of memory.

* Is a list of items that are iterable and the size of the array is immutable
* Each element in the array have to be of the same data type
* Positions are indexed

Limitation of Enhanced For and Foreach loop is that we can’t decrement nor can we increment by any other number than 1.

break: terminates the loop
continue: Terminates the current loop but will carry on the loop if the loop condition is still met

You can’t add a break or continue statement inside of an if/else if but you can have it inside of an if/else if when the if else/if statement is inside of a loop.

```java
if() {
  break;     
}

for() {
  if() {
    break;
  }
}
```

### POJOs (objects)
POJO = Plain old Java object
Analagous to "real objects" or any data entity we plan on working with

Should always have a “Driver” or “MainDriver” class that has our main class.
Auto-import with Eclipse/STS:
Ctrl + shift + O

### Access Modifiers:

(Most restrictive to least restrictive)
* Private: Only accessible inside the class
* Default (implicit): Accessible within the same class and other classes within the same package.
* Protected : Accessible within the same class and other classes within the same package additionally accessible to child classes that inherit from it.
* Public: Accessed anywhere in the project

### Terminology:

Functions: Takes in arguments, executes logic, returns a value
Methods: is a function associated with an object
Procedures: takes in arguments, executes logic, does not return a value (void)

extends - IS-A relationship
new - HAS-A relationship

When no constructor is defined, the JVM will provide a constructor, specifically a no args constructor:

* If we implement our own constructor, we can implement our own logic.

### Overloading:

Can overload methods using the same method name as long as each method has different arguments. BUT changing the data type does not constitute a large enough difference because JVM will confuse one for the other since we don’t specify the data type returned when calling the method.


#### How do we overload?
- Change the number of arguments
- change the data type
- change the order of arguments/params

### The Object Class:
* Every class in Java is a child class of the Object class (i.e., the root class)
* Object class comes with some methods built in:
   * Some regarding threads: notiff(), notifyall(), wait()...
   * .toString(), which will print out our object as a string
   * .toClass() will return the class and package
   * .toHashCode() will return a hashed representation of the object

### Tangent:
        Hashing vs Encryption:
* Encryption is two-way. When you encrypt a value you expect to decrypt it.
* Hashing is one-way. 

### Inheritance:

In homogeneous inheritance:
* Class -> Class: extends
* Abstract Class -> Class: extends
* Class -> Abstract Class: extends
* Interface -> Interface: extends

In heterogeneous inheritance:
* Interface -> Class: implements

Definition of Inheritance:
* Allows you to adopt/inherit the method and variables (behaviors and attributes).
* Allows us to reuse code
* A -> B -> C, C will have access to all the methods and variables in B and A (assuming appropriate access modifiers).
* C’s will have all of A’s and B’s methods and attributes
* B will have access to all of A’s methods and variables but not C’s
* A will not have access to methods and variables from B or C

public void jumpAHurdle()

Overriding is modifying methods that we inherit from a parent class.
We need to use @Override because it provides meta data to JVM to tell us that this method is being inherited.


Return type and the method signature has to be the same unlike method overloading.


### Casting:

IS-A relationship

Downcasting is dangerous

### Memory:

#### Stack:
Specific to each thread, and stores variables and reference variables.
(h1, a1, h2, ath1, a2)
#### Heap:
Stores objects, this is where the memory allocation is. Much larger than the stack, all threads have access to the same heap. However it is slower to access and retrieve data from. 
(Animal, Animal, Human)

When we instantiate a new object, we are pointing the object name (h1) in the stack to the Human object in the heap. Every time we use the “new” keyword, we are creating a new object in the heap.

#### Why would we want to do this?
Well we might like the implementation of a child classes method in certain scenarios. 
We might still want a Human implementation but just a specific method implementation from Athlete.

### Interfaces:

Interface and Abstract classes are how Abstractions in Java is implemented!
Interfaces are for abstraction (before Java8/7) and Abstract classes are partial abstraction.
* Hiding it’s inner working from the user.
* Focus more on the behavior rather than the implementation
* More on what it does as opposed to how
* 

In an interface, we basically create a “contract”.
The contract is stating that we want our entity to be able to:
* accelerate()
* brake()
* steer()
* refuel()
* start()
* stop()

We don’t care how it does it, we are setting a contract on what to expect.
* Still an IS-A relationship
* We physically cannot make anything in memory because interfaces DO NOT HAVE CONSTRUCTORS

Variables in Interfaces must be `public static final` because they should be shared and implemented.

static: belongs to the data type Car, not an instance of it.

final: makes variables a constant //immutable, cannot change the variable once it’s been defined.

### Abstract Classes:
* Partial abstractions
* Abstract classes 

Classes can only, at-most, inherit from one class. Whereas with interfaces, 

Multiple-inheritance (extending more than one class) is NOT allowed because if classes have the same method signature, but with different implementations then Java gets confused.

This isn’t a problem with interfaces because there is no implementation, just contracts.

Note: Cannot have static classes

what does the final keyword do in methods and classes?

### --- Ben’s notes ---

OOP
    Inheritance:
        Multiple level inheritance (grandfather to child)
        Sharing constructors
        super keyword 
        extends and implements keyword. 


    Abstraction:
        What it is? Why we do it?
        Implementations:
            (Full) Interface
            (Partial) Abstract Classes 


    Polymorphism:
        Overloading (what these are and how to achieve it)
        Overriding (when can I override)
            Can I override Constructors?


    Arrays, For each loops, break and continue keywords.
