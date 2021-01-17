# Day 01 Notes copied from Geo

## What is Java?
* General purpose programming language following the OOP paradigm.
* Object Oriented Programming

## What are the features?
* WORA (Write once, run anywhere)
* Statically typed language (strongly typed)
* Compiled Language: Language has to be compiled first before its run
* Java code is turned into bytecode. Bytecode is converted into machine code by the JVM.
* Anything that can run a JVM, can run Java.
* Garbage collection
   * Don’t have to manage our memory allocation.
   * No need to manage pointers
* Java is simple to learn and easy to read. Based on C. 
* Java is secure: Due to a lack of manual memory management and no accessing out of bounds array. Means less chances of security flaws occurring such as stack corruption.
* Java is Open-source: lots of tools and IDEs, many frameworks, open source libraries. Lots and lots of documentation.

## What is OOP?
* Reusability
   * Less work that we and our machines need to do
* Encapsulation
* Polymorphism
* Abstraction
* Inheritance

The more you sell Java, the more you sell yourselves. Practice articulating your answers.

## Primitive Data Types:
* Java is not 100% OOP. It contains primitive, which are very basic data types:

| TYPE    | BYTESIZE | BITSIZE               |
|---------|----------|-----------------------|
| int     | 4 bytes  | 32 bits               |
| boolean |          | >= 1 bit, JVM decides |
| char    | 2 bytes  | 16 bits               |
| float   | 4 bytes  | 32 bits               |
| long    | 8 bytes  | 64 bits               |
| double  | 8 byte   | 64 bits               |
| byte    | 1 byte   | 8 bits                |
| short   | 2 bytes  | 16 bits               |

## Declaration and Assignment:
```java
Int varName; // Declaration

varName = 1; // Assignment
```
* Java variables can be reassigned values.  But can’t be assigned different datatypes.

```java
char charVariable = ‘a’;
// char must use single quotes and is limited to a single string character.
```

## Control Flow Statements:

```java
//Scenario: I want to add something 100 times.
Int myNumber = 0;
myNumber = myNumber + 50;
myNumber = myNumber + 50;
myNumber = myNumber + 50;
myNumber = myNumber + 50;
// ...etc
```

### for loop
```java
//for loop
// 1: declare a variable inside the scope of the for loop and give it an initial value;
// 2: Will specify the end condition (conditional expression);
// 3: Incrementing expression, specifies by how much we want to increment our incrementing variable

For (int i = 1; i <= 100; i++){
        System.out.println(i);
}
```

### while loop
```java
//while loop
// A while loop will loop as long as the conditional expression has been met
Int i = 1;
while(i <= 100) {
        I = i +10;
System.out.println(i);
}

// do while loop
Do {
        // The logic inside Do will execute at least once, regardless of whether the condition has been met

I = i + 10;
System.out.println(i); 
}while (i <= 100);
```

### switch statement
```java
//switch
// Switch gives you multiple expression to evaluate

char d = ‘m’;

switch(d) {
  case ‘t’:
    System.out.println(“Happy Tuesday or Thursday”);

  case ‘m’:
    //if a condition is met for a case, this block of code will execute
    System.out.println(“Happy Monday!”)
    break; 

  default:
    // We don’t need a condition for default to execute
    System.out.println(“Must be Friday or the weekend!”);
}
```
- Without a break statement, all cases after the matching case will execute!!
- Good to add default statement as well
- Within a switch statement, we have to use numeric literals so it’s great for char.
- Switch statements are more convenient for the JVM (and for the developer)

## Packages

Com.revature.operators

C://workspace/com/revature/operators…

What are packages?
* They are like folders

Why do we use packages?
* Provides control access (offers another level of encapsulation)
* Prevents naming conflicts
* Searching/locating classes, interfaces.

## Operators in Java:

### Arithmetic Operators:
        (x, y)
* Add +
* Subtract -
* Multiply *
* Divide /
* Modulus %

(x)
* Increment/Decrement ++/--

### Assignment Operators:
        (x,y)
* = : assigns a variable to be equal to the value on the right hand side.
* += : Adds in addition to the original value and reassigns
* -= : Deducts from the original value and reassigns
* *= : 
* /= : 
* %= : returns the remainders of original value

### Comparison Operators:
        (x, y)
* == : equal to
* != : not equal to
* > : Greater than
* < : Less than
* >= : GTET
* <= : LTET

### Java Logical Operators:
* Or one has to be true : ||
* And both have to be true : &&
* Not flips the expression value : !

## Class and Objects:

What is a class?
* Essentially a blueprint for the instantiation of an object. Typically if you want to access the methods and attributes ‘within’ a class you’ll instantiate it into an object (unless you use a static method).

What are objects?
* Implementation of a class

Blueprint for a car: 
  - It has seats (attribute)
  - It has a model name (attribute)
  - It should be able to accelerate (behavior, method)
  - Check whether engine is running or not (attribute)
  - Should be able to brake (behavior, method)

Jeff’s car. 
* Has 3 seats
* Honda Civic
* It can accelerate and break

```java
// Let’s create some object attributes:
Int intNumber = 4;
Double doubly = 4.0;
Boolean goodWeather = true;

//A method is a function that belongs to an object
// Access modifier, Return type, Method name, Parens
Public void bark() {
}

Public int fetch() {
  Return 0;
}
```


The “new” keyword can be thought of as creating a physical instance of a class

```java
BasicClass myObject = new BasicClass();
BasicClass myObject2 = myObject;.
```


Changes to myObject2 will also make changes to myObject.

```java
This is considered a “pass by reference”.
// Objects are passed by reference because they are so much bigger than primitives because they hold attributes, specific methods, but also built-in methods.
```

```java
Int myInty = 1;
Int myInty2 = myInty;

myInty2 = 35;
// myInty stays as 1 because this is a “pass by value”
// Because primitives are so small, the variable itself holds the data in memory. 
```


## OOP:
What if the benefits of OOP?
* Demonstrated in Planet.java and Mars.java


## Git:
* Clone
* Pull/Push

## Mini-Homework:
What is the JVM, JRE, & JDK


## JVM:
* Loads code
* Verifies code
* Executes code
* Provides runtime environment

The JVM compiles code to bytecode, checks for any security breaches, then converts bytecode into native machine code using an execution engine. Just in time (JIT) compiling.

Component of the JRE, a virtual machine to load the code and execute it on a machine.

### JRE:
* Set of software tools used for developing Java applications (such as a launcher).
* It is the actual implementation of JVM and includes a JVM.
* It contains a set of libraries and other files that JVM uses at runtime.
* Doesn’t contain any development tools!

### JDK:
* Software Development environment used to develop Java applications and applets
* Like the JRE, it physically exists. It is the implementation of one of the following:
   * SE
   * EE
   * ME
   * etc.
* It contains the JRE and other development tools.
* Contains a private JVM, interpreter (java), compiler/loader (javac), archiver (jar), documentation generator (JavaDoc), etc.
