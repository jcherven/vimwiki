# Polymorphism in Java

Polymorphism is a fun word. The word itself means “Many Forms”, and it refers to
the “is-a” relationship created by two objects through inheritance. When one
class inherits from another, it creates a relationship that can be described by
the verb “is”. If class Dog extends class Animal, then you can say an instance
of a Dog is also an instance of an Animal. A Dog is-an Animal. We also discussed
how you can use this concept in reverse to figure out how your classes and
their inheritances should be organized. If you can describe one class as being a
more specific example of another class, then you can probably have the more
specific class inherit some properties or behaviors from the more generic
class. Through the principles of OOP, we know that a Dog object is an instance
of the Dog class. But the principle of polymorphism also says that a Dog object
is an instance of an Animal class too. Because a child class inherits all public
and protected variables and methods from its super class, the child class is
guaranteed to have at least those variables and methods– it may implement its
own, or override the functionalities therein, but if the Animal class has a
public eat() method, then the Dog class that extends it is also guaranteed to
have an eat() method, even if it works differently. You might recall from
another video that when you create an object in memory with the “new” keyword,
you store a reference to that object in a reference variable, that uses the
object’s class as a type. When I say “Dog myDog = new Dog()”, I am creating a
Dog object by using the new keyword to invoke the constructor of the Dog class,
and I am storing a reference to the Dog object in a variable of type Dog named
“myDog. ”Understanding polymorphism requires understanding what that reference
variable type actually does. To do that, you can think of the reference variable
type as a mask you put over your object’s code. Your Dog object has all the code
for methods defined in the Dog class, and the reference variable type is like a
sheet of paper that sits overtop of that code, with holes cut away for certain
methods to be seen through, while others are hidden. The holes that are cut away
and thus allow access to the object code underneath, are placed to only allow
access to the methods defined in the class being used as the type. For example,
let’s say our Animal class defines the method “eat()”, and the Dog class
extends Animal and additionally defines the method “bark()”. If I store a
reference to our Dog object in a Dog type reference variable, then I can access
the logic for the eat() and bark() methods as defined in the Dog class. But if I
use an Animal reference type instead, then I only have access to the eat()
method that is defined in the Animal class – even though the logic for that
method will be the implementation used in the Dog class. The process of storing
a more specific value in a less specific type is called “upcasting”. But what
about variables?Well, those are kind of tricky. Just like with methods, the
reference type you use acts as a kind of mask, exposing and allowing access
only to the variables defined in the reference type. However, the initialization
of those variables is also dependent on the type!This is like writing the
initialization on the mask directly. For example, let’s say that our Animal
class defines a variable named “legs” and initializes its value to 4. The Human
class extends Animal, but it defines its own “legs” variable that is
initialized to 2. If I create a Human object, but store it in an Animal
reference type…I will have access to the legs variable, but it will be
initialized to 4, instead of 2. Here’s a direct example of this:Here I have an
Animal class defined, which has a single method – eat, which just prints a
message to the console. Likewise, I have a Dog class, which extends Animal, and
additionally defines a bark() method. I also have a Boolean variable, “hasFur”,
which is initialized to “false” in Animal but “true” in Dog. When I create a new
Dog object and store it in an Animal class reference, eclipse won’t complain –
a Dog is-an Animal, so this works. Using the reference variable, I can invoke
the eat() method declared in the Animal class – but as defined in the Dog
class. I cannot however, invoke the bark() method, because the Animal reference
type does not grant access to methods that are not defined in the AnimalIf I
try to print the value in the “hasFur” variable, you’ll see it prints “false” –
the variable exists in both classes, but it is initialized according to the
reference type, not the object type. Remember that we can only use polymorphism
like this so long as two conditions are met: first, the object type must have
an inheritance relationship with the reference variable type. We cannot store an
object in an unrelated reference variable!With the mask metaphor, remember that
the mask only reveals methods and variables that are guaranteed to be there –
and you cannot guarantee that two unrelated classes will have a subset of
matching methods. Secondly, the reference type cannot be more specific than the
object type. For example, we cannot store an Animal type object into a Dog
reference type!To use the mask metaphor, this would result in our mask having a
hole cut out where a method should be, but no underlying method!You can
“downcast” an object into a more specific type though!Just remember that the
same is-a relationship rules apply. The new reference type must have an is-a
relationship with the object type. For example, let’s say we have our Animal and
Dog classes, but we also have a Bird class that extends Animal. We could upcast
a Dog object to an Animal reference type, and then downcast that animal
reference type back to a Dog reference type, but we could not downcast it to a
Bird reference type. No matter the reference type, the object is still a Dog
object. We can upcast the Dog object to an Animal reference type because the Dog
object is-an Animal type, and we can further downcast the Dog object back into
a Dog reference type because of course a Dog object is also a Dog type. But a
Dog object is never a Bird type. Downcasting like this is often considered
unsafe, because it can be difficult to guarantee that the downcasted reference
type actually has an is-a relationship with whatever the object type is. Just to
be safe, we can use the instanceof keyword to test whether the object a
reference variable points to has an is-a relationship with a particular
class. Here, I only downcast to Dog if the underlying object is also an instance
of a Dog, protecting me from a bad cast. Let’s wrap up this discussion of
Polymorphism with a real-world example. Let’s say you’re programming a video
game, where you have a lot of monsters roaming around the world. You need to
make sure that every couple of seconds, every monster moves to a new random
location, but you have a lot of different types of monster classes, each with
their own logic. By applying our knowledge of polymorphism, we can make each
monster class inherit from a shared superclass, Creature, which declares a
method called “roam()”. Every monster class might have unique logic for the
roam() method, but they are guaranteed to at least possess a roam() method. In
our game logic now, we can store all of our individual monster classes in a
collection of Creature type reference variables, and iterate over each Creature
reference type to call the roam() method on each. Now these few lines of code
can handle the roaming behavior for 10 monsters or 10,000, even if each monster
is a unique class with unique behavior. This is the power of polymorphism. 

< [Polymorphism](Polymorphism) | [Abstraction and Encapsulation](Abstraction-and-Encapsulation)  >
