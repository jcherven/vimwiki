# Polymorphism

Polymorphism - literally "many forms" - is the ability for some code structures
in an OOP language to be treated as different structures at runtime. This
sounds complicated, but it's really not - you've already seen examples of it!

## Object Polymorphism

When discussing inheritance, it was explained that when class B inherits from
class A, an object of class B is also considered to be an object of class A.
That's object polymorphism. To revisit a prior example...

```java
public class Automobile { 
    public int position = 3;
    
    public void move() {
        position += 4;
    }
}

public class Sedan extends Automobile { }

public class Example {

    private static moveAutomobile(Automobile auto) {
        auto.move();
    }

    public static void main(String[] args) {
        Sedan car = new Sedan();
        moveAutomobile(car); 
    }
}
```
Here a Sedan inherits from the Automobile class, and so a Sedan object is also
considered to be an Automobile object. The moveAutomobile() method accepts a
reference variable which refers to an Automobile object as input, and this lets
us use the reference to the Sedan object as input when we invoke that method.

Object polymorphism lets us write generic code that can be used with families
of related objects instead of just individual types.
 
## Casting

There's something else going on with the above example. The moveAutomobile
method accepts any reference to an object that has an IS-A relationship to
Automobile. The method treats the passed-in reference as if it were an
Automobile type reference, i.e. it stores the reference in an Automobile
reference variable to use within the method. But the underlying object is still
actually a Sedan object, it is only being access through an Automobile type.
This is called casting, and while the above example is in Java, this is a
feature of all OOP languages.

Casting is the process of storing a reference to an object in memory inside a
reference variable of a type different than the object itself, or the last type
of reference variable used.

We can upcast a reference by storing a reference to an object in a
base-class-typed reference variable. To continue using Automobiles and Sedans,
this is an example of upcasting:
```java
Automobile car = new Sedan();
```
This example stores a reference to a Sedan object in a reference variable that
has a type that is a base or parent class to the object. You could also say
it's a less-specific type.

Downcasting is when we take a previously upcast reference, and store that
reference in a reference variable that is a type closer to that of the actual
object being referenced. For example:
```java
Automobile car = new Sedan();
Sedan otherCar = (Sedan) car;
```
This is in the Java syntax, but most OOP languages have the same casting syntax
of "(NewType)". In this example, we have upcast the reference to a Sedan object
to an Automobile type, and then downcast it back to a Sedan reference type. The
entire time, the actual object is still a Sedan.

You cannot however, downcast a reference past the actual type of the object in
memory. For example
```java
class Animal {}
class Dog extends Animal { }
class Labrador extends Dog {}

public class Test {
  public static void main(String[] args) {
    
    Animal firstRef = new Dog();              // upcasting		
    Dog secondRef = (Dog) firstRef;           // downcasting
    Labrador thirdRef = (Labrador) secondRef; // too far!
  }
}
```
Here, the actual object in memory is a Dog object. We can upcast a reference to
that object to an Animal type, and we can downcast the reference back to a Dog
type, but we can never downcast it to a Labrador type. A Labrador object is-a
Dog object, but a Dog object is not a Labrador object.

 
## Method Polymorphism

In most OOP languages, methods are differentiated by one another by their
signature, which is a combination of the method's name, and the types, number
and order of parameters that are passed in. This system of differentiation
allows us to override and overload methods.

When a method in a derived class has the same signature as a method in the base
class, it will override the implementation given in the base class. For example
```java
class Base {
    public void message() {
        System.out.println("Hello!");
    }
}

class Derived extends Base {
    public void message() {
        System.out.println("Goodbye!");
    }
}

public class Example {
    public static void main(String[] args) {
        Derived der = new Derived();
        der.message();
    }
}
```
In this example, we create an instance of the Derived class, and invoke the
message()  method as defined in that object. The message() method has the same
name, and accepts the same type/number/order of parameters as the message()
method in the base class (none). Therefore, when we call the message() method
against a Derived object, this will print "Goodbye!" to the console.

It is important to remember that the definition of a method is determined by
the type of the object itself. The type of the reference variable only
determines which methods can be invoked.

Method overriding is sometimes called runtime polymorphism, because the
implementation of the method that will be used is determined by the type of the
object being referenced at runtime.

On the other hand, we have method overloading. This happens when two methods
share the same name, but have a different signature - that is, when they share
the same name, but the type/order/number of parameters they accept are
different. Consider this example:
```java
class Maths {

    public int calculate(int a, int b) {
        return a + b;
    }

    public double calculate(double a, double b) {
        return a - b;
    }
}

public class Example {
    public static void main(String[] args) {
        Maths math = new Maths();

        int x,y = 1;
        double c,d = 1;

        math.calculate(x, y); // returns 2
        math.calculate(c, d); // returns 0.0
    }
}
```
The Maths class has two methods that share the name "calculate", but one
accepts two ints and the other accepts two doubles. The type of returned value
is not part of the signature. When we invoke the calculate() method, the actual
implementation used will be determined by the types of parameters that we pass
in. If we pass in two integers, we invoke the version that sums the two
parameters. If we pass in two double-precision numbers, we invoke the version
that subtracts the two parameters.

Method overloading is called compile-time polymorphism, because these methods
are differentiated by the compiler based on the parameters they are given. The
JVM might not know the type of object that will executing a method ahead of
time (per the discussion on method overriding), but the compiler will always
know the types of parameters being given to that method ahead of time.

< [Relationships](Relationships) | [Polymorphism in Java](Polymorphism-in-Java) >
