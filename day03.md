# Week 01 day 03

## final keyword with classes & methods

what does the final keyword do to methods and what does it do to classes?

- final interfaces can't be extended, only the existing methods can be implemented
- final methods are inherited, but can't be overridden. 
- final classes can't be extended
- final variables can be blank. these can be initialized once and only once per object, in the instantiated object's constructor.
- final properties (variables) should be all caps, like constants in other languages
- final used in a method parameter can't be changed anywhere in the function
- a constructor is never inherited, so it can't be declared final. besides, we have the ability to declare the class final.

## protected

why does trying to make an interface protected give you an error in the IDE?
- ??

## Day 02 review

### inheritance

#### What is Inheritance:

- a child object inherits all the features, datatypes, variables, and methods
- an example of an IS-A relationship
- parent passes on generic information that could be specialised into its own unique instance (perhaps this is more polymorphic than inheritance)
- multiple inheritance of classes is not supported
- is A -> B -> C multiple inheritance? :
  - no. each has only one direct parent, and each child class only extends one class. rather, this is an inheritance chain
- multiple inheritance of interfaces is supported, however

In open ended questions like this, structure the answer for yourself like so: what, why, and how. Above describes what it is, now answer the rest.

#### why:

- promotes reusability
- buildes up on existing code
- readability, code is segmented and easy to see where everything is getting data from

#### how is it done in java:

- using the extends keyword to create child classes
- using the implements keyword for interfaces

### polymorphism

#### what is polymorphism:

- and object's ability to take on many forms
- an object is not bound by the restrictions of an IS-A relationship.

#### why use polymorphism:

- allows a single variable to store multiple datatypes
- Two scenarios that you'll be grilled on:
  - it gives us flexibility in our code to change the behavior of entities

#### how do you use polymorphism:

- you will be asked about this
- overriding and overloading methods:
  - overriding is changes the behavior of an inherited method in the more specific child class. has the exact same method signature and return type
  - (benjamin goes on a tangent here):
    - access modifiers can't be made more protective in overrides. they can be made more permissive though:
      - `public void drive(){}` cannot become `protected void drive(){}` in a `@Override`
    - an example of Runtime Polymorphism
    - the rr in override can stand for 'runtime' to help you remember which is which
  - overloading:
    - (ran out of time to cover this)
    - methods:
      - the same method name, different parameter
      - parameter can have different order, count, or datatypes
      - what about return type?
      - the parameter arg names can be different or the same, as they are local to the method
      - methods must be on the same level of access
      - an example of Compile Time Polymorphism

### encapsulation

#### what is encapsulation:

- hiding important information, restricting access
- process of wrapping the members and mthods into a single unit so we have full control over how it's accessed

#### why use ecapsulation:

- hide the data to protect it from unsafe changes

#### how to use enacapsulation:

- private variables
- public getters and setters

### abstraction

#### what is abstraction:

- hiding implementation to show functionality 

#### why use abstraction:

- simplify code, reduce complexity by capitalizing on functionality
- allows us one to focus on their own responsibilities
- avoids reinventing the wheel to do simple things

### interfaces

### abstract classes

interfaces (full) and abstract classes (partial)

### Access Modifiers

- public
- protected (default)
- private
- 

## Day 3 material

#### POJO vs Java Beans

when we create models, we have to encapsulate our object. we'll use private variables to protect them from accidental modification, and use public getters and setters to read an write them on a privileged basis.

```java
//com.example.propper.pojo.User.java


private String name;
private String emailAddress;
private long idNumber;
private boolean adminPrivileges;

//getts and setter for name
public String getName() {
  return this.name;
}

public void setName(String name) {
  this.name = name;
}
```
```java
//com.example.Driver.java

public static void main(String[] arggs) {
User user1 = new User();

user1.setName("Bob");
System.out.println(user1.getName());
// prints out `Bob`
}
```

This is long winded but allows us to put business logic in the setter and getter methods. It's much more powerful than this simple example. You can add data validation with regex, a security check, write a log, etc.

we want to create a valid toString() mehtod
we want to 

##### Overriding the toString() method

This can make a getter very powerful.

```java
@Override
public String toString() {
  return "";
}
```

The return of the overridden toString() method could be something like `"User = {name: " + this.name + "}"` and give the caller some json, for instance.

Eclipse will generate this for you automatically via menu. That's how common this is to do. It's considered a best practice to encapsulate by overriding the toString() method of the Object class.

- The point here is that a getter can keep you from rewriting the same code every time you want to get some data. Put your business logic in the getter, make that getter the official way to get data from your object, and it will be run the "right way" according to your business logic every time.

