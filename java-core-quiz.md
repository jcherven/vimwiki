# java-core-quiz

## Legend

`Correct answer`
X Wrong Answer


## Which of these is NOT true for Java?

    `Java allows direct manipulation of memory addresses`
    Java is an Object Oriented language
    Java code only needs to be compiled once, then it can be run on any system.

## Which of these is NOT a valid way to declare an array?

    public int[] myArray = new int[3];
    `public []int myArray = new int[3];`
    public int myArray[] = new int[3];
    public int[] myArray = {1, 2, 3};

## A do-while statement will never execute if it's conditional check is false.

    TRUE
    `FALSE`

## what is the output of this code?

```java
int count = 0;
while (count <  2) {
    System.out.print("Hi ");
}
```

    `The loop will run forever`
    "Hi Hi Hi"
    "Hi"

## What is the boolean value of this statement?

```java
String string1 = "TEST";
string1.equals(string1.toLowerCase());
```

    `FALSE`
    TRUE

## What is the result?

```java
String a = "Good morning!";
System.out.println(a.charAt(9));
```

    "n"
    `"i"`
    "g"

## True or False: The relationship between a class and its members is a, HAS-A" relationship

    `TRUE`
    FALSE

## What is a constructor?

    A class used to create other classes
    `A special method called at instantiation, used to create an object and initialize variables`
    A method that returns the value of a private variable
    
## True or False: Child classes must have the same variable values as their parent class

    TRUE
    `FALSE`

## True or False: A class in Java can extend multiple parent classes

    TRUE
    `FALSE`

## What is wrong with this code?

```java
public class Question {  
    public void doThing() {}  
    public static void main(String[] args) {      
        doThing();  
    }
}
```

    Nothing, the code will compile and execute without exception.
    `The doThing() method must be declared static to be used in main()`
    The main() method should not be declared static

## Java supports multiple inheritance of classes

    TRUE
    `FALSE`

## You should catch errors where possible

    `FALSE`
    TRUE

## True or false: the following code is valid?

```java
public class Question {   
    public static void myMethod(Object o) {}   
    public static void main(String[] args) {      
        myMethod(new String("Test"));   
    }
}
```

    `TRUE`
    FALSE

## True or False: Because sets have no ordering, there is no way to retrieve a specific object from a Set immediately.

    FALSE
    `TRUE`

## Because LinkedLists in java implement List, they have an index.

    `TRUE`
    FALSE

## How many objects are created with the following code?

```java
String a = new String(); // this is definitely an object
String b = a; // this *might* be an object
a = "Hello"; // this is a reference, not an object
```

    2
    3
    4
    X 1

## Abstract classes:

    cannot be extended.
    contain only abstract methods.
    can extend other abstract classes multiple times.
    `are made to be extended not instantiated.`

## The "transient" keyword...

    Prevents two different streams from accessing data
    Guarantees data will be serialized
    Prevents data from being serialized
    Changes data as it is serialized.

## Marshalling is...

    `the process of converting an object instance into a data format that describes it`
    The process of sending data to a destination
    The process of collecting data in a single location
    Preventing data from being transferred

## True or False: You can use both annotations and mapping files in the same project

    TRUE
    FALSE

## True or False: Mapping with annotations requires you to identify the mapped classes in your configuration document.

    TRUE
    FALSE

## True or False: Mapping annotations are exclusive - an annotated method will only be accessible to requests sent to a matching URL, with no partial matches

    FALSE
    TRUE

## Which of these is the symbol for an annotation?

    *
    #
    $
    @

## True or False: Annotations are used to provide extra information to the Java compiler

    `TRUE`
    FALSE

## Which of these is a valid location for an annotation in Java 8?

    Before a class declaration
    Before the use of a type
    All of these
    Before a method declaration

## True or False: The Object reference can be used to polymorphically store a reference to an instance of any class in Java

    `TRUE`
    FALSE

