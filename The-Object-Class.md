# Java Basics

## The Object Class

There is one class to rule them all, in Java, and that is the very confusingly named Object class.

The object class is the parent class of all classes defined in Java, even if you do not explicitly extend it. The Object class provides several methods as a convenience for developers, and acts as a wrapper for any polymorphic code.

The Object class defines several methods.  All are which are protected so you can override them to provide your specific implementation.

the toString method gives a string representation of the object. This method is called when you directly print an object to the console.  By default, this prints the memory address of the object. 

hashCode is used to provide a unique identifier for the object. 

equals is used to compare two objects.  By default,it compares memory addresses, and so its functionally equivalent to the == operator unless overridden. 

The finalize method is a method that is called by the garbage collector for any object instance before it is removed from memory. 

clone will create a copy of the object. 

So let’s demonstrate the use of some of these methods. 

```java
package examples;

class Person {
  private String name;
  
  public String getName() { return name; }
  public void setName(String name) { this.name = name; }
}

public class ObjectTest {
  public static String print(Object o) {
    return o.toString();
  }
  
  public static void main(String[] args) {
    Person someone = new Person();
    
    System.out.println(someone);
  }
}
```

Here in eclipse we have written a Person class. The Person class has a private property name as well as methods to get and set the name property – a getter and setter.

As you can see, although we are not using the “extends” keyword, we are implicitly extending the Object class.

Now that we have our model of a Person set up, we’ll write a TestPerson class. In the main method, we’ll instantiate a new Person and then we’ll print the Person object directly to the console. The print method takes a string as an argument and an object will return the result of its toString method. The default implementation is to return the name of the class and that instance’s hashCode. Let’s run this program and you’ll see the result as Person and the default hashCode.

```output
examples.Person@659e0bfd
```

We’ll update the Person class again to override the toString method. We’ll return the name of the Person. 

```java
package examples;

class Person {
  private String name;
  
  public String getName() { return name; }
  public void setName(String name) { this.name = name; }
  public String toString() {
  return "Hi, I'm " + this.name;
  }
}

public class ObjectTest {
  public static String print(Object o) {
    return o.toString();
  }
  
  public static void main(String[] args) {
    Person someone = new Person();
    
    someone.setName("Joe");
    System.out.println(someone);
  }
}
```

```output
Hi, I'm Joe
```

Running the program, you’ll see that the Person’s name is the only thing printed. Thus we have effectively overridden the toString method.

As a Best Practice you should get into the habit of overriding some of the methods the object classprovides in order to take advantage of functionality like toString or equals. 

For example, because the == operator already compares memory locations to determine object equality,the equals method is often overridden to compare the values of instance variables to determine equivalence between two objects. Oftentimes, you’ll also see the Object class used in utility methods that provide generic functionality for any class. Because every object is an Object, you can always upcast anything to an Object type reference.  I’ll see you next time. 
