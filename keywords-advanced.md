# keywords-advanced

As we’ve mentioned previously,keywords are reserved words in Java that give the
compiler specific instructions,and so cannot be used to name fields, methods,
or classes. We’re going to cover three new keywords today, static, final, and
abstract, out of the fifty or so keywords in Java. 

The modifier “static” defines “class” variable and methods, as opposed to
“instance” members. Static members are globally available to all instances of a
class. A word of caution: a static method can only use other static members
within the same class. Eclipse will warn you when you break this rule. Also,
you can use a static member with the dot operator on the class WITHOUT
instantiating the class first. 

```java
class StaticDemo {
  static int counter = 0;
  int number = 0;
  
  public StaticDemo(){
    counter++;
    number++;
  }
}

public class StaticExample {
  public static void main(String[] args) {
    StaticDemo instanceA = new StaticDemo();
    System.out.println("instanceA counter: " + instanceA.counter);
    System.out.println("instanceA number: " + instanceA.number);
    
    StaticDemo instanceB = new StaticDemo();
    System.out.println("instanceB counter: " + instanceB.counter);
    System.out.println("instanceB number: " + instanceB.number);
  }
}
```

Here in eclipse, we have created a demo class with two counters: “number”which
is an instance variable and “counter” which is a class variable. We see here
that every time the constructor is called it increments both counters. Back in
the test class we have created two instances of the StaticDemo class and called
print method on each one. 

When we run this code we get a curious result. The first “number” is associated
with the created demo1 object and correctly shows a value of one for each
StaticDemo instance. However, the static variable “counter”which is globally
available to all instances of StaticDemo is actually counting the number of
instances that were created or “two.” It should be clear that this static
variable is shared across all instances of a class. 

The keyword final makes things immutable in Java. With variables, it’s easy to
understand what this means – it’s immutable, it can’t be changed! Once
initialized, a variable will always have the same constant value. But we can
have final methods and classes too – what does it mean to make the behavior of
a class unchangeable, or the class itself?You certainly don’t really change the
code inside a method or class in the middle of execution!  Instead,this means
that a final method can’t be overridden, and a final class cannot be extended.
These are hard rules, and your application won’t even compile if you try to
break them. 

The keyword abstract defines an incomplete entity in Java. When a method is
tagged “abstract,” it contains no body,An abstract class cannot be
instantiated, it can only ever be extended. If a class contains any abstract
methods then it becomes an abstract class and must be declared as such, or your
application simply wont compile. However, you may declare a class abstract even
if it only contains concrete methods – it will still be non-instantiable. Also
remember – if a child class extends an abstract class, it must override all
inherited abstract methods to provide an implementation of its own . If you do
not do this, the subclass must also be declared abstract – it’s not complete
yet. 

```java
abstract class Animal {
  public void eat() {
    System.out.println("The animal munches on some food");
  }
  
  abstract void move();
}
/*-------------------------------------------*/
class Dog extends Animal {
  public void move() {
    System.out.println("The dog walks around");
  }
  public void beg() {
    System.out.println("The dog looks cute to get food");
  }
}
/*-------------------------------------------*/
public class AbstractExample {
  public static void main(String[] args) {
    Dog myDog = new Dog();
    myDog.eat();
    myDog.move();
    myDog.beg();
  }
}
```

Back in eclipse, we have made our Animal class abstract so it can only be
inherited. It contains a concrete method, eat and an abstract one, move. Both
methods will be inherited; however, the abstract method guarantees that each
concrete subclass will be forced to define implementation details for itself.
In the Dog class we have a method local to dogs, beg, and an overridden move
method. This allows us to instantiate a Dog object, and call its move behavior.
This concludes our run-through of these three important keywords. The quirks of
each frequently appear as questions in interviews, and knowing how to use them
properly can save you a lot of hassle. 

# Lecture Notes

## Java Keywords
A keyword is a reserved word in Java that has specific meaning to the compiler. You cannot use the name of a keyword as a variable, method or class.

### static
static is a modifier used to define a class-wide variable or method. It is a globally accessible field. A method marked staticcan only use other staticvariables or methods.

## final 
The keyword final is used to specify a field or method as immutable. final variablesA variable marked finalcannot be assigned a new value once initialized.

NOTE: A final reference variable can have properties that can value, but the reference itself cannot change.

##final methods
A method marked final cannot be overridden. final classesA class marked finalcannot be extended. 

## abstract
The keyword abstractdeclares a method or class as incomplete or as a template. An abstractmethod has no body.

An abstract class cannot be instantiated and should be extended.If you declare at least one method abstract, then the class must be declared as abstract

- If you declare a class as abstract, you do not need to specify any methods as abstract
- You cannot instantiate an abstractclass


