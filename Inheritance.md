# Inheritance

< [Classes, Objects, and References](Classes-Objects-and-References) | [Inheritance in Java](Inheritance-in-Java) >

If all Object Oriented Programming was for was separating your code into
reusable objects, then the only benefit would be some improved or easier
reusability of code. Thankfully, we can do a lot more than that. By creating
relationships between objects, we can write code that applies to families or
collections of related types of objects. Ultimately, this allows us to write
*less* code by writing more *generic* code.

One way we can create a relationship between two objects is **Inheritance**.
When one class inherits from another, an object that is an instance of the
first class will also contain the states and behaviors of the second class.
Let's clarify some terminology:

A class that is *inherited from* is called a **base**, **super**, or **parent**
class.

A class that *inherits* from another is likewise called a **derived**, **sub**,
or **child** class.

Different languages favor different terms, but they all mean the same thing.
The syntax of expressing inheritance can also different in different languages.
For example, both these snippets show a Sedan class that inherits from an
Automobile class:

In Java:
```java
class Automobile { }
class Sedan extends Automobile { }
```

In C#:
```csharp
class Automobile { }
class Sedan : Automobile { }
```

In both these examples, an object of the Sedan class would possess copies of
any variables or methods defined in the Automobile class in addition to any
variables or methods defined in the Sedan class. In this way, we can say that
inheritance creates **IS-A(N)** relationships. An object of class Sedan is also
an object of class Automobile. This isn't a coincidence, it's guaranteed - and
that guarantee allows us to write more generic code.

For example, you can now write code that applies to an object of any subclass
of Automobile, so long as that code only operates on the states and behaviors
defined in the Automobile class. Since the Sedan class inherits from the
Automobile class, we can run our generic code against a Sedan object, because
the Sedan object is guaranteed to have inherited the states and behaviors of
the Automobile class.

Here's an example of this, in Java's syntax:

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
        car.move();
        moveAutomobile(car); 
    }
}
```

The Sedan class inherits the position variable and the move() method from the
Automobile class, and defines no new states or behaviors of its own. The
example class has a main() method that creates a Sedan object, and stores the
reference in a reference variable of type Sedan. The Example class also has a
moveAutomobile() method that accepts a reference to an Automobile object, and
invokes the move() method of the object referred to by that reference.

A Sedan is-an Automobile, so the Sedan object possesses the move() method
defined in the Automobile class - it inherits it. So the move() method can be
called directly on a Sedan object, as shown.

A Sedan is-an Automobile, so we can send a pass a reference to a Sedan object
in memory into our moveAutomobile() method. Because a Sedan object is-an
Automobile object, a Sedan is guaranteed to possess a position variable and a
move() method of its own, and that allows this to code to work.

Imagine that we also had a Truck class that inherited from Automobile - we
could use the moveAutomobile() method on a Truck object too, just like we can
use it for a Sedan.

 

When class B inherits from class A, class B has its own individual copies of
the states and behaviors defined in class A. If class C inherits from class B,
then class C will also end up inheriting the states and behaviors of class A,
and those defined solely in class B. In this way, we can create an inheritance
chain or tree.

 

Some languages also allow for *multiple inheritance*, where a single class can
directly inherit from two base classes. This is different from inheriting
through a tree. Compare the difference between:

Single inheritance (C# syntax):
```csharp
public class A { }
public class B : A { }
public class C : B { }
```

and multiple inheritance (C# syntax):
```csharp
public class A { }
public class B { }
public class C : A, B { }
```

In this example of multiple inheritance, an object of class B is not also an
object of class A, but an object of class C is also an instance of classes A
and B.

This can create problems. Imagine if classes A and B both had methods defined
with the same name, and accepted the same parameters, as shown here in the Java
syntax:

```java
public class Automobile {
    int position = 0;

    public void move() {
        position += 3;
    }
}

public class FourDoor {
    int position = 2;

    public void move() {
        position += 5;
    }
}

public class Sedan extends Automobile, FourDoor { }

public class Example {

    public static void main(String[] args) {
        Sedan car = new Sedan();
        car.move();
    }

}
```

Class Sedan will inherit both of these position variables and move() methods,
and it will be impossible to determine which move() method should be invoked in
the main() method, or what the final value of the position variable should be.

This is why most OOP languages **do not support multiple inheritance**. The
above example will not work in Java, because Java is one of those languages
that does not support this practice. Do not confuse multiple inheritence with a
chain of single inheritance relationships.

< [Classes, Objects, and References](Classes-Objects-and-References) | [Inheritance in Java](Inheritance-in-Java) >

Back to [OOP Concepts](OOP-Concepts)
