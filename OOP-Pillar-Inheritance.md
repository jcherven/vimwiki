# OOP Pillars

## Polymorphism

### Polymorphism

    - Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.
    - Any Java object that can pass more than one IS-A test is considered to be polymorphic. In Java, all Java objects are polymorphic since any object will pass the IS-A test for their own type and for the class Object.

### Method Overloading 

    - If a class has multiple methods having same name but different in parameters, it is known as **Method Overloading**. 
    - If we have to perform only one operation, having same name of the methods increases the readability of the program. 
    - Suppose you have to perform addition of the given numbers but there can be any number of arguments, if you write the method such as a(int,int) for two parameters, and b(int,int,int) for three parameters then it may be difficult for you as well as other programmers to understand the behavior of the method because its name differs. 

### Different ways to overload a method?

There are two ways to overload the method in java
    - By changing number of arguments
    - By changing the data type

#### Method Overloading  - Changing the number of arguments

```java
class Adder{  
   static int add(int a,int b){return a+b;}  // 2 arguments
   static int add(int a,int b,int c){return a+b+c;}  //3 arguments
}  

class TestOverloading1{  
   public static void main(String[] args){  
      System.out.println(Adder.add(11,11));  
      System.out.println(Adder.add(11,11,11));  
   }
} 
```
In the above example, we have created two methods, first add() method performs addition of two numbers and second add method performs addition of three numbers.

In the above example, we are **creating static methods so that we don't need to create instance for calling methods**.

#### Method Overloading - Changing data type of arguments

```java
class Adder{  
   static int add(int a, int b){return a+b;}  // 2 arguments of int data type
   static double add(double a, double b){return a+b;}  // 2 arguments of double data type 
}  

class TestOverloading2{  
   public static void main(String[] args){  
      System.out.println(Adder.add(11,11));  
      System.out.println(Adder.add(12.3,12.6));  
   }
} 
```
In the above example, we have created two methods that differs in data type. The first add method receives two integer arguments and second add method receives two double arguments. 

**Note : Method overloading is not possible by changing the return type of the method.**

### Overloading the main() method in Java

```java
class TestOverloading4{  
   public static void main(String[] args){System.out.println("main with String[]");}  
   public static void main(String args){System.out.println("main with String");}  
   public static void main(){System.out.println("main without args");}  
}  
```

Yes, by method overloading. You can have any number of main methods in a class by method overloading. But JVM calls main() method which receives string array as arguments only. 

### Method Overriding

    - If subclass (child class) has the same method as declared in the parent class, it is known as method overriding in Java. 
    - In other words, If a subclass provides the specific implementation of the method that has been declared by one of its parent class, it is known as method overriding.

### Usage and Rules for Method Overriding

#### Usage : 

    - Method overriding is used to provide the specific implementation of a method which is already provided by its superclass.
    - Method overriding is used for runtime polymorphism

#### Rules : 

    - The method must have the same name as in the parent class
    - The method must have the same parameter as in the parent class.
    - There must be an IS-A relationship (inheritance).

### Example for Method Overriding 

```java
class ABC{
   //Overridden method
   public void disp()
   {
     System.out.println("disp() method of parent class");
   }     
}

class Demo extends ABC{
   //Overriding method
   public void disp(){
     System.out.println("disp() method of Child class");
   }
   
   public void newMethod(){
     System.out.println("new method of child class");
   }

   public static void main( String args[]) {
     ABC obj = new ABC();
     obj.disp();
     ABC obj2 = new Demo(); // Covariance with reference types
     obj2.disp();
   }
}
```

In the above example, we have defined the disp() method in the subclass as defined in the parent class but it has some specific implementation. The name and parameter list of the methods are the same, and there is IS-A relationship between the classes.

### Can a static method be overridden?

No, a static method cannot be overridden. It can be proved by runtime polymorphism, so we will learn it later. 

It is because the static method is bound with class whereas instance method is bound with an object. Static belongs to the class area, and an instance belongs to the heap area. 

### Method Overloading vs Method Overriding

#### Method Overloading : 

    - Method overloading is used to increase the readability of the program. 
    - Method overloading is performed within class. 
    - In case of method overloading, parameter must be different.
    - Method overloading is the example of compile time polymorphism. 
    - In java, method overloading can't be performed by changing return type of the method only. Return type can be same or different in method overloading. But you must have to change the parameter. 
    
#### Method Overriding : 

    - Method overriding is used to provide the specific implementation of the method that is already provided by its super class. 
    - Method overriding occurs in two classes that have IS-A (inheritance) relationship. 
    - In case of method overriding, parameter must be same.
    - Method overriding is the example of run time polymorphism. 
    - Return type must be same or covariant in method overriding. 

### Sample Exercise 

Consider a scenario where Bank is a class that provides functionality to get the rate of interest. However, the rate of interest varies according to banks. For example, SBI, ICICI and AXIS banks could provide 8%, 7%, and 9% rate of interest. 

Go ahead and code the above scenario. 

NEXT: [OOP Pillar Polymorphism](OOP-Pillar-Polymorphism)
< [OOP Pillars](OOP-Pillars)
< [OOP Study Guide](OOP-Study-Guide)
< [Index](Index)
