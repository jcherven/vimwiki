# Usage of Keywords

## Usage of "this" keyword 

There can be a lot of usage of java `this` keyword. In java, `this` is a reference
variable that refers to the current enclosing object. 

Here is given the 6 usage of java this keyword.

    - `this` can be used to refer current class instance variable.
    - `this` can be used to invoke current class method (implicitly)
    - `this()` can be used to invoke current class constructor.
    - `this` can be passed as an argument in the method call.
    - `this` can be passed as argument in the constructor call.
    - `this` can be used to return the current class instance from the method.


## "this" : to refer current class instance variable

The this keyword can be used to refer current class instance variable. If there
is ambiguity between the instance variables and parameters, `this` keyword
resolves the problem of ambiguity. 

```java
class Student {  
  int rollno;  
  String name;  
  float fee;  
  Student(int rollno, String name, float fee) {  
    this.rollno = rollno; // Refers class instance variable rollno 
    this.name = name;  // Refers class instance variable name
    this.fee = fee;   // Refers class instance variable fee
  }  
  void display() {System.out.println( rollno + " " + name + " " + fee );}  
}  

class TestThis2 {  
  public static void main(String args[]) {  
    Student s1 = new Student(111,"ankit",5000f);  
    Student s2 = new Student(112,"sumit",6000f);  
    s1.display();  
    s2.display();  
  }
} 
```

## "this" : to invoke current class method

You may invoke the method of the current class by using the this keyword. If
you don't use the this keyword, compiler automatically adds this keyword while
invoking the method. 

Example

```java
class A {  
    void m(){System.out.println("hello m");}  
    void n() {  
      System.out.println("hello n");  
      //m();//same as this.m()  
      this.m();  // By default added by the compiler
    }  
}  

class TestThis4 {  
  public static void main(String args[]) {  
    A a = new A();  
    a.n();  
  }
}
```

## "this" : to invoke current class constructor

The this() constructor call can be used to invoke the current class
constructor. It is used to reuse the constructor. In other words, it is used
for constructor chaining. 

Example 

```java
class A {  
  A(){System.out.println("hello a");}  
  A(int x) {  
    this();  // Current class constructor is called.
    System.out.println(x);  
  }  
}  

class TestThis5 {  
  public static void main(String args[]) {  
    A a = new A(10);  
  }
}  
```

## Usage of the "new" keyword

When you are declaring a class in java, you are just creating a new data type.
A class provides the blueprint for objects. You can create an object from a
class. 

Declaration : First, you must declare a variable of the class type. This
variable does not define an object.

Instantiation and Initialization : Second, you must acquire an actual, physical
copy of the object and assign it to that variable. You can do this using the
new operator. The new operator instantiates a class by dynamically
allocating(i.e, allocation at run time) memory for a new object and returning a
reference to that memory. This reference is then stored in the variable. Thus,
in Java, all class objects must be dynamically allocated. 

The new operator is also followed by a call to a class constructor, which
initializes the new object. A constructor defines what occurs when an object of
a class is created. Constructors are an important part of all classes and have
many significant attributes.  Example

Let us say that we have a class called Student and we need to instantiate this
class. The following syntax does that : 

```java
Student anil = new Student();
```

## Usage of "super" keyword

The super keyword in Java is a reference variable which is used to refer
immediate parent class object.

Whenever you create the instance of subclass, an instance of parent class is
created implicitly which is referred by super reference variable.

    - super can be used to refer immediate parent class instance variable.
    - super can be used to invoke immediate parent class method.
    - super() can be used to invoke immediate parent class constructor.

### Using "super" to refer parent class instance variable

We can use super keyword to access the data member or field of parent class. It
is used if parent class and child class have same fields. 

```java
class Animal {  
  String color="white";  
}  

class Dog extends Animal {  
  String color="black";  
  void printColor() {  
    System.out.println(color);  //prints color of Dog class  
    System.out.println(super.color);  //prints color of Animal class  
  }  
}  

class TestSuper1{  
  public static void main(String args[]) {  
    Dog d=new Dog();  
    d.printColor();  
  }
} 
```

## Using "super" to invoke parent class method

