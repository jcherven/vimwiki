# interfaces-advanced

An interface is a special type of construct in Java, which is used as a
contract to guarantee implementation of certain behaviors in a subclass. It’s
an abstract entity - all methods are implicitly “public abstract” while
instance variables, if there are any, are “public static final.” With these
tools, they declare specific behavior for objects. 

Interfaces are written similar to classes – but they use the word interface
instead of class. To implement an interface in your class, you use the
implements keyword in the class declaration - after extending a class, if you
do. This is a compiler enforced contract. Each method in the interface must be
supplied with a concrete implementation by the implementing class. If the
implementing class tries to not implement some interface methods, then it must
become an abstract class – because the implementing class would then still have
an abstract method, and you’re not allowed to have a concrete class that
doesn’t implement every method it declares. 

Because an interface acts as a contract, they’re not considered a traditional
form of inheritance. However, you’ll often see them referred to as “type
inheritance.” Just like when you extend a class, you also create an is-a
relationship when you implement an interface. 

Interfaces should be named as adjectives, which helps reinforce this
relationship in common language. If a Dog implements the Domesticated
interface, we can say a Dog is-a Domesticated thing. This means that if you use
polymorphism to store a Dog object in a Domesticated type reference variable,
you can still use that variable to invoke any behaviors declared in the
Domesticated interface. 

A class can only be extend one other concrete or abstract class, but it can
implement multiple interfaces. An interface isn’t a class, so they kind of get
around the one-extension-only rule. An interface can extend multiple other
interfaces, but they can’t extend other classes, and they don’t implement
anything. 

```java
public class InterfacesExample {
  public static void main(String[] args) {
    Domesticated domesticatedThing = new Dog();
  }
}

interface Domesticated {
  public void doWork();
}

class Animal {
  public void eat() {
    System.out.println("I eat food");
  }
}

class Wolf extends Animal {
  public void eat() {
    System.out.println("I eat fresh meat");
  }
}

class Dog extends Animal implements Domesticated {
  public void eat() {
    System.out.println("I eat kibble");
  }
  public void doWork() {
    System.out.println("I perform a trick!");
  }
}
```

Here in eclipse we have defined a Domesticated interface and an Animal class.
The animal class defines an “eat” method, and the Domesticated interface
dictates that an implementing class must complete the doWork method. Here we
also have the Wolf class defined, which extends Animal, and our Dog class both
extends Animal, and implements Domesticated. Wolf and Dog both override eat.
Because Dog implements the Domesticated interface, it also implements the
doWork method. Here, I use polymorphism to refer to my Dog object with a
Domesticated type reference variable. I can only use this variable to call the
doWork() method – I can’t call the eat() method from a Domesticated type
reference variable, because the eat() method isn’t declared in the interface.
On the other hand, because I’m using a Domesticated interface type, this code
can now support any Domesticated object – a HouseCat object, a Cow object, etc.
They are all guaranteed to have an implementation for the doWork() method. And
as long as we implement the Domesticated interface we can be assured that
future changes to the “doWork” implementation in the Dog class will NEVER break
the code that invokes it. 

Now, Java 8 also introduced a new feature to Interfaces, that completely
flipped old ideas about interfaces on their head, and allowed them to break a
lot of the old rules they were bound to. But to understand why the developers
behind the Java language did this, you need some context. 

Imagine you wrote a software library that was used by tens of thousands of
developers around the world. In this software library, you have an interface
that other developers can implement when they use your library to write their
own code. And they do! Now these tens of thousands of developers have written
programs used around the world, and each one is heavily dependent on code that
you wrote. One day, you’re working on an update to your library, and you decide
that the interface you wrote needs an additional method. You add that method
declaration to your interface, and publish version 1.1 of your library. All
those developers download your update… and their code doesn’t work anymore! By
introducing a new method declaration to your interface, you have required every
class that implements that interface – in every program written by every
developer - to provide a definition for the new method! Because those classes
did not previously have a definition for the new method, their classes are
considered abstract, and can’t be instantiated where they previously were. It’s
a mess! Every developer now has to either stick with your old version, or write
new code and update their own programs because of a decision you made. 

This meant that for a long time, interfaces were bound by their popularity. The
moment you published an interface that the public could use, it was extremely
difficult in practice to make any changes to it. To combat this, Java 8
introduced the default method to interfaces. Now, an interface is allowed to
provide a default implementation to some methods. Because an implementation is
present in the interface, classes that implement that interface are not
required to implement the method. 

To use a default method, you just add the default keyword before the method
declaration in the interface. Then you can provide an implementation, like
normal. While instance variables declared in an interface are always public,
static, and final - meaning they can’t be changed once given a value, and are
constant across all objects that implement this interface – you can still
declare local variables inside a default method. Default methods can also call
other methods that are declared by the interface, even if they are not defined
there. The guarantee with an interface is that the implementing class will
provide an implementation for those other methods, so they are safe to call. 

Interfaces are also allowed to have static methods with definitions. Like any
other static method, you can invoke these without creating an instance of a
class that implements the interface. And because they are static methods, they
can only call other static methods, or access methods through local reference
variable. A default method can call methods declared elsewhere in the
interface, because you still have to create an object from a class that
implements the interface to invoke the default method, which in turn guarantees
that those other methods will have an implementation somewhere. 

