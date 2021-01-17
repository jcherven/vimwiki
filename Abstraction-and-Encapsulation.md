# Abstraction and Encapsulation

## Abstraction
Abstraction and Encapsulation are two more core concepts of Object Oriented
Programming. Abstraction is the principle of "using simple things to represent
complex things." We often shorthand this as "data hiding," because the
principle is the same: when you break your code into objects, the user (whether
it's an actual user or another developer using your code to write their own
programs) doesn't need to know how something works, they just need to know what
it does, and what the inputs and outputs are.

A common analogy for abstraction is using a remote to change the channel on
your television. When you press the "Channel Up" button, you want to increase
the channel number by 1. You don't need to know that the remote is flashing an
infrared light in a pattern at your television, and you don't need to know that
your television is tuning a receiver to isolate a different frequency of
electrical signal from the cable line. Push button, change channel. The
mechanical and electrical processes have been abstracted through a button.

It's the same concept when you're writing code. Consider this Java code
segment, which creates a connection to a PostgreSQL database using a library
called JDBC:
```java
public class ConnectionManager {
  private static String CONNECTION_USERNAME = "postgres";
  private static String CONNECTION_PASSWORD = "password";
  private static String URL = "jdbc:postgresql://localhost:5432/MyDatabase";
  private static Connection connection;

  public static Connection getConnection() throws SQLException {
    if (connection == null) {
      try {
        Class.forName("org.postgresql.Driver");
      } catch (ClassNotFoundException e) {
        System.out.println("Could not register driver!");
        e.printStackTrace();
      }
      connection = DriverManager.getConnection(URL, CONNECTION_USERNAME, CONNECTION_PASSWORD);
    }
      return connection;
  }
}
```
This looks really complicated, and unless you're familiar with JDBC, it's not
immediately obvious what each line is doing. But as a developer, if you wanted
to use this code in my program, all you need to do is this:
```java
public class Example {

    public static void main(String[] args) {

        Connection dbConn = ConnectionManager.getConnection();

    }
}
```

All of this complicated behavior has been abstracted into a single method call:
by invoking ConnectionManager.getConnection(), you receive a reference to a
Connection object in memory that is configured to connect to a specific
PostgreSQL database.

Even the original method code contains a lot of examples of abstraction! How
does Class.forName() work, or ClassNotFoundException.printStackTrace()? You
don't need to know the specifics instructions involved to use these methods.

In short, the division of code into Classes and Objects is abstraction.
 
## Encapsulation
Encapsulation is how you go about restricting access to your abstracted code, by using access modifiers. You've seen these around in multiple examples, and most languages have at least these three:

    - public: the code is visible to all other classes
    - protected: the code is only visible within the current class, or any derived/child classes
    - private: the code is visible only within the current class

One of the design concepts of Object-Oriented Programming is that your code
will not only be used by your expected users, but can be re-used by other
developers to write their own programs. However, there are likely variables or
methods in your code that you do not want other developers to be able to access
directly. There might be a variable that you do not want to be given a value
less than 0. There might be utility methods that your classes and objects use
to perform their jobs, but shouldn't be used by any other developers or
programs.

Here's an example of a Java class representing a person:
```java
public class Person {
    public int age = 0;

    public void setAge(int a) {
        if (a < 0)
            age = 0;
        else
            age = a;
    }
}
```
In this example, I could set the age of the person by calling the setAge()
method. This method makes sure the age is always greater than or equal to 0,
since it wouldn't make sense to have a person with a negative age! But because
the "age" variable is public, it's possible to bypass the setAge() method and
set the age directly!
```java
public class Example {

    public static void main(String[] args) {
        Person someGuy = new Person();
        
        someGuy.setAge(25);
        someguy.age = -10;
    }
}
```

If we want to enforce our rules about minimum ages, we need to force other
developers to go through the setAge() method. We could do that by changing the
access modifier of the age variable:
```java
public class Person {
    protected int age = 0;

    public void setAge(int a) {
        if (a < 0)
            age = 0;
        else
            age = a;
    }
}
```

Now, the age variable can only be changed from within the Person class (like
through the setAge() method), or through any other class that inherits from the
Person class. The protected access modifier restricts only classes that are in
a different package but not subclasses from setting the variable directly, This
leaves a vulnerability for subclasses to still change the variable directly. 

For instance, another developer might take the above code, and then write this:
```java
public class DerivedPerson extends Person {

    public void setAge(int a) {
        age = a;
    }
}
```

Now, this other developer could create instances of DerivedPerson instead of
Person. Because a DerivedPerson object has an is-a relationship to Person, a
DerivedPerson object can be used in any code that expects a Person object. The
DerivedPerson also inherits the age variable, and the setAge() method of the
DerivedPerson overrides the setAge() method inherited from the Person object.
The end result is that the protected variable can still be assigned an invalid
value:
```java
public class Example {

    public static void main(String[] args) {
        DerivedPerson someGuy = new DerivedPerson();
        
        someGuy.setAge(-15);
    }
}
```

If the age variable were private, however, this would not work. A private
variable is not accessible outside of the class in which it is located - so it
could be changed through a Person object's setAge() method, but nowhere else.
Being private, it will also not be inherited by any derived classes.

Generally, it is considered a best practice to make all states and behaviors
private initially, and only change them to protected or public if necessary.

There are other ways to implement encapsulation as well, but the specific ways
to do so differ between different languages. These include...

    - Preventing a class from being instantiated by declaring it "abstract"
    - Preventing a class from being derived / extended / inherited from
    - Creating a private class nested inside another to prevent use
    - Using namespaces, assemblies, or packages to separate unrelated classes


< [Polymorphism in Java](Polymorphism in Java) | [Java Encapsulation](Java-Encapsulation) >