The super keyword can also be used to invoke parent class method. It should be
used if subclass contains the same method as parent class. In other words, it
is used if method is overridden. 

```java
class Animal {  
  void eat(){System.out.println("eating...");}  
}  

class Dog extends Animal {  
  void eat(){System.out.println("eating bread...");}  
  void bark(){System.out.println("barking...");}  
  void work() {  
    super.eat();  // Calling the parent class eat() method using super keyword
    bark();  
  }  
}  

class TestSuper2 {  
  public static void main(String args[]) {  
    Dog d=new Dog();  
    d.work();  
  }
}
```

## Using "super" to invoke parent class constructor

The super keyword can also be used to invoke the parent class constructor. 

```java
class Animal {  
  Animal(){System.out.println("animal is created");}  
}  

class Dog extends Animal {  
  Dog() {  
    super(); // using super keyword to access the parent class constructor. 
    System.out.println("dog is created");  
  }  
}  

class TestSuper3 {  
  public static void main(String args[]) {  
    Dog d=new Dog();  
  }
} 
```

Note : While using "super" keyword to access the parent class constructor,
remember that it has to be in the first line within the subclass constructor.

## Static Keyword

The static keyword in Java is used for memory management mainly. We can apply
java static keyword with variables, methods, blocks and nested class. The
static keyword belongs to the class rather than an instance of the class. 

The static can be:

    - Variable (also known as a class variable)
    - Method (also known as a class method)
    - Block
    - Nested class

## Static variable

If you declare any variable as static, it is known as a static variable.

    - The static variable can be used to refer to the common property of all
      objects (which is not unique for each object), for example, the company
      name of employees, college name of students, etc.
    - The static variable gets memory only once in the class area at the time
      of class loading.

## Advantages

    It makes your program memory efficient (i.e., it saves memory). 

Example

```java
//Java Program to demonstrate the use of static variable  
class Student {  
   int rollno;//instance variable  
   String name;  
   static String college ="ITS"; //static variable  
   
   //constructor  
   Student(int r, String n) {  
     rollno = r;  
     name = n;  
   }  
   //method to display the values  
   void display () {System.out.println(rollno+" "+name+" "+college);}  
}  

//Test class to show the values of objects  
public class TestStaticVariable1 {  
  public static void main(String args[]) {  
    Student s1 = new Student(111,"Karan");  
    Student s2 = new Student(222,"Aryan");  
    //we can change the college of all objects by the single line of code  
    //Student.college="BBDIT";  
    s1.display();  
    s2.display();  
  }  
}  
```

## Static Explanation

Notice the stack, heap and class area in the diagram.

| Stack Memory | Heap Memory         | Class Area  |
|              |                     | college=ITS |
| s2           | id=222; name=Arya;  | college=ITS |
| s1           | id=111; namesKaran; | college=ITS |

## Final Keyword

The final keyword in java is used to restrict the user. The java final keyword
can be used in many context. Final can be:

    - variable
    - method
    - class

The final keyword can be applied with the variables, a final variable that have
no value it is called blank final variable or uninitialized final variable. It
can be initialized in the constructor only. The blank final variable can be
static also which will be initialized in the static block only.

## Example

### Final Variable : 

```java
class Bike9 {  
  final int speedlimit=90; //final variable  
  void run() {  
    speedlimit=400;  // Compile Time Error (Cant change final variable value)
  }  

  public static void main(String args[]) {  
    Bike9 obj = new Bike9();  
    obj.run();  
  }  
} //end of class 
```

### Final Method : 

```java
class Bike {  
  final void run(){System.out.println("running");}  
}  

class Honda extends Bike {  
  void run(){System.out.println("running safely with 100kmph");}  // Compile Time Error (Cant override final method)
  public static void main(String args[]) {  
    Honda honda= new Honda();  
    honda.run();  
  }  
} 
```

### Final Class : 

```java
final class Bike {}  
class Honda1 extends Bike {  // Compile Time Error (Cant extend final class)
  void run(){System.out.println("running safely with 100kmph");}  
  
  public static void main(String args[]) {  
    Honda1 honda = new Honda1();  
    honda.run();  
  }  
} 
```