### benj's constructor tangent
benj likes to generate two constructors, which eclipse can provide for you.
- ?? (review recording to get this part)
- an all-args constructor from fields

Here's a good template for what to do when making a new child class:
- private variables
- public getters and setters
- toString()
- Constructors

## Scanner Object

### what's the Scanner?

It's a `final` class that receives input from, for instance, console input from the user.

The Scanner package in in one of the core libraries, `java.util`.

```java
// com.example.scanner.ScannerDriver.java
import java.util.Scanner;

// instantiate a new Scanner object, pass in the system input stream
Scanner sc = new Scanner(System.in);
System.out.println("Welcome User, please give us an input.");

// there are many methods for input, but nextLine() will wait for the next console input.
String input = sc.nextLine();

System.out.println(input + "was entered.");
// prints to the console just what you'd expect here.
```

- student question: when sc.next() is used, what datatype is it using? :
  - you can pass in args, and the IDE will show you all of the different overloaded ways you can call `next()`
- is there something like a template literal in javascript? :
  - not in the java libs. maybe with a 3rd party lib.

- independent assignment for fun:
  - play around making some small apps that get user input and does stuff with the Scanner lib.

#### in class assignment app:

typically assignments will involve the use of things that haven't been taught in class. it's up to you to research what you need.

- console menu for ordering food:
  - order one at a time
  - order more? yes or no
  - return itemized list of all items ordered and total price

```
Create a basic cafe interface
Cafe will contain a set of items from a menu. 
    The Menu will contain food and drink items.

As a customer I can "purchase" multiple food items through a console menu. 

The console will return the completed order 
    (number of items and the cost of associated order)
```

#### benj's solution for the console cafe

1. create a main driver
2. consider the data structures needed
3. class MenuItems would use name, calories, price
4. makes some getters and setters in the constructor
5. make another class called Food, one called Drink
6. these can extend MenuItem
7. Drink can have a local property called capacity
8. generate getters and setters for drink
9. override the toString() to return the calculation of the drink price and capacity
10. create a package repo
11. create a class kitchen storage in repo which contains all the instances of your models
12. store list of items in a private array menuItems[4]
13. manually hardcode the items into the array
14. make a mthod that returns a menu items array of all the menu items
15. in main, run a method that displays intro/greeting
16. in main, run a while loop for the ordering logic
17. the while loop has a ordering = true boolean flag to persist the loop while the user has more items to order
18. display the menu
19. start the scanner outside of the loop as it can be reused for multiple user inputs
20. use if blocks or a switch to accept the order item
21. ask the user if they are done, this input sets the ordering flag
22. if ordering flad is set flase, break out of the while loop
23. if ordering is false, display the order and total

## Working with Strings

### Stack and Heap review

memory in java is generally divided by stack and heap.

#### Stack:
- much faster than the heap
- quicker retrievals
- contains primitive vars and object reference vars
- used by a thread (memory is only accessible the thread using it)
- cleared onced the thread is finished with it

#### Heap:
- much more storage capacity
- contains the instantiated objects
- globally accessible to the system (all threads)
- memory is not cleared until the application is closed

### pass by value vs pass by reference

#### PBV
- creates a copy when we assign it

#### PBR
- points to the exact same instance of the object

### building up to the string
string is an object with an array of chars. allows creation and manipulation of strings.

the String class is immutable and the class is final. the string can't be changed, and the class cannot be extended.

```java
String s1 = "Hello!";
// text in double quotes are a string literal.
// there's a string pool in the heap.

string s2 = "Hello Again";

String s3 = s1;
System.out.println(s3);
//prints Hello!
s3 = "Hi";
// both s1 and s3 should be modified right? No.
System.out.println(s3);
// prints Hi
System.out.println(s1);
// prints Hello!
```

This demonstrates that strings can't be changed. a string literal is created in the string pool (part of the heap). if two String objects are created with the same string literal value, they point to the same object in the string pool. (it checks if the value exists already, and if yes, the new variable points to it in the string pool). strings are integral to java. they are so important that java tries to optimize the memory they use.

```java
System.out.println(s1 == s3);
// prints true
String s4 = "Hello!";
System.out.println(s1 == s4);
// prints true
String s3 = new String("Hello!");
System.out.println(s1 == s4);
// prints false. don't do this, because it goes around java's memory management strategy for no good reason.
```

The reason strings are immutable because it protects existing strings in the string pool from being messed with in this memory optimization strategy. The string is unique from other objects in this manner. other objects don't get this kind of memory management strategy.

### string methods

