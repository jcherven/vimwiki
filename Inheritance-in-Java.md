# Inheritance in Java
< [Inheritance](Inheritance) | [Inheritance in Csharp](Inheritance-in-Csharp) >

You may recall hearing at some point that inheritance is a major feature of
Java, and in fact all object oriented programming languages.Inheritance gives
access to the states and behaviors of one class to another, in much the same
way that a child inherits certain properties and behaviors from their parent.

Consider a book, which has properties describing the number of pages contained,
and a title. It has methods describing the behavior of turning a page. We say
that Book is a “super, base, or parent” class, and from Book we extend
Magazine. Magazine is a “sub, derived, or child” class of Book. The “extends”
keyword in Java goes in the class definition, right after the name. A class in
Java can only extend one other class. You can use this to create a chain of
inheritance, Where class C extends B, and B extends class A. Therefore class C
has access to the variables and methods of classes B and A. But class C can't
extend both B and A directly! This is called multiple inheritance, and can lead
to some weird problems.

Java does not support it… At least not in name. As of Java 8 there are some
situations in which Java can sort-of achieve multiple inheritance, but that
doesn't make it an improvement – it's still something to be avoided. So
Magazine automatically inherits the public and protected fields of book, like
title and numPages. This does not mean that a magazine must have the same title
or the same number of pages as another instance of a book, it just means that a
magazine can also have a title or a page count. Similarly, the magazine
automatically has a default page-turning implementation that it gets from Book.
However, Magazines might also need their own fields, like a list of articles,
or behaviors for dropping subscription forms all over your floor.

So what does inheritance buy us? Well as a developer, you no longer need to
code duplicate functions into every type of specialized Book. The code is now
far less cluttered in general then it would be without inheritance. Should the
shared behavior ever be changed in the future, without inheritance you would
have re-write that code in every class in which it appeared. With inheritance,
you only have to make the change once in the superclass.

Inheritance creates an is-a relationship between the child class and the parent
class. Our Magazine class is-a Book, but the converse isn't necessarily true –
not all Books are Magazines. Just like all squares are rectangles, but not all
rectangles are squares. You can use this “is-a” rule to work backwards and
determine which classes in your code can inherit from each other. If you can
describe a class as being an example of another type of class, you can create
an is-a relationship and thus an inheritance.

Inheritance is also the gateway to polymorphism. This is an incredibly
important concept in the world of OOP – simply put, it’s the ability for an
object to also be considered an instance of every object in its inheritance
chain. For example, not only is USA Today an instance of a Magazine, it’s also
an instance of a Book, which is an instance of the Object class. Therefore, USA
Today can be treated as a magazine, a book, or an object. Let’s go to eclipse
to see how inheritance can be used in this way.

```java
package examples;

class Animal {
  public void speak() {
    System.out.println("\"generic animal sounds!\"");
  }
}

class Dog extends Animal {
  public void speak() {
    System.out.println("Woof!");
  }
  public void beg() {
    System.out.println("The dog looks cute for food.");
  }
}


public class InheritanceTest {
  public static void saySomething(Animal a) {
    a.speak();
    
    if (a instanceof Dog)
      ((Dog) a).beg();
  }
  
  public static void main(String[] args) {
    Animal myAnimal = new Animal();
    Dog myDog = new Dog();
    
    saySomething(myAnimal);
    saySomething(myDog);
  }
}
```

Here I have an Animal class defined, which has a single method defined – speak,
which just prints a message to the console. Likewise, I have a Dog class, which
extends Animal, but defines no new behaviors of its own. Note that the
“extends” keyword is how we show inheritance in Java. Unlike some other
languages, a class in Java can only ever extend one other class – Java does not
support multiple inheritance. In my test class, I define a method that accepts
any Animal object, and calls the speak method of the object that is passed in.
I can create an instance of both an Animal and a Dog, and when passed into the
method, both will speak. This is because a Dog is always also an Animal. In
fact, the whole reason I can pass a dog into the method at all is because it’s
an animal.

Let’s see what happens though, when we give Dog its own speak method. After
all, dogs don’t make generic animal noises, they bark! When we run the
application again, we can see that our output has changed. When we pass in a
Dog, Instead of calling the speak method defined in Animal, we call the speak
method defined in Dog! This is an example of **method overriding**, not to be
confused with method overloading.

Did you catch that last bit? A child class inherits public and protected
methods from a parent class, but it can override the implementation of those
methods with its own. This is useful, because you'll often find yourself
needing certain methods in different subclasses to be called by the same name,
but you need some or all of those subclasses to have a unique implementation.
Overriding a method isn't anything special, you're just hiding it behind a new
method that has the same name, and the same number and types of parameters
getting passed in.

Suppose we had a Book class, with a method turnPage(). In the Book class, the
turn page increments the pageNumber by one, retrieves the text for that page,
and displays it to the user. But our child class, PopUpBook, also needs to
unfold the picture on the new page. The PopUpBook class then declares its own
turnPage() method, with the exact same signature of Book's turnPage() method –
only it has a new line of code inside. If we create an instance of PopUpBook
and call the turnPage() method, we'll get the implementation defined in
PopUpBook, not Book.

But we're repeating a lot of the code in the child class method that's also
present in the super class method. Is there a way we could simplify that? You
can with super! The “super” keyword is a reference to the parent class, kind of
like the “this” keyword is a reference to the current object. You can use it in
the same way – you can use the super keyword with the dot operator to invoke a
method defined in the current classes' superclass.

We can now re-write our PopUpBook's turnPage method to first call
super.turnPage(), followed by the code unique to PopUpBook. This keeps the
generic code in the generic class, and the specific code in the specific
classTaking full advantage of inheritance in your application can promote
re-usability, ease of maintenance, and reduces the amount of code you have to
write. Be careful not to inject inheritance where it’s not needed however, as
this can make your code just as complex and messy as not using it at all.

< [Inheritance](Inheritance) | [Inheritance in Csharp](Inheritance-in-Csharp) >
Back to [OOP Concepts](OOP-Concepts)
