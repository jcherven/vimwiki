## Package?

A java package is a group of similar types of classes, interfaces and
sub-packages. 

Package in java can be categorized in two form, built-in package and
user-defined package. 

There are many built-in packages such as java, lang, awt, javax, swing, net,
io, util, sql etc.

## Advantages Of Packages

    - Java package is used to categorize the classes and interfaces so that
      they can be easily maintained.
    - Java package provides access protection.
    - Java package removes naming collision.

Example

```java
//save as Simple.java  
package com.revature;  
public class Simple{  
  public static void main(String args[]){  
    System.out.println("Welcome to package");  
  }  
}
```

## Accessing a package from other packages

There are three ways to access the package from outside the package.

    - `import package.*;`
    - `import package.classname;`
    - fully qualified name.

### Using packagename.* 

If you use package.* then all the classes and interfaces of this package will
be accessible but not subpackages. 

The import keyword is used to make the classes and interface of another package
accessible to the current package.

```java
//save by A.java  
package pack;  
public class A{  
  public void msg(){System.out.println("Hello");}  
}  
```

```java
//save as B.java
package mypack;  
import pack.*;  //Importing the package named pack which contains class A.

class B{  
  public static void main(String args[]){  
    A obj = new A();  
    obj.msg();  
  }  
} 
```

### Using packagename.classname

If you import package.classname then only declared class of this package will
be accessible. 

```java
//save by A.java  
package pack;  
public class A{  
  public void msg(){System.out.println("Hello");}  
}  
```

```java
//save by B.java  
package mypack;  
import pack.A;  //Importing class A from packagename pack which gives us access to only A.

class B{  
  public static void main(String args[]){  
    A obj = new A();  
    obj.msg();  
  }  
}  
```

### Using fully qualified name

If you use fully qualified name then only declared class of this package will
be accessible. Now there is no need to import. But you need to use fully
qualified name every time when you are accessing the class or interface.

It is generally used when two packages have same class name e.g. java.util and
java.sql packages contain Date class.

```java
//save by A.java  
package pack;  
public class A{  
  public void msg(){System.out.println("Hello");}  
}  
```

```java
//save by B.java  
package mypack;  
class B{  
  public static void main(String args[]){  
    pack.A obj = new pack.A(); // using fully qualified name  
    obj.msg();  
  }  
} 
```

## Sequence of program

Sequence of the program must be package then import then class.
