# Relationships: IS-A vs HAS-A

Inheritance isn't the only way of creating relationships between objects.
Inheritance creates an Is-A relationship, but there one object might also have
a Has-A relationship to another object. 

## Inheritance (IS-A)

Take a look at the following snippet, in the Java syntax:
```java
public class Animal {}

public class Dog extends Animal {}
```
In the above scenario, class Dog represents an **IS-A** relationship to Animal.
It is valid to say that an instance of class Dog is also an instance of class
Animal.

Extending this concept further, take a look at the following snippet in the
Java syntax.
```java
public class Animal {}

public class Bird extends Animal {}

public class Hawk extends Bird {}
```
Based on the above, both class Hawk and class Bird represent an IS-A
relationship with class Animal. Additionally, an object of class Hawk IS-AN
object of class Bird. Note that these relationships are unidirectional - it is
not appropriate to say an Animal IS-A Hawk.
 
## Composition (HAS-A)

Next, take a look at the following snippet:
```java
public class Dog {}

public class Person {
  Dog myDog = new Dog();
}
```
Based on the above, you'll see that Person has an reference variable myDog that
points to an object that is an instance of class Dog. Considering this, we say
that class Person HAS-A class Dog.

Thus, a reference variable creates a HAS-A relationship. Many times you'll see
this referred to as Composition or Aggregation. What's the difference?
technically, if Object B cannot exist without Object A, (if our program design
indicates that a Dog object can never be created independent of or outside of a
Person object) it is an example of Composition. If a Person object has-a Dog
object, but our application also creates independent Dog objects elsewhere
(like wild Dogs), then this relationship is called Aggregation. Generally, you
would be forgiven for referring to both as Composition, but there are times
when clarity is important.

Composition and Inheritance are not mutually exclusive. For example, consider
this segment in the Java syntax:
```java
class Dog {}
class Labrador extends Dog {}

public class Person {
    Dog myDog = new Labrador();
}
```
This is verging on an example of polymorphism, but recall that a reference
variable is allowed to store the reference of an object that IS-AN instance of
the reference variable's type. We say that a Person HAS-A Dog object, but that
Dog-type reference variable refers to a Labrador object. This is okay, because
a Labrador object IS-A Dog object too.

Of course, following the same rules as we set out before, we could only use the
myDog reference variable to access the states or behaviors of the Labrador
object that are defined in the Dog class.
 
## Why is the Distinction Between Relationships Important?

Besides being a common and basic interview question, understanding the
differences between these relationships can inform how you design your code. If
you are writing code to simulate the operation of a car. Does a car have an
engine, or is an engine a subtype of car? When the answer is obvious, it can
prevent you from making mistakes with your design. If a Car has-an Engine, a
FuelTank, and other such structures, are these structures subtypes of some
concept? For example, are an Engine object and a FuelTank object each more
specific examples of a generic CarPart structure?

But sometimes, the answer to these types of questions isn't obvious, or is in
fact driven by a business decision. Imagine you are writing software for a a
social media platform: Does a post have comments, or are comments a type of
post? Depending on how you answer this question, you wind up with Facebook or
Twitter. Two different platforms that answered the same question in different
ways.

< [Inheritance in Csharp](Inheritance-in-Csharp) | [Polymorphism](Polymorphism) >
