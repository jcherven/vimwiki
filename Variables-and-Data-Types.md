< [Java Basics](Java-Basics) | [Operators](Operators) >

# Java Basics

## Variables and Data Types

Every programming language, from the ancient Assembly to the modern Java, has
the idea of a variable. A variable is a structure for temporarily storing data
in your computer’s memory, and it would be impossible to do anything meaningful
without them. 

Java is a strongly-typed language, which means that each variable has a single
type of data that it can store. Broadly speaking, there are two forms of
variables in Java: primitive and reference variables. 

Primitive variables are data types like integers, decimals, and alphanumeric
characters. 

Reference variables store memory addresses where Objects are located, and are
strongly typed too – a reference variable has a type that is the class whose
objects the reference variable can point to. 

Primitives variable types are called “primitive” because they hearken back to a
time before Object Oriented Programming and reference variables were a thing.
Primitive types of variables take up specific, predefined amounts of space in
memory, and so each type has a corresponding limit to the range of values they
can store. There are eight primitive data types in Java. All primitive data
types are lower-case, and by default they contain a the lowest value they can –
0 for numbers, false for boolean, and the null character for chars. 

  - A boolean variable only holds a value of true or false, and so it only
    requires one bit of memory – ultimately it stores a 0 or a 1. However, Java
    doesn’t support what other languages call “truthy” values, where an integer
    0 is the same as a boolean false. 
  - A byte holds a two’s compliment integer, and true to its name, it requires
    8 bits of memory. An 8-bit two’s compliment number can range from -128 to
    127. 
  - A short is a 16-bit two’s compliment integer, and it ranges from -2^15 to
    2^15-1. 
  - A char is a 16-bit data type that holds a single Unicode character.
    Character values sit between single quotes, and you can either type the
    character directly or use forward-slash-‘u’ followed by the character’s
    4-digit code. 
  - An int is a 32-bit integer, and it’s probably going to be the most common
    integer data type you use. An int can range from -2^31 to 2^31 – 1. 
  - A float is a 32-bit floating point number, which means it can store decimal
    values. However, because of the way floating point math works on computers,
    a 32-bit floating point number is not as precise as the double type. 
  - A number can be specified as a float by following it with an ‘f’.
    Interestingly, a float value can also incorporate e to represent a number
    in scientific notation. 
  - Long is a 64-bit integer, and their values can range from -2^63 to 2^63 –
    1. To specify a number as a long value instead of an int, you can follow it
    with a capital L. 
  - The last primitive data type is the double-precision floating point, called
    “double” for short. A double is a 64-bit floating point number, and they
    can be differentiated from a float value by following the number with a
    ‘d’. Typically, this will be the default decimal datatype you use. 

Reference variables on the other hand, use a class name as their type. The
reference variable can then only point to an object that is an instance of that
class. You can then use the dot operator to access the variables or methods in
the object being referenced. This does NOT mean that the reference variable IS
the object, and this distinction becomes very important to understanding Java’s
mechanics and quirks under the hood. But we’ll save that discussion for another
video. 

In either case, you use the assignment operator – more commonly known as the
equals sign – to assign a value to a variable. The assignment operator works
right to left, meaning whatever exists on the right side of the equals sign is
worked through and stored in the variable on the left side. To put it even more
simply, in Java we say X = 3, not 3 = x. We’ll cover more operators in a later
video, but let’s look at a quick example of variable declaration and usage. 

```java
boolean myBoolean = false;
byte myByte = 2;
short myShort = 3;
char mychar = 'b';
int myInt = 5;
float myFloat = 0.25f;
long myLong = 9999999999999L;
double mydouble = 5.999d;
String myString = new String("Object, created with a constructor");
```

Here we can see a number of primitive variables being declared, and assigned
values with the assignment operator – the equals sign. You can also see an
example of a reference variable, for the String class. This reference variable
can hold a String object, which it creates with a constructor here. All objects
are instantiated using the new keyword and a constructor as shown here, but
we’ll cover these in a later video. We can also see some basic arithmetic
operations being performed, and the console output validates the results. Pay
attention to what happens when we divide a whole-number data type like int with
another whole-number type…The resulting answer is also a whole-number, and any
decimals are truncated. 

There is one other type of data structure that is important to discuss, and
that is the array. An array is a collection of primitive values or object
references, stored in a single variable with an index. You can think of an
array as a row of boxes, where the first box is “index 0,” the next is “index
1” and so forth. An array always has a fixed length or number of boxes, and a
fixed data type, both of which are assigned when it is instantiated. You can
instantiate an array in one of two ways: you can use the new keyword to create
an empty array of a certain size. That syntax looks like this, if you wanted to
create an array of 10 ints. 

```java
int[] intArray = new int[10];
```

You could also initialize an array with its values directly, using curly braces
as shown. 

```java
int[] intArray = {2, 4, 6};
```

This will create an int array of size 3, which comes preloaded with the values
2, 4, and 6. Accessing a value in an array is as simple as using the variable
name, followed by the desired index between brackets. You can also use this
syntax to store a value directly to an index in an array. 

All arrays have a built in length property, which stores the number of indices
the array possesses. You might have noticed from the use of the new keyword,
that an Array is technically an object in Java, and so an array variable is a
reference variable. Because of this, you can use the dot operator to access the
length variable of the Array object. 

If that weren’t enough, you can have Arrays of arrays, otherwise known as a
multidimensional array. To visualize this, think of the first array as a
vertical row of boxes, where each box contains another horizontal row. To
create a multidimensional array, you just use multiple sets of brackets, or
nested curly braces. To refer to a specific index, you have to give the index
of the first array, followed by the index of the array contained at the first
index. 

```java
public class ArraysExample {
  public static void main(String[] args) {
    int[] firstArray = new int[];
    int[] secondArray = {1, 2, 3};
    
    firstArray[0] = 2;
    firstArray[1] = 4;
    firstArray[2] = 6;
    
    System.out.println("1st array's [1] is " = firstArray[1]);
    System.out.println("2nd array's length is " = secondArray.length);
  }
}
```

Here is an example of the several ways to create an array. One way is to use
the square brackets as shown here, where you simply state the data type, and
the size of the array. If you know what values you want inside of the array,
you can also plug those values in at creation by using the curly braces as
shown here. Accessing a value in an array is as simple as referring to the
index location of that value. You can also access the length property of an
array by using the dot operator. 

Now, variables also have some classifications depending on where they are
declared. When a variable is declared in a particular scope, it is visible to
all lower level scopes, but not any higher level scopes. A variable declared in
the class scope – that is, after the class declaration but outside of any
methods – it’s called an instance variable. Each instance of the class will
have a copy of that variable, with a value unique to each instance. 

```java
public class Dog {
  String furColor;
}
```

Here, every Dog object will have a furColor variable, but one Dog object might
have black fur, while another has brown. If a variable also has the keyword
static, it becomes a class variable, or a global variable. This means that
every object of that class will share the same value for that variable, and if
you change it in one object it is changed for all of them. 

If a variable is declared inside a method, it’s called a local variable. A
local variable doesn’t exist outside the method in which it is declared. When
the method is done executing, the variable is deleted from memory. 

If you’ve ever programmed in another language, most of this is probably
familiar to you. Where Java differs from many other languages is its use of
strong typing, the selection of data types available, and the amount of memory
reserved by each. Java doesn’t really bring anything special or new to the
table here, these are just things you ought to be aware of. 

< [Java Basics](Java-Basics) | [Operators](Operators) >

