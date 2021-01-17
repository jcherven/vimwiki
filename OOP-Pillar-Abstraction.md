# OOP Pillars

## OOP Pillar Abstraction

Abstraction is a process of hiding the implementation details and showing only
functionality to the user.

Another way, it shows only essential things to the user and hides the internal
details, for example, sending SMS where you type the text and send the message.
You don't know the internal processing about the message delivery.

Abstraction lets you focus on what the object does instead of how it does it. 

## Generalization

Generalization is the process of extracting shared characteristics from two or
more classes, and combining them into a generalized superclass. Shared
characteristics can be attributes, associations, or methods. 

Eg : The classes Piece of Luggage  and Piece of Cargo partially share the same
attributes. From a domain perspective, the two classes are also very similar.
During generalization, the shared characteristics  are combined and used to
create a new superclass Freight . Piece of Luggage and Piece of Cargo become
subclasses of the class Freight. Therefore the properties that are common to
the classes Piece of Luggage and Piece of Cargo are placed in the superclass
Freight - Identification, Weight and ID-Number are those properties.

## Specialization

Specialization means creating new subclasses from an existing class. If it
turns out that certain attributes, associations, or methods only apply to some
of the objects of the class, a subclass can be created. 

In the previous example for Generalization, we saw that the classes Piece of
Luggage and Piece of Cargo shared similar properties that were placed in a
superclass called Freight. When it comes to Specialization, if there is a
property that is only applicable to a specific subclass, such as Degree of
Hazardousness, that property is placed in the class Piece of Cargo where-in
this class also has all the properties of the Freight class with the concept of
Generalization. 

## Ways to achieve abstraction?

There are two ways to achieve abstraction in java

    - Abstract class (0 to 100%)
    - Interface (100%)

## Abstract Class

A class which is declared as abstract is known as an abstract class. It can
have abstract and non-abstract methods. It needs to be extended and its method
implemented. It cannot be instantiated.  Some points to remember : 

    - An abstract class must be declared with an abstract keyword.
    - It can have abstract and non-abstract methods.
    - It cannot be instantiated.
    - It can have constructors and static methods also.
    - It can have final methods which will force the subclass not to change the
      body of the method.

## Abstract Method

A method which is declared as abstract and does not have implementation is
known as an abstract method. 

```java
abstract void printStatus();  //no method body and abstract  
Example of Abstract Class with an Abstract Method
abstract class Bike{  // Abstract class 
  abstract void run();  // Abstract method
}  

class Honda4 extends Bike{  
  void run(){
    System.out.println("running safely");
  }  
  public static void main(String args[]){  
    Bike obj = new Honda4();  
    obj.run();  
  }  
} 
```

## Sample Exercise : 

    1. To create an abstract class called Bank.
    2. To create an abstract method called getRateOfInterest();
    3. To create two subclasses called SBI - 7% and PNB - 5% as two banks that
       extend the abstract class Bank.
    4. To implement different functionalities for the getRateOfInterest()
       method in the SBI and PNB classes through the concept of method
       overriding and print out the interest rate inside the main() method
       created separately in a test class called TestBank

```java
```

## End of OOP Study Guide

NEXT: [OOP Study Guide](OOP-Study-Guide)
< [OOP Pillar Polymorphism](OOP-Pillar-Polymorphism)
< [OOP-Pillars](OOP-Pillars)
< [OOP Study Guide](OOP-Study-Guide)
< [Index](Index)