```java
s2.charAt(2); // returns the char at position 2
s2.length(); // should be obvious
s2.substring(3,4); // returns a string of chars between 3 and 4 inclusive
s2. indexOf("abc"); // what happens if this doesn't exist?
s2.toLowerCase(); //does nothing
s2 = s2.toLowerCase(); // creates a new literal in the string pool with s2 in all lowers, and now s2 points to the new string literal
```

## memory allocation tangent: garbage collection in java

GC is the reason java programmers don't need to worry about memory allocation (out of memory errors), which is the source of a lot of security and stability issues with other languages. you can be lazy and bad in java. just kidding. but it is less complex and a little more chill. 

the garbage collector is a daemon thread (daemon - always present, thread - isolated sequence of code execution). its purpose is to clear the HEAP memory to free up space for other objects. you don't have to malloc() and free(). it remove objects that are eligible for removal.

what does it take to get marked for GC?
- be unreachable (have no more references pointing to you)

how do you remove the reference?
```java
// nullify the reference
Object o1 = new Object();
o1 = null;

// reassign the ref
Object o2 = new Object();
Object o3 = new Object();
o2 = o3; // o2 in the heap will be GC'd

// create an object in a method
// (see recorind to get this part)
```

in general the GC only runs when the system is running out of memory. but you can invoke it maybe? 

```java
System.gc();
// kind of finicky, it's more of a request than a command. it might or might not actually come and collect garbage.
```

let's override it.

```java
@Override
public void finalize() {
  // this is a method of the Object class that is called just before the GC comes around
  // this allows you to execute some code before the object is destroyed.
  // sometimes calling finalize() might invoke the GC. depends on what the JVM is doing.
  System.out.println("Help me");
}

Object o1 = new Garbage();
o1 = null;
// if the jvm decides to send the GC after o1, you should see it screaming in the console.
```

Finalize can be leveraged to do some cleanup of db connections, network connections, complete a read/write op, etc.

## Collections

### why use the collections framework?

- array objects in java are limited
  - how about a custom method that takes an array and a new element, and it will automatically extend the length of the array?
  - sure, but it's not generalized. others can't use it without some extra work.

in java we use the collections framework instead. it's called a framework, but it's more like a library. it provides interfaces and classes that allow developers to more easily manage groups of objects.

a 'collection' object is designed to store a group of objects with more flexibility than an array.

### advantages

- reduced effort (provides DS&A for you, already implemented. just call the method.)
- better performance (someone else already figured out the best way to implement your DS&A)
- encourages software reuse (provides standard interfaces)

#### collections hierarchy

- the hierarchy is as such:
  - iterable (an interface)
    - collection (an interface)
      - list (in interface)
        - ArrayList (a class)
      - set (an interface)
      - queue (an interface)
        

### lists

`<>` denote generics. they're called angle brackets. don't make a shape with your hands in your interviews, call it by its name.

Generics enforce type safety. when we define a collection entity with <ClassType> that means it will check the entity being added to the DS is of the correct type.

```java
// import these from java awt
import java.awt.util.List;
import java.awt.util.ArrayList;

// you need a child class to instantiate this, because it's an interface.
List<Integer> listOfInts = new ArrayList<Integer>();
// you can also leave the angle brackets empty in the new constructor call if you want
listOfInts.add(73);
listOfInts.add(76);
listOfInts.add(79);

System.out.prinln(listOfInts);
// prints [73, 76, 79]
// the order is kept, in order that elements were added
System.out.prinln(listOfInts.get(1));
// prints 76

listOfInts.add(0, 1000);
// puts the value 1000 at position 0. this add method is overloaded.
```
### what's a list:

- A list is an ordered collection
- it can contain duplicate elements.
- access via index (positional access)
- for lists to be equal, they have to have the same elements in the same position
- 

### nice methods:

these are generally self explanatory:
- .get()
- .set()
- .add()
- .addAll() will append the passed in list
- .remove()
- .indexOf()
- .lastIndexOf()
- .sublist() (sic)
- .contains()

## maven

review the recording for the steps to create and work with maven projects in the IDE.

Maven helps you more easily include 3rd party libraries (dependencies) into a java project. it takes a bit more work without Maven.

The pom.xml is the project config file.

## P0 part 1

- Project 1 part 1.
- Due Monday the 14th

A console based bank app. See docs for details.

You're being tested on what you learned this week, not on what other technologies you know.

Do take some time to make sure the presentation will be good. No powerpoint is necessary. But have a working app first and foremost.

## self learning for this day

- wrapper classes
- boxing
- unboxing
- autoboxing
