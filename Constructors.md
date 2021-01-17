# Constructors

## Constructor

In Java, a constructor is a block of codes similar to the method. It is called
when an instance of the object is created, and memory is allocated for the
object. 

It is a special type of method which is used to initialize the object. 

## When is a constructor called?

When an object is created, compiler makes sure that constructors for all of its
subobjects (its member and inherited objects) are called. If members have
default constructors or constructor without parameter then these constructors
are called automatically, otherwise parameterized constructors can be called
using initializer list. 

Note: It is called constructor because it constructs the values at the time of
object creation. It is not necessary to write a constructor for a class. It is
because java compiler creates a default constructor if your class doesn't have
any. 

## Rules to remember while creating a constructor

There are three rules defined for the constructor.

    - Constructor name must be the same as its class name
    - A Constructor must have no explicit return type
    - A Java constructor cannot be abstract, static, final, and synchronized

## Types of constructors

    - Default Constructor
    - Parameterized Constructor

### Default Constructor

The default constructor is a no-args constructor that the Java compiler inserts
on your behalf; it contains a default call to super(); which is the default
behavior. If you implement any constructor then you no longer receive a default
constructor. 

Note : If there is no constructor in the class, the compiler adds a default
constructor

### No-Argument Constructor

```java
public Bicycle() {
    gear = 1;
    cadence = 10;
    speed = 0;
}
```

`Bicycle yourBike = new Bicycle();` invokes the no-argument constructor to
create a new Bicycle object called yourBike. 

Note : The diagram below describes that a default constructor is added by the
compiler when there is no constructor declared in the class. 

`class Bike {}` => Compiler => `class Bike{ Bike(){} }`

## Parameterized Constructor

A constructor which has a specific number of parameters is called a
parameterized constructor. 

The parameterized constructor is used to provide different values to the
distinct objects. However, you can provide the same values also. 

```java
class Student4{  
    int id;  
    String name;  
    Student4(int i,String n){  
    id = i;  
    name = n;  
    }  

    void display(){System.out.println(id+" "+name);}  

    public static void main(String args[]){  
       Student4 s1 = new Student4(111,"Karan");  
       Student4 s2 = new Student4(222,"Aryan");   
       s1.display();  
       s2.display();  
   }  
}  
```

In the above example, we have created the constructor of Student class that
have two parameters. We can have any number of parameters in the constructor.
Constructor Overloading

In Java, a constructor is just like a method but without return type. It can
also be overloaded like Java methods. 

Constructor overloading in Java is a technique of having more than one
constructor with different parameter lists. They are arranged in a way that
each constructor performs a different task. They are differentiated by the
compiler by the number of parameters in the list and their types. 

```java
class Student5{  
    int id;  
    String name;  
    int age;  

    //creating two argument constructor  
    Student5(int i,String n){  
    id = i;  
    name = n;  
    }  

    //creating three argument constructor  
    Student5(int i,String n,int a){  
    id = i;  
    name = n;  
    age=a;  
    }  

    void display(){System.out.println(id+" "+name+" "+age);}  

    public static void main(String args[]){  
       Student5 s1 = new Student5(111,"Karan");  
       Student5 s2 = new Student5(222,"Aryan",25);  
       s1.display();  
       s2.display();  
   }  
}  
```

## Constructor vs Method

### Constructor : 
    - A constructor is used to initialize the state of an object. 
    - A constructor must not have a return type. 
    - The constructor is invoked implicitly. 
    - The Java compiler provides a default constructor if you don't have any
      constructor in a class. 
    - The constructor name must be same as the class name. 

### Method : 
    - A method is used to expose the behavior of an object. 
    - A method must have a return type. 
    - The method is invoked explicitly.
    - The method is not provided by the compiler in any case. 
    - The method name may or may not be same as class name. 

NEXT: [OOP Pillars](OOP-Pillars)
< [Classes and Objects](Classes-and-Objects)
< [OOP Study Guide](OOP-Study-Guide)
< [Index](Index)
