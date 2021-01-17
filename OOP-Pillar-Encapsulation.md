# OOP Pillars

## Encapsulation
    - Encapsulation in Java is a process of wrapping code and data together
      into a single unit, for example, a capsule which is mixed of several
      medicines. 
    - We can create a fully encapsulated class in Java by making all the data
      members of the class private. Now we can use setter and getter methods to
      set and get the data in it. 
    - The Java Bean class is the example of a fully encapsulated class. 

## Advantages of Encapsulation

    - By providing only a setter or getter method, you can make the class
      read-only or write-only. In other words, you can skip the getter or
      setter methods.
    - It provides you the control over the data. Suppose you want to set the
      value of id which should be greater than 100 only, you can write the
      logic inside the setter method. You can write the logic not to store the
      negative numbers in the setter methods.
    - It is a way to achieve data hiding in Java because other class will not
      be able to access the data through the private data members.
    - The encapsulate class is easy to test. So, it is better for unit testing.

## Example for Encapsulation

```java
package com.revature;  
public class Student{  
   //private data member  
   private String name;  
   //getter method for name  
   public String getName(){  
      return name;  
   }  
   //setter method for name  
   public void setName(String name){  
      this.name=name  
   }  
}
```

```java
//A Java class to test the encapsulated class.  
package com.revature;  
class Test{  
   public static void main(String[] args){  
      //creating instance of the encapsulated class  
      Student s=new Student();  
      //setting value in the name member  
      s.setName("vijay");  
      //getting value of the name member  
      System.out.println(s.getName());  
   }  
}
```

The above is an example of encapsulation of a class called Student that has
only one field with its setter and getter methods. 

## Read-Only Class

```java
//A Java class which has only getter methods.  
public class Student{  
   //private data member  
   private String college="AKG";  
   //getter method for college  
   public String getCollege(){  
      return college;  
   }  
} 
```

The above class is an example of a Read-Only class because it has only a getter
to access the college name. If the user tries to change the value of the
college name, a compile-time error is rendered. 

## Write-Only Class

```java
//A Java class which has only setter methods.  
public class Student{  
   //private data member  
   private String college;  
   //setter method for college  
   public void setCollege(String college){  
      this.college=college;  
   }  
} 
```

The above class is an example of a Write-Only class because it has only setters
to change the value of the college name and cannot read the college name. Even
if tried to access outside of this class a compile-time error is displayed only
because the variable is declared as private. 

## Access Modifiers

    - There are two types of modifiers in java: access modifiers and non-access
      modifiers. 
    - The access modifiers in java specifies accessibility (scope) of a data
      member, method, constructor or class. 

There are 4 types of java access modifiers:

    - private
    - default
    - protected
    - public

There are many non-access modifiers such as static, abstract, synchronized,
native, volatile, transient etc. Here, we will learn access modifiers. 

## Access Modifiers with Method Overriding

```java
class A{  
   protected void msg(){
      System.out.println("Hello java");
   }  
}  

public class Simple extends A{  
   void msg(){
      System.out.println("Hello java");
   }
// Error because Class Simple method msg() is
// more restrictive that Class A method msg() 

   public static void main(String args[]){  
      Simple obj=new Simple();  
      obj.msg();  
   }  
}
```

If you are overriding any method, overridden method (i.e. declared in subclass)
must not be more restrictive.

## Sample Exercise

Create an encapsulated class with 4 fields and the respective methods to access
and edit those fields. Then go ahead and create a test class to verify. 

    Class Name : Student
    Field Names : studentId, studentName, collegeName, address
    Test Class Name : TestStudent
    
```java
// Student.java - example of an encapsulated class
public class Student {
	private String studentId;
	private String studentName;
	private String collegeName;
	private String address;
	
	public void setStudentId(String newStudentId) {
		studentId = newStudentId;
	}
	public void setStudentName(String newStudentName) {
		studentName = newStudentName;
	}
	public void setCollegeName(String newCollegeName) {
		collegeName = newCollegeName;
	}
	public void setAddress(String newAdress) {
		address = newAdress;
	}
	
	public String getStudentId() {
		return studentId;
	}
	public String getStudentName() {
		return studentName;
	}
	public String getCollegeName() {
		return collegeName;
	}
	public String getAddress() {
		return address;
	}

}
```

```java
// Main.java - test class for the encapsulated Student class
public class Main {
	public static void main(String[] args) {
		Student testStudent = new Student();
		testStudent.setStudentId("YUBI900MAN");
		testStudent.setStudentName("Korone Inugami");
		testStudent.setCollegeName("Hololive Polytechnic Institute");
		testStudent.setAddress("1058 Pan Dori Kyary Cho Tokyo Japan");
		
		System.out.println("Student ID: " + testStudent.getStudentId());
		System.out.println("Student Name: " + testStudent.getStudentName());
		System.out.println("College Name: " + testStudent.getCollegeName());
		System.out.println("Address: " + testStudent.getAddress());
	}
}
```

NEXT: [OOP Pillar Abstraction](OOP-Pillar-Abstraction)
< [OOP Pillar Polymorphism](OOP-Pillar-Polymorphism)
< [OOP-Pillars](OOP-Pillars)
< [OOP Study Guide](OOP-Study-Guide)
< [Index](Index)
