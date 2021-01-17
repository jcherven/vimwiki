# Interface?

    - An interface is a reference type in Java. It is similar to class. It is a
      collection of abstract methods. A class implements an interface, thereby
      inheriting the abstract methods of the interface.
    - Along with abstract methods, an interface may also contain constants,
      default methods, static methods, and nested types. Method bodies exist
      only for default methods and static methods.
    - Writing an interface is similar to writing a class. But a class describes
      the attributes and behaviors of an object. And an interface contains
      behaviors that a class implements.
    - Unless the class that implements the interface is abstract, all the
      methods of the interface need to be defined in the class.

## Similarities between an interface and a class

    - An interface can contain any number of methods.
    - An interface is written in a file with a .java extension, with the name
      of the interface matching the name of the file.
    - The byte code of an interface appears in a .class file.
    - Interfaces appear in packages, and their corresponding bytecode file must
      be in a directory structure that matches the package name.

## Differences between an interface and a class

    - You cannot instantiate an interface.
    - An interface does not contain any constructors.
    - All of the methods in an interface are abstract.
    - An interface cannot contain instance fields. The only fields that can
      appear in an interface must be declared both static and final.
    - An interface is not extended by a class, it is implemented by a class.
    - An interface can extend multiple interfaces.

## Declaring Interfaces

The interface keyword is used to declare an interface. 

```java
/* File name : NameOfInterface.java */
import java.lang.*;
// Any number of import statements

public interface NameOfInterface {
   // Any number of final, static fields
   // Any number of abstract method declarations\
}
```

    - An interface is implicitly abstract. You do not need to use the abstract
      keyword while declaring an interface.
    - Each method in an interface is also implicitly abstract, so the abstract
      keyword is not needed.
    - Methods in an interface are implicitly public.

Example

```java
/* File name : Animal.java */
interface Animal {
   public void eat();
   public void travel();
}
```

## Implementing Interfaces

When a class implements an interface, you can think of the class as signing a
contract, agreeing to perform the specific behaviors of the interface. If a
class does not perform all the behaviors of the interface, the class must
declare itself as abstract.

A class uses the implements keyword to implement an interface. The implements
keyword appears in the class declaration following the extends portion of the
declaration.

Example

```java
/* File name : MammalInt.java */
public class MammalInt implements Animal {
   public void eat() {
      System.out.println("Mammal eats");
   }

   public void travel() {
      System.out.println("Mammal travels");
   } 

   public int noOfLegs() {
      return 0;
   }

   public static void main(String args[]) {
      MammalInt m = new MammalInt();
      m.eat();
      m.travel();
   }
} 
```

## Rules to Remember : 

    - A class can implement more than one interface at a time.
    - A class can extend only one class, but implement many interfaces.
    - An interface can extend another interface, in a similar way as a class
      can extend another class.

## Extending Interfaces

An interface can extend another interface in the same way that a class can
extend another class. The extends keyword is used to extend an interface, and
the child interface inherits the methods of the parent interface. 

Example

```java
// Filename: Sports.java
public interface Sports {
   public void setHomeTeam(String name);
   public void setVisitingTeam(String name);
}
```

```java
// Filename: Football.java
public interface Football extends Sports {
   public void homeTeamScored(int points);
   public void visitingTeamScored(int points);
   public void endOfQuarter(int quarter);
}
```

```java
// Filename: Hockey.java
public interface Hockey extends Sports {
   public void homeGoalScored();
   public void visitingGoalScored();
   public void endOfPeriod(int period);
   public void overtimePeriod(int ot);
}
```

The Hockey interface has four methods, but it inherits two from Sports. Thus, a
class that implements Hockey needs to implement all six methods. Similarly, a
class that implements Football needs to define the three methods from Football
and the two methods from Sports.  Extending Multiple Interfaces

A Java class can only extend one parent class. Multiple inheritance is not
allowed. Interfaces are not classes, however, and an interface can extend more
than one parent interface.

The extends keyword is used once, and the parent interfaces are declared in a
comma-separated list.

Example

```java
public interface Hockey extends Sports, Event
```