With a static method, you can call them directly off the Interface without
creating an object, so there’s no guarantee that other non-static methods will
have an implementation at the time you make the call. Here’s an example of an
interface that has a standard abstract method, a default method, and a static
method. 

```java
import java.util.ArrayList;

public class Java8InterfaceExample {
  public static void main(String[] args) {
    Domesticated myDog = new Dog();
    Domesticated.register(myDog);
    myDog.doWork();
    myDog.doWork("Play fetch!");
    System.out.println("Domesticated Animals: " + Domesticated.animals);
  }
}

interface Domesticated {
  ArrayList<String> animals = new ArrayList<>();
  ArrayList<String> plants = new ArrayList<>();
  
  static void register(Domesticated Species) {
    if (species instanceof Animal)
      animals.add(species.getClass().getName());
    else if (species instanceof Pland)
      plants.add(species.getClass().getName());
  }
  
  void doWork();
  
  default void doWork(String job) {
  System.out.println("I " + job);
  }
}

abstract class Animal {}
abstract class Plant {}

class Dog extends Animal implements Domesticated {
  public void doWork() {
    System.out.println("I hunt for food!");
  }
}
class Wheat extends Plant implements Domesticated {
  public void doWork() {
    System.out.println("I produce a lot of food!");
  }
}
```

The Domesticated interface has two ArrayLists of Strings that track
domesticated plant and animal species. The variables are public, static, and
final – meaning that the reference variables can be accessed by anyone, without
creating an instance of an implementing class, will be shared across the entire
program, and will always point to the same object in memory. We can add object
references to the ArrayLists without changing the fact that the reference
variables points to the ArrayLists themselves. First is the static method
register(), which adds anything Domesticated to one of the two ArrayLists. The
object passed in must be an object that implements Domesticated, but we still
test whether the Domesticated thing is an Animal or a Plant before adding it to
the appropriate list. The doWork() method, which must be implemented by another
class. Species are domesticated so they can do a job for humans, even if it’s
just to entertain or feed us. The exact job they do is dependent on the class
that implements the interface – what species is domesticated. The default
method doWork(String) might have been added later, to allow a Domesticated
object to do a job specified by the programmer, rather than the classes’
implementation. This could be a good idea if we have a species of Dog that has
two jobs. 

Of course, having default methods like this can lead to a big problem: multiple
inheritance. If I have two interfaces that have default methods with the same
name - like a Domesticated interface and a Worker interface that both have
default methods named doWork() – and my class SeeingEyeDog implements them
both, now SeeingEyeDog has two different implementations for the same method!
It’s best not to let this happen, but if it can’t be avoided, then you can
always specify the implementation you are referring to by using the super
keyword. `Domesticated.super.doWork()` will use the default doWork()
implementation from the Domesticated interface, and `Worker.super.doWork()`
will use the default implementation in the Worker interface. 

Abstract classes and interfaces have important differences worth remembering.
Abstract classes can have instance variables that are not are not automatically
public, static and final. They can also have non-public methods. This doesn’t
mean one is better than the other, you use them both in different
circumstances. Remember that interfaces are contractual, and you can always use
them polymorphically as reference types to guarantee access to certain methods. 

# lecture notes
An interface is a special construct that acts as a contract. 

All methods in an interface are public and abstract. 

All variables are implicitly public static final. 

Use the keyword interfaceto declare an interface.

## Implementing Interfaces
A class that implements an interface must define each method in the interface.

Interfaces support type inheritance, but are not considered a traditional form of inheritance. You still have an IS-A relationship, however and polymorphism still applies. 

A class can implement multiple interfaces. 

An interface can extendmultiple other interfaces. 

## Default Methods (Java 8) 
As of Java 8, an interface can define a default method. This functionality is added as a backwards compatibility feature to support classes that implement a previous version of the interface that did not specify the newly added method. 

With Java 8, you can provide a default implementation for it. Thus, a class that implements an interface with a default method is not required to override it.

```java
interface Domesticated{
  . . . 
  default void doWord(String job){
    System.out.println("I " + job);
  }
}

```
You can declare local variables in a default method. You can also call other (unimplemented) methods on the interface from a default method.

## Static Methods
An interface is allowed to have a static method. These methods carry the same restrictions as other static methods (Ex. you cannot call instance methods or use variables from within a static context)

A static method can call a default method.

```java
interface Domesticated{
  . . . 
  static void register(Domesticated species){
    . . . 
  }
  . . . 
}
```
## Inheriting Default Methods
Since default methods are inherited and a class can implement multiple interfaces, they may arise a situation where a class inherits the same method from two interfaces (multiple inheritance). In this instance, you can override the method and can specify which default by using the keyword super:

```java
Domesticated.super.doWork();
```

## Abstract Classes vs. Interfaces
The following are key differences between abstract classes and interfaces:

  - Abstract classes can have instance variables (that are not automatically public static final)
  - A class can only extend one class (be it abstract or not), but a class can implement multiple interfaces