## What is the purpose of the hashcode() method?

    To identify which class an object is an instance of
    To generate a random number
    `To provide a unique identifier for an instance of an object`
    To print the values of all an object's properties

## Can you catch an Error?

    Yes, and you should - Errors can be dangerous if not handled
    No
    `Yes, but you should not - an application can rarely handle them properly, or continue running after they occur`

## Should you catch all Throwable objects?

    Yes, all problems with a program's execution should be handled
    `No, Errors are Throwable, and should not be caught`

## Which exception will be thrown from this code?

```java
int[] a = new int[0];
System.out.println(a[1/0]);
```

    ClassCastException
    `ArithmeticException`
    ArrayIndexOutOfBoundsException
    NumberFormatException

## True or False: A finally block will always execute, regardless of whether an exception is caught

    `TRUE`
    FALSE

## True or False: A final class cannot be instantiated

    `TRUE`
    FALSE

## True or False: Inherited behaviors can be overriden in a subclass

    `TRUE`
    FALSE

## Which keyword is used to show inheritance in Java?

    is
    :
    `extends`
    implements

## True or False: Interface implementation is a form of inheritance

    `FALSE`
    TRUE

## True or False: The main() method must be static, in order to be executed by the JVM.

    `TRUE`
    FALSE

## Which of these is a consequnce of removing a method declaration from an interface after it has been implemented?

    There are no consequences, interfaces can always be modified to remove methods
    The method definitions would need to be removed from every subclass that implements the interface
    `Code would break whenever an interface reference is used to polymorphicaly call the method in an instance of an implementing class.`

## Which of these is a consequence of adding a method declaration to an interface after it has been implemented?

    There are no consequences, interfaces can always be modified to add methods
    `Every implementing subclass would need to add a definition for the new method.`
    Every implementing subclass would no longer be able to be stored polymorphically in an interface reference

## You need a collection to represent secret agents. Every agent has a unique codename that identifies them, and an Agent object that represents them. The best collection for this would be?

    A HashSet< Agent >
    `A HashMap< String, Agent >`
    An ArrayList< Agent >

## "Collections" is?

    The interface that all java collections implement
    `A class filled with static methods used to manipulate collections`

## What is the output of the following code?

```java
int i = 0;
while(i!=4) {
  switch(i) {
    case 0:
      System.out.print(0);
      break;
    case 1:
      System.out.print(0);
    default:
      System.out.print("X");
      break;
  }
  i ++;
}
```

    01XX
    `01XXX`
    01XXXX
    01X

## What is the output of the following code?

```java
Integer i = new Integer(0);
if(i == 0) System.out.print("=");
if(i != 0) System.out.print("!");
if(i > 0) System.out.print(">");
if(i < 0) System.out.print("<");
```

    =!><
    !
    Nothing prints
    `=`

## What is the output of the following code?

```java
String x = "bob"; // object
String y = x; // reference to x
String b = new String("bob"); // new object
String a = "bob"; // reference to "bob" at x
if(x == y) System.out.print("1");
if(x == b) System.out.print("2");
if(x == a) System.out.print("3");
```

    1
    12
    23
    `13`

## Which one of the following is a valid class declaration?

    class example implements Serializable, Runnable
    class Example extends ArrayList, HashMap
    X class example implements ArrayList
    static abstract class example implements Serializable extends ArrayList

## What is the standard signature for the main method?

    public void main(String args[])
    public void static main(String args[])
    public static void main()
    `public static void main(String args[])`

## Given the command line argument in quotes "1 2 3" what will be the output of the following code?

    temp
    1 2 3
    Nothing prints
    X 123

## The keyword "static" means:

    something belongs to a specific instance.
    something is a constant.
    something is locally available to a single instance of the class.
    `something belongs to the class and is globally available to all instances.`

## What is a reserved word, or keyword?

    X A term used by the operating system to run Java code
    A word used by the JVM to represent an instruction
    A word used by the IDE to understand Java code

## True or False: Java can be run on any machine that has a JVM

    `TRUE`
    FALSE

