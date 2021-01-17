# OOP Concepts

## Java Encapsulation with Access Modifiers

In Java, a class is is a structure that can have states and behaviors. It
serves as a template for objects, which are instances of a class with a
specific state. For example a Robot class might have a state consisting of many
possible characteristics such as size, weight, propulsion, articulation,
mission, etc. Moreover, all robots have a range of common behaviors like
communicate,are tracking objects in their environment, and travelling just a
name a few. The robot class serves as a blueprint for a specific robot, like
Optimus Prime,who shares behaviors with all other robots, though he may possess
behaviors unique to himself, and has a unique state. Today, we're going to
examine some of the features that go into Java classes.

Let's start with access modifiers, which are keywords that control the ability
for outside code to access or change the states and behaviors of a class.

Java has four access modifiers public, private, protected, and default last one
is indicated by not specifying another modifier. For fields, methods, and
constructors any of these modifiers may be used. However, only “public” and
“default” make sense for classes.  Why is this?

Access modifiers control how access to data is shared between a class and other
classesin the same package, other packages, and child or subclasses.

Public data can be accessed or modified by any other class in the
application,no matter if it's in the same package, or another.

Protected data can be used by any class in the same package,or any subclasses –
even if they are in another package. 

Data with no access modifier specified has “default” access privileges. It's
accessible by any class or subclass in the same package, but is invisible to
code outside of the package.

Private data is only accessible within the same class it is declared.  It can't
even be used by subclasses.

If you want to expose data in a class to outside manipulation,it's best to do
that by making the data in a class private, and creating simple methods called
accessor and mutator methods – often short hand “getters and setters.” An
accessor or getter method just returns the value of a variable stored in an
object, and a setter method allows the user to changes the value. Let's see how
this works.

Here in eclipse we have a simple robot class.

```java
package examples;
public class Robot {
  private int maxSpeed;
  public int getMaxSpeed() {
    return maxSpeed;
  }
  public void setMaxSpeed(int maxSpeed) {
  if (maxSpeed >= 0)
    this.maxSpeed = maxSpeed;
  else
    this.maxSpeed = 0;
  }
  public void travel() {
    System.out.println("The robot moves a distance of " + maxSpeed + " units.");
  }
}
```

Notice there is no main method here; therefore, this class cannot be the
starting point of our application. That’s okay we will create a test class with
a main method later that will call the robot class. The robot class has a
maxSpeed field which can also be called an instance variable. It deserves this
name, because each instance of the robot class can have its own personal
maxSpeed. Fields obey the HAS-A relationship in that a robot HAS-A max speed.
This field is marked as private which means nothing can see it outside the
robot class. This is a good thing because no one can tamper with our robot
leaving it in an unpredictable state. We can set the maxSpeed field with a
setter method as shown. This is acceptable because we control the range of
allowable maxSpeeds if we wish. In fact, here we test to make sure the maxSpeed
provided is greater than or equal to 0.  If it's lower,we set it to 0. The
private field and the setter method form a powerful encapsulation scheme. The
only way to change the maxSpeed field is through the setter. Because the setter
contains its own validation,it prevents our application or a user from
accidentally setting the value to -30,which would make no sense. The travel
method is public and for now simply reports back the maxSpeed.

We will return to this class later. Here we see our RobotTester class. Here we
see the line of code used to instantiate a class.

```java
package examples;
public class RobotTester {
  public static void main(String[] args) {
    Robot myrobo = new Robot();
    myRobo.travel();
  }
}
```

The keyword “new” makes it all happen – it tells the JVM to create a new
instance of Robot, and calls the constructor method to initialize the object.
By assigning a reference type variable to this new instance, we create a link
to it that we can use to call its methods.

But here we are calling a constructor, and we don't even know what they are!
Well,a constructor is used to create an object of a class and to set its
initial state. Once we have the object we can use the fields and methods which
were defined in the class. A constructor has the same name as the class and no
return type. All classes have at least one constructor - if you don't write one
yourself, the JVM will give you a “default” constructor. This default
constructor will take no arguments, and doesn't set any values.

A class can have many constructors all with the same name, but must be
differentiated by the number or type of parameters they accept. This is called
method overloading, and we'll talk about it shortly.

Let's go back to our Robot class, and write a constructor. It will take no
arguments, and will just initialize the maxSpeed variable to 1. Because we are
coding the constructor ourselves, the JVM will no longer give us a free one.

```java
package examples;
public class Robot {
  private int maxSpeed;
  
  public Robot() {
    this.maxSpeed = 1;
  }
  
  public int getMaxSpeed() {
    return maxSpeed;
  }
  public void setMaxSpeed(int maxSpeed) {
  if (maxSpeed >= 0)
    this.maxSpeed = maxSpeed;
  else
    this.maxSpeed = 0;
  }
  public void travel() {
    System.out.println("The robot moves a distance of " + maxSpeed + " units.");
  }
}
```

Back in our RobotTester class, in the main method,we have instantiated Robot
using “new” and making the call to its constructor. Once we have the robot
object we can then use the dot operator to access its methods. When we run this
we get the max speed back from the travel method as expected. As I mentioned
before, methods and constructors in Java can be overloaded. Since the names all
the same in this case, the only way to tell one method apart from another is
through the input parameters. Either changing the types or the number of the
input parameters is acceptable to the compiler. For example if the overloaded
method is called “finder” one finder method may accept a string while another
accepts an int.

Back in eclipse, we have re-written the Robot class to include overloaded
constructors using the keyword: “this.”

```java
package examples;
public class Robot {
  private int maxSpeed;

  public Robot() {
    this.maxSpeed = 1;
  }

  public int getMaxSpeed() {
    return maxspeed;
  }
  
  public void setMaxSpeed(int maxSpeed) {
  if (maxSpeed >= 0)
    this.maxSpeed = maxSpeed;
  else
    this.maxSpeed = 0;
  }
  
  public void travel() {
    System.out.println("The robot moves a distance of " + maxSpeed + " units.");
  }
}
```

This is a keyword in Java that refers specifically to the object in which the
keyword appears. You can see it used here in an overloaded constructor that
accepts a maxSpeed argument. We use this and the dot operator to refer to the
object's instance variable maxSpeed, to differentiate it from the passed-in
variable maxSpeed.

In conclusion, Java classes follow OOP principles and have a both state and
behavior,and access modifiers determine the visibility of these states and
behaviors to other classes. The “new” keyword followed by a constructor call
creates an object of the class in memory. With an object in hand, a calling
program can make use of that object’s fields and methods. Those methods and
constructors can be overloaded,by having multiple methods that share the same
name, but accept a different number or types of parameters. 

[OOP-Concepts](OOP-Concepts.md)
